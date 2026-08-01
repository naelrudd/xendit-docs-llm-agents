---
title: "Get Product by ID"
slug: "get-product-by-id"
updated: 2026-04-01T03:43:19Z
published: 2026-04-01T03:43:19Z
canonical: "docs.xendit.co/get-product-by-id"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Product by ID

Get/bill-payments/v1/product/{id}

Gets a specific product by its ID

SecurityHTTPType Basic

Path parametersidstringRequired

Product ID

ExamplePLN_PREPAID_50K

Responses200

Successful response

<select class='api-response-data' aria-label='Media type'><option value='c70005a6-f2ea-4175-bd65-0327a3b40b02'>application/json</option>
</select>Expand Allobject  typestring    

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

404

The provided `id` does not exist. Please review the `id` and try again

<select class='api-response-data' aria-label='Media type'><option value='22f52077-dcbc-4a90-82e9-7cf4f4882eba'>application/json</option>
</select>object  error_codestring    Valid values[
  "RATE_LIMIT_EXCEEDED"
]
messagestring    
errors Array  OneOfstringstring
objectobject
