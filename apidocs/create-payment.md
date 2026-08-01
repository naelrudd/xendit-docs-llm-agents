---
title: "Create Payment"
slug: "create-payment"
updated: 2026-04-01T03:43:19Z
published: 2026-04-01T03:43:19Z
canonical: "docs.xendit.co/create-payment"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Payment

Post/bill-payments/v1/payment

This endpoint allows users to submit a payment for a specific product. It can be used for various types of payments, including utility bills, prepaid services, and other products that may or may not require a prior inquiry.

SecurityHTTPType Basic

Header parametersIdempotency-KeystringRequired

Unique key to prevent duplicate payments. Must be unique for each payment request.

Exampleunique-idempotency-key-123

Body parameters<select class='api-response-data' aria-label='Media type'><option value='bf78422e-cfbf-439e-9da3-6bb6b2523292'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='55a8d3bc-51a0-47bf-b4eb-b10a2f7b2466'>plnPrepaid</option>
<option value='d615656b-e900-471b-af25-7108652d5ba9'>plnPostpaid</option>
</select>plnPrepaid

PLN Prepaid Payment

```json
{
  "product_id": "PLN_PREPAID_50K",
  "customer_number": "12345678910",
  "inquiry_id": "inq-98765",
  "reference_id": "tx-pln-001",
  "total_amount": 53200,
  "additional_properties": {}
}
```

plnPostpaid

PLN Postpaid Payment

```json
{
  "product_id": "PLN_POSTPAID",
  "customer_number": "22345678910",
  "inquiry_id": "inq-98766",
  "reference_id": "tx-pln-postpaid-001",
  "total_amount": 159500
}
```

Expand Allobject  product_idstring    Required

Product identifier

customer_numberstring    Required

Customer's account/service number

inquiry_idstring    

Inquiry ID from POST /inquiry (optional)

reference_idstring    Required

Partner's unique transaction reference

total_amountnumber    Required

Total payment amount including admin fee

additional_propertiesobject  

Additional parameters required for specific products

Responses200

Payment accepted for processing

<select class='api-response-data' aria-label='Media type'><option value='8fb6a243-1268-441c-8931-35a3ae8baed0'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='3332ddac-9e95-4077-9073-a13c741a8c2c'>plnPrepaidPending</option>
</select>plnPrepaidPending

PLN Prepaid Payment - Pending

```json
{
  "data": {
    "business_id": "5f27a14a9bf05c73dd040bc8",
    "type": "payment",
    "id": "trx-98765",
    "properties": {
      "product_id": "PLN_PREPAID_50K",
      "customer_number": "12345678910",
      "reference_id": "tx-pln-001",
      "admin_amount": 3200,
      "base_amount": 50000,
      "total_amount": 53200,
      "currency": "IDR",
      "status": "PENDING",
      "fulfilled_at": null,
      "failure_code": null,
      "failure_reason": null,
      "customer_details": [],
      "product_details": [],
      "bill_details": [],
      "payment_details": []
    }
  }
}
```

Expand Allobject  dataobject  business_idstring    

Xendit's Business ID

typestring    

Type of response, always "payment"

Valid values[
  "payment"
]
idstring    

Unique payment transaction ID

propertiesobject  reference_idstring    

Partner's transaction reference

product_idstring    

Product identifier

customer_numberstring    

Customer's account/service number

admin_amountnumber    

Administrative fee amount

base_amountnumber    

Base product amount

total_amountnumber    

Total amount including admin fee

currencystring    

Currency of the product

statusstring    

Payment status

Valid values[
  "PENDING",
  "SUCCEEDED",
  "FAILED"
]
fulfilled_atstring  (date-time)   | null  

ISO8601 timestamp when payment completed (null when pending)

failure_codestring   | null  

Error code in case of FAILED status

failure_reasonstring   | null  

Error message in case of FAILED status

customer_details Array of object (BillPaymentDetailKeyValue)   

Array of customer information key-value pairs

object  keystring    

Name of the detail field

valuestring    

Value of the detail field

product_details Array of object (BillPaymentDetailKeyValue)   

Array of product information key-value pairs

object  keystring    

Name of the detail field

valuestring    

Value of the detail field

bill_details Array of object (BillPaymentDetailKeyValue)   

Array of billing information key-value pairs

object  keystring    

Name of the detail field

valuestring    

Value of the detail field

payment_details Array of object (BillPaymentDetailKeyValue)   

Array of payment information key-value pairs

object  keystring    

Name of the detail field

valuestring    

Value of the detail field

400

Inputs are failing validation. The errors field contains details about which fields are violating validation.

<select class='api-response-data' aria-label='Media type'><option value='d2b5b21d-1293-408f-8f2b-9d21a7676a88'>application/json</option>
</select>object  error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "FEATURE_NOT_AVAILABLE"
]
messagestring    
errors Array  OneOfstringstring
objectobject

402

Payment Required - Insufficient balance

<select class='api-response-data' aria-label='Media type'><option value='c2f7e092-e726-4d5e-b7ee-edc09e5ea4d0'>application/json</option>
</select>object  error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "FEATURE_NOT_AVAILABLE"
]
messagestring    
errors Array  OneOfstringstring
objectobject

404

The provided `id` does not exist. Please review the `id` and try again

<select class='api-response-data' aria-label='Media type'><option value='2e1e3e10-9af0-4716-bef4-e23e2354aee4'>application/json</option>
</select>object  error_codestring    Valid values[
  "RATE_LIMIT_EXCEEDED"
]
messagestring    
errors Array  OneOfstringstring
objectobject

409

Conflict

<select class='api-response-data' aria-label='Media type'><option value='ffea7abf-7dc8-4b68-bb81-1775ff36992d'>application/json</option>
</select>object  error_codestring    Valid values[
  "DUPLICATE_ERROR",
  "IDEMPOTENCY_ERROR"
]
messagestring    
errors Array  OneOfstringstring
objectobject

502

Bad Gateway - Biller error

<select class='api-response-data' aria-label='Media type'><option value='38088dbd-7768-4612-9586-47acc2548211'>application/json</option>
</select>object  error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "FEATURE_NOT_AVAILABLE"
]
messagestring    
errors Array  OneOfstringstring
objectobject

503

Service Unavailable - Biller maintenance

<select class='api-response-data' aria-label='Media type'><option value='6acd0179-00cf-4cc9-9cc6-3e903882ddaa'>application/json</option>
</select>object  error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "FEATURE_NOT_AVAILABLE"
]
messagestring    
errors Array  OneOfstringstring
objectobject

504

Gateway Timeout - Biller timeout

<select class='api-response-data' aria-label='Media type'><option value='8251b473-8053-4165-b15c-26ee23763492'>application/json</option>
</select>object  error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "FEATURE_NOT_AVAILABLE"
]
messagestring    
errors Array  OneOfstringstring
objectobject
