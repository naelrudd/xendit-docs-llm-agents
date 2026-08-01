---
title: "Create transfers"
slug: "create-transfers"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/create-transfers"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create transfers

Post/transfers

The Transfers API allows you to transfer balances: i) from your sub-accounts to your master account and vice versa, ii) between your sub-accounts. Use this to manage, or split payments between your platform and your sub accounts within the Xendit ecosystem.

> You can only create transfers using the Platform's API key. Sub-accounts that you manage through xenPlatform have no ability to create transfers through this endpoint

SecurityHTTPType basic

Body parameters<select class='api-response-data' aria-label='Media type'><option value='00e3ab89-2091-4b90-b4c7-3b1cc174daac'>application/json</option>
</select>object  referencestring    Required

A unique reference for this Transfer that you set when making the request

amountnumber    Required
source_user_idstring    Required

The source of the transfer. This is the user_id of either your master or sub account

destination_user_idstring    Required

The destination of the transfer. This is the `user_id` of either your master or sub account

Responses200<select class='api-response-data' aria-label='Media type'><option value='14123447-f2e1-4d35-aefe-41688c484193'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='cc7a774b-0241-4a07-aaaa-fdd9215f82d7'>Transfer</option>
</select>Transfer

```json
{
  "created": "2020-11-30T02:47:53.061Z",
  "transfer_id": "bd1cc56b-ce7f-4ad7-8901-3eaa689e90eb",
  "source_user_id": "`5cafeb170a2b18519b1b8768",
  "destination_user_id": "5f8d0c0603ffe06b7d4d9fcf",
  "status": "SUCCESSFUL",
  "amount": "90000",
  "reference": "Monthly_Transfers_1234"
}
```

object  

Object that would be generated upon creation of a Transfer

createdstring  (date-time)    

Timestamp of when the object was created

transfer_idstring    

A unique reference for this Transfer set by Xendit systems

referencestring    

A unique reference for this Transfer that you set when making the request

source_user_idstring    

The source of the transfer. This is the user_id of either your master or sub account

destination_user_idstring    

The destination of the transfer. This is the `user_id` of either your master or sub account

statusstring    

The status of the Transfer. Available values `SUCCESSFUL`,`PENDING`, `FAILED`

amountnumber    

The amount that was transferred

400<select class='api-response-data' aria-label='Media type'><option value='fa4bea54-e74e-4631-8b6e-23ccc46bc999'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='e0ec7e8e-5445-4511-a0ee-8ad93d3b20c8'>API_VALIDATION_ERROR</option>
<option value='28914224-d5b3-4def-9b6b-44c43a5895db'>INVALID_JSON_FORMAT</option>
<option value='f04c0c16-79c9-4faf-bc3f-ec0e428df9b1'>INVALID_SOURCE_OR_DESTINATION_ERROR</option>
<option value='ce1f9474-aeb3-40bf-8f94-7f72de9e42b7'>INSUFFICIENT_BALANCE</option>
<option value='4e3a6e2d-7f10-4ddb-86cd-6278dc2f7c09'>MISMATCH_PAYLOAD_FOR_REFERENCE</option>
<option value='4c79e51f-0674-49c3-86e7-6bfc544282c2'>INVALID_AMOUNT</option>
</select>API_VALIDATION_ERROR

```json
{
  "error_code": "API_VALIDATION_ERROR",
  "message": "Inputs are failing validation. The errors field contains details about which fields are violating validation.",
  "errors": [
    "Detailed description here"
  ]
}
```

INVALID_JSON_FORMAT

```json
{
  "error_code": "INVALID_JSON_FORMAT",
  "message": "The request body is not a valid JSON format.",
  "errors": [
    "Detailed description here"
  ]
}
```

INVALID_SOURCE_OR_DESTINATION_ERROR

```json
{
  "error_code": "INVALID_SOURCE_OR_DESTINATION_ERROR",
  "message": "Source or destination account does not exist. Please input a valid business ID within your xenPlatform account.",
  "errors": [
    "Detailed description here"
  ]
}
```

INSUFFICIENT_BALANCE

```json
{
  "error_code": "INSUFFICIENT_BALANCE",
  "message": "The cash balance of your source account is insufficient.",
  "errors": [
    "Detailed description here"
  ]
}
```

MISMATCH_PAYLOAD_FOR_REFERENCE

```json
{
  "error_code": "MISMATCH_PAYLOAD_FOR_REFERENCE",
  "message": "Reference has been used before. If you'd like to retry this transfer, please use the same payload as your previous request.",
  "errors": [
    "Detailed description here"
  ]
}
```

INVALID_AMOUNT

```json
{
  "error_code": "INVALID_AMOUNT",
  "message": "Transfer amount has to be greater than 0, Transfer amount of IDR currency should not have decimal point, Transfer amount of PHP currency can only have max 2 decimal point.",
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

401

Validation error

<select class='api-response-data' aria-label='Media type'><option value='06b2bde3-39be-48b0-adb8-bec855f77fac'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='71fa1d98-c02c-4fbe-af07-81cc3a203905'>INVALID_API_KEY</option>
</select>INVALID_API_KEY

```json
{
  "error_code": "INVALID_API_KEY",
  "message": "The API key format is invalid",
  "errors": [
    "Detailed description here"
  ]
}
```

object  

Invalid API key

error_codestring    Valid values[
  "INVALID_API_KEY"
]
messagestring    
errors Array  OneOfstringstring
objectobject

403<select class='api-response-data' aria-label='Media type'><option value='d6bb0cd0-5c4c-4c2a-8f76-1694af8abad2'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='4f0e331a-0847-47fc-a24a-ec1ffb6aed12'>REQUEST_FORBIDDEN_ERROR</option>
<option value='17ba6ecb-9464-4968-86b6-dbf4ec0cf8df'>DUPLICATE_REFERENCE</option>
<option value='52a2b64e-e1ca-41f1-9b5a-ea88a03e6e55'>XEN_PLATFORM_SUB_ACCOUNT_NOT_LIVE</option>
<option value='5691d48c-ebb4-40d4-8373-f4c70ab1fa88'>API_KEY_ENVIRONMENT_NOT_MATCH</option>
</select>REQUEST_FORBIDDEN_ERROR

```json
{
  "error_code": "REQUEST_FORBIDDEN_ERROR",
  "message": "API key in use does not have necessary permissions to perform the request. Please assign proper permissions for the key",
  "errors": [
    "Detailed description here"
  ]
}
```

DUPLICATE_REFERENCE

```json
{
  "error_code": "DUPLICATE_REFERENCE",
  "message": "The reference parameter should be unique.",
  "errors": [
    "Detailed description here"
  ]
}
```

XEN_PLATFORM_SUB_ACCOUNT_NOT_LIVE

```json
{
  "error_code": "XEN_PLATFORM_SUB_ACCOUNT_NOT_LIVE",
  "message": "Your source or destination account is not live yet. Please specify live accounts for live transfers.",
  "errors": [
    "Detailed description here"
  ]
}
```

API_KEY_ENVIRONMENT_NOT_MATCH

```json
{
  "error_code": "API_KEY_ENVIRONMENT_NOT_MATCH",
  "message": "Use your LIVE API key to transfer between LIVE accounts, or use TEST API key to transfer between TEST accounts.",
  "errors": [
    "Detailed description here"
  ]
}
```

object  

Forbidden request

error_codestring    Valid values[
  "REQUEST_FORBIDDEN_ERROR",
  "FEATURE_NOT_ACTIVATED",
  "DUPLICATE_REFERENCE",
  "XEN_PLATFORM_SUB_ACCOUNT_NOT_LIVE",
  "API_KEY_ENVIRONMENT_NOT_MATCH",
  "CHANNEL_ACTIVATION_IN_PROGRESS",
  "CHANNEL_HAS_BEEN_ACTIVATED",
  "KYC_VERIFICATION_IN_PROGRESS"
]
messagestring    
errors Array  OneOfstringstring
objectobject

425<select class='api-response-data' aria-label='Media type'><option value='1d7362b9-586e-419e-8783-1d06a5875502'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='70d4b1f6-37d1-44a8-b2f0-fbb25e3da61e'>TRANSFER_IN_PROGRESS</option>
</select>TRANSFER_IN_PROGRESS

```json
{
  "error_code": "TRANSFER_IN_PROGRESS",
  "message": "Transfer is currently being processed. Use `GET Transfer By Reference` to check its latest status",
  "errors": [
    "Detailed description here"
  ]
}
```

object  

Transfer is currently being processed. Use GET Transfer By Reference to check its latest status

error_codestring    Valid values[
  "TRANSFER_IN_PROGRESS"
]
messagestring    
errors Array  OneOfstringstring
objectobject
