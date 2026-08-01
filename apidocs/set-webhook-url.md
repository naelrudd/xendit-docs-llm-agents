---
title: "Set webhook URL"
slug: "set-webhook-url"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/set-webhook-url"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Set webhook URL

Post/callback_urls/{type}

> ℹ️ Info
> 
> 
> This API can only be used to set Webhook URLs for our [Legacy Payment and Payout APIs](https://archive.developers.xendit.co/api-reference/#payments-api). For the latest APIs, as a Master Account, you can set up your sub-accounts to send webhooks for their activities to your configured URLs. Otherwise you may set the webhook URLs from each sub-account's Settings page in their Dashboards.

The following can be used in the `type` path parameter:

Money-In

- `invoice`: Xendit notifies your system when Invoice has been paid or expired.
- `fva_status`: Xendit notifies your system when Virtual Account has been created or updated successfully. Support: Indonesia only 🇲🇨
- `fva_paid`: Xendit notifies your system when Virtual Account has been paid successfully. Support: Indonesia only 🇲🇨
- `ro_fpc_paid`: Xendit notifies your system when Retail Outlet payment code (Alfamart/Indomaret) in Indonesia has been paid successfully. Support: Indonesia only 🇲🇨
- `regional_ro_paid`: Xendit notifies your system when Over-the-Counter payment code (7 Eleven, Cebuana, ECPay) in Philippines has been paid successfully. Support: Philippines only 🇵🇭
- `ewallet`: New eWallet type to receive charge and other eWallet events across eWallets channels from /ewallets/charges API.
- `payment_method`: Xendit notifies your system when payment method is expiring and/or has expired. Payment Method is a mandatory step to abstract Debit Card/Bank Account for Direct Debit transactions.
- `payment_method_v2`: Xendit notifies your system when payment method V2 is expiring and/or has activated or expired. Learn more about Payment Method V2 here.
- `direct_debit`: A Direct Debit payment event will be sent to your system for any successful transactions. Use direct_debit type to receive Direct Debit payment event via webhook.
- `qr_code`: Xendit notifies your system when QR payment has been made or QR refund has been completed. This field is only supported for qr_codes API version 2022-07-31.
- `recurring`: Xendit notifies your system when Subscription plan has been activated/inactivated, cycle created/succeeded/retrying/failed, or force attempt failed.
- `payment_succeeded`: Xendit notifies your system when a payment has been successfully confirmed or received from the partner channel (Only for payments initiated via new Payments API). Support: All businesses
- `payment_awaiting_capture`: Xendit notifies your system when a payment request with capture_method set to MANUAL has been intialized and a call to the Payment Capture API needed to complete the payment. Support: All businesses
- `payment_pending`: Xendit notifies your system when a payment is being processed by the partner channel awaiting for the terminal status of it (Only for payments initiated via new Payments API). Support: All businesses
- `payment_failed`: Xendit notifies your system when a pending payment has failed (Only for payments initiated via new Payments API). Support: All businesses
- `capture_succeeded`: Xendit notifies your system when a manual capture via the Payment Capture API has succeeded. Support: All businesses
- `capture_failed`: Xendit notifies your system when a manual capture via the Payment Capture API has Failed. Support: All businesses
- `payment_request_completed`: Xendit notifies your system when a Direct Debit or E-Wallet payment request has succeeded or failed. Please Note that this is for the Payment Request API only. Make sure that other payment callbacks for Direct Debit or E-wallet are not set to prevent duplication. Support: Thailand 🇹🇭 and Malaysia 🇲🇾 only

Money-Out

- `disbursement`: Xendit notifies your system when disbursement has been executed successfully by Xendit, either with COMPLETED or FAILED status. Support: Indonesia only 🇲🇨
- `ph_disbursement`: Xendit notifies your system when disbursement has been executed successfully by Xendit, either with COMPLETED or FAILED status. Support: Philippines only 🇵🇭
- `batch_disbursement`: Xendit notifies your system when Batch Disbursement has been executed successfully by Xendit. Support: Indonesia only 🇲🇨
- `payout`: Xendit notifies your system upon failed and successful payouts. Learn more about Payouts V2 webhooks here. Others
- `report`: Xendit notifies your system to send the report to the specified URLs. Support: All businesses

SecurityHTTPType basic

Header parametersfor-user-idstringExample5cafeb170a2b18519b1b8761

Path parameterstypestringRequired

The type of Webhook URL you want to set

Valid values[
  "invoice",
  "fva_status",
  "fva_paid",
  "ro_fpc_paid",
  "regional_ro_paid",
  "ewallet",
  "payment_method",
  "payment_method_v2",
  "direct_debit",
  "qr_code",
  "recurring",
  "disbursement",
  "ph_disbursement",
  "batch_disbursement",
  "report",
  "payment_succeeded",
  "payment_awaiting_capture",
  "payment_pending",
  "payment_failed",
  "capture_succeeded",
  "capture_failed",
  "payment_request_completed"
]

Body parameters<select class='api-response-data' aria-label='Media type'><option value='d0b0d216-eed3-4d76-a51a-c9845186e02a'>application/json</option>
</select>

```json
{
  "url": "https://www.xendit.co/webhook_catcher"
}
```

object  urlstring    Required

The URL of your server that you want to receive our Webhooks

Min length1

Responses200<select class='api-response-data' aria-label='Media type'><option value='27b815b6-3521-44dc-a4d8-6d56c838b050'>application/json</option>
</select>

```json
{
  "status": "SUCCESSFUL",
  "user_id": "5e6b30d967627b957de8c123",
  "url": "https://www.xendit.co/webhook_catcher",
  "environment": "TEST",
  "callback_token": "66a6680348e1c33ed2b9053a8eb9291b9e2230ff4f4d3057c9f4ac26405d2123"
}
```

object  statusstring    

The status of setting the Webhook URL

Valid values[
  "SUCCESSFUL"
]
user_idstring    

The user_id on which the Webhook URL has been set

urlstring    

The Webhook URL that has been set

environmentstring    

The environment on which the Webhook URL has been set

Valid values[
  "TEST",
  "LIVE"
]
callback_tokenstring    

The unique Webhook token that is attached to each sub-account. Use this to validate that a Webhook is sent from Xendit's servers.

400

Validation error

<select class='api-response-data' aria-label='Media type'><option value='2fc2739b-d307-4982-a25c-e6553e4a111a'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='fef5b46f-306d-4843-8fd8-c0987f4e48fa'>INVALID_URL_FORMAT</option>
</select>INVALID_URL_FORMAT

```json
{
  "error_code": "INVALID_URL_FORMAT",
  "message": "You have provided an invalid URL format",
  "errors": [
    "Detailed description here"
  ]
}
```

object  

Inputs are failing validation. The errors field contains details about which fields are violating validation.

error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "INVALID_CONFIGURATION",
  "INVALID_JSON_FORMAT",
  "TYPE_AND_CONFIGURATION_CONFLICT",
  "INVALID_SOURCE_OR_DESTINATION_ERROR",
  "INSUFFICIENT_BALANCE",
  "INVALID_FEE_AMOUNT",
  "DUPLICATE_ERROR",
  "INVALID_AMOUNT",
  "INSUFFICIENT_ACCOUNT_HOLDER_DATA",
  "MISMATCH_PAYLOAD_FOR_REFERENCE",
  "INVALID_URL_FORMAT"
]
messagestring    
errors Array  OneOfstringstring
objectobject

404

Validation error

<select class='api-response-data' aria-label='Media type'><option value='7246bfe4-e0fa-4968-88ae-4d56f5540291'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='347077e1-96e2-40f2-b234-55ca777b67fb'>CALLBACK_AUTHENTICATION_TOKEN_NOT_FOUND_ERROR</option>
</select>CALLBACK_AUTHENTICATION_TOKEN_NOT_FOUND_ERROR

```json
{
  "error_code": "CALLBACK_AUTHENTICATION_TOKEN_NOT_FOUND_ERROR",
  "message": "No webhook verification token found for this business, please contact help@xendit.co to resolve this issue",
  "errors": [
    "Detailed description here"
  ]
}
```

object  

The object being referenced does not exist

error_codestring    Valid values[
  "DESTINATION_ACCOUNT_NOT_FOUND",
  "DATA_NOT_FOUND",
  "CALLBACK_AUTHENTICATION_TOKEN_NOT_FOUND_ERROR"
]
messagestring    
errors Array  OneOfstringstring
objectobject
