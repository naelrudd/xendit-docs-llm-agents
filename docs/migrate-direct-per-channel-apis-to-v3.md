---
title: "Migrate Direct per-Channel APIs to Payments API v3"
slug: "migrate-direct-per-channel-apis-to-v3"
updated: 2026-07-27T06:02:57Z
published: 2026-07-27T06:02:57Z
canonical: "docs.xendit.co/migrate-direct-per-channel-apis-to-v3"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Migrate Direct per-Channel APIs to Payments API v3

This document provides guidelines on how to migrate from direct per-Channel APIs to Payments API v3. If your current integration is using per-channel endpoint such as `/credit_card_charges` , `/ewallets`, `/qr_codes`, /`callback_virtual_accounts`, it means you are still using Xendit’s direct per-channel APIs.

---

## Why you need to migrate

- **Unified Payment Architecture**
  - Direct per-Channel APIs: Required separate logic and distinct API models for different payment methods (e.g., separate implementations for Virtual Accounts, Credit Cards, E-Wallets).
  - Payments API v3: Built on an unified architecture. By integrating once with unified resources (such as `payment_request`and `payment_token`, you can enable various channels and use cases such as: one-time payments, saved payment methods, and recurring subscriptions without rewriting your integration for each channel. You build an integration which easy to scale from the start.
- **Access to All New Payment Channels & Regional Expansion**
  - Direct per-Channel APIs: Restricted to older payment channels, legacy flow types, and limited regional availability.
  - Payments API v3: Automatically unlocks access to Xendits’ newest payment channels and new features

## Overall changes

In the **Direct per-Channel APIs**, every payment method operated separately. If you wanted to accept Virtual Accounts, E-Wallets, Cards, and QR codes, your had to maintain 4 distinct endpoints (`/callback_virtual_accounts`, `/ewallets/charges`, `/credit_card_charges`, `/qr_codes`), each with different payload shapes, different header parameters, and separate status lifecycle conventions.

In **Payments API v3**, a **Payment Request** (`/v3/payment_requests`) acts as the single core engine for all payment channels. Instead of picking a channel-specific API route, you send every transaction to one unified endpoint and simply pass a `channel_code` and `channel_properties`. You instruct Xendit what you intend to do using the `type` parameter (`PAY`, `PAY_AND_SAVE`, or `REUSABLE_PAYMENT_CODE`), and tokenization or saving customer payment details only happens when you explicitly tell the API to do so.

| Channel | Use case / flow | Legacy flow | v3 flow |
| --- | --- | --- | --- |
| eWallets | One-time payment | `POST /ewallets` with `checkout_method: ` `ONE_TIME_PAYMENT` | `POST /v3/payment_requests` with `type: "PAY"` |
| eWallets | Tokenize + charge for repeat use | `POST /ewallets`with `checkout_method: TOKENIZED_PAYMENT` | `POST /v3/payment_requests` with `type: "PAY_AND_SAVE"` |
| eWallets | Repeat/recurring charge using a saved wallet | Re-use the linked payment method on a subsequent `POST /ewallets call` | `POST /v3/payment_requests` with `type: "PAY" + payment_token_id` |
| QR Codes | One-time payment | `POST /qr_codes` with `type: "DYNAMIC"` | `POST /v3/payment_requests` with `type: "PAY"` |
| QR Codes | Reusable/open payment code (any amount, multiple payments) | `POST /qr_codes `with `type: "STATIC"` | `POST /v3/payment_requests ` with `type: "REUSABLE_PAYMENT_CODE"` |
| Direct Debit | Account linking (one-time setup, incl. OTP) | `POST /linked_account_tokens` → validate_otp → `POST /payment_methods` | `POST /v3/payment_tokens` with `type: "SAVE"` |
| Direct Debit | One-time payment against a linked account | `POST /direct_debits` with `payment_method_id` | `POST /v3/payment_requests ` with `type: "PAY" + payment_token_id` |
| Direct Debit | Repeat/recurring charge | Repeated `POST /direct_debits calls` reusing the same `payment_method_id` | Repeated `POST /v3/payment_requests calls ` reusing the same `payment_token_id` |
| Virtual Accounts | One-time payment | `POST /callback_virtual_accounts `with `is_closed: true` | `POST /v3/payment_requests` with `type: "PAY"` |
| Virtual Accounts | Reusable/open VA (top-up style, any amount, multiple payments) | `POST /callback_virtual_accounts` with `is_closed: false` | `POST /v3/payment_requests` with `type: "REUSABLE_PAYMENT_CODE"` |
| Retail Outlets (ID & PH) | Reusable payment code (customer pays at counter, any time before expiry) | `POST /fixed_payment_code` or `POST /payment_codes` | `POST /v3/payment_requests` with `type: "REUSABLE_PAYMENT_CODE"` |
| Cards | One-time payment, full PAN entered directly (no stored token) | `POST /credit_card_tokens (single-use)` → `POST /credit_card_charges` | `POST /v3/payment_requests` with `type: "PAY" and full card details inline in channel_properties.card_details — no separate tokenization call needed` |
| Cards | Tokenization for future reuse (multiple-use token) | `POST /credit_card_tokens` with `is_multiple_use: true` | `POST /v3/payment_tokens` with `type: "SAVE", or type: "PAY_AND_SAVE" `on the Payment Request if charging in the same call |

## Endpoint Mapping

| Channel | Direct per-Channel | v3 endpoint | v3 type | Legacy ID prefix → v3 |
| --- | --- | --- | --- | --- |
| eWallets | `POST /ewallets` | `POST /v3/payment_requests` | `PAY` or `PAY_AND_SAVE` | ewc- → py- |
| QR Codes | `POST /qr_codes` | `POST /v3/payment_requests` | `PAY` (for dynamic QR) or `REUSABLE_PAYMENT_CODE` (for static QR) | qr_ → py- |
| Direct Debit | `POST /linked_account_tokens, ` `POST /payment_methods, POST /direct_debits` | `POST /v3/payment_tokens (linking) + POST /v3/payment_requests (charging)` | `POST Payment Token` for account linking or `PAY` | lat-/pm- → pt- dd- → py- |
| Virtual Accounts | `POST /callback_virtual_accounts` | `POST /v3/payment_requests` | `PAY` (for closed/fixed amount) or `REUSABLE_PAYMENT_CODE` (for open VA number) | numeric Mongo-style ID → py- |
| Retail Outlets (ID) | `POST /fixed_payment_code` | `POST /v3/payment_requests` | `REUSABLE_PAYMENT_CODE` | numeric Mongo-style ID → py- |
| Retail Outlets (PH) | `POST /payment_codes` | `POST /v3/payment_requests` | `REUSABLE_PAYMENT_CODE` | pymt-/generated ID → py- |
| Credit Cards | `POST /credit_card_tokens, POST /credit_card_charges` | `POST /v3/payment_tokens (tokenize) + POST /v3/payment_requests` (charge) | Collect card information` SAVE` (token) + `PAY/PAY_AND_SAVE` (charge) | token ID → pt- charge ID → py- |

---

## Detailed Changes

### eWallets

Legacy `POST /ewallets` was already fairly close in shape to v3 — this is generally the most straightforward channel to migrate.

**Legacy API**

```json
// Legacy — POST https://api.xendit.co/ewallets
{
  "reference_id": "order-id-123",
  "currency": "IDR",
  "amount": 25000,
  "checkout_method": "ONE_TIME_PAYMENT",
  "channel_code": "ID_DANA",
  "channel_properties": {
    "success_redirect_url": "https://redirect.me/payment"
  }
}
```

**Payments API v3**

```json
// v3 — POST https://api.xendit.co/v3/payment_requests
// header: api-version: 2024-11-11
{
  "reference_id": "order-id-123",
  "type": "PAY",
  "country": "ID",
  "currency": "IDR",
  "request_amount": 25000,
  "channel_code": "DANA",
  "channel_properties": {
    "success_return_url": "https://redirect.me/payment"
  }
```

> [!NOTE]
> Notes:
> 
> - `checkout_method: ONE_TIME_PAYMENT` →` type: "PAY" `(use `PAY_AND_SAVE` if you also want to save the wallet for reuse, replacing legacy `checkout_method: TOKENIZED_PAYMENT`

### QR Codes

**Legacy API**

```json
// Legacy — POST https://api.xendit.co/qr_codes
{
  "reference_id": "testing_id_1669118631",
  "type": "DYNAMIC",
  "currency": "IDR",
  "channel_code": "ID_DANA",
  "amount": 1000,
  "callback_url": "https://yourwebsite.com/callback"
}
```

**Payments API v3**

```json
// v3 — POST https://api.xendit.co/v3/payment_requests
// header: api-version: 2024-11-11
{
  "reference_id": "testing_id_1669118631",
  "type": "PAY",
  "country": "ID",
  "currency": "IDR",
  "request_amount": 1000,
  "channel_code": "QRIS"
}
```

### Direct Debit

Direct Debit API integration was multi-step: link the account, save it as a Payment Method, then charge it. v3 keeps a similar shape but flattens the objects involved.

**Legacy API**

```json
// Legacy step 1 — POST https://api.xendit.co/linked_account_tokens
{
  "customer_id": "cust-239c16f4-866d-43e8-9341-7badafbc019f",
  "channel_code": "DC_BRI",
  "properties": { "account_mobile_number": "+62812345678", "card_last_four": "8888" }
}
// Legacy step 2 — POST https://api.xendit.co/payment_methods
{
  "customer_id": "cust-239c16f4-866d-43e8-9341-7badafbc019f",
  "type": "DEBIT_CARD",
  "properties": { "id": "la-fac7e744-ab40-4100-a447-cbbb16f29ded" }
}
// Legacy step 3 — POST https://api.xendit.co/direct_debits
{
  "reference_id": "direct-debit-ref-1594718940",
  "payment_method_id": "pm-b6116aea-8c23-42d0-a1e6-33227b52fccd",
  "currency": "IDR",
  "amount": 60000,
  "enable_otp": true
}
```

**Payments API v3**

```json
// v3 — POST https://api.xendit.co/v3/payment_tokens (linking/saving)
// header: api-version: 2024-11-11
{
  "reference_id": "token_bri_user_001",
  "country": "ID",
  "currency": "IDR",
  "channel_code": "BRI_DIRECT_DEBIT",
  "customer": {
    "reference_id": "cust_user_001",
    "type": "INDIVIDUAL",
    "individual_detail": {
      "given_names": "John",
      "surname": "Doe"
    },
    "email": "johndoe@example.com",
    "mobile_number": "+628123456789"
  },
  "channel_properties": {
    "card_last_four_digits": "1234",
    "email": "johndoe@example.com",
    "mobile_number": "+628123456789",
    "success_return_url": "https://yourwebsite.com/save-payment/success",
    "failure_return_url": "https://yourwebsite.com/save-payment/failure"
  }
}
// v3 — POST https://api.xendit.co/v3/payment_requests (charging)
// header: api-version: 2024-11-11
{
  "reference_id": "req_bri_charge_002",
  "type": "PAY",
  "payment_token_id": "pt-12345678-abcd-1234-abcd-1234567890ab",
  "country": "ID",
  "currency": "IDR",
  "amount": 100000,
  "channel_properties": {
    "account_mobile_number": "+628123456789",
    "success_return_url": "https://yourwebsite.com/success",
    "failure_return_url": "https://yourwebsite.com/failure"
  }
}
```

### Virtual Accounts

**Legacy API**

```json
// Legacy — POST https://api.xendit.co/callback_virtual_accounts
{
  "external_id": "ORDER-2020-123",
  "bank_code": "BCA",
  "name": "John Doe",
  "is_closed": true,
  "expected_amount": 3000000,
  "is_single_use": true
}
```

**Payments API v3**

```json
// v3 — POST https://api.xendit.co/v3/payment_requests
// header: api-version: 2024-11-11
{
  "reference_id": "order_bca_va_12345",
  "type": "PAY",
  "country": "ID",
  "currency": "IDR",
  "request_amount": 3000000,
  "channel_code": "BCA_VIRTUAL_ACCOUNT",
  "channel_properties": {
    "expires_at": "2026-07-23T11:00:00Z",
    "display_name": "John Doe",
    "virtual_account_number": "886969696988",
    "success_return_url": "https://xendit.co/success"
  }
}
```

### Retail Outlets — Indonesia (OTC ID)

**Legacy API**

```json
// Legacy — POST https://api.xendit.co/fixed_payment_code
{
  "external_id": "FPC-1619132067",
  "retail_outlet_name": "ALFAMART",
  "name": "John Doe",
  "expected_amount": 25000
}
```

**Payments API v3**

```json
// v3 — POST https://api.xendit.co/v3/payment_requests
// header: api-version: 2024-11-11
{
  "reference_id": "FPC-1619132067",
  "type": "REUSABLE_PAYMENT_CODE",
  "country": "ID",
  "currency": "IDR",
  "request_amount": 25000,
  "channel_code": "ALFAMART",
  "channel_properties": {
    "customer_name": "John Doe"
  }
}
```

> [!NOTE]
> Notes
> 
> - use `type: "REUSABLE_PAYMENT_CODE"` since OTC codes accept payment at any point before expiry (matching legacy behavior even for is_single_use: true codes)
> - the returned payment_code/prefix combination moves into actions[].value with a` PRESENT_TO_CUSTOMER` action.

### Retail Outlets — Philippines (OTC PH)

**Legacy API**

```json
// Legacy — POST https://api.xendit.co/payment_codes
{
  "reference_id": "123",
  "channel_code": "7ELEVEN",
  "customer_name": "John Doe",
  "amount": 50,
  "currency": "PHP"
}
```

**Payments API v3**

```json
// v3 — POST https://api.xendit.co/v3/payment_requests
// header: api-version: 2024-11-11
{
  "reference_id": "123",
  "type": "REUSABLE_PAYMENT_CODE",
  "country": "PH",
  "currency": "PHP",
  "request_amount": 50,
  "channel_code": "7ELEVEN_CLIQQ",
  "channel_properties": {
    "expires_at" : "2024-06-01T11:00:00Z",
    "payer_name" : "John Doe",
    "payment_code" : "A1B2C3"
  }
}
```

### Credit Cards

The migration from `Xendit.JS` to `Components `is the most involved migration, previously handling tokenization, authorization, capture and charge on separate endpoints, now moving to 1 single endpoint

You can access [Xendit Payment Components](/v1/docs/components-overview#high-level-flow) to see the guidelines to implement Xendit Payment Components

#### For the Xendit.JS Integration use case

| Actions | Direct per-Channel API (Legacy) | Sessions |
| --- | --- | --- |
| Collecting card information | Use client-side integration (Xendit.js) to collect card details and perform tokenizations then sent the resulting token_id to merchant’s backend server to create a charge | Merchant can collect and capture payments using Xendit Payment Components Merchants’s server first creates a Payment Session (define the flow that you want either doing one time payment (PAY) or PAY_AND_SAVE), passes the components_sdk_key to the frontend, for front end to initialize the Xendit UI components |
| Perform charge to cards | Use `POST https://api.xendit.co/credit_card_charges` |

**Full PAN Integrations (PCI-DSS Level 1 Compliant merchants)**

#### Actions: Perform charge to cards

**Legacy**

Merchant send `POST https://api.xendit.co/credit_card_charges`

```json
{
  "external_id": "order_001",
  "amount": 250000,
  "card_data": {
    "account_number": "4000000000001091",
    "exp_month": "12",
    "exp_year": "2028",
    "card_cvn": "123"
  },
  "capture": true,
  "descriptor": "MERCHANT STORE"
}
```

**Payments API v3**

Merchant send `POST https://api.xendit.co/v3/payment_requests`

```json
{
  "reference_id": "order_001",
  "type": "PAY",
  "country": "ID",
  "currency": "IDR",
  "amount": 250000,
  "capture_method": "AUTOMATIC",
  "channel_code": "CARDS",
  "channel_properties": {
    "card_details": {
      "card_number": "4000000000001091",
      "expiry_month": "12",
      "expiry_year": "2028",
      "cvn": "123",
      "cardholder_first_name": "John",
      "cardholder_last_name": "Doe"
    },
    "success_return_url": "https://yourwebsite.com/checkout/success",
    "failure_return_url": "https://yourwebsite.com/checkout/failure"
  }
}
```

#### Actions: Perform 0-auth

**Legacy**

Merchant send `POST https://api.xendit.co/credit_card_charges`

```json
{
  "external_id": "order_001",
  "amount": 0,
  "card_data": {
    "account_number": "4000000000001091",
    "exp_month": "12",
    "exp_year": "2028",
    "card_cvn": "123"
  },
  "capture": true,
  "descriptor": "MERCHANT STORE"
}
```

**Payments API v3**

Merchant send `POST https://api.xendit.co/v3/payment_requests`

```json
{
  "reference_id": "verify_card_cust_789",
  "type": "VERIFY_PAYMENT_METHOD",
  "country": "ID",
  "currency": "IDR",
  "customer_id": "cust-abc123",
  "channel_code": "CARDS",
  "channel_properties": {
    "card_details": {
      "cvn": "123",
      "card_number": "4000000000001091",
      "expiry_year": "2027",
      "expiry_month": "09",
      "cardholder_first_name": "Budi",
      "cardholder_last_name": "Santoso",
      "cardholder_email": "budi@example.com",
      "cardholder_phone_number": "+628123456789"
    },
    "card_on_file_type": "MERCHANT_UNSCHEDULED"
    "success_return_url": "https://merchant.co/verify/success",
    "failure_return_url": "https://merchant.co/verify/failure"
  },
  "description": "Card verification — no charge"
}
```

For further details, can access [Payment Verify Method](/v1/docs/card-verification#payment-method-verification-verifypaymentmethod)

> [!NOTE]
> Notes:
> 
> - Existing card `token_id` from legacy API needs to be migrated to `payment_token_id` in Payments API v3
> - Contact our support help@xendit.co for migration assistance.

## Field Mappings

### eWallets

| Legacy field (/ewallets) | v3 field (/v3/payment_requests) | Notes |
| --- | --- | --- |
| `id (prefix ewc-)` | `payment_id (prefix py-)` | Renamed prefix. |
| `reference_id` | `reference_id` | Unchanged. |
| `currency` | `currency` | Unchanged. |
| `amount` | `request_amount` | Renamed. |
| checkout_method (`ONE_TIME_PAYMENT` / `TOKENIZED_PAYMENT`) | `type` (`PAY / PAY_AND_SAVE`) | Renamed and re-scoped |
| `channel_code` (e.g. `ID_DANA`) | `channel_code` (e.g. `DANA`) | Country prefix generally dropped |
| `channel_properties.success_redirect_url` | `channel_properties.success_return_url` | Renamed. |
| `channel_properties.failure_redirect_url` | `channel_properties.failure_return_url` | Renamed. |
| `charge_amount` / `capture_amount` (response) | `request_amount&nbsp;`/ `captured amount` surfaced via status | Consolidated. |
| `actions.mobile_web_checkout_url` / `desktop_web_checkout_url` / `mobile_deeplink_checkout_url` | `actions[].type: "REDIRECT_CUSTOMER"`, value, descriptor | Standardized |
| `customer_id` | `customer_id` | Unchanged. |
| `payment_method_id` | `payment_token_id` | Renamed — only present for tokenized/repeat charges. |
| n/a | `country` | New, required in v3. |

### QR Codes

| Legacy field (/qr_codes) | v3 field (/v3/payment_requests) | Notes |
| --- | --- | --- |
| `id (prefix qr_)` | `payment_id (prefix py-)` | Renamed prefix. |
| `reference_id` | `reference_id` | Unchanged. |
| `type (DYNAMIC / STATIC)` | `type (PAY / REUSABLE_PAYMENT_CODE)` | Renamed and re-scoped |
| `currency` | `currency` | Unchanged. |
| `amount` | `request_amount` | Renamed; omitted entirely for REUSABLE_PAYMENT_CODE. |
| `channel_code` | `channel_code` (e.g. QRIS) | Verify exact value |
| `callback_url` | *(removed — configure webhook URL in Dashboard)* | No longer a per-request field. |
| `expires_at` | `channel_properties.expires_at&nbsp;`or`request-level equivalent` | Confirm current field location via API reference. |
| `qr_string` (response) | `actions[].value (with descriptor indicating QR string)` | Standardized |
| `description` | `description` | Unchanged. |
| `metadata` | `metadata` | Unchanged. |

### Direct Debit

| Legacy field | v3 field | Notes |
| --- | --- | --- |
| `id`(prefix ddpy-) | `payment_id`(prefix py-) | Format changed |
| `POST /linked_account_tokens + POST /payment_methods` (two calls) | `POST /v3/payment_tokens` (one call) | Collapsed |
| `customer_id` | `customer_id` | Unchanged. |
| `channel_code` (e.g. DC_BRI) | `channel_code` (e.g. BRI) | Using exact value |
| `properties` (linked account object) | `channel_properties` | Flattened/renamed. |
| Payment Method id (prefix pm-) | payment_token_id (prefix pt-) | Renamed. |
| `POST /direct_debits: reference_id` | `reference_id` | Unchanged. |
| `payment_method_id` | `payment_token_id` | Renamed. |
| `currency` | `currency` | Unchanged. |
| `amount` | `request_amount` | Renamed. |
| enable_otp | Surfaced via actions[] | No longer a dedicated flag |
| `callback_url` | *(removed — configure webhook URL in Dashboard)* | No longer a per-request field. |
| POST /direct_debits/{id}/validate_otp | Handled via the actions[] flow on the Payment Request | Restructured |

### Virtual Accounts

| Legacy field (/callback_virtual_accounts) | v3 field (/v3/payment_requests) | Notes |
| --- | --- | --- |
| `external_id` | `reference_id` | Renamed. |
| `bank_code` | `channel_code` | Renamed |
| `name` | `channel_properties.display_name` | Moved. |
| `expected_amount` | `request_amount` | Renamed; omitted for REUSABLE_PAYMENT_CODE. |
| `is_closed` + `is_single_use` | `type` (`PAY` for closed/single-use, `REUSABLE_PAYMENT_CODE` for open) | Consolidated into one field |
| `expiration_date` | Request-level expiry equivalent (confirm current field via API reference) | Renamed/restructured. |
| `virtual_account_number&nbsp;`(response) | actions[].value (with `PRESENT_TO_CUSTOMER`) | Standardized |
| `id` (numeric Mongo-style) | `id` (prefix pr-) | Format changed. |
| `payment_id` | `payment_id` (prefix py-) | Format changed. |

### Retail Outlets — Indonesia (OTC ID)

| Legacy field (/fixed_payment_code) | v3 field (/v3/payment_requests) | Notes |
| --- | --- | --- |
| `external_id` | `reference_id` | Renamed. |
| `retail_outlet_name` | `channel_code` | Renamed. |
| `name` | `channel_properties.customer_name` | Moved. |
| `expected_amount` | `request_amount` | Renamed. |
| `is_single_use` | *(implied — use* `REUSABLE_PAYMENT_CODE` *type regardless)* |  |
| `expiration_date` | `channel_properties.expires_at` | Renamed/restructured. |
| `payment_code` + `prefix` (response) | actions[].value (with `PRESENT_TO_CUSTOMER`) | Standardized |
| `id` (numeric Mongo-style) / `payment_id` | payment_id (prefix py-) | Format changed. |
| `fixed_payment_code_id` | `id` (prefix pr-) | Format changed. |

### Retail Outlets — Philippines (OTC PH)

| Legacy field (/payment_codes) | v3 field (/v3/payment_requests) | Notes |
| --- | --- | --- |
| `reference_id` | `reference_id` | Unchanged. |
| `channel_code` | `channel_code` | Unchanged. |
| `customer_name` | `channel_properties.payer_name` | Moved under channel_properties. |
| `amount` | `request_amount` | Renamed. |
| `currency` | `currency` | Unchanged. |
| `market` | `country` | Renamed. |
| `payment_code` (response) | actions[].value (with `PRESENT_TO_CUSTOMER`) | Standardized |
| `id`(prefix pymt-) | `payment_id` (prefix py-) | Format changed |
| payment_code_id | `id`(prefix pr-) |  |

### Credit Cards

| Legacy field | v3 field | Notes |
| --- | --- | --- |
| `card_data.account_number` | `channel_properties.card_details.card_number` | Moved under Payment Request/Token channel_properties. |
| `card_data.exp_month` | `channel_properties.card_details.expiry_month` | Renamed. |
| `card_data.exp_year` | `channel_properties.card_details.expiry_year` | Renamed. |
| `card_data.cvn` | `channel_properties.card_details.cvn` | Renamed. |
| `is_multiple_use` | `type: "PAY_AND_SAVE"` on the Payment Request, or a standalone `POST /v3/payment_tokens` | Re-scoped |
| `should_authenticate` | `channel_properties.skip_three_ds` | Renamed, boolean sense inverted |
| `external_id` | `reference_id` | Renamed. |
| `amount` | `request_amount` | Renamed. |
| `mid_label` | `channel_properties.mid_label` | Moved under channel_properties. |
| Legacy Authorization + Capture Charge (two calls) | `capture_method: "MANUAL"` on a single Payment Request + capture call using `/v3/payments/{payment_id}/capture` |  |
| `id` (charge/token ID) | `payment_id` (prefix py-) / `payment_token_id` (prefix pt-) | Format changed. |
| Recurring set up | in `credential_on_file` object: ```json "credential_on_file": { "type": "RECURRING", "sequence": "SUBSEQUENT" "network_transaction_id": "1251251511" } ``` JSON | Moved to [channel_properties](https://doc-widget.xendit.co/channel-data-finder/): ```json "channel_properties": { "card_on_file_type": "RECURRING", "transaction_sequence":"SUBSEQUENT", "network_transaction_id": "1251251511" } ``` JSON Note: The field names remain the same. |

## Reference Links

- [Available payment channels](https://docs.xendit.co/docs/available-payment-channels)
- [Channel Code and Channel Properties](https://doc-widget.xendit.co/channel-data-finder/)
- [Payments API v3 overview](https://docs.xendit.co/docs/payments-via-api-overview)
- [How Payments API work (concepts)](https://docs.xendit.co/docs/how-payments-api-work)
- [Create Payment Request](https://docs.xendit.co/apidocs/create-payment-request) (v3 API reference)
- [Create Payment Token](https://docs.xendit.co/apidocs/create-payment-token) (v3 API reference)
