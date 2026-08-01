---
title: "Get Payment Detail"
slug: "get-payment-detail"
updated: 2026-04-01T03:43:19Z
published: 2026-04-01T03:43:19Z
canonical: "docs.xendit.co/get-payment-detail"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Payment Detail

Get/bill-payments/v1/payment/{id}

This endpoint retrieves detailed information about a specific payment, including its current status and fulfillment results if available.

SecurityHTTPType Basic

Path parametersidstringRequired

Payment transaction ID from post payment response

Exampletrx-98765

Responses200

Payment details retrieved successfully

<select class='api-response-data' aria-label='Media type'><option value='f38436da-4bbc-4fa6-9b11-d1c28483cd1f'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='b4e5180a-34d5-4a03-ba7e-0bfc3e5ddae3'>plnPrepaidSuccess</option>
</select>plnPrepaidSuccess

PLN Prepaid Payment - Success

```json
{
  "data": {
    "business_id": "5f27a14a9bf05c73dd040bc8",
    "type": "payment",
    "id": "trx-98765",
    "properties": {
      "reference_id": "tx-pln-001",
      "product_id": "PLN_PREPAID_50K",
      "customer_number": "12345678910",
      "admin_amount": 3200,
      "base_amount": 50000,
      "total_amount": 53200,
      "currency": "IDR",
      "status": "SUCCEEDED",
      "fulfilled_at": "2024-01-23T08:15:30Z",
      "failure_code": null,
      "failure_reason": null,
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
        }
      ],
      "bill_details": [
        {
          "key": "Admin",
          "value": "3200"
        }
      ],
      "payment_details": [
        {
          "key": "Token",
          "value": "1234-5678-9012-3456-7890"
        },
        {
          "key": "Serial Number",
          "value": "PLN987654321"
        }
      ]
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

404

The provided `id` does not exist. Please review the `id` and try again

<select class='api-response-data' aria-label='Media type'><option value='49b6509d-c059-4a78-baf2-1b7952c81794'>application/json</option>
</select>object  error_codestring    Valid values[
  "RATE_LIMIT_EXCEEDED"
]
messagestring    
errors Array  OneOfstringstring
objectobject
