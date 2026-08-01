---
title: "Migrate Payment API v2 to v3"
slug: "migrate-payment-api-v2-to-v3"
updated: 2026-07-27T05:38:22Z
published: 2026-07-27T05:38:22Z
canonical: "docs.xendit.co/migrate-payment-api-v2-to-v3"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Migrate Payment API v2 to v3

This guide explains how to migrate existing Xendit Payment API v2 integrations (Payment Method, Payment Request, and Payment objects) to Payment API v3 (`/v3/payment_requests` and `/v3/payment_tokens`).

> [!NOTE]
> Scoped to the generic Payment API v2. If you're integrating directly per-channel (e.g. `/ewallets`, `/qr_codes`, `/credit_card_charges`), see the separate Legacy [direct-channel APIs → Payments API v3 guide](/v1/docs/migrate-direct-per-channel-apis-to-v3).

---

## Why you should migrate

- **Faster time-to-market for new channels.** Because every channel now shares the same `channel_code` + `channel_properties` shape instead of a `payment_method` sub-object, adding a new payment channel is only a configuration change on your end.
- **Use case-centric model.** In v3, you can define explicitly the use case of your Payment Request (`PAY`, `PAY_AND_SAVE`, `REUSABLE_PAYMENT_CODE`) while saving end user payment method account separately handled by Payment Token. This structure will make the flow more predictable.
- v2 required per-channel logic to interpret `url_type` (`API`/`WEB`/`MOBILE`/`DEEPLINK`) and `action` (`AUTH`/`RESEND_AUTH`) fields. v3 standardizes this into two universal action types, so your checkout UI logic no longer needs an implicit channel-specific switch statement.
- **Clearer separation of concerns for saved payment methods.** Saving a payment method (`Payment Token`) is now explicitly decoupled from charging (`Payment Request`), instead of being entangled in one object.
  - **v2** treats the Payment Method as the mandatory gate every transaction must pass through. A `Payment Request` cannot exist without a `Payment Method` — either created inline or referenced by ID. This means the "instrument" object and the "charge intent" object are tightly coupled, even when you don't need reusability.
  - **v3** treats the Payment Request as self-sufficient. It carries its own `channel_code`, `channel_properties`, and an explicit `type` describing the intended flow. A Payment Token is an optional, independent object that you only create when you genuinely need to save a payment method for future use.

## Overall changes

The change is not just a new URL — it's a different way of modeling a transaction. In v2, every payment is created *through* a Payment Method. In v3, a Payment Request stands on its own: you pass `channel_code` and `channel_properties` directly, tell Xendit what you want with `type`, and only bring a Payment Token into the picture if you actually need to charge the customer again later.

Before touching any code, there are a few things engineers should be aware of going in:

- **This is not a drop-in field rename.** Some code paths won't just need renamed fields — they'll need to be restructured or removed entirely (e.g. any logic that creates a Payment Method purely to immediately charge it once).
- **The** `type` **field is reused with a different meaning.** v2 had a `type` field on the *Payment Method* (`EWALLET`, `CARD`, etc.). v3 has a `type` field on the *Payment Request* (`PAY`, `PAY_AND_SAVE`, `REUSABLE_PAYMENT_CODE`). These are not the same concept.
- Payment Request in v3 is an independent object, creating a Payment Request won’t need Payment Method object as v2 concept.
- **Webhook payloads and event names both changed.** This isn't just `payment.failed` → `payment.failure` — the `payment_method.expired` event that v2 sends after every successful one-time payment has no v3 equivalent, and any logic (alerts, retries, reconciliation) built around it needs to be removed, not remapped.
- In v3, everything specific to a channel sits inside `channel_properties`, and which fields are required there depends on the `channel_code` and `type` you're using.

| Area | v2 | v3 |
| --- | --- | --- |
| Create a payment request — URL | `POST https://api.xendit.co/payment_requests` | `POST https://api.xendit.co/v3/payment_requests` |
| Save end user payment method — URL | `POST https://api.xendit.co/v2/payment_methods` | `POST https://api.xendit.co/v3/payment_tokens` |
| Core objects | `Payment Method`, `Payment Request`, `Payment` | `Payment Token`, `Payment Request`, `Payment` |
| Relationship between objects | Payment Request **requires** a Payment Method (inline or by reference) | Payment Request is self-contained; Payment Token is optional |
| Tokenization | Implicit — happens for every payment, even one-off ones | Explicit/opt-in — only via `PAY_AND_SAVE` or a standalone Payment Token creation call |
| How you select a channel | Nested inside a `payment_method` sub-object (`payment_method.ewallet.channel_code`, etc.) | Top-level `channel_code` + `channel_properties` |
| How you declare intent | Implied by `payment_method.reusability` | Explicit `type` field: `PAY`, `PAY_AND_SAVE`, `REUSABLE_PAYMENT_CODE`, or `PAY` + `payment_token_id` |
| End-user action model | Channel-specific `url_type` / `action` combinations | Standardized `REDIRECT_CUSTOMER` / `PRESENT_TO_CUSTOMER` |
| Webhooks | `payment.succeeded`, `payment.failed`, `payment_method.activated`, `payment_method.expired`, `payment_method.failed` | `payment.capture`, `payment.failure`, `payment_token.activation` , `payment_token.expiry` , `payment_token.failure` |
| API versioning | No `api-version` header | Requires `api-version` header (e.g. `2024-11-11`) |

---

## Detailed changes

### Endpoint URLs

| Action | v2 | v3 |
| --- | --- | --- |
| Create a payment | `POST https://api.xendit.co/payment_requests` | `POST https://api.xendit.co/v3/payment_requests` |
| Get a payment request | `GET https://api.xendit.co/payment_requests/{id}` | `GET https://api.xendit.co/v3/payment_requests/{id}` |
| List payment requests | `GET https://api.xendit.co/payment_requests` | `GET https://api.xendit.co/v3/payment_requests` |
| Save end user payment method | `POST https://api.xendit.co/v2/payment_methods` | `POST https://api.xendit.co/v3/payment_tokens` |
| Get a saved payment method/token | `GET https://api.xendit.co/v2/payment_methods/{id}` | `GET https://api.xendit.co/v3/payment_tokens/{id}` |
| List saved payment methods/tokens | `GET https://api.xendit.co/v2/payment_methods` | `GET https://api.xendit.co/v3/payment_tokens` |
| Update a saved payment method/token | `PATCH https://api.xendit.co/v2/payment_methods/{id}` | `PATCH https://api.xendit.co/v3/payment_tokens/{id}` |

### Mandatory Payment Method (v2) vs. self-defined flow (v3)

In v2, `POST /payment_requests` always requires a Payment Method — either inline or by `payment_method_id` while on v3, `POST /v3/payment_requests` have a type to identify the flow explicitly

**v2 Example**

```json
// v2 — POST https://api.xendit.co/payment_requests
{
  "currency": "IDR",
  "amount": 100000,
  "payment_method": {
    "type": "EWALLET",
    "reusability": "ONE_TIME_USE",
    "ewallet": {
      "channel_code": "SHOPEEPAY",
      "channel_properties": {
        "success_return_url": "https://your-redirect-website.com/success"
      }
    }
  },
  "customer_id": "fc4c060b-3c41-4707-b7b2-df9c3376edde"
}
```

**v3 Example**

```json
// v3 — POST https://api.xendit.co/v3/payment_requests
// header: api-version: 2024-11-11
{
  "reference_id": "order-id-123",
  "type": "PAY",
  "country": "ID",
  "currency": "IDR",
  "request_amount": 100000,
  "channel_code": "SHOPEEPAY",
  "channel_properties": {
    "success_return_url": "https://redirect.me/payment"
  }
```

### The `type` field — declaring intent explicitly

Refer to Payment API v3 [integration guidelin](/v1/docs/payments-via-api-overview)e to see supported use cases and type mapping.

### `channel_code` and `channel_properties` reference

> Available `channel_code` values and supported `channel_properties` for a given `channel_code` can be find [here](https://doc-widget.xendit.co/channel-data-finder/)

### Standardized action handling

v2's `actions` array used channel-specific `url_type` values (`API`, `WEB`, `MOBILE`, `DEEPLINK`) and `action` purposes (`AUTH`, `RESEND_AUTH`), requiring per-channel client logic.

v3 collapses this into two universal action types:

| v3 `actions[].type` | Meaning | Roughly maps to v2's... |
| --- | --- | --- |
| `REDIRECT_CUSTOMER` | Send the customer to a URL to authenticate | `url_type: WEB/MOBILE/DEEPLINK`, `action: AUTH` |
| `PRESENT_TO_CUSTOMER` | Show a code/value to the customer directly (no redirect) | Values previously read off channel-specific sub-objects (e.g. `qr_code.channel_properties.qr_string`, `virtual_account.channel_properties.virtual_account_number`) |

### ⚠️ The misleading `payment_method.expired` webhook (v2) — and how v3 removes it

**In v2:** for a one-time-use payment, Xendit creates a Payment Method under the hood with `reusability: ONE_TIME_USE`. Once that payment succeeds, the Payment Method has served its purpose and Xendit immediately expires it — firing a `payment_method.expired` webhook, essentially simultaneously with the `payment.succeeded` webhook for the same transaction.

This is expected behaviour, but it reads as an error: engineers frequently see `payment_method.expired` land right after a successful payment and assume something failed, when the payment actually succeeded and the "expiry" is just the one-time-use object being retired.

**Rule of thumb:** treat `payment.capture` / `payment.failed` (the `Payment` object status) as the single source of truth for transaction outcome.

**In v3:** this ambiguity is removed structurally. A `type: "PAY"` request never creates a Payment Token, so there is no expiry webhook to misinterpret. `payment_token.*` events only fire when a token was explicitly requested via `PAY_AND_SAVE` or Payment Token creation, and such tokens don't auto-expire immediately after use.

## Field mapping

### Payment Request object — what’s change

| v2 field | v3 field | Notes |
| --- | --- | --- |
| `id` (prefix `pr-`) | `id` (prefix `pr-`) | Unchanged format. |
| `amount` | `request_amount` | **Renamed.** |
| `status` | `status` | Status lifecycle changes \| v2 \| v3 \| Notes \| \| --- \| --- \| --- \| \| `REQUIRES_ACTION` \| `REQUIRES_ACTION` \| Unchanged. Waiting for end user to take action to complete the payment \| \| `REQUIRES_ACTION` \| `ACCEPTING_PAYMENTS` \| For REUSABLE_PAYMENT_CODE type. The payment request can accept multiple payments \| \| `SUCCEEDED` \| `SUCCEEDED` \| Unchanged. Payment request SUCCEEDED. You will received a `payment.capture` webhook \| \| `FAILED` \| `FAILED` \| Unchanged. Payment request if failed. You will receive a `payment.failure`webhook \| \| n/a \| `CANCELED` \| Payment request no longer can accept the payment due to manual cancellation from your end. \| \| `AWAITING_CAPTURE` \| `AUTHORIZED` \| Payment request with capture method MANUAL (feature specifically available only for CARDS). Authorized is end state status for Payment Request v3. You may/may not capture the payment. \| \| n/a \| `EXPIRED` \| Payment request no longer can accept the payment due to its natural expiry time. \| |
| v2 | v3 | Notes |
| `REQUIRES_ACTION` | `REQUIRES_ACTION` | Unchanged. Waiting for end user to take action to complete the payment |
| `REQUIRES_ACTION` | `ACCEPTING_PAYMENTS` | For REUSABLE_PAYMENT_CODE type. The payment request can accept multiple payments |
| `SUCCEEDED` | `SUCCEEDED` | Unchanged. Payment request SUCCEEDED. You will received a `payment.capture` webhook |
| `FAILED` | `FAILED` | Unchanged. Payment request if failed. You will receive a `payment.failure`webhook |
| n/a | `CANCELED` | Payment request no longer can accept the payment due to manual cancellation from your end. |
| `AWAITING_CAPTURE` | `AUTHORIZED` | Payment request with capture method MANUAL (feature specifically available only for CARDS). Authorized is end state status for Payment Request v3. You may/may not capture the payment. |
| n/a | `EXPIRED` | Payment request no longer can accept the payment due to its natural expiry time. |
| `payment_method` (nested object containing `type`, `reusability`, and a channel-specific sub-object) | *(removed — replaced by* `channel_code` *+* `channel_properties` *at top level)* | Can be found [here](https://doc-widget.xendit.co/channel-data-finder/) |
| `payment_method.{ewallet\|direct_debit\|card\|...}.channel_code` | `channel_code` (top-level) | Moved to the top level |
| `payment_method.{ewallet\|direct_debit\|card\|...}.channel_properties` | `channel_properties` (top-level) | Moved to the top level. |
| `payment_method_id` | `payment_token_id` | **Renamed** — only present when charging a previously saved token. Prefix changed from `pm-` to `pt-` |
| *(implied by* `payment_method.reusability`*)* | `type`: `PAY` \| `PAY_AND_SAVE` \| `REUSABLE_PAYMENT_CODE` | New, explicit field. Note: v2 also had a field called `type` but on the nested `payment_method` object (meaning `EWALLET`/`CARD`/etc.) — don't confuse the two; v3's top-level `type` means something different. |
| `actions` (array of `{method, url_type, action, url}`) | `actions` (array of `{type, value, descriptor}`) | Restructured. |
| `capture_method` | `capture_method` | Unchanged (`AUTOMATIC` / `MANUAL`, cards only). |
| `initiator` (`CUSTOMER` / `MERCHANT`) | `channel_properties.card_on_file_type` | Specifically only for `channel_code` CARDS |
| `channel_properties` (top-level, used to override `payment_method`'s copy) | `channel_properties` (top-level, now the primary and only location) | No longer an "override" — it's the only place these fields live. |

### Payment Method (v2) → Payment Token (v3) — full field mapping

| v2 field (`Payment Method`) | v3 field (`Payment Token`) | Notes |
| --- | --- | --- |
| `id` (prefix `pm-`) | `payment_token_id` (prefix `pt-`) | **Renamed field and prefix.** |
| *(not present at top level — implied by channel)* | `currency` | New top-level field in v3. |
| `status` | `status` | Same general lifecycle (`REQUIRES_ACTION`, `ACTIVE`, `INACTIVE`, `EXPIRED`, `PENDING`, `FAILED`). |
| `actions` (array of `{method, url_type, action, url}`) | `actions` (array of `{type, value, descriptor}`) | Restructured. |
| `type` (`EWALLET`, `DIRECT_DEBIT`, `CARD`, `VIRTUAL_ACCOUNT`, `OVER_THE_COUNTER`, `QR_CODE`) | *(removed)* | No longer needed — `channel_code` alone determines the channel. |
| `{type}.channel_code` (e.g. `ewallet.channel_code`) | `channel_code` (top-level) | Moved to the top level. |
| `{type}.channel_properties` (e.g. `ewallet.channel_properties`) | `channel_properties` (top-level) | Moved to the top level. |
| `ewallet` / `direct_debit` / `card` / `over_the_counter` / `virtual_account` / `qr_code` (channel-specific nested object, e.g. `card.card_information`, `direct_debit.bank_account`) | Channel-specific fields returned directly on the token response object | Structure simplified — confirm exact response shape per channel via the [Get Payment Token reference](https://docs.xendit.co/apidocs/get-payment-token). |

> **Migrate existing saved Payment Methods to Payment Tokens.** You can reuse the same identifier — just swap the prefix from `pm-` to `pt-` (e.g. `pm-6ff0b6f2-f5de-457f-b08f-bc98fbae485a` becomes `pt-6ff0b6f2-f5de-457f-b08f-bc98fbae485a`). Update any stored references (database columns, customer profiles, recurring billing schedules) accordingly before switching charge calls over to `payment_token_id`.

### Webhook event mapping

| v2 event | v3 event | Notes |
| --- | --- | --- |
| `payment.succeeded` | `payment.capture` | Same purpose; payload shape updated. |
| `payment.failed` | `payment.failure` | Renamed. |
|  | `payment.authorization` | For payment with AUTHORIZED status. Supported only for CARDS with manual capture method. |
| `payment_method.activated` | `payment_token.activation` | Only fires in v3 when a token was actually requested (`PAY_AND_SAVE` or `Payment Token creation`). |
| `payment_method.expired` | `payment_token.expiry`*(removed for one-off payments.* | For explicitly deactivated tokens, check `status` via `GET /v3/payment_tokens/{id}` instead of expecting an auto-expiry webhook. |
| `payment_method.failed` | `payment_token.failure` | Renamed. |
| n/a | `payment_request.expiry` | To identify that payment request can no longer accepting payment. For example virtual account number expired, or redirection to partner is no longer valid. |

## Reference links

- [Available payment channels](https://docs.xendit.co/docs/available-payment-channels)
- [Channel Code and Channel Properties](https://doc-widget.xendit.co/channel-data-finder/)
- [Payments API v3 overview](https://docs.xendit.co/docs/payments-via-api-overview)
- [How Payments API work (concepts)](https://docs.xendit.co/docs/how-payments-api-work)
- [Create Payment Request](https://docs.xendit.co/apidocs/create-payment-request) (v3 API reference)
- [Create Payment Token](https://docs.xendit.co/apidocs/create-payment-token) (v3 API reference)
