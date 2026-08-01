---
title: "Migrate from (legacy) Payment Links/Invoice to Payment Session"
slug: "migrate-to-payment-session"
updated: 2026-07-27T05:38:39Z
published: 2026-07-27T05:38:39Z
canonical: "docs.xendit.co/migrate-to-payment-session"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Migrate from (legacy) Payment Links/Invoice to Payment Session

This guide explains how to migrate existing Xendit legacy Payment Link integrations `/v2/invoices)` to the Payment Sessions API `/sessions`) using `mode: PAYMENT_LINK`.

> Scoped to merchants using the Xendit-hosted checkout flow. If you plan to build your own checkout UI instead of using the Xendit-hosted page, see the [Xendit Components integration](/v1/docs/components-overview#serverside-responsibilities) guide `mode: COMPONENTS`) instead — this doc focuses on the drop-in hosted-page replacement.

## Terminology

- **Legacy Payment Link**: It’s referring to the legacy payment link (previously called Invoice)
- **Payment Link** (New): It’s referring to the new Payment Sessions API with `mode: PAYMENT LINK`. It might be interchangeable terms with the Payment Sessions on this page

## Why you should migrate

- **One integration for every use case.** Legacy Payment Link only ever does one thing — a one-time payment link. Payment Sessions lets you declare a `session_type` `PAY`, `SAVE`, or `SUBSCRIPTION`) and reuse the same endpoint and hosted-page experience for one-off payments, saving a payment method, and recurring billing — instead of stitching together separate legacy products (Invoice, Payment Method, Recurring).
- **Full channel and region coverage**. Legacy Payment Link is capped at a limited, older set of payment channels and specific regions. Payment Sessions gives you access to every channel Xendit supports, in every supported country, through the same `allowed_payment_channels` field.
- **Visibility into failed attempts**. Legacy Payment Link never tells you when a customer tried and failed to pay — you only ever hear about success or expiry. Payment Sessions (via the underlying Payment v3 object) fires `payment.failure` for every failed attempt, which materially improves your reconciliation and drop-off analytics.
- **Save-and-charge-later, done right.** In the legacy payment link, saving a payment method for reuse required a separate Payment Method integration and non existent flow. `allow_save_payment_method` `DISABLED` / `OPTIONAL` / `FORCED`) is a native option on a `PAY` session, and `SAVE` to store the token for future use.

### Overal changes

The change is not just a new URL — it's a different model. In the legacy payment link you "create an invoice" and get back a `PENDING` object that becomes `PAID`. In the new session you "create a Session" and explicitly declare what you want the session to accomplish `session_type`) and *how the customer should complete it* (`mode`).

Before touching any code, a few things your team should know going in:

- **This is not a drop-in field rename**. Some concepts don't map 1:1 — `fees` becomes a line item of `type: FEE` inside items rather than its own field.
- `amount` **behaves differently depending on** `session_type`**.** For `PAY` and `SUBSCRIPTION`, `amount` must be greater than zero. For `SAVE`, amount must be exactly 0. A validation error `INVALID_AMOUNT`) will reject anything else — this trips up teams that copy a `PAY` payload to build a `SAVE` request.
- **Webhook payloads and event names both changed.** This isn't just `Invoice paid` → `Payment Session Completed` — the new model also separates the session-lifecycle webhook from the underlying Payment/Payment Token status webhooks. Don't assume one webhook tells you everything; see Webhook event mapping below.
- `customer` **is now closer to mandatory**. Unlike legacy payment link (where `payer_email` was optional and loosely structured), the Session API requires a `customer` object or `customer_id` whenever session_type is `SAVE`, `allow_save_payment_method` is `FORCED`/ `OPTIONAL`. Plan your data collection accordingly.
- `mode` **is a new, required concept.** Legacy Payment Link had no equivalent field — it was always a hosted redirect. Payment Sessions require you to explicitly declare `mode: PAYMENT_LINK` (hosted redirect, same UX as legacy) or `mode: COMPONENTS` (embedded fields via SDK).

| Area | Legacy Payment Link | Payment Session |
| --- | --- | --- |
| Core object | Invoice | Payment Session (backed by Payment API v3 principle) |
| Payment flows supported | One-time payment only | `PAY` (one-time), `SAVE` (store payment method), `SUBSCRIPTION` (recurring) in one integration |
| Channel / region availability | Limited to legacy channels and specific regions | All channels and regions Xendit supports |
| Failed-attempt visibility | None — silent until success or expiry | `payment.failure` webhook fires per failed attempt |
| Saving a payment method | None — was only supported for one time payment | Native via `SAVE` session type or `allow_save_payment_method` on PAY |
| Recurring billing | Not supported by this product | Native via `SUBSCRIPTION` session type |
| Primary Identifier | `id` (Invoice ID) | `payment_session_id` |

## Detailed changes

### Endpoint URLs

| Feature | Legacy Payment Link | Payment Session |
| --- | --- | --- |
| Create | `POST /v2/invoices` | `POST /sessions` |
| Get status | `GET /v2/invoices/{id}` | `GET /sessions/{payment_session_id}` |

### Declaring intent: `session_type` (new, explicit field)

Legacy Payment Link had no equivalent — every Invoice implied the same one-time-payment intent. Payment Sessions requires you to declare it up front:

| session_type | What it does | Typical use case |
| --- | --- | --- |
| `PAY` | Collects exactly one payment. Optionally saves the payment method if allow_save_payment_method is set. | Standard checkout — the direct replacement for a legacy payment link. |
| `SAVE` | Collects no payment (amount must be 0); only stores a payment method as a Payment Token. | Onboarding / registration flows where you need to store a card or account before any charge occurs. |
| `SUBSCRIPTION` | Registers the customer onto a recurring billing schedule (interval, total_recurrence, retry rules). | Recurring plans — previously required a separate product; now unified into the same endpoint to display the registration |

`allow_save_payment_method` `DISABLED` / `OPTIONAL` / `FORCED`) is a modifier on `PAY`, not a separate flow — this is the "pay and save" pattern that legacy Payment Link couldn't express in a single call.

**Session PAY**

```json
{
  "reference_id": "order_12345_PAY",
  "session_type": "PAY",
  "mode": "PAYMENT_LINK",
  "amount": 10000,
  "currency": "PHP",
  "country": "PH",
  "customer": {
    "reference_id": "cust_Lorem_Ipsum",
    "type": "INDIVIDUAL",
    "email": "test@yourdomain.com",
    "mobile_number": "+6212345678",
    "individual_detail": {
      "given_names": "Lorem",
      "surname": "Ipsum"
    }
  },
  "items": [
    {
      "reference_id": "item_001",
      "name": "Clothes",
      "type": "PHYSICAL_PRODUCT",
      "category": "CLOTHES",
      "net_unit_amount": 5000,
      "quantity": 1,
      "currency": "PHP"
    },
    {
      "reference_id": "item_002",
      "name": "Pants",
      "type": "PHYSICAL_PRODUCT",
      "category": "CLOTHES",
      "net_unit_amount": 5000,
      "quantity": 1,
      "currency": "PHP"
    }
  ],
  "capture_method": "AUTOMATIC",
  "description": "Sample one-time payment using Payment Session",
  "success_return_url": "https://yourcompany.com/success",
  "cancel_return_url": "https://yourcompany.com/cancel"
}
```

**Legacy Payment Link**

```json
{
          "external_id": "payment-link-example",
          "amount": 510000,
          "description": "Invoice Demo #123",
          "invoice_duration": 86400,
          "customer": {
            "given_names": "John",
            "surname": "Doe",
            "email": "johndoe@example.com",
            "mobile_number": "+6287774441111",
            "addresses": [
              {
                "city": "Jakarta Selatan",
                "country": "Indonesia",
                "postal_code": "12345",
                "state": "Daerah Khusus Ibukota Jakarta",
                "street_line1": "Jalan Makan",
                "street_line2": "Kecamatan Kebayoran Baru"
              }
            ]
          },
          "success_redirect_url": "https://www.google.com",
          "failure_redirect_url": "https://www.google.com",
          "currency": "IDR",
          "items": [
            {
              "name": "Air Conditioner",
              "quantity": 1,
              "price": 100000,
              "category": "Electronic",
              "url": "https://yourcompany.com/example_item"
            }
          ],
          "fees": [
            {
              "type": "ADMIN",
              "value": 5000
            }
          ],
          "payment_methods": [
            "CREDIT_CARD"
          ]
        }
```

### Parameter / field mapping

| Legacy Payment Link | Payment Session | Notes |
| --- | --- | --- |
| `external_id` | `reference_id` | **Renamed.** |
| `payer_email` / `customer` | `customer` object or `customer_id` | Structured customer object; can be created up-front via the [Customer API](/v1-api/apidocs/create-customer-request) and referenced by `customer_id`. |
| `invoice_duration` | `expires_at` | Now a specific ISO 8601 timestamp rather than a duration in seconds. |
| `payment_methods` | `allowed_payment_channels` | Defines which channels appear on the hosted page. Omit to show all activated channels. |
| `mid_label` | `channel_properties.cards.mid_label` | Stored under the channel properties for cards |
| `should_authenticate_credit_card` | `channel_properties.cards.skip_three_ds` | Stored under the channel properties for cards |
| `fees` | `items` with `type: FEE` | Fees are now modeled as line items rather than a dedicated field. |
| `id` | `payment_session_id` | New primary identifier, prefixed `ps-` |

### Status lifecycle

| Legacy Payment Link Status | Payment Session Status | Notes |
| --- | --- | --- |
| `PENDING` | `ACTIVE` | Awaiting customer action. |
| `PAID` / `SETTLED` | `COMPLETED` | Session's underlying Payment succeeded; `payment_id` or `payment_token_id` is populated on the session object. |
| `EXPIRED` | `EXPIRED` | Unchanged |
|  | `CANCELED` | New: no direct legacy equivalent (e.g. customer or merchant explicitly aborted the flow). |

> **Rule of thumb:** Treat the Session's own status field as the lifecycle source of truth (did the customer complete checkout), and treat the underlying Payment object's status as the transaction source of truth (did the money move) — the same separation-of-concerns pattern used in the [v2→v3 Payment API migration](/v1/docs/migrate-payment-api-v2-to-v3).

### Webhook event mapping

[Adjust the webhook URL](/v1/docs/integration-setup-3#3-set-up-your-webhooks) to receive the information upon your payment sessions lifecycle.

**Legacy Payment Link API**

- `Invoices paid`: Xendit will send webhook for paid invoices
- `Invoice expired`: Xendit will send webhook for expired invoices

**Payment Sessions API**

- `Payment Session Completed`: Xendit will send webhook when the payment session has completed
- `Payment Session Expired`: Xendit will send webhook when the payment session has expired

#### Optional but recommended

**Payment v3 – Payment Status**

Xendit sends webhooks whenever there is a status update on a Payment object.

- `payment.succeeded` Identifies successful payments and includes full payment details.
- `payment.failure`Identifies failed payment attempts, including failures that occur on the Xendit hosted page.

**Payment Tokens v3 – Payment Token Status**

Xendit sends webhooks whenever there is a status update on a Payment Token object.

This applies to `PAY` sessions with payment method saving enabled and `SAVE` **session types.**

## Reference links

- [Create a Session](/v1-api/apidocs/create-session)
- [How Payment Session work](/v1/docs/how-payment-sessions-work)
- [How Payments API work (concepts)](/v1/docs/how-payments-api-work)
