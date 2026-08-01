---
title: "Create split rule"
slug: "create-split-rule"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/create-split-rule"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create split rule

Post/split_rules

A Split Rule object defines how payments in xenPlatform can be routed and split to multiple sub-accounts or the Master account.

Include the `split_rule_id` returned in the response in supported transaction endpoints to automatically route and split payments to multiple account destinations once payments settle.

SecurityHTTPType basic

Body parameters<select class='api-response-data' aria-label='Media type'><option value='4a90cae3-c5d4-45f1-b634-5f57e7089924'>application/json</option>
</select>

```json
{
  "name": "Platform and Delivery Fees",
  "description": "Platform fee and delivery fee for a Marketplace",
  "routes": [
    {
      "flat_amount": 3000,
      "currency": "IDR",
      "destination_account_id": "5f8d0c0603ffe06b7d4d9fcf",
      "reference_id": "reference-1"
    },
    {
      "percent_amount": 5.25,
      "currency": "IDR",
      "destination_account_id": "5f8d0c0603ffe06b7d4d9fcf",
      "reference_id": "reference-2"
    }
  ]
}
```

Expand Allobject  namestring    Required

Name to identify a split rule. Typically based on transaction and/or sub-merchant types and does not have to be unique. e.g. "standard platform fee and delivery fee", "commission"

descriptionstring    

Describes the purpose of the object

routes Array of object (route)   Requiredobject  

Defines a single amount and destination within a split rule

flat_amountnumber    

Amount of payments to be split, using a flat rate as a unit. This will be null if not applicable, and is required if `percent_amount` is null. All units must be a positive number

percent_amountnumber    

Amount of payments to be split, using a percent rate as unit. This will be null if not applicable. This will be required if `flat_amount` is null All units must be a positive number, with decimals supported up to 2 decimal places. Percent amounts have to be between 0 and 100 Percent amounts are rounded off to the nearest monetary unit (e.g. 0.50 IDR will be rounded to 1 IDR; 0.49 IDR will be rounded to 0 IDR)

currencystring    

ISO 4217 Currency Code

Valid values[
  "IDR",
  "PHP",
  "VND",
  "MYR",
  "THB",
  "SGD",
  "USD"
]
destination_account_idstring    

Business ID of the destination account where the amount is routed to.This could be the Business ID of your Master or Sub-account.

reference_idstring    

Reference ID which acts as an identifier of the route itself. This is used to distinguish in case one split rule has multiple routes of the same destinations. Its value must be unique and case sensitive for every route object under the same Split Rule.

Responses200<select class='api-response-data' aria-label='Media type'><option value='7774c346-ffb5-4788-87d3-28e034438243'>application/json</option>
</select>

```json
{
  "id": "splitru_d9e069f2-4da7-4562-93b7-ded87023d749",
  "name": "Standard platform fee",
  "description": "Platform fee for all transactions accepted on behalf of vendors",
  "routes": [
    {
      "flat_amount": 3000,
      "currency": "IDR",
      "destination_account_id": "5f8d0c0603ffe06b7d4d9fcf",
      "reference_id": "reference-1"
    },
    {
      "percent_amount": 5.25,
      "currency": "IDR",
      "destination_account_id": "5cafeb170a2b18519b1b8768",
      "reference_id": "reference-2"
    }
  ],
  "created": "2020-09-01T07:00:00.007Z",
  "updated": "2020-09-01T07:00:00.007Z",
  "metadata": {}
}
```

Expand Allobject  idstring    

The unique Split Rule ID

namestring    

Name to identify a split rule. Typically based on transaction and/or sub-merchant types and does not have to be unique. e.g. "standard platform fee and delivery fee", "commission"

descriptionstring    

Describes the purpose of the object

routes Array of object (route)   object  

Defines a single amount and destination within a split rule

flat_amountnumber    

Amount of payments to be split, using a flat rate as a unit. This will be null if not applicable, and is required if `percent_amount` is null. All units must be a positive number

percent_amountnumber    

Amount of payments to be split, using a percent rate as unit. This will be null if not applicable. This will be required if `flat_amount` is null All units must be a positive number, with decimals supported up to 2 decimal places. Percent amounts have to be between 0 and 100 Percent amounts are rounded off to the nearest monetary unit (e.g. 0.50 IDR will be rounded to 1 IDR; 0.49 IDR will be rounded to 0 IDR)

currencystring    

ISO 4217 Currency Code

Valid values[
  "IDR",
  "PHP",
  "VND",
  "MYR",
  "THB",
  "SGD",
  "USD"
]
destination_account_idstring    

Business ID of the destination account where the amount is routed to.This could be the Business ID of your Master or Sub-account.

reference_idstring    

Reference ID which acts as an identifier of the route itself. This is used to distinguish in case one split rule has multiple routes of the same destinations. Its value must be unique and case sensitive for every route object under the same Split Rule.

createdstring  (date-time)    

Timestamp of when the object was created

updatedstring  (date-time)    

Timestamp of when the object was updated

metadataobject (metadata)  

Object of additional key-value pairs that the merchants may use like internal system parameters (business ID, shopping cart). User defines the JSON properties and values. You can specify up to 50 keys, with key names up to 40 characters long and values up to 500 characters long. Otherwise `NULL`

400

Validation error

<select class='api-response-data' aria-label='Media type'><option value='cacc34fb-4af7-4ce4-b938-16b2569cb881'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='33307ec1-aaf2-47d7-a929-e5cfe401bcf3'>API_VALIDATION_ERROR</option>
<option value='40d584ba-078c-4549-a9e0-a32a55244d65'>INVALID_FEE_AMOUNT</option>
<option value='9ede6c71-2404-4226-a31c-92f6325aa966'>DUPLICATE_ERROR</option>
</select>API_VALIDATION_ERROR

```json
{
  "error_code": "INVALID_CONFIGURATION",
  "message": "Inputs are failing validation. The errors field contains details about which fields are violating validation.",
  "errors": [
    "Detailed description here"
  ]
}
```

INVALID_FEE_AMOUNT

```json
{
  "error_code": "INVALID_FEE_AMOUNT",
  "message": "Fee amount and/or unit is negative number or incorrect format.",
  "errors": [
    "Detailed description here"
  ]
}
```

DUPLICATE_ERROR

```json
{
  "error_code": "DUPLICATE_ERROR",
  "message": "Returned if provided `reference_id` is not unique for the routes",
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

<select class='api-response-data' aria-label='Media type'><option value='a5dbc282-5684-4fb4-b5c0-86cd165d7733'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='75026b4f-0d33-404a-8294-e93a395db87a'>DESTINATION_ACCOUNT_NOT_FOUND</option>
</select>DESTINATION_ACCOUNT_NOT_FOUND

```json
{
  "error_code": "DESTINATION_ACCOUNT_NOT_FOUND",
  "message": "Returned when destination_account_id is invalid or not connected to this xenPlatform account",
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
