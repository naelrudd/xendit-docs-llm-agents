---
title: "XenPlatform V3 API Migration Guide"
slug: "xenplatform-v3-api-migration-guide"
description: "Migrate to the latest version of XenPlatform on Xendit"
tags: ["xenplatform", "migration"]
updated: 2026-11-03T07:15:16Z
published: 2026-11-03T07:15:16Z
canonical: "docs.xendit.co/xenplatform-v3-api-migration-guide"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# XenPlatform V3 API Migration Guide

With the new Accounts API V3, there are some key concepts that have changed as compared to the previous V2 Accounts API.

## Key changes

> [!NOTE]
> The below list highlights the key changes from the previous version
> 
> The V3 API is also constantly update and we will update the main documentation when we make changes and additions to the resource.

| Area | Legacy (V2) | Accounts API (V3) |
| --- | --- | --- |
| Endpoint | `POST /v2/accounts` | `POST /v3/accounts` |
| Sub-account type | `type`: `OWNED` or `MANAGED` | - |
| Sub-account name | `public_profile.business_name` | `name` |
| Sub-account e-mail | `email`(optional) | `email`(required) |
| Legal identity | - | `identity.country_of_incorporation` and `identity.entity_type`, both required |
| Settings | `configurations` | `configuration`, with a new shape: `users.send_email_invite` and `webhooks.recipient` |
| Webhook recipient values | `MASTER`, `SUB` | `MASTER_ACCOUNT`, `SUB_ACCOUNT` |
| Response | `type`, `public_profile`, top-level `country` | `identity` and `configuration` objects |
| Account statuses | `INVITED`, `REGISTERED`, `AWAITING_DOCS`, `PENDING_VERIFICATION`, `LIVE`, `SUSPENDED` | Adds `AWAITING_RESUBMISSION`, `DECLINED`, `DORMANT`, `CLOSED`. `INVITED` is no longer returned. |
| KYC status updates | Account status webhooks (`account.registered`, `account.activated`) | `account.verification` webhook with a `kyc.status` field |
| Submitting KYC by API | `POST /account_verification` | Only via the Xendit Dashboard |

The API key you call with decides which master account the sub-account links to. It needs the **Account Write** permission.

### Request example

Legacy (V2):

```json
POST /v2/accounts
{
  "email": "owner@tokoberkah.co.id",
  "type": "MANAGED",
  "public_profile": { "business_name": "Toko Berkah" }
}
```

Accounts API (V3):

```json
POST /v3/accounts
{
  "name": "Toko Berkah",
  "email": "owner@tokoberkah.co.id",
  "identity": {
    "country_of_incorporation": "ID",
    "entity_type": "INDIVIDUAL"
  },
  "configuration": {
    "users": { "send_email_invite": true },
    "webhooks": { "recipient": "SUB_ACCOUNT" }
  }
}
```

A successful V3 call returns the sub-account with status `REGISTERED`.

### Accepted entity types

The `entity_type` you send must be valid for the country. Any country not listed follows the Singapore list.

| Country | Entity types |
| --- | --- |
| Indonesia (ID) | `CORPORATION`, `SOLE_PROPRIETORSHIP`, `PARTNERSHIP`, `NON_PROFIT`, `INDIVIDUAL`, `COOPERATIVE` |
| Philippines (PH) | `CORPORATION`, `SOLE_PROPRIETORSHIP`, `PARTNERSHIP`, `INDIVIDUAL`, `ONE_PERSON_CORPORATION` |
| Vietnam (VN) | `CORPORATION`, `SOLE_PROPRIETORSHIP`, `PARTNERSHIP`, `LIMITED_LIABILITY_COMPANY` |
| Thailand (TH) | `CORPORATION`, `PARTNERSHIP`, `NON_PROFIT`, `INDIVIDUAL` |
| Malaysia (MY) | `CORPORATION`, `SOLE_PROPRIETORSHIP`, `PARTNERSHIP`, `NON_PROFIT` |
| Singapore (SG) | `CORPORATION`, `PARTNERSHIP` |
| Hong Kong (HK) | `CORPORATION`, `PARTNERSHIP` |
| Mexico (MX) | `CORPORATION`, `SOLE_PROPRIETORSHIP`, `PARTNERSHIP`, `NON_PROFIT` |

An invalid combination returns `400 INVALID_DATA_PROVIDED`. If you set the wrong entity type, create a new sub-account with the correct one.

### Behavioural changes

| Behaviour | Legacy (V2) | Accounts API (V3) | What to do |
| --- | --- | --- | --- |
| Webhook routing | Managed sub-account events go to the sub-account's own webhook URLs | Events go to the **master account's** URLs unless you set `webhooks.recipient` to `SUB_ACCOUNT` | Set `recipient` explicitly so events land where your systems expect them |
| Owner invitation | Managed sub-accounts get an invitation email automatically | No email is sent unless `users.send_email_invite` is `true` | Set it to `true` if sub-merchants complete verification on the Dashboard |
| Ready to transact | Wait for the `account.created` callback | The sub-account starts at `REGISTERED` and can process live payments only once verification passes | Wait for `kyc.status` = `PASSED` before routing live payments |
| Resubmission | No field-level detail | `AWAITING_RESUBMISSION` arrives with `kyc.failure_reasons`, one entry per field to fix | Show the reasons to the sub-merchant and collect only what's listed |
| Missed webhooks | Varies by event | No resend for `account.verification` | Poll the Retrieve account verification API as a fallback |
| Webhook delivery logs | Shown on the account the URL belongs to | Shown on the sub-account's dashboard, even when routed to the master URL | Check the sub-account's dashboard when debugging |
| Country | Sub-accounts in your supported markets | `country_of_incorporation` must match your master account's country unless cross-country is enabled for you | Speak to your Account Manager before creating sub-accounts in another country |
| Payment channels | Owned sub-accounts inherit the master's channels | Each sub-account activates its own channels | Plan channel activation into your onboarding flow |
| Moving funds between accounts | In-house transfers available | Paused from 1 February 2027 | Use split rules at payment time instead of moving balances afterwards |
| Test mode | Owned or Managed test sub-accounts | `CORPORATION` only, same country as the master, no invite, master recipient; goes `LIVE` immediately; 500 test sub-accounts max | Test other entity types in Live mode with a real sub-merchant |

### The verification webhook

Set the **Account Verification Status** webhook URL on your master account. Each event looks like this:

```json
{
  "event": "account.verification",
  "business_id": "<master account ID>",
  "data": {
    "id": "<sub-account ID>",
    "kyc": {
      "status": "AWAITING_RESUBMISSION",
      "failure_reasons": [
        {
          "field": "authorized_person_selfie_document",
          "reason": "BLURRY_IMAGE",
          "message": "This document is blurry."
        }
      ]
    }
  }
}
```

`kyc.status` is one of `VERIFICATION_IN_PROGRESS`, `PASSED`, `AWAITING_RESUBMISSION` or `FAILED`. `reason` is one of `NEW_DOCUMENT`, `WRONG_DOCUMENT`, `NEW_INFORMATION` or `BLURRY_IMAGE`. If no URL is set, events aren't delivered.

### Migration steps

1. Give your API key the Account Write permission.
2. Set the Account Verification Status webhook URL on your master account and build a handler for `account.verification`.
3. Map your sub-merchant records to `identity.country_of_incorporation` and `identity.entity_type`.
4. Switch sub-account creation to `POST /v3/accounts`, setting `configuration.users.send_email_invite` and `configuration.webhooks.recipient` explicitly.
5. Gate live payments on `kyc.status` = `PASSED`, and handle `AWAITING_RESUBMISSION` and `FAILED`.
6. Re-create split rules with the [Create split rule API](https://docs.xendit.co/apidocs/create-split-rule).
7. Test in Test mode, then run one real sub-merchant end to end in Live mode before switching all traffic.

Reference: [Create account (V3)](https://docs.xendit.co/apidocs/create-account-v3), [Account verification webhook](https://docs.xendit.co/apidocs/account-verification-webhook-notification), [Create account (V2, legacy)](https://docs.xendit.co/apidocs/create-account).
