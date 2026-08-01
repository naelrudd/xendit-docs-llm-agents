---
title: "Available Payment Channels"
slug: "available-payment-channels"
updated: 2026-07-08T14:06:20Z
published: 2026-07-08T14:06:20Z
canonical: "docs.xendit.co/available-payment-channels"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Available payment channels

This table provides a high level overview on payment channels available via Xendit and their corresponding features. You can use filter or search to find information about specific payment channels.

[Embedded content](https://doc-widget.xendit.co/payment-channels/)

### More information about columns and values

| Column Name | Description |
| --- | --- |
| Channel code | Unique identifier for the payment channel, used in API integration. |
| Display name | Branding name of the payment channel that end users will see during their payment journey. |
| Currency | Currency supported by the payment channel (e.g., IDR, PHP, USD). |
| Country | Country where the payment channel can be used. |
| Type | Category or flow for payment channels (e.g., e-wallet, bank transfer, card, over-the-counter, etc.). This will be useful for grouping payment channel in checkout page. |
| Min. amount | Floor value that can be collected via this payment channel. |
| Max. amount | Ceiling value that can be collected via this payment channel. |
| Settlement time | **Business Days** — Settlement happens on working days (Monday to Friday, excluding weekends and public holidays). Timeline: T+X means X working days after payment confirmation. Example: If a payment is confirmed on Friday with T+2, the settlement will arrive on Tuesday (assuming Monday is not a holiday). **Calendar Days** — Settlement happens every day, including weekends and public holidays. Timeline: T+X means X days after payment confirmation. Example: If a payment is confirmed on Friday at 3 PM with T+2, the settlement will arrive on Sunday at 3 PM. **Instant** — Settlement happens almost right away. Timeline: usually within 5 minutes of payment confirmation. Example: If a payment is confirmed on Friday at 3 PM, the settlement will arrive by around 3:05 PM the same day. |
| Save | Feature for linking or tokenizing payment information for future use is available. |
| Reusable payment code | Feature for collecting multiple payments via one payment code is available (e.g. a static QR code in physical stores). |
| Display name | Business name that end users will see during their payment journey. |
| User approval flow | **Redirect** — End users will be redirected on their device to log in and authenticate the transaction. **Present to customers** — End users will be presented a payment code for them to take action on a separate device / application. **Skip** — End users involvement are not required to complete payment. **Push Notification** — End users will need to complete the payment on payment channel partner app. |
| Merchant-initiated transactions | Feature for merchants to collect money without involving end users is available. |
| Payment processing time | Time delay between end user completing payment step until the payment is confirmed by the payment method provider. **Business days** — Payment result occurs approximately after 24 hours * T+X from payment initiated, excludes weekend or public holidays. **Instant** — Payment result occurs approximately a few minutes from payment initiated (most of payment channels’s behavior). |
| Custom payment code | Feature to configure the payment code with specific values is available. |
| Installments | Feature for end user to break down the payment is available and served by the payment method provider. |
| Auth & capture | Two-step payment process: **Auth** (authorization) to reserve funds, followed by **Capture** to settle the funds. |
| Partial capture | Ability to capture less than the authorized amount. |
| Multiple partial capture | Ability to capture the authorized amount in several parts until fully captured. |
| Desktop support | Payment channel is supported on desktop devices. |
| Mobile support | Payment channel is supported on mobile devices. |
| Display merchant name | Merchant business name displayed to the end user during the payment process. The displayed name can be: - Your business name - Xendit's name - Your business name prefixed with "Xendit" |
| Customize display name | Customize the name displayed to the end user during the payment process. For example, you can customize the name associated with a Virtual Account so that it displays your customer's name instead of the default merchant name. |
| Payment request expiry (hours) | Duration in hours before a payment request expires if not completed. |
| Payment token validity (years) | Maximum validity period of a saved payment token. |
| Refund | Feature for returning full collected amount to user is available via the original payment route. |
| Partial refund | Feature for returning a subset of collected money to user is available via the original payment route. |
| Multiple partial refund | Feature for merchants to return funds in multiple partial refunds until the full collected amount is refunded. |
| Refund validity (days) | Maximum number of days after the original transaction that a refund request can be made. |
| Payment link | Whether the channel supports creation of a hosted payment page (payment link) for collection. |
| Fund flow | The settlement funds routing from the end user to the merchant. **Aggregator -** will be settle to Xendit’s account balance **Gateway** - directly settle to merchant’s bank account |

This paragraph is hidden from users but still visible to screen readers and SEO bots.

****ID****

**AKULAKU IDR**

| Channel Code | AKULAKU |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1,000.00 |
| Max Amount | 25,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | INDEFINITE |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | ✓ |

**ALFAMART IDR**

| Channel Code | ALFAMART |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 10,000.00 |
| Max Amount | 5,000,000.00 |
| Settlement Time (hours) | T+5 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**ASTRAPAY IDR**

| Channel Code | ASTRAPAY |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 100.00 |
| Max Amount | 20,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**ATOME IDR**

| Channel Code | ATOME |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 50,000.00 |
| Max Amount | 6,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | INDEFINITE |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | ✓ |

**BCA_VIRTUAL_ACCOUNT IDR**

| Channel Code | BCA_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT,MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 10,000.00 |
| Max Amount | 50,000,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BJB_VIRTUAL_ACCOUNT IDR**

| Channel Code | BJB_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT,MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 2,000,000,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BNC_VIRTUAL_ACCOUNT IDR**

| Channel Code | BNC_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 50,000,000,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BNI_VIRTUAL_ACCOUNT IDR**

| Channel Code | BNI_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT,MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 50,000,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BRI_DIRECT_DEBIT IDR**

| Channel Code | BRI_DIRECT_DEBIT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 50,000,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | — |
| Refund Validity (days) | 120 |
| Save | ✓ |
| Payment Token Validity (years) | CARD EXPIRY |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BRI_VIRTUAL_ACCOUNT IDR**

| Channel Code | BRI_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT,MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 50,000,000,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BSI_VIRTUAL_ACCOUNT IDR**

| Channel Code | BSI_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT,MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 50,000,000,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BSS_VIRTUAL_ACCOUNT IDR**

| Channel Code | BSS_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT,MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 50,000,000,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**CARDS IDR**

| Channel Code | CARDS |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT, MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 5,000.00 |
| Max Amount | 200,000,000.00 |
| Settlement Time (hours) | T+5 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 365 |
| Save | ✓ |
| Payment Token Validity (years) | CARD EXPIRY |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | ✓ |
| Partial Capture | ✓ |
| Installments | — |

**CIMB_VIRTUAL_ACCOUNT IDR**

| Channel Code | CIMB_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT,MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 50,000,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**DANA IDR**

| Channel Code | DANA |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 100.00 |
| Max Amount | 20,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 30 |
| Save | ✓ |
| Payment Token Validity (years) | 10 |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | ✓ |

**GOPAY IDR**

| Channel Code | GOPAY |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 50,000,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 45 |
| Save | ✓ |
| Payment Token Validity (years) | INDEFINITE |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**GOPAY_RECURRING IDR**

| Channel Code | GOPAY_RECURRING |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 50,000,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 45 |
| Save | ✓ |
| Payment Token Validity (years) | INDEFINITE |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**HANA_VIRTUAL_ACCOUNT IDR**

| Channel Code | HANA_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 50,000,000,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**INDODANA IDR**

| Channel Code | INDODANA |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 10,000.00 |
| Max Amount | 25,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 30 |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | ✓ |

**INDOMARET IDR**

| Channel Code | INDOMARET |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 10,000.00 |
| Max Amount | 2,500,000.00 |
| Settlement Time (hours) | T+5 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**JENIUSPAY IDR**

| Channel Code | JENIUSPAY |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1,000.00 |
| Max Amount | 20,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | INDEFINITE |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**KREDIVO IDR**

| Channel Code | KREDIVO |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1,000.00 |
| Max Amount | 30,000,000.00 |
| Settlement Time (hours) | T+4 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 14 |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | ✓ |

**LINKAJA IDR**

| Channel Code | LINKAJA |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 20,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | — |
| Refund Validity (days) | 30 |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**MANDIRI_VIRTUAL_ACCOUNT IDR**

| Channel Code | MANDIRI_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT,MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 50,000,000,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**MUAMALAT_VIRTUAL_ACCOUNT IDR**

| Channel Code | MUAMALAT_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 50,000,000,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**NEXCASH IDR**

| Channel Code | NEXCASH |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 20,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | ✓ |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**OVO IDR**

| Channel Code | OVO |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 100.00 |
| Max Amount | 20,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 14 |
| Save | ✓ |
| Payment Token Validity (years) | INDEFINITE |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | ✓ |

**PERMATA_VIRTUAL_ACCOUNT IDR**

| Channel Code | PERMATA_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | XENDIT,MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 9,999,999,999.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**QRIS IDR**

| Channel Code | QRIS |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 20,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | — |
| Refund Validity (days) | 30 |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**SHOPEEPAY IDR**

| Channel Code | SHOPEEPAY |
| --- | --- |
| Country | ID |
| Currency | IDR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 20,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 365 |
| Save | ✓ |
| Payment Token Validity (years) | 5 |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | ✓ |

****MY****

**AFFIN_FPX MYR**

| Channel Code | AFFIN_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**AFFIN_FPX_BUSINESS MYR**

| Channel Code | AFFIN_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**AGRO_FPX MYR**

| Channel Code | AGRO_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**AGRO_FPX_BUSINESS MYR**

| Channel Code | AGRO_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**ALLIANCE_FPX MYR**

| Channel Code | ALLIANCE_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**ALLIANCE_FPX_BUSINESS MYR**

| Channel Code | ALLIANCE_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**AMBANK_FPX MYR**

| Channel Code | AMBANK_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**AMBANK_FPX_BUSINESS MYR**

| Channel Code | AMBANK_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**AMBANK_VIRTUAL_ACCOUNT MYR**

| Channel Code | AMBANK_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | - |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BNP_FPX_BUSINESS MYR**

| Channel Code | BNP_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BOC_FPX MYR**

| Channel Code | BOC_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BSN_FPX MYR**

| Channel Code | BSN_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**CARDS MYR**

| Channel Code | CARDS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT, MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 5,000.00 |
| Settlement Time (hours) | T+5 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 365 |
| Save | ✓ |
| Payment Token Validity (years) | CARD EXPIRY |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | ✓ |
| Partial Capture | ✓ |
| Installments | — |

**CIMB_FPX MYR**

| Channel Code | CIMB_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**CIMB_FPX_BUSINESS MYR**

| Channel Code | CIMB_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**CITIBANK_FPX_BUSINESS MYR**

| Channel Code | CITIBANK_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**DEUTSCHE_FPX_BUSINESS MYR**

| Channel Code | DEUTSCHE_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**GRABPAY MYR**

| Channel Code | GRABPAY |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 1,500.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 365 |
| Save | ✓ |
| Payment Token Validity (years) | 10 |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | ✓ |

**HLB_FPX MYR**

| Channel Code | HLB_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**HLB_FPX_BUSINESS MYR**

| Channel Code | HLB_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**HSBC_FPX MYR**

| Channel Code | HSBC_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**HSBC_FPX_BUSINESS MYR**

| Channel Code | HSBC_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**ISLAM_FPX MYR**

| Channel Code | ISLAM_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**ISLAM_FPX_BUSINESS MYR**

| Channel Code | ISLAM_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**KFH_FPX MYR**

| Channel Code | KFH_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**KFH_FPX_BUSINESS MYR**

| Channel Code | KFH_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**MAYB2E_FPX MYR**

| Channel Code | MAYB2E_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**MAYB2E_FPX_BUSINESS MYR**

| Channel Code | MAYB2E_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**MAYB2U_FPX MYR**

| Channel Code | MAYB2U_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**MUAMALAT_FPX MYR**

| Channel Code | MUAMALAT_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**MUAMALAT_FPX_BUSINESS MYR**

| Channel Code | MUAMALAT_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**OCBC_FPX MYR**

| Channel Code | OCBC_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**OCBC_FPX_BUSINESS MYR**

| Channel Code | OCBC_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**PUBLIC_FPX MYR**

| Channel Code | PUBLIC_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**PUBLIC_FPX_BUSINESS MYR**

| Channel Code | PUBLIC_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**RAKYAT_FPX MYR**

| Channel Code | RAKYAT_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**RAKYAT_FPX_BUSINESS MYR**

| Channel Code | RAKYAT_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**RHB_FPX MYR**

| Channel Code | RHB_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**RHB_FPX_BUSINESS MYR**

| Channel Code | RHB_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**SCH_FPX MYR**

| Channel Code | SCH_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**SCH_FPX_BUSINESS MYR**

| Channel Code | SCH_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**SHOPEEPAY MYR**

| Channel Code | SHOPEEPAY |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 4,999.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 365 |
| Save | ✓ |
| Payment Token Validity (years) | 5 |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | ✓ |

**TOUCHNGO MYR**

| Channel Code | TOUCHNGO |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 20,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 30 |
| Save | ✓ |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**UOB_FPX MYR**

| Channel Code | UOB_FPX |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**UOB_FPX_BUSINESS MYR**

| Channel Code | UOB_FPX_BUSINESS |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**WECHATPAY MYR**

| Channel Code | WECHATPAY |
| --- | --- |
| Country | MY |
| Currency | MYR |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 4,999.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | — |
| Refund Validity (days) | 365 |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

****PH****

**7ELEVEN PHP**

| Channel Code | 7ELEVEN |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 50,000.00 |
| Settlement Time (hours) | T+5 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**7ELEVEN_CLIQQ PHP**

| Channel Code | 7ELEVEN_CLIQQ |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 50,000.00 |
| Settlement Time (hours) | T+5 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BANK_TRANSFER PHP**

| Channel Code | BANK_TRANSFER |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 200,000,000.00 |
| Settlement Time (hours) | T+3 BUSINESS DAYS |
| Payment Processing Time (hours) | T+1 BUSINESS DAYS |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BDO_ONLINE_BANKING PHP**

| Channel Code | BDO_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 2,000,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | 0.5 |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BILLEASE PHP**

| Channel Code | BILLEASE |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 50.00 |
| Max Amount | 150,000.00 |
| Settlement Time (hours) | T+3 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | — |
| Refund Validity (days) | INDEFINITE |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | ✓ |

**BOC_ONLINE_BANKING PHP**

| Channel Code | BOC_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 10.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BPI_DIRECT_DEBIT PHP**

| Channel Code | BPI_DIRECT_DEBIT |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 500,000.00 |
| Settlement Time (hours) | T+1 CALENDAR DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 30 |
| Save | ✓ |
| Payment Token Validity (years) | 0.25 |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BPI_ONLINE_BANKING PHP**

| Channel Code | BPI_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 250,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BPI_RECURRING PHP**

| Channel Code | BPI_RECURRING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 500,000.00 |
| Settlement Time (hours) | T+1 CALENDAR DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 30 |
| Save | ✓ |
| Payment Token Validity (years) | 0.25 |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**CARDS PHP**

| Channel Code | CARDS |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT, MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 20.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | T+5 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 365 |
| Save | ✓ |
| Payment Token Validity (years) | CARD EXPIRY |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | ✓ |
| Partial Capture | ✓ |
| Installments | — |

**CEBUANA PHP**

| Channel Code | CEBUANA |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**CHINABANK_DIRECT_DEBIT PHP**

| Channel Code | CHINABANK_DIRECT_DEBIT |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 50,000.00 |
| Settlement Time (hours) | T+1 CALENDAR DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 30 |
| Save | ✓ |
| Payment Token Validity (years) | 0.25 |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**CHINABANK_ONLINE_BANKING PHP**

| Channel Code | CHINABANK_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | 24 |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**CVM PHP**

| Channel Code | CVM |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 30,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**ECPAY PHP**

| Channel Code | ECPAY |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 50,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**ECPAY_DRAGONLOAN PHP**

| Channel Code | ECPAY_DRAGONLOAN |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 20,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**ECPAY_SCHOOL PHP**

| Channel Code | ECPAY_SCHOOL |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 50,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**GCASH PHP**

| Channel Code | GCASH |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 100,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 180 |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | ✓ |

**GRABPAY PHP**

| Channel Code | GRABPAY |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 100,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 365 |
| Save | ✓ |
| Payment Token Validity (years) | 10 |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**INSTAPAY_ONLINE_BANKING PHP**

| Channel Code | INSTAPAY_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 35,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**LANDBANK_ONLINE_BANKING PHP**

| Channel Code | LANDBANK_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 250,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | 24 |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**LBC PHP**

| Channel Code | LBC |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 200,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**MAYBANK_ONLINE_BANKING PHP**

| Channel Code | MAYBANK_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**METROBANK_ONLINE_BANKING PHP**

| Channel Code | METROBANK_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 2,000,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**MLHUILLIER PHP**

| Channel Code | MLHUILLIER |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 200,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**PALAWAN PHP**

| Channel Code | PALAWAN |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 20,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**PAYMAYA PHP**

| Channel Code | PAYMAYA |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 100,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 365 |
| Save | ✓ |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**PESONET_ONLINE_BANKING PHP**

| Channel Code | PESONET_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 50,000.01 |
| Max Amount | 20,000,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | 24 |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**PNB_ONLINE_BANKING PHP**

| Channel Code | PNB_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | 24 |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**PSBANK_ONLINE_BANKING PHP**

| Channel Code | PSBANK_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 10.00 |
| Max Amount | 25,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | 24 |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**QRPH PHP**

| Channel Code | QRPH |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 50,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**RCBC_DIRECT_DEBIT PHP**

| Channel Code | RCBC_DIRECT_DEBIT |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 50,000.00 |
| Settlement Time (hours) | T+1 CALENDAR DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 30 |
| Save | ✓ |
| Payment Token Validity (years) | INDEFINITE |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**RCBC_ONLINE_BANKING PHP**

| Channel Code | RCBC_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 500.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**RD_PAWNSHOP PHP**

| Channel Code | RD_PAWNSHOP |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 20,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**ROBINSONS_BANK_ONLINE_BANKING PHP**

| Channel Code | ROBINSONS_BANK_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 10.00 |
| Max Amount | 1,000,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**ROBINSONS_BILLS_PAYMENT PHP**

| Channel Code | ROBINSONS_BILLS_PAYMENT |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 200,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**SECURITY_BANK_ONLINE_BANKING PHP**

| Channel Code | SECURITY_BANK_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 500,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**SHOPEEPAY PHP**

| Channel Code | SHOPEEPAY |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 100,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 90 |
| Save | ✓ |
| Payment Token Validity (years) | 5 |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | ✓ |

**SM_BILLS_PAYMENT PHP**

| Channel Code | SM_BILLS_PAYMENT |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 200,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**UBP_DIRECT_DEBIT PHP**

| Channel Code | UBP_DIRECT_DEBIT |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 100,000.00 |
| Settlement Time (hours) | T+1 CALENDAR DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 30 |
| Save | ✓ |
| Payment Token Validity (years) | 1 |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**UBP_EADA PHP**

| Channel Code | UBP_EADA |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 100,000.00 |
| Settlement Time (hours) | T+1 CALENDAR DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 30 |
| Save | ✓ |
| Payment Token Validity (years) | 1 |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**UNIONBANK_ONLINE_BANKING PHP**

| Channel Code | UNIONBANK_ONLINE_BANKING |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 100,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**USSC PHP**

| Channel Code | USSC |
| --- | --- |
| Country | PH |
| Currency | PHP |
| Display Merchant Name | XENDIT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 50.00 |
| Max Amount | 20,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

****TH****

**BBL_DIRECT_DEBIT THB**

| Channel Code | BBL_DIRECT_DEBIT |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 20.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | ✓ |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BBL_MOBILE_BANKING THB**

| Channel Code | BBL_MOBILE_BANKING |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 20.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**CARDS THB**

| Channel Code | CARDS |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | XENDIT, MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | T+5 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 365 |
| Save | ✓ |
| Payment Token Validity (years) | CARD EXPIRY |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | ✓ |
| Partial Capture | ✓ |
| Installments | — |

**KBANK_MOBILE_BANKING THB**

| Channel Code | KBANK_MOBILE_BANKING |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 20.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**KRUNGSRI_DIRECT_DEBIT THB**

| Channel Code | KRUNGSRI_DIRECT_DEBIT |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 20.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | ✓ |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**KRUNGSRI_MOBILE_BANKING THB**

| Channel Code | KRUNGSRI_MOBILE_BANKING |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 20.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**KTB_DIRECT_DEBIT THB**

| Channel Code | KTB_DIRECT_DEBIT |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 20.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | ✓ |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**KTB_MOBILE_BANKING THB**

| Channel Code | KTB_MOBILE_BANKING |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 20.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**LINEPAY THB**

| Channel Code | LINEPAY |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 50,000.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | Coming soon |
| Partial Refund | Coming soon |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**PROMPTPAY THB**

| Channel Code | PROMPTPAY |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 1.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**SCB_DIRECT_DEBIT THB**

| Channel Code | SCB_DIRECT_DEBIT |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 20.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | ✓ |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**SCB_MOBILE_BANKING THB**

| Channel Code | SCB_MOBILE_BANKING |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 20.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**SHOPEEPAY THB**

| Channel Code | SHOPEEPAY |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 200,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | Coming soon |
| Partial Refund | Coming soon |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | 5 |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**STANDARD_CHARTERED_VIRTUAL_ACCOUNT THB**

| Channel Code | STANDARD_CHARTERED_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 20.00 |
| Max Amount | 700,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**TRUEMONEY THB**

| Channel Code | TRUEMONEY |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 50,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | Coming soon |
| Partial Refund | Coming soon |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**WECHATPAY THB**

| Channel Code | WECHATPAY |
| --- | --- |
| Country | TH |
| Currency | THB |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 70,000.00 |
| Settlement Time (hours) | INSTANT |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | Coming soon |
| Partial Refund | Coming soon |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

****VN****

**APPOTA VND**

| Channel Code | APPOTA |
| --- | --- |
| Country | VN |
| Currency | VND |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 50,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | — |
| Refund Validity (days) | INDEFINITE |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**BIDV_VIRTUAL_ACCOUNT VND**

| Channel Code | BIDV_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | VN |
| Currency | VND |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 10,000.00 |
| Max Amount | 499,999,999.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**CARDS VND**

| Channel Code | CARDS |
| --- | --- |
| Country | VN |
| Currency | VND |
| Display Merchant Name | XENDIT, MERCHANT |
| User Approval Flow | REDIRECT, SKIP |
| Min Amount | 1,000.00 |
| Max Amount | 100,000.00 |
| Settlement Time (hours) | T+5 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 365 |
| Save | ✓ |
| Payment Token Validity (years) | CARD EXPIRY |
| Merchant Initiated Transaction | ✓ |
| Auth & Capture | ✓ |
| Partial Capture | ✓ |
| Installments | — |

**MOMO VND**

| Channel Code | MOMO |
| --- | --- |
| Country | VN |
| Currency | VND |
| Display Merchant Name | MERCHANT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 50,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | INDEFINITE |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**MSB_VIRTUAL_ACCOUNT VND**

| Channel Code | MSB_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | VN |
| Currency | VND |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 10,000.00 |
| Max Amount | 499,999,999.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**PV_VIRTUAL_ACCOUNT VND**

| Channel Code | PV_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | VN |
| Currency | VND |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 10,000.00 |
| Max Amount | 499,999,999.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | ✓ |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**SHOPEEPAY VND**

| Channel Code | SHOPEEPAY |
| --- | --- |
| Country | VN |
| Currency | VND |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 50,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 90 |
| Save | — |
| Payment Token Validity (years) | 5 |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**VIETCAPITAL_VIRTUAL_ACCOUNT VND**

| Channel Code | VIETCAPITAL_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | VN |
| Currency | VND |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 10,000.00 |
| Max Amount | 499,999,999.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**VNPTWALLET VND**

| Channel Code | VNPTWALLET |
| --- | --- |
| Country | VN |
| Currency | VND |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 50,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | — |
| Refund Validity (days) | INDEFINITE |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**VPB_VIRTUAL_ACCOUNT VND**

| Channel Code | VPB_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | VN |
| Currency | VND |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 10,000.00 |
| Max Amount | 499,999,999.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**WOORI_VIRTUAL_ACCOUNT VND**

| Channel Code | WOORI_VIRTUAL_ACCOUNT |
| --- | --- |
| Country | VN |
| Currency | VND |
| Display Merchant Name | MERCHANT |
| User Approval Flow | PRESENT TO CUSTOMER |
| Min Amount | 10,000.00 |
| Max Amount | 499,999,999.00 |
| Settlement Time (hours) | T+1 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | ✓ |
| Custom Payment Code | — |
| Refund | — |
| Partial Refund | — |
| Refund Validity (days) | - |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |

**ZALOPAY VND**

| Channel Code | ZALOPAY |
| --- | --- |
| Country | VN |
| Currency | VND |
| Display Merchant Name | XENDIT |
| User Approval Flow | REDIRECT |
| Min Amount | 1.00 |
| Max Amount | 50,000,000.00 |
| Settlement Time (hours) | T+2 BUSINESS DAYS |
| Payment Processing Time (hours) | INSTANT |
| Reusable Payment Code | — |
| Custom Payment Code | — |
| Refund | ✓ |
| Partial Refund | ✓ |
| Refund Validity (days) | 180 |
| Save | — |
| Payment Token Validity (years) | - |
| Merchant Initiated Transaction | — |
| Auth & Capture | — |
| Partial Capture | — |
| Installments | — |
