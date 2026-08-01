---
title: "GoPay"
slug: "gopay"
updated: 2026-01-12T10:02:55Z
published: 2026-01-12T10:02:55Z
canonical: "docs.xendit.co/gopay"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# GoPay

![](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/image(128).png)

GoPay is Indonesia's leading digital wallet and payment platform, originally developed by Gojek. It has become one of the most widely adopted e-wallet services in Indonesia, integrated across the Gojek ecosystem including GoFood, GoRide, and numerous merchant partners throughout the country.

When customers select GoPay at checkout, they are redirected to the GoPay interface where they can authorize the payment using their GoPay account. The transaction is completed instantly once the customer confirms the payment with their GoPay PIN or biometric authentication through the GoPay app.

Effective 1 January 2026, GoPay transactions can only be completed through the GoPay mobile application. Customers must authorize and confirm their payments directly within the GoPay app using their registered account.

## Features

GoPay offers two channel codes for different payment scenarios:

- **GOPAY**: Use this for one-time payment
- **GOPAY_RECURRING***: Use this for recurring payment

*: additional activation process with partner is needed

| **Channel Code** | GOPAY_RECURRING |
| --- | --- |
| **Display Name** | GoPay |
| **Currency** | IDR |
| **Country** | ID |
| **Type** | EWALLET |
| **Min Amount** | 1 |
| **Max Amount** | 50,000,000.00 |
| **User Approval Flow** | REDIRECT, SKIP |
| **Reusable Payment Code** | - |
| **Save** | ✓ |
| **Merchant Initiated Transaction** | ✓ |
| **Auth & Capture** | - |
| **Partial Capture** | - |
| **Multiple Partial Capture** | - |
| **Desktop Support** | WEB URL |
| **Mobile Support** | DEEPLINK URL |
| **Custom Payment Code** | - |
| **Display Merchant Name** | MERCHANT |
| **Display User Name** | - |
| **Set Expiry** | - |
| **Payment Request Expiry (hours)** | 0.5 |
| **Payment Token Validity (years)** | INDEFINITE |
| **Payment Processing Time (hours)** | INSTANT |
| **Settlement Time** | T+1 CALENDAR DAYS* |
| **Installments** | - |
| **Refund** | ✓ |
| **Partial Refund** | ✓ |
| **Multiple Partial Refund** | ✓ |
| **Refund Validity (days)** | 45 |
| **Payment Link** | ✓ |
| **Fund Flow** | AGGREGATOR |

## Payment Flow

### One-Time Payment

![](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/image(159).png)

### Save Payment Method

![](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/image(160).png)
