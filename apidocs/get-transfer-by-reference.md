---
title: "Get transfer by reference"
slug: "get-transfer-by-reference"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/get-transfer-by-reference"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Get transfer by reference

Get/transfers/reference={reference}

This endpoint queries the current status of a transfer. This is often used for checking the status of a transaction.

SecurityHTTPType basic

Path parametersreferencestringRequiredExamplemonthly_transfers_1234

Responses200<select class='api-response-data' aria-label='Media type'><option value='deab164d-4d98-41cd-97db-1f62cacf93ea'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='c1a1fe75-aad1-4777-a38c-73555f0d773b'>Default Transfer</option>
</select>Default Transfer

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

400<select class='api-response-data' aria-label='Media type'><option value='e173cc51-2df7-4f4c-bd7a-d4a2c6181e7d'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='860f14a9-3ca2-4863-9152-35c9596d812f'>DATA_NOT_FOUND</option>
</select>DATA_NOT_FOUND

```json
{
  "error_code": "DATA_NOT_FOUND",
  "message": "Could not find transfer by reference because reference may be invalid.",
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

401<select class='api-response-data' aria-label='Media type'><option value='24fc3557-56cc-494c-82c1-ae09fbf56dd0'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='ffbcacf4-abef-470d-9220-f583804e6a81'>INVALID_API_KEY</option>
</select>INVALID_API_KEY

```json
{
  "error_code": "INVALID_API_KEY",
  "message": "API key is not authorized for this API service, access to xenPlatform is needed",
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
