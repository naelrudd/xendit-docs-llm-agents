---
title: "Get account"
slug: "get-account"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/get-account"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Get account

Get/v2/accounts/{id}

The Get Account API allows you to retrieve a sub-account's information.

SecurityHTTPType basic

Path parametersidstringRequiredExample5cafeb170a2b18519b1b8761

Responses200<select class='api-response-data' aria-label='Media type'><option value='4b1f9c35-af3c-4add-a3af-455a11b9760f'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='638ad445-bee4-4922-8207-22d3c7825836'>Owned Sub-account</option>
</select>Owned Sub-account

```json
{
  "id": "5cafeb170a2b18519b1b8761",
  "created": "2021-01-01T10:00:00Z",
  "updated": "2021-01-01T10:00:00Z",
  "type": "OWNED",
  "email": "angie@pinkpanther.com",
  "public_profile": {
    "business_name": "Angie's lemonade stand"
  },
  "status": "LIVE"
}
```

Expand Allobject  idstring    

ID of your Account, use this in the for-user-id header to create transactions on behalf of your Account

createdstring  (date-time)    

Timestamp of when the object was created

updatedstring  (date-time)    

Timestamp of when the object was updated

typestring    

The type of account created

Valid values[
  "MANAGED",
  "OWNED"
]
emailstring  (email)    

A valid email address associated with the object

Max length255Exampletest@example.co
public_profileobject (public_profile)  business_namestring    

Public name of the account.

descriptionstring    

Additional description visible publicly.

countrystring    

The country (based on ISO 3166-1 Alpha-2) of incorporation for a business, or the country of residence for an individual.

Valid values[
  "ID",
  "PH",
  "VN",
  "MY",
  "TH"
]
statusstring    

Status of the Account you are creating.

Valid values[
  "INVITED",
  "REGISTERED",
  "AWAITING_DOCS",
  "PENDING_VERIFICATION",
  "LIVE",
  "SUSPENDED"
]
reference_idstring    

Your reference for the sub-account, if one was provided on creation

404

Not found error

<select class='api-response-data' aria-label='Media type'><option value='97d595f0-e4ab-4139-950e-c8288433cb6c'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='42d93c2e-a5a0-4ff3-9b6a-06ce788c34be'>DATA_NOT_FOUND</option>
</select>DATA_NOT_FOUND

```json
{
  "error_code": "DATA_NOT_FOUND",
  "message": "Could not find payout with the corresponding ID. Please try again with a valid ID.",
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
