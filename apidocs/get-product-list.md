---
title: "Get Product List"
slug: "get-product-list"
updated: 2026-04-01T03:43:19Z
published: 2026-04-01T03:43:19Z
canonical: "docs.xendit.co/get-product-list"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Product List

Get/bill-payments/v1/product

Gets a list of available products with optional filtering capabilities

SecurityHTTPType Basic

Query parametersidstring

Filter by specific product ID

ExamplePLN_PREPAID_50K
billerstring

Filter by biller name

ExamplePLN
categorystring

Filter by product category

Valid values[
  "ELECTRICITY"
]ExampleELECTRICITY
countrystring

Filter by country code (e.g. ID)

ExampleID
availability_statusstring

Filter by product availability status

Valid values[
  "AVAILABLE",
  "TEMPORARILY_UNAVAILABLE",
  "DISCONTINUED"
]ExampleAVAILABLE
requires_inquiryboolean

Filter products that require inquiry step

Exampletrue
limitinteger

Number of records to be fetched per page

Default50Example50
cursorstring

Cursor value for paginating the result

Exampledummy-cursor-value-001==

Responses200

Successful response

<select class='api-response-data' aria-label='Media type'><option value='e2d352ea-e41c-4896-8e7c-12c26a85970c'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='cbc15771-6052-4e4c-bd6e-ebbe15d189ca'>plnPrepaid</option>
</select>plnPrepaid

PLN Prepaid 50K Example

```json
{
  "limit": 50,
  "cursor": "dummy-cursor-value-001==",
  "data": [
    {
      "type": "product",
      "id": "PLN_PREPAID_50K",
      "properties": {
        "product_name": "PLN Prepaid 50K",
        "category": "ELECTRICITY",
        "biller": "PLN",
        "country": "ID",
        "currency": "IDR",
        "requires_inquiry": false,
        "availability_status": "AVAILABLE",
        "admin_amount": 3200,
        "base_amount": 50000,
        "total_amount": 53200,
        "revenue_share_amount": 1000,
        "locale": {
          "en": "PLN Prepaid 50.000",
          "id": "PLN Prabayar 50.000"
        }
      }
    }
  ]
}
```

Expand Allobject  data Array of object (BillPaymentProduct)   

Array of product objects

object  typestring    

Type of object, always "product"

Valid values[
  "product"
]
idstring    

Unique product identifier

propertiesobject  product_namestring    

Display name of the product

categorystring    

Product category

Valid values[
  "ELECTRICITY"
]
billerstring    

Name of the biller/provider

countrystring    

Country code in ISO 3166-1 alpha-2 format

currencystring    

Currency code in ISO 4217 format

requires_inquiryboolean    

Whether product requires inquiry before purchase

availability_statusstring    

Product availability status

Valid values[
  "AVAILABLE",
  "TEMPORARILY_UNAVAILABLE",
  "DISCONTINUED"
]
admin_amountnumber    

Administrative fee amount

base_amountnumber    

Base product amount (0 for postpaid products)

total_amountnumber    

Total amount including admin fee

revenue_share_amountnumber    

Merchant revenue share amount

localeobject  

Localized product names

enstring    

Product name in English

idstring    

Product name in Indonesian

next_cursorstring    

Cursor value for next page. Empty if the last page reached

limitinteger    

Number of records per page

400

Inputs are failing validation. The errors field contains details about which fields are violating validation.

<select class='api-response-data' aria-label='Media type'><option value='86fcf002-7cb9-4c0a-bc03-a40cfc3177c5'>application/json</option>
</select>object  error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "FEATURE_NOT_AVAILABLE"
]
messagestring    
errors Array  OneOfstringstring
objectobject

401

API key in use does not have necessary permissions to perform the request. Please assign proper permissions for the key.

<select class='api-response-data' aria-label='Media type'><option value='5a0b3a91-16a8-48bd-b420-d984c974b466'>application/json</option>
</select>object  error_codestring    Valid values[
  "RATE_LIMIT_EXCEEDED"
]
messagestring    
errors Array  OneOfstringstring
objectobject

500

Internal Server Error

<select class='api-response-data' aria-label='Media type'><option value='cb4b7a40-eac6-493a-97d5-8ca43702918e'>application/json</option>
</select>object  error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "FEATURE_NOT_AVAILABLE"
]
messagestring    
errors Array  OneOfstringstring
objectobject
