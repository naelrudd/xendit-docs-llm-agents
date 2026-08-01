---
title: "Accept payments for sub-accounts"
slug: "accepting-payments-for-sub-accounts"
updated: 2026-07-07T03:15:43Z
published: 2026-07-09T00:00:00Z
canonical: "docs.xendit.co/accepting-payments-for-sub-accounts"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Accept payments for sub-accounts

Before creating payments on behalf of your merchants, you may need to confirm that the necessary payment channels are activated for each sub-account.

## Flow & implementation

You or your merchants can use the Dashboard and our APIs to create payments. However Owned sub-accounts cannot create API keys and hence are unable to create their own API requests:

|  | Master Account | Sub-accounts |
| --- | --- | --- |
| Create invoices via Dashboard | ✅ | ✅ |
| Create payments via API | ✅ | ✅ |

With the Master account API key, you can send `Create payments` requests via API on behalf of sub-accounts using a header parameter called `for-user-id`. The following flowcharts are some examples on what the process looks like.

### Payment Links

![](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/xp-invoice-eng.webp)

### Fixed Virtual Accounts

![](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/xp-fva-eng.webp)

## Merchant name displayed to customers

When customers pay, they will see the name of your merchant in various touch points. Whose name gets displayed name depend on the sub-account type as well as the interface that the customer is on.

- For Sub-Accounts, all payment methods will display your merchant’s name, except for channels that allow for customization in the transaction request (Virtual Accounts, Over-The-Counter).

![](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/xp-name-displayed_f9eafe.webp)

## Receiving payment event webhooks

To receive webhooks on events occurring on your merchant’s accounts, you may need to set relevant webhook URLs on the sub-account depending on its type. For example, to receive Payment Status webhook for your merchant, you have to make sure that your merchant’s sub-account has already been set for Payment Status webhook URL.

There are two methods to set webhook URLs for sub-accounts:

- Your merchants can log in and set their own webhook URL by navigating to Webhook Settings
- The Master Account can set webhook URL during the sub-account creation, determining if the webhooks will get sent to the `MASTER_ACCOUNT` or the `SUB_ACCOUNT`
