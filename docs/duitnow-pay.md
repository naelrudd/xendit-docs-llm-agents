---
title: "Duitnow Pay"
slug: "duitnow-pay"
updated: 2026-07-24T08:55:08Z
published: 2026-07-24T08:55:08Z
canonical: "docs.xendit.co/duitnow-pay"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Duitnow Pay

DuitNow Pay is a seamless online payment solution provided by PayNet, enabling businesses to offer fast and secure checkouts directly from a customer's account with reduced friction.

When customers select DuitNow Pay at checkout, they can seamlessly authorize payments directly from their preferred bank account. Once the payment is processed, you receive an instant confirmation, ensuring a frictionless and high-conversion transaction experience for you and your customers.

| **Channel Code** | DUITNOW_PAY |
| --- | --- |
| **Display Name** | DuitNow Pay |
| **Currency** | MYR |
| **Country** | MY |
| **Type** | ONLINE BANKING |
| **Min Amount** | 1.00 |
| **Max Amount** | 30,000.00 |
| **User Approval Flow** | REDIRECT |
| **Reusable Payment Code** | - |
| **Save** | - |
| **Merchant Initiated Transaction** | - |
| **Auth & Capture** | - |
| **Partial Capture** | - |
| **Multiple Partial Capture** | - |
| **Desktop Support** | WEB URL |
| **Mobile Support** | MOBILE WEB URL |
| **Custom Payment Code** | - |
| **Display Merchant Name** | XENDIT |
| **Display User Name** | - |
| **Set Expiry** | - |
| **Payment Request Expiry (hours)** | 0.5 |
| **Payment Token Validity (years)** | INDEFINITE |
| **Payment Processing Time (hours)** | INSTANT |
| **Settlement Time** | T+1 BUSINESS DAY |
| **Installments** | - |
| **Refund** | ✓ |
| **Partial Refund** | ✓ |
| **Multiple Partial Refund** | ✓ |
| **Refund Validity (days)** | 90 |
| **Payment Link** | ✓ |
| **Fund Flow** | AGGREGATOR, GATEWAY |

## Payment Flows

![](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/image(219).png)

## Supported Issuers

| **Issuer Name** | **BIC Code (DuitNow Pay)** | **Retail** | **Corporate** | **FPX** | **DuitNow Pay** |
| --- | --- | --- | --- | --- | --- |
| Affin Bank | PHBMMYKL | ✅ | ✅ | ✅ | ✅ |
| Alliance Bank Malaysia Berhad | MFBBMYKL | ✅ | ✅ | ✅ | ✅ |
| MBSB Bank Berhad | AFBQMYKL | ✅ | ✅ | ❌ | ✅ |
| Agro Bank | AGOBMYKL | ✅ | ✅ | ✅ | ✅ |
| Ambank Berhad | ARBKMYKL | ✅ | ✅ | ✅ | ✅ |
| CIMB Bank | CIBBMYKL | ✅ | ✅ | ✅ | ✅ |
| Bank Islam | BIMBMYKL | ✅ | ✅ | ✅ | ✅ |
| Bank of China (M) Berhad | BKCHMYKL | ✅ | ❌ | ❌ | ✅ |
| Bank Kerjasama Rakyat Malaysia Berhad | — | ✅ | ❌ | ✅ | ❌ |
| Bank Muamalat | BMMBMYKL | ✅ | ✅ | ✅ | ✅ |
| Boost Bank | BOBEMYK2 | ✅ | ❌ | ❌ | ✅ |
| Bank Simpanan Nasional Berhad | BSNAMYK1 | ✅ | ❌ | ✅ | ✅ |
| Finexus | FNXSMYNB | ✅ | ❌ | ❌ | ✅ |
| HSBC Bank | HBMBMYKL | ✅ | ❌ | ✅ | ✅ |
| Hong Leong Bank Berhad | HLBBMYKL | ✅ | ❌ | ✅ | ✅ |
| Kuwait Finance House | — | ✅ | ❌ | ✅ | ❌ |
| Maybank | MBBEMYKL | ✅ | ✅ | ✅ | ✅ |
| MobilityOne | MBLOMYNB | ✅ | ❌ | ❌ | ✅ |
| OCBC Bank (Malaysia) Berhad | OCBCMYKL | ✅ | ❌ | ✅ | ✅ |
| Public Bank Berhad | PBBEMYKL | ✅ | ✅ | ✅ | ✅ |
| RHB Banking Group | RHBBMYKL | ✅ | ✅ | ✅ | ✅ |
| Al-Rajhi Bank | RJHIMYKL | ✅ | ❌ | ❌ | ✅ |
| Standard Chartered Bank Malaysia Berhad | — | ✅ | ❌ | ✅ | ❌ |
| United Overseas Bank Berhad (UOB) | UOVBMYKL | ✅ | ✅ | ✅ | ✅ |
| JP Morgan Chase Bank Berhad | CHASMYKX | ❌ | ✅ | ❌ | ✅ |
| Deutsche Bank (Malaysia) Berhad | DEUTMYKL | ❌ | ✅ | ❌ | ✅ |
| Sumitomo Mitsui Banking Corporation (M) Berhad | SMBCMYKL | ❌ | ✅ | ❌ | ✅ |

**Notes**

**Retail** – Available for consumer/personal banking accounts.

**Corporate** – Available for business/corporate banking accounts.

**FPX** – The issuer supports payments via the FPX payment rail.

**DuitNow Pay** – The issuer supports payments via the DuitNow Pay (Online Banking/Open Banking) payment rail.
