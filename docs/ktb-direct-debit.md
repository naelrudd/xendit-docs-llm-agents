---
title: "KTB Direct Debit"
slug: "ktb-direct-debit"
updated: 2025-09-08T08:07:12Z
published: 2025-09-08T08:07:12Z
canonical: "docs.xendit.co/ktb-direct-debit"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# KTB Direct Debit

---

## Features & Requirements

| **Channel code** | `KTB_DIRECT_DEBIT` |
| --- | --- |
| **Currency** | THB |
| **Minimum amount** | 20 |
| **Maximum amount** | 700,000 |
| **User approval flow** | REDIRECT |
| **Save** | ✅ |
| **Recurring** | ✅ |
| **Display merchant name** | Xendit |
| **Display user name** | ❌ |
| **Set expiry** | ❌ |
| **Settlement Time** | Instant |
| **Refund** | ❌ |
| **Partial refund** | ❌ |
| **Multiple partial refund** | ❌ |
| **Refund validity** | ❌ |
| **User data required by Bank*** | - Mobile Number - Identity Number or Passport Number |
| **Compatible integration** | Payment API, Payment Session, Subscription, Recurring |

*Bank will validate the login credential to the mobile phone number & ID No. sent during Payment Request

## Account Linking flow

End customer select the bank to link on checkout page and process authorization (Account Linking)

![](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/Payment session - DD linking.jpg)

![Steps to link a bank account using Krungthai NEXT app for transactions.](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/KTB DD.jpg)
