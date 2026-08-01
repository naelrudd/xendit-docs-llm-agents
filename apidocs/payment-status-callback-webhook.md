---
title: "Payment Status Callback (Webhook)"
slug: "payment-status-callback-webhook"
updated: 2026-04-01T03:43:19Z
published: 2026-04-01T03:43:19Z
canonical: "docs.xendit.co/payment-status-callback-webhook"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Payment Status Callback (Webhook)

Post/bill-payments/your-callback-url

Callback endpoint that Xendit will POST to your configured webhook URL when payment status updates occur. This endpoint should be implemented by your server to receive payment notifications.

Header parametersX-Callback-SignaturestringRequired

HMAC SHA256 signature for webhook verification

X-Callback-TimestampstringRequired

Unix timestamp when callback was generated

Body parameters<select class='api-response-data' aria-label='Media type'><option value='9add894c-574d-4f4a-8f26-df42ad740e08'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='a2f0ef77-5c05-4912-ac69-0fce0fe99816'>billPaymentSucceeded</option>
</select>billPaymentSucceeded

Bill Payment Succeeded Webhook

```json
{
  "created": "2025-08-01T10:46:08.208Z",
  "business_id": "60c820d70d4499475d05adb2",
  "event": "bill_payment.succeeded",
  "data": {
    "data": {
      "status": "SUCCEEDDED",
      "created_at": "2025-08-01T10:46:03Z",
      "payment_id": "3dd4ebd4-f6cf-4042-bc65-dd847adcfb77",
      "product_id": "PLN_PREPAID_50K",
      "updated_at": "2025-08-01T10:46:03Z",
      "reference_id": "PLN-20250801174603-5TV45",
      "total_amount": 53200,
      "customer_number": "50170719442",
      "ledger_transaction_id": ""
    },
    "event": "bill_payment.succeeded",
    "business_id": "60c820d70d4499475d05adb2"
  },
  "api_version": "v1"
}
```

Expand Allobject  createdstring  (date-time)    Required

Timestamp when callback was created

business_idstring    Required

Xendit's Business ID

eventstring    Required

Event type

Valid values[
  "bill_payment.succeeded",
  "bill_payment.failed"
]
dataobject  Requireddataobject  Requiredstatusstring    RequiredValid values[
  "SUCCEEDDED",
  "FAILED"
]
created_atstring  (date-time)    Required
payment_idstring    Required
product_idstring    Required
updated_atstring  (date-time)    Required
bill_details Array of object (BillPaymentDetailKeyValue)   object  keystring    Required

Name of the detail field

valuestring    Required

Value of the detail field

failure_codestring   | null  
fulfilled_atstring  (date-time)   | null  
reference_idstring    Required
total_amountnumber    Required
failure_reasonstring   | null  
customer_numberstring    Required
payment_details Array of object (BillPaymentDetailKeyValue)   object  keystring    Required

Name of the detail field

valuestring    Required

Value of the detail field

product_details Array of object (BillPaymentDetailKeyValue)   object  keystring    Required

Name of the detail field

valuestring    Required

Value of the detail field

customer_details Array of object (BillPaymentDetailKeyValue)   object  keystring    Required

Name of the detail field

valuestring    Required

Value of the detail field

ledger_transaction_idstring    

eventstring    RequiredValid values[
  "bill_payment.succeeded",
  "bill_payment.failed"
]
business_idstring    Required

api_versionstring    RequiredValid values[
  "v1"
]

Responses200

Webhook acknowledged successfully
