---
title: "XenPlatform Migration Guide"
slug: "xp-migration-guide"
description: "Migrate to the latest XenPlatform integration on Xendit"
tags: ["migration", "xenplatform"]
updated: 2026-11-03T07:14:49Z
published: 2026-11-03T07:14:49Z
canonical: "docs.xendit.co/xp-migration-guide"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# XenPlatform Migration Guide

> [!WARNING]
> Not sure if you need to migrate?
> 
> Reach out to your dedicated account manager or get in touch with our [Support Team](mailto:help@xendit.co) for assistance.

From 1st February 2027, XenPlatform will only provide merchants with the ability to create managed sub-accounts via the Accounts API. This means that all sub-accounts created through the Accounts API will be required to:

- Onboard directly to Xendit
- Agree to Xendit’s Terms & Conditions
- Directly complete account verification with Xendit

As XenPlatform is built solely for platforms and marketplaces that provide payment services to their own sub-merchants, if your business uses sub-accounts today to organize your own branches, outlets or different business lines, you will be required to migrate to standalone Xendit accounts. This guide will explain which path applies to you and how you can migrate to the respective integration.

## Step 1: Identify which XenPlatform offering you have

> [!NOTE]
> Not sure which XenPlatform offering you have?
> 
> Please reach out to your dedicated account manager or get in touch with our [Support Team](mailto:help@xendit.co) for assistance.

| Your current XenPlatform offering | What you’ll need to do |
| --- | --- |
| Your sub-accounts are your own branches, outlets, entities or separate business lines | Path 1: Migrate to standalone Xendit accounts |
| You're an existing platform or marketplace, and your sub-merchants were created with the legacy XenPlatform API with `type: 'OWNED'` | Path 2: Migrate to the Accounts API and re-onboard sub-merchants that were previously tagged as “Owned” |
| You’re an existing platform or marketplace, and your sub-merchants were created with the legacy XenPlatform API with both `type: ‘OWNED’` and `type: 'MANAGED'` | Path 2: Migrate to the Accounts API and **only** re-onboard sub-merchants that were previously tagged as “Owned” |
| You're an existing platform or marketplace, and your sub-merchants were created with the legacy XenPlatform API with `type: 'MANAGED'` | Path 3: Migrate to the Accounts API |

## Step 2: Migrating your XenPlatform integration

### Path 1: Migrate to standalone Xendit accounts

This option applies to you if you are currently onboarding your own branches, outlets, entities or separate business lines as sub-accounts. Your account will no longer be flagged as a XenPlatform master account, and each line of business will have it’s own Xendit account.

**Key changes**

- Your master account (master BID) will no longer be flagged as a XenPlatform master account
- All XenPlatform permissions will be disabled on your master account
- You can no longer create sub-accounts with the Accounts API
- Your existing Managed sub-accounts can continue operating until further notice
- If you have previously onboarded “Owned” sub-accounts, you will need to re-onboard them as a standalone Xendit account

**What you need to do**

1. For each “Owned” sub-account that you have onboarded, you will need to re-onboard this as a new Xendit account, and complete the respective onboarding flows
2. For any new branch, outlet or business line, open a new Xendit account for each of them
3. Withdraw any remaining balance from your “Owned” sub-accounts as soon as possible

> [!WARNING]
> Providing your sub-merchants with access to the Xendit dashboard
> 
> You can follow this guide on how to invite your team members and sub-merchants to get access to the Xendit dashboard to complete the verification process. You can also specify in the API if you’d like to send them an e-mail invite upon creation

There is no need to update your existing API integration as you will no longer be able to use the XenPlatform APIs.

### Path 2: Migrate to the Accounts API and re-onboard “Owned” sub-merchants

> [!NOTE]
> Early migration to the Accounts API
> 
> Migrating early to the Accounts API will provide you with more time and clarity in terms of the new flows that you will need to support. If you need help with the API migration, please reach out to your dedicated account manager or get in touch with our [Support Team](mailto:help@xendit.co) for assistance.

This option applies to you if you are an existing platform or marketplace who has onboarded “Owned” sub-merchants on the legacy XenPlatform API. As we are no longer supporting “Owned” sub-merchants, you will need to re-onboard these sub-merchants to Xendit.

**Key changes**

- Each sub-merchant will get a new Business ID (BID) and a new set of API keys.
- Each sub-merchant will complete verification with Xendit on the Xendit Dashboard
- Each sub-merchant will accept Xendit’s terms electronically
- Each sub-merchant no longer inherits payment methods from the master account automatically. They must be activated separately for each sub-merchant
- Split rules will need to be re-added once you’ve re-onboarded your sub-merchants

**What you need to do**

1. Create a new sub-account for each sub-merchant with the [Accounts API](https://docs.xendit.co/apidocs/create-account-v3). **A detailed technical migration guide can be found here.**
2. Update your systems to ingest the new set of webhooks that come with the Accounts API
  1. [Account Verification webhook](https://docs.xendit.co/apidocs/account-verification-webhook-notification)
  2. [Account Suspension webhook](https://docs.xendit.co/apidocs/account-suspension-webhook-notification)
  3. [Split Payments Status Notification webhook](https://docs.xendit.co/apidocs/split-payment-status-notification-webhook)
3. Re-create your split rules with the Split Rules API (if you currently use them as your sub-merchants will have new BIDs)
4. Inform your sub-merchants that they will need to complete verification and accept Xendit’s terms on the Xendit Dashboard
5. Move or withdraw the balance from each “Owned” sub-merchant as soon as possible

> [!WARNING]
> Providing your sub-merchants with access to the Xendit dashboard
> 
> You can follow this guide on how to invite your team members and sub-merchants to get access to the Xendit dashboard to complete the verification process. You can also specify in the API if you’d like to send them an e-mail invite upon creation

Once you have fully re-onboarded your “Owned” sub-merchants via the [Accounts API](https://docs.xendit.co/apidocs/create-account-v3), you have completed the migration.

### Path 3: Migrate to the Accounts API

> [!NOTE]
> Early migration to the Accounts API
> 
> Migrating early to the Accounts API will provide you with more time and clarity in terms of the new flows that you will need to support. If you need help with the API migration, please reach out to your dedicated account manager or get in touch with our [Support Team](mailto:help@xendit.co) for assistance.

This option applies to you if you are an existing platform or marketplace who has **only** onboarded “Managed” sub-merchants on the legacy XenPlatform API. If you have onboarded a “Owned’ sub-merchant, please refer to Option 2.

**Key changes**

- New sub-accounts are created via the [Accounts API](https://docs.xendit.co/apidocs/create-account-v3)
- The [legacy APIs](https://docs.xendit.co/apidocs/create-account) cannot be used in conjunction with the new [Accounts API](https://docs.xendit.co/apidocs/create-account-v3)

**What you need to do**

1. Migrate your sub-account creation flow to use the [Accounts API](https://docs.xendit.co/apidocs/create-account-v3). **A detailed technical migration guide can be found here.**
2. Update your systems to ingest the new set of webhooks that come with the [Accounts API](https://docs.xendit.co/apidocs/create-account-v3)
  1. [Account Verification webhook](https://docs.xendit.co/apidocs/account-verification-webhook-notification)
  2. [Account Suspension webhook](https://docs.xendit.co/apidocs/account-suspension-webhook-notification)
  3. [Split Payments Status Notification webhook](https://docs.xendit.co/apidocs/split-payment-status-notification-webhook)
3. Inform your sub-merchants that they will need to complete verification and accept Xendit’s terms on the Xendit Dashboard

Once you have completed the above steps, the migration to the new XenPlatform API is complete.

## Frequently Asked Questions

**Will Xendit migrate my sub-accounts for me?**

Xendit will not migrate your sub-accounts automatically. As you have the existing relationship with your sub-merchants, we encourage you to drive the migration exercise with your sub-merchants.

**Do my sub-accounts keep their existing Business ID (BID), API keys and transaction history?**

Yes. Your existing sub-accounts will keep their existing Business ID, API keys & transaction history. However, these owned accounts will no longer be allowed to transact from the 1st of February, 2027.

**What happens to balances that are left in the “Owned’ sub-accounts?**

All balances on “Owned” sub-accounts will have to be moved or withdrawn by you (or the owner) before the 1st of February, 2027.

**Where can my sub-merchants complete their verification? Is there an API?**

Your sub-merchants will complete verification on the Xendit Dashboard. We do not have an API for sub-merchants to complete the verification process.
