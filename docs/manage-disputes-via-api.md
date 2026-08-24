---
title: "Manage Disputes via API"
slug: "manage-disputes-via-api"
status: "custom"
updated: 2026-08-20T09:29:10Z
published: 2026-08-20T09:29:10Z
canonical: "docs.xendit.co/manage-disputes-via-api"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Manage Disputes via API

### Prerequisites

- A Xendit account with card or QR payment methods enabled.
- A webhook endpoint registered to receive dispute events (see [Webhooks](/docs/manage-disputes-via-api#webhooks) below).
- Your Secret API Key. Every request in this guide uses Xendit's standard API authentication: HTTP Basic Auth, with your Secret API Key as the username and an empty password, over HTTPS. This is the same scheme used across all Xendit merchant-facing APIs; see the [Quick setup guide](https://docs.xendit.co/apidocs/quick-setup) for details.
- Running a xenPlatform business? See the platform note under [Webhooks](/docs/manage-disputes-via-api#webhooks) before you integrate sub-account disputes.

---

## How disputes reach you

Disputes reach you through **webhooks**, not polling. You'll be notified the moment a dispute is raised, and again at every status change.

```
Dispute raised
   → webhook: dispute.action_required
      → you decide: challenge or accept
         → challenge: POST /evidences (submit evidence) → POST /challenge → webhook: dispute.under_review → webhook: dispute.won / dispute.lost
         → accept: POST /accept → webhook: dispute.lost
```

Each webhook payload gives you the `id` you'll use for every action below, plus `payment_id` and `reference_id` to match the dispute to your own order records.

### Dispute statuses

The Disputes API (webhook payloads and the optional GET endpoint) returns these as uppercase values; the Dashboard shows them in sentence case.

| Status (API value) | Shown as | What it means |
| --- | --- | --- |
| `ACTION_REQUIRED` | Action required | A dispute has been raised. Review it and decide whether to challenge or accept before `due_date`. |
| `UNDER_REVIEW` | Under review | You've challenged the dispute. Your evidence is being reviewed by the card network or payment scheme. |
| `WON` | Won | The dispute was resolved in your favor. |
| `LOST` | Lost | The dispute was resolved against you, or you accepted it. |

### Status reasons

`status_reason` adds context to a status change. It's nullable, and most reasons pair with a terminal status (`WON` or `LOST`), except `NEED_MORE_INFORMATION`.

| Reason | Meaning |
| --- | --- |
| `EXCEEDED_DEADLINE` | You didn't respond before the deadline, so the dispute defaulted against you. |
| `ACCEPTED` | You accepted the dispute rather than challenging it. |
| `CHALLENGED` | The outcome followed your challenge and evidence submission. |
| `WITHDRAWN` | The customer or issuing bank withdrew the dispute. |
| `NEED_MORE_INFORMATION` | The reviewer needs more information before deciding. Unlike the other reasons, this pairs with `ACTION_REQUIRED`, not a terminal status: the dispute returns to you for another response. This is how you tell a follow-up `dispute.action_required` apart from the original: the first occurrence has `status_reason: null`, a follow-up has `status_reason: NEED_MORE_INFORMATION`. |

> **Note on amounts:** Every dispute has an `amount.initial` (amount when raised) and an `amount.terminal` (final resolved amount, `null` until resolved) that usually match but can differ for a partial resolution. Design your reconciliation logic around `amount.terminal`, not just the status.

---

## Webhooks

Register a webhook endpoint in your Xendit Dashboard to receive these events:

| Event | Fires when |
| --- | --- |
| `dispute.action_required` | A new dispute needs your decision. |
| `dispute.under_review` | Your challenge and evidence have been submitted and are being reviewed. |
| `dispute.won` | The dispute resolved in your favor. |
| `dispute.lost` | The dispute resolved against you. |

Each payload contains the full public state of the dispute, including which evidence you're allowed to submit:

```
{
  "event": "dispute.action_required",
  "id": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7",
  "channel_code": "CARDS",
  "card_brands": "VISA",
  "status": "ACTION_REQUIRED",
  "status_reason": null,
  "currency": "USD",
  "amount": { "initial": "1000.00", "terminal": null },
  "created_at": "2026-03-01T19:50:51.724Z",
  "updated_at": "2026-03-01T19:50:51.724Z",
  "due_date": "2026-03-15T19:50:51.724Z",
  "note": "Please provide evidence of delivery.",
  "category": {
    "name": "fraud",
    "allowed_evidence": [
      { "name": "proof_of_delivery", "type": "FILE", "max_length": 5242880, "is_recommended": true, "max_evidences": 3 },
      { "name": "explanation", "type": "TEXT", "max_length": 255, "is_recommended": false, "max_evidences": 3 }
    ]
  },
  "related_disputes": [],
  "payment_id": "py-59a3cf39-2a7d-4733-a3e3-8177c78090f7",
  "reference_id": "ref-123456",
  "evidences": []
}
```

`category.allowed_evidence` tells you exactly what you can submit for this dispute:

| Field | Meaning |
| --- | --- |
| `name` | The evidence slug. Use this as the form field name when you submit evidence. |
| `type` | `FILE` or `TEXT`. |
| `max_length` | The size limit for this item: bytes for `FILE`, characters for `TEXT`. |
| `is_recommended` | Whether Xendit recommends including this evidence for a stronger challenge. Not mandatory. |
| `max_evidences` | The maximum number of items you can submit for this slug. |

`dispute.action_required` can fire more than once for the same dispute: the first occurrence has `status_reason: null`, and a later one with `status_reason: NEED_MORE_INFORMATION` means the reviewer needs more from you, not a duplicate delivery. Build your handler to be **idempotent** regardless: webhook delivery isn't guaranteed exactly once, so key your processing off the dispute `id`, `status`, `status_reason`, and `updated_at`. Track `due_date` from this payload and set your own reminder; there is no separate deadline reminder webhook.

> **Platform (xenPlatform) merchants:** Subscribe to dispute webhooks once on your master Business ID; this covers every sub-account, with no separate subscription needed.
> 
> 
> To act on a sub-account's dispute (evidences, challenge, or accept), include a `for-user-id` header set to the sub-account's Business ID, authenticated with your master account's API key. See the [xenPlatform overview](https://docs.xendit.co/docs/xenplatform-overview) and the [`for-user-id` guide](https://help.xendit.co/hc/en-us/articles/10534695308185-How-Do-I-Use-for-user-id-Parameter-to-Do-Transaction-as-Master-Account-on-Behalf-of-my-Sub-Account) for the general pattern.

---

## Responding to a dispute

Once you receive `dispute.action_required`, there are exactly two things to do before `due_date`: **challenge** it with evidence, or **accept** it. The webhook payload already tells you what evidence you can submit (`category.allowed_evidence`, above); you don't need a separate lookup to get started. Miss the deadline, and it defaults to `LOST` with `status_reason: EXCEEDED_DEADLINE`.

### Option A: Challenge the dispute

**Step 1: submit evidence**

```
POST /v1/disputes/{dispute_id}/evidences
Content-Type: multipart/form-data
```

Each form field name is one of the evidence slugs from `category.allowed_evidence` (for example `proof_of_delivery`); the value is a file or a text string, matching that slug's `type`.

- Up to 10 evidence items per request.
- File and text evidence can be submitted together.
- One submission per slug, up to that slug's `max_evidences`. Use `PATCH` (below) to revise text evidence you've already submitted.

```
curl https://api.xendit.co/v1/disputes/mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7/evidences \
  -u $SECRET_API_KEY: \
  -F "proof_of_delivery=@delivery_receipt.pdf" \
  -F "explanation=The customer completed the transaction at our store."
```

The response reports successes and failures item by item, so a partial failure doesn't block the rest of your submission:

```
{
  "dispute_id": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7",
  "evidences_succeeded": [
    { "id": "mi-dspt-evd-12345", "category_slug": "proof_of_delivery", "filename": "delivery_receipt.pdf", "mime_type": "application/pdf", "type": "FILE" }
  ],
  "evidences_failed": [
    { "filename": "invalid_category", "reason": "Evidence category is not allowed for this dispute." }
  ],
  "message": "1 evidence(s) submitted successfully, 1 failed."
}
```

`201 Created` on success. Check `evidences_failed` on every response, even a `201`; a request can partially succeed.

| Error code | Meaning |
| --- | --- |
| `ILLEGAL_STATE` | The dispute isn't in a state that accepts evidence (for example, already under review or resolved). |
| `EVIDENCE_CATEGORY_NOT_ALLOWED` | This slug isn't valid for this dispute. |
| `CATEGORY_LIMIT_REACHED` | You've already reached that slug's `max_evidences`. |
| `UNSUPPORTED_EVIDENCE_TYPE` | The uploaded file type isn't supported. |

**Updating or removing evidence before you challenge**

Evidence is immutable only after you finalize your challenge (`POST /challenge`). Until then, you can revise text evidence or remove any item:

```
PATCH /v1/disputes/{dispute_id}/evidences/{evidence_id}
```

```
{ "text_content": "Updated statement: the customer completed the transaction and signed the receipt." }
```

`204 No Content` on success. Only `TEXT` evidence can be updated this way; `PATCH`ing a `FILE` item returns `422 EVIDENCE_NOT_TEXT`. Delete any evidence item (file or text) with:

```
DELETE /v1/disputes/{dispute_id}/evidences/{evidence_id}
```

`204 No Content` on success.

**Step 2: finalize your challenge**

```
POST /v1/disputes/{dispute_id}/challenge
```

This locks in your submitted evidence and sends it for review; you can't add more evidence afterward.

```
{ "dispute_id": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7", "message": "Challenge accepted. The dispute will be processed asynchronously." }
```

`202 Accepted`. The review itself happens asynchronously; you'll get `dispute.under_review`, then `dispute.won` or `dispute.lost`, via webhook.

| Error code | Meaning |
| --- | --- |
| `ILLEGAL_STATE` | The dispute isn't in a state that can be challenged right now. |
| `INVALID_REQUEST` | You haven't submitted any evidence yet. Submit at least one item before challenging. |

### Option B: Accept the dispute

Accepting returns the disputed amount to your customer and immediately resolves the dispute as **Lost** (`status_reason: ACCEPTED`); this can't be undone, so only accept if you don't intend to challenge:

```
POST /v1/disputes/{dispute_id}/accept
```

```
{ "dispute_id": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7", "message": "Accept acknowledged. The dispute will be processed asynchronously." }
```

`202 Accepted`. Processing is asynchronous; you'll receive `dispute.lost` via webhook once it's final. `ILLEGAL_STATE` (`400`) if the dispute is no longer in a state where it can be accepted.

---

## Looking up a dispute

Everything you need to respond to a dispute already arrives in the webhook payload. This endpoint is optional: use it to re-check a dispute's current state, for example to recover from a missed webhook.

```
GET /v1/disputes/{dispute_id}
```

Returns the same fields as the webhook payload, including the current `category.allowed_evidence`. `200` on success, `404` if the dispute ID doesn't exist.

---

## Testing in sandbox

This endpoint works only in the sandbox environment, has no effect on production data, and exists purely so you can test your evidence, challenge, and accept flow before a real dispute occurs.

```
POST /v1/disputes/simulate
```

**Create a simulated dispute** against a settled sandbox payment:

```
{
  "scenario": "CREATE_DISPUTE",
  "payment_id": "py-59a3cf39-2a7d-4733-a3e3-8177c78090f7",
  "amount": "1000.00",
  "currency": "USD",
  "channel_code": "CARDS"
}
```

The payment must already be settled, or you'll get `422 PAYMENT_NOT_SETTLED`. This triggers a real `dispute.action_required` webhook, so you can test your full evidence, challenge, and accept flow end to end.

**Resolve a simulated dispute** once you've challenged or accepted it:

```
{ "scenario": "DISPUTE_WON", "dispute_id": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7" }
```

```
{ "scenario": "DISPUTE_LOST", "dispute_id": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7" }
```

All three scenarios return `201 Created`:

```
{ "dispute_id": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7", "created_at": "2026-03-01T19:50:51.724Z" }
```

| Error code | Meaning |
| --- | --- |
| `PAYMENT_NOT_SETTLED` | The payment exists but hasn't finished settling yet. |
| `PAYMENT_NOT_FOUND` | The payment ID doesn't exist. |
