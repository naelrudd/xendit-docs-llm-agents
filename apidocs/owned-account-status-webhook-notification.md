---
title: "Owned account status webhook notification"
slug: "owned-account-status-webhook-notification"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/owned-account-status-webhook-notification"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Owned account status webhook notification

Post/your_xenplatform_owned_webhook_url

A webhook event sent when your `OWNED` sub-account has been successfully created

Body parameters<select class='api-response-data' aria-label='Media type'><option value='08480f72-3b30-4651-bc13-5b27b60dc570'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='cf8cd11b-e891-4060-a215-3cdaa44afbd2'>Account Created</option>
</select>Account Created

```json
{
  "event": "account.created",
  "created": "2026-06-19T04:50:51.967Z",
  "business_id": "68b65fa5c2d38abe0de734ce",
  "data": {
    "id": "6a34caaa8a9c47963f1b7abc",
    "type": "OWNED",
    "email": "email+owned+id01@example.com",
    "status": "LIVE",
    "country": "ID",
    "created": "2026-06-19T04:50:50.223Z",
    "updated": "2026-06-19T04:50:51.705Z",
    "reference_id": "samplereferenceid0001",
    "public_profile": {
      "business_name": "Test Submerchant OWNED id001"
    }
  }
}
```

Expand Allobject  eventstring    

Your `OWNED` sub-account has been successfully created

Valid values[
  "account.created"
]Exampleaccount.created
business_idstring    

ID of your Account, use this in the for-user-id header to create transactions on behalf of your Account

createdstring    

Timestamp of when the webhook was sent

updatedstring    

Timestamp of when the webhook was updated

dataobject (CreateAccountResponseSchema)  idstring    

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

Responses200

OK

400

Bad Request - Invalid webhook payload
