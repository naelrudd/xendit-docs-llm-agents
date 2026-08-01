---
title: "Update account"
slug: "update-account"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/update-account"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Update account

Patch/v2/accounts/{id}

The Update Account API allows you to update a sub-account's information or link an Account Holder to verify the account.

**Account verification**

This endpoint is the final step of verifying your sub-accounts via the Account Holder flow:

1. Upload the KYC documents with the Upload File API (`POST /files`)
2. [Create an Account Holder](/apidocs/update-account#operation/createAccountHolder) with the business,
individual and document details
3. Link the Account Holder to your sub-account by passing `account_holder_id` to
this endpoint — this submits the account for verification and its KYC status
becomes `VERIFICATION_IN_PROGRESS`

The verification result is delivered to your webhook URL via the [Account verification webhook](/apidocs/update-account#operation/accountVerificationWebhook).

SecurityHTTPType basic

Path parametersidstringRequiredExample5cafeb170a2b18519b1b8761

Body parameters<select class='api-response-data' aria-label='Media type'><option value='ecbc6ce2-63f6-45de-8385-775207f35e73'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='847d9465-c803-4f16-b6cb-2253ceca53f3'>Update Business Name</option>
<option value='cf42a179-67ef-4ddf-8399-9241a1cab357'>Link Account Holder</option>
</select>Update Business Name

```json
{
  "public profile": {
    "business_name": "New Business Name"
  }
}
```

Link Account Holder

```json
{
  "account_holder_id": "4376b7b0-1c44-46be-8640-828f79cdc8be"
}
```

Expand Allobject  emailstring  (email)    

A valid email address associated with the object

Max length255Exampletest@example.co
public_profileobject (public_profile)  business_namestring    

Public name of the account.

descriptionstring    

Additional description visible publicly.

account_holder_idstring    

The unique ID of an Account Holder object

Responses200<select class='api-response-data' aria-label='Media type'><option value='964b06a7-a097-4e4a-825d-2897be8c2b79'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='f558783e-7750-4a28-9e1f-0d45fe6a3ace'>Owned Sub-account</option>
<option value='6b3631d1-ecf1-469c-9807-04d533efbf75'>Link Account Holder</option>
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

Link Account Holder

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
  "status": "LIVE",
  "account_holder_id": "4376b7b0-1c44-46be-8640-828f79cdc8be"
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

<select class='api-response-data' aria-label='Media type'><option value='f256b6ac-a0e0-4fa6-afe8-6eab2f79c17d'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='fb9cc04e-fa93-4928-9043-99287dfb85f3'>DATA_NOT_FOUND</option>
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
