---
title: "Create Inquiry"
slug: "create-inquiry"
updated: 2026-04-01T03:43:19Z
published: 2026-04-01T03:43:19Z
canonical: "docs.xendit.co/create-inquiry"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Inquiry

Post/bill-payments/v1/inquiry

Facilitates pre-payment verification for products requiring upfront bill checks, such as PLN electricity services. The response includes comprehensive bill information and the total amount due.

SecurityHTTPType Basic

Body parameters<select class='api-response-data' aria-label='Media type'><option value='d40f2df0-9402-47f4-a626-1a9c7ca10bc8'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='9b8b6ac0-efc6-4d94-b202-f80dcb924423'>plnPrepaid</option>
<option value='8fbbbacd-9773-4a70-ba9c-17a9f9f782e2'>plnPostpaid</option>
</select>plnPrepaid

PLN Prepaid Inquiry

```json
{
  "product_id": "PLN_PREPAID_50K",
  "customer_number": "12345678910"
}
```

plnPostpaid

PLN Postpaid Inquiry

```json
{
  "product_id": "PLN_POSTPAID",
  "customer_number": "22345678910"
}
```

Expand Allobject  product_idstring    Required

Product identifier

customer_numberstring    Required

Customer's account/service number

additional_propertiesobject  

Additional parameters required for specific products

Responses200

Successful inquiry response

<select class='api-response-data' aria-label='Media type'><option value='0f5d2a9c-cc47-41a0-ba3b-15fc17cb864d'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='9b259f4f-d5d7-4de7-9fa1-580b8cb046b0'>plnPrepaid</option>
</select>plnPrepaid

PLN Prepaid Inquiry Response

```json
{
  "data": {
    "business_id": "5f27a14a9bf05c73dd040bc8",
    "type": "inquiry",
    "id": "inq-98765",
    "properties": {
      "product_id": "PLN_PREPAID_50K",
      "admin_amount": 3200,
      "base_amount": 50000,
      "total_amount": 53200,
      "revenue_share_amount": 500,
      "currency": "IDR",
      "customer_number": "12345678910",
      "customer_details": [
        {
          "key": "Nama Pelanggan",
          "value": "John Doe"
        },
        {
          "key": "Nomor Pelanggan",
          "value": "12345678910"
        }
      ],
      "product_details": [
        {
          "key": "Tarif/Daya",
          "value": "R2/000003500"
        },
        {
          "key": "Denom",
          "value": "100.000"
        }
      ],
      "bill_details": [
        {
          "key": "Admin",
          "value": "3200"
        }
      ]
    }
  }
}
```

Expand Allobject  dataobject  business_idstring    

Xendit's Business ID

typestring    

Type of response, always "inquiry"

Valid values[
  "inquiry"
]
idstring    

Unique inquiry identifier

propertiesobject  product_idstring    

Product identifier

admin_amountnumber    

Administrative fee amount

base_amountnumber    

Base product amount

total_amountnumber    

Total amount including admin fee

revenue_share_amountnumber    

Partner revenue share amount

currencystring    

Currency of the product

customer_numberstring    

Customer's account/service number

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

400

Inputs are failing validation. The errors field contains details about which fields are violating validation.

<select class='api-response-data' aria-label='Media type'><option value='6e385fe6-b685-4440-a16e-ea4547eb08cf'>application/json</option>
</select>object  error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "FEATURE_NOT_AVAILABLE"
]
messagestring    
errors Array  OneOfstringstring
objectobject

404

The provided `id` does not exist. Please review the `id` and try again

<select class='api-response-data' aria-label='Media type'><option value='f6f1c673-a4e2-476b-a057-31545b8c7cb7'>application/json</option>
</select>object  error_codestring    Valid values[
  "RATE_LIMIT_EXCEEDED"
]
messagestring    
errors Array  OneOfstringstring
objectobject

409

Conflict

<select class='api-response-data' aria-label='Media type'><option value='d7b342e4-1971-49d0-bd57-080c3c7b9a90'>application/json</option>
</select>object  error_codestring    Valid values[
  "DUPLICATE_ERROR",
  "IDEMPOTENCY_ERROR"
]
messagestring    
errors Array  OneOfstringstring
objectobject

502

Bad Gateway - Biller error

<select class='api-response-data' aria-label='Media type'><option value='350cf8be-2230-48fa-8874-e69cc640039d'>application/json</option>
</select>object  error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "FEATURE_NOT_AVAILABLE"
]
messagestring    
errors Array  OneOfstringstring
objectobject

503

Service Unavailable - Biller maintenance

<select class='api-response-data' aria-label='Media type'><option value='0d8ddbba-9c0b-4928-ae32-32b9a4ed598b'>application/json</option>
</select>object  error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "FEATURE_NOT_AVAILABLE"
]
messagestring    
errors Array  OneOfstringstring
objectobject

504

Gateway Timeout - Biller timeout

<select class='api-response-data' aria-label='Media type'><option value='c4f253a2-3c7c-44b0-8358-f3a8f5e3643f'>application/json</option>
</select>object  error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "FEATURE_NOT_AVAILABLE"
]
messagestring    
errors Array  OneOfstringstring
objectobject
