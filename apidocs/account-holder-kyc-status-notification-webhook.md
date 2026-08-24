---
title: "Account holder KYC status notification webhook"
slug: "account-holder-kyc-status-notification-webhook"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/account-holder-kyc-status-notification-webhook"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Account holder KYC status notification webhook

Post/your_account_holder_kyc_webhook_url

These events will be sent when there is an update on a sub-account's KYC status

Body parameters<select class='api-response-data' aria-label='Media type'><option value='bb13655b-cb87-4380-ba2e-b97b3cd2a971'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='7aeca7b9-09a7-4408-87f7-ecb77eae9135'>Account Holder KYC Callback</option>
</select>Account Holder KYC Callback

```json
{
  "event": "account_holder.kyc.status",
  "created": "2021-01-01T10:00:00Z",
  "business_id": "5fe2b0137b7d62542fe6d7de",
  "data": {
    "id": "57fb4e076fa3fa296b7f5a97",
    "created": "2021-01-01T10:00:00Z",
    "updated": "2021-01-01T10:00:00Z",
    "kyc": {
      "status": "PASSED",
      "verified_at": "2021-01-01T10:00:00Z",
      "requested_at": "2021-01-01T10:00:00Z",
      "kyc_passed_at": "2021-01-01T10:00:00Z"
    }
  }
}
```

Expand Allobject  eventstring    

Event that occurred for this webhook

Valid values[
  "account_holder.kyc.status"
]Exampleaccount_holder.kyc.status
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

kycobject (account_holder_kyc_response)  statusstring    Valid values[
  "PASSED",
  "FAILED",
  "RESUBMISSION_REQUIRED"
]
requested_atstring  (date-time)    

Timestamp of when the object was updated

kyc_passed_atstring  (date-time)    

Timestamp of when the object was updated

verified_atstring  (date-time)    

Timestamp of when the object was updated

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
