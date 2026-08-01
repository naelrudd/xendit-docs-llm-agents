---
title: "Indonesia"
slug: "payout-coverage-indonesia"
updated: 2026-07-09T02:30:11Z
published: 2026-07-09T02:30:11Z
canonical: "docs.xendit.co/payout-coverage-indonesia"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Indonesia

## Overview

| Payout Rail | Local - BI Fast | Local - RTGS |
| --- | --- | --- |
| Supported Currencies | IDR | IDR |
| Estimated Time of Arrival | 15 minutes | 2 hours |
| Cut-off Time | N/A | 14:00 GMT+7 |
| Transaction Limit | 250,000,000 | Unlimited |
| Description Support | Yes | Yes |
| Supported Use Case | B2B, B2C, C2B, C2C | B2B, B2C, C2B, C2C |

## Supported Channels

Learn the different payout destinations that we support along with its destination-specific information in the table below:

[Embedded content](https://airtable.com/embed/appa8YthqtdBznm0k/shrgBfVnvtxbZQxRR)

## Account length limit

### Bank accounts

The number of digits in a bank account number for each of the banks in Indonesia varies according to the bank. The following is the guideline of bank account length for the top banks in Indonesia.

| **Bank Code** | **Account Number Length** |
| --- | --- |
| BCA | 10 Digits |
| BRI* | 13-17 Digits |
| BNI | 7-11 Digits |
| MANDIRI* | 12-17 Digits |
| PERMATA* | 7-16 Digits |

**Note: The number of digits may include the length for Virtual Accounts.*

Notes for BRI : Please make sure to add an extra 0 prefix in the case of a bank accounts with 14 digits. This is not applicable to VA accounts. (eg. 012345678901234)

### E-Wallet Accounts

E-wallet accounts in Indonesia are based on Indonesian mobile numbers. While mobile numbers are usually written to include the country code, when mobile numbers are used as e-wallet account numbers, it is more common to use the format that contains 11 digits and where the prefix starts with zero (0). Example: `0XXXYYYZZZZ`

## Payout Identifier

When creating a payout, you can also include a unique identifier (e.g. Order ID, your business name, etc.) in the `description` field. If your recipient's bank supports it, they'll see this in their transaction history. Otherwise, they’ll see Xendit’s sender name. Note that character limits vary by bank, so keep your identifier short.

| **Destination Channel** | **Amount** | **Max. Characters** |
| --- | --- | --- |
| BCA | Less than IDR 9,999 or more than IDR 50,000,001 | 30 characters |
| BCA | IDR 10,000 - IDR 50,000,000 | 15 characters |
| BRI | Any amount | 29 characters |
| BNI | Any amount | 14 characters |
| MANDIRI | Any amount | 14 characters |
| PERMATA | Any amount | 20 characters |
| CIMB | IDR 10,000 - IDR 50,000,000 | 18 characters |
| MAYBANK | IDR 10,000 - IDR 50,000,000 | 17 characters |
| Other banks | IDR 10,000 - IDR 50,000,000 | Description may not be supported |

## Recipient Interface

### Bank Channels

See below for examples of what is shown in your recipient’s bank statement. If supported, the bank statement will display Xendit as sender and the `description` you input.

| **Channel** | **Sample of line on bank statement** |
| --- | --- |
| BCA | TRSF E-BANKING CR 0410/FTSCY/WS95051 1000.00 2NU6g~[Description] SINAR DIGITAL TERD, or SWITCHING CR TRANSFER DR 523 [Description] KPO BSS |
| BNI | TRANSFER DARI XENDIT One Gate Payment #201910090128466362836245 [Description] 201910090128466362836245 SINAR DIGITAL TERDEPAN |
| BRI | ~3SeQr SNR [Description] |
| MANDIRI | 1260007569477 10/10/2019 10/10/2019 7820 MCM InhouseTrf CS-CS DARI SINAR DIGITAL TERDEPAN [Description] #2PmKJ 0 123 |

### E-Wallet Channels

See below for examples of what shows up on your recipient's e-wallet apps. If supported, the app will display Xendit as the sender and the `description` you input.

![](https://archive.docs.xendit.co/_next/image?url=https%3A%2F%2Fstatic.xendit.co%2Fxendit-docs%2Fa9125230-562d-4205-9c43-c427d85f3ee6%2F2021%2F7%2F27%2F33127265-ba0b-45f7-87d5-e39ab9c7248a%2Fscreenshot-2021-05-06-at-2.29.21-pm.png&amp;w=1200&amp;q=75)
