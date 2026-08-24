---
title: "Account holder capabilities notification webhook"
slug: "account-holder-capabilities-notification-webhook"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/account-holder-capabilities-notification-webhook"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Account holder capabilities notification webhook

Post/your_account_holder_capabilities_webhook_url

These events will be sent when there is an update on a sub-account's payment activation status

Body parameters<select class='api-response-data' aria-label='Media type'><option value='8a9eab67-2dbe-4f25-9c92-54baa057c4f1'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='7cb21b51-f31e-4cf5-9a5f-878c20cefb62'>Resubmission Required</option>
</select>Resubmission Required

```json
{
  "event": "account_holder.capabilities.status",
  "created": "2021-01-01T10:00:00Z",
  "business_id": "5fe2b0137b7d62542fe6d7de",
  "data": {
    "id": "57fb4e076fa3fa296b7f5a97",
    "created": "2021-01-01T10:00:00Z",
    "updated": "2021-01-01T10:00:00Z",
    "capabilities": [
      {
        "type": "MONEY_IN",
        "channel_code": "GCASH",
        "activated_at": "2021-01-01T10:00:00Z",
        "verified_at": "2021-01-01T10:00:00Z",
        "requested_at": "2021-01-01T10:00:00Z",
        "status": "RESUBMISSION_REQUIRED",
        "failure_reason": "Your website URL is not related to your business"
      }
    ]
  }
}
```

Expand Allobject  eventstring    

Event that occurred for this webhook

Valid values[
  "account_holder.capabilities.status"
]Exampleaccount_holder.capabilities.status
business_idstring    

ID of your Account, use this in the for-user-id header to create transactions on behalf of your Account

createdstring    

Timestamp of when the webhook was sent

updatedstring    

Timestamp of when the webhook was updated

dataobject  idstring    

The unique ID of an Account Holder object

createdstring    

Timestamp of when the webhook was sent

updatedstring    

Timestamp of when the webhook was updated

capabilities Array of object (account_holder_capability_response)   object  

An object containing the details of the Account Holder capabilities activation process

typestring    
channel_codestring    
statusstring    Valid values[
  "LIVE",
  "VERIFICATION_IN_PROGRESS",
  "RESUBMISSION_REQUIRED",
  "DECLINED"
]
failure_reasonstring    
activated_atstring  (date-time)    

Timestamp of when the object was updated

verified_atstring  (date-time)    

Timestamp of when the object was updated

requested_atstring  (date-time)    

Timestamp of when the object was updated

Responses200

OK

400

Bad Request - Invalid webhook payload
