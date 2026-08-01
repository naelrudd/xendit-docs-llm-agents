---
title: "Create account"
slug: "create-account"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/create-account"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create account

Post/v2/accounts

> **Legacy** — this endpoint is superseded by [Create account (v3)](/apidocs/create-account#operation/createxenPlatformAccountV3). Use the v3 endpoint for new integrations.

Create Account API allows you to create Accounts for your Partners on your Platform. Once an Account is created, you can accept and route payments through the Transfers API or Platform Fee API. Read more about account types [here](https://docs.xendit.co/docs/sub-accounts).

Remember to store the returned account ID value to make transactions for that Account in the future.

> **Notes**:
> 
> 
> - For the `/v2/accounts` endpoint, we allow a maximum of 5 write requests per second.
> - The `OWNED` type is currently restricted for accounts in Indonesia.
> 
> 
> Please contact help@xendit.co if you need the above features.

**Version**

This version of the API is asynchronous to improve performance and scalability. We have also added API permissions in this version. If you are using an existing API key, please edit your permissions in your Settings page.

It is mandatory to wait for the `account.created` callback before attempting to create transactions. Set a Callback URL in your Dashboard to receive Account Updated Callbacks and know when payments can be processed for your Accounts.

> Use API key permission Account Write to perform this request

**Account Suspension Callbacks**

The Account Suspension webhook can be used to let your system know when Xendit has suspected, suspended or cleared the Accounts linked to your Platform. Our teams and systems automatically and regularly review Account behaviour to help Platforms mitigate potential fraud.

These events may occur if we have reason to believe that the Account has engaged in fraudulent activity. When these events occur, only the transactions occurring on that specific Account will be affected. This approach allows your Platform to continue accepting payments for your other Accounts normally.

SecurityHTTPType basic

Body parameters<select class='api-response-data' aria-label='Media type'><option value='20125aa1-3be3-495e-aee5-9e6ee0a5b657'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='b8ecbaac-f3ea-4999-a59b-1a49924acdc4'>Owned Type</option>
</select>Owned Type

```json
{
  "email": "angie@pinkpanther.com",
  "type": "OWNED",
  "public_profile": {
    "business_name": "Owned Business Account"
  }
}
```

Expand Allobject  emailstring  (email)    Required

A valid email address associated with the object

Max length255Exampletest@example.co
typestring    

The type of account created

Valid values[
  "MANAGED",
  "OWNED"
]
public_profileobject (public_profile)  Requiredbusiness_namestring    

Public name of the account.

descriptionstring    

Additional description visible publicly.

Responses200<select class='api-response-data' aria-label='Media type'><option value='d0fd106a-1e10-44c8-a1fc-6cba948c1499'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='108d56cd-599e-4fa1-a742-abab37cafa12'>Owned Sub-account</option>
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

400

Validation errors for creating accounts

<select class='api-response-data' aria-label='Media type'><option value='4d19cf06-96dd-49d2-b6ce-1f1c3746e109'>application/json</option>
</select>OneOf400ApiValidationErrorobject (400ApiValidationError)error_codestring    ExampleAPI_VALIDATION_ERROR
error_messagestring    ExampleInputs are failing validation. The errors field contains details about which fields are violating validation.

400InvalidConfigurationErrorobject (400InvalidConfigurationError)error_codestring    ExampleINVALID_CONFIGURATION
error_messagestring    ExampleThe `configurations` parameter combination is invalid. Please follow the requirement of each parameter written in Request section.

400TypeConfigConflictErrorobject (400TypeConfigConflictError)error_codestring    ExampleTYPE_AND_CONFIGURATION_CONFLICT
error_messagestring    ExamplePlease provide either one of the `type` field or the `configurations` field
