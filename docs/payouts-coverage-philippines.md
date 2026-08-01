---
title: "Philippines"
slug: "payouts-coverage-philippines"
updated: 2026-07-09T02:30:56Z
published: 2026-07-09T02:30:56Z
canonical: "docs.xendit.co/payouts-coverage-philippines"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Philippines

| Payout Rail | Local - InstaPay | Local - PESONet |
| --- | --- | --- |
| Supported Currencies | PHP | PHP |
| Estimated Time of Arrival | 15 minutes | Same day |
| Cut-off Time | N/A | 14:00 GMT+08 |
| Transaction Limit | 50,000 | Unlimited |
| Description Support | No | No |
| Supported Use Case | B2B, B2C, C2B, C2C | B2B, B2C, C2B, C2C |

## Supported Channels

Learn the different payout destinations that we support along with its destination-specific information in the table below:

[Embedded content](https://airtable.com/embed/appa8YthqtdBznm0k/shrfGsv5sXm9189Oi)

## Payout Identifier

When creating a payout, you can also include a unique identifier (e.g. Order ID, your business name, etc.) in the `description` field. If your recipient's bank supports it, they'll see this in their transaction history. Otherwise, they’ll see Xendit’s sender name. Note that character limits vary by bank, so keep your identifier short.

| **Destination Channel** | **Amount** | **Max. Characters** |
| --- | --- | --- |
| `PH_UBP` | Any amount | 50 characters |
| Other banks | Any amount | Description may not be supported |

## Recipient Interface

### Bank Channels

See below for examples of what is shown in your recipient’s bank statement. If supported, the bank statement will display Xendit as sender and the `description` you input.

| **Channel** | **Sample of line on bank statement** |
| --- | --- |
| `PH_GCASH` | You have received GCash from xendit-fds |
| `PH_BPI` | PARTNER Transfer FROM:XENDIT PHILIPPINES INC |
| `PH_BDO` | 00083650008365 9 IBTD 801695801695 |
| `PH_SEC` | ONLINE TRANSFER |

### E-Wallet Channels

See below for examples of what is shown in your recipient's e-wallet apps. If supported, the app will display Xendit as the sender and the `description` you input.

![](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/image(129).png)
