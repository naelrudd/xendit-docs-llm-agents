---
title: "Managed account status webhook notification"
slug: "managed-account-status-webhook-notification"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/managed-account-status-webhook-notification"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Managed account status webhook notification

Post/your_xenplatform_managed_webhook_url

Webhook events sent for your `MANAGED` sub-accounts when they have registered or are activated.

Body parameters<select class='api-response-data' aria-label='Media type'><option value='23406427-a2c8-4c86-8c89-ee45d98441fe'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='f11b551d-981d-4fdb-940b-b20790e68282'>Account Registered</option>
<option value='65efb2f5-5c7b-4efa-9b65-3be8801ee24f'>Account Activated</option>
</select>Account Registered

```json
{
  "event": "account.registered",
  "created": "2021-01-01T10:00:00Z",
  "data": {
    "user_id": "5cafeb170a2b18519b1b8761",
    "account_info": {
      "payments_enabled": false
    }
  }
}
```

Account Activated

```json
{
  "event": "account.activated",
  "created": "2021-01-01T10:00:00Z",
  "master_acc_business_id": "5cafeb170a2b18529b6120a4",
  "data": {
    "user_id": "5cafeb170a2b18519b1b8761",
    "created": "2021-01-01T10:00:00Z",
    "account_info": {
      "payments_enabled": true
    }
  }
}
```

Expand Allobject  eventstring    

`account.registered`: Your `MANAGED` sub-account has successfully registered `account.activated`: Your `MANAGED` sub-account has been verified and enabled for live payments

Valid values[
  "account.registered",
  "account.activated"
]Exampleaccount.created
business_idstring    

ID of your Account, use this in the for-user-id header to create transactions on behalf of your Account

createdstring    

Timestamp of when the webhook was sent

updatedstring    

Timestamp of when the webhook was updated

dataobject (AccountCallbackDataSchema)  user_idstring    

The sub-account business ID

account_infoobject  payments_enabledboolean    

Indicates whether live payments are enabled for the account

Responses200

OK

400

Bad Request - Invalid webhook payload
