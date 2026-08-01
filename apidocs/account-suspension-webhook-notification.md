---
title: "Account suspension webhook notification"
slug: "account-suspension-webhook-notification"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/account-suspension-webhook-notification"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Account suspension webhook notification

Post/your_account_suspension_status_callback_url

These events may occur if we have reason to believe that the Account has engaged in fraudulent activity.

Body parameters<select class='api-response-data' aria-label='Media type'><option value='f71a81d0-ba34-4853-b945-205271eb8903'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='40b00c0c-f3fe-470d-b51b-ac956fdaeae0'>Account Suspended</option>
</select>Account Suspended

```json
{
  "event": "account.suspended",
  "created": "2021-01-01T10:00:00Z",
  "data": {
    "id": "5cafeb170a2b18519b1b8761",
    "created": "2021-01-01T10:00:00Z",
    "updated": "2021-01-01T10:00:00Z",
    "email": "test@xendit.co",
    "public_profile": {
      "business_name": "My Store"
    },
    "status": "SUSPENDED",
    "reason": "FRAUD_PROMO_ABUSE"
  }
}
```

Expand Allobject  eventstring    

These events may occur if we have reason to believe that the Account has engaged in fraudulent activity.

Valid values[
  "account.suspected",
  "account.suspended",
  "account.cleared"
]Exampleaccount.suspended
business_idstring    

ID of your Account, use this in the for-user-id header to create transactions on behalf of your Account

createdstring    

Timestamp of when the webhook was sent

updatedstring    

Timestamp of when the webhook was updated

dataobject (AccountSuspensionCallbackSchema)  idstring    

ID of your Account, use this in the for-user-id header to create transactions on behalf of your Account

createdstring  (date-time)    

Timestamp of when the object was created

updatedstring  (date-time)    

Timestamp of when the object was updated

emailstring  (email)    

A valid email address associated with the object

Max length255Exampletest@example.co
public_profileobject (public_profile)  business_namestring    

Public name of the account.

descriptionstring    

Additional description visible publicly.

statusstring    Valid values[
  "SUSPECTED",
  "SUSPENDED",
  "CLEARED"
]
reasonstring    

Reason given for the status change

Responses200

OK

400

Bad Request - Invalid webhook payload
