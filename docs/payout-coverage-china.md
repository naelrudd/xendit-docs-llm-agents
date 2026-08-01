---
title: "China"
slug: "payout-coverage-china"
updated: 2026-07-09T02:33:19Z
published: 2026-07-09T02:33:19Z
canonical: "docs.xendit.co/payout-coverage-china"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# China

## Overview

| Payout Rail | Local - CIPS | Local - Alipay |
| --- | --- | --- |
| Supported Currencies | CNY | CNY |
| Estimated Time of Arrival | T+3 business days at 16:30 | Instant |
| Cut-off Time | 09:00 (Asia/Shanghai GMT+08:00) | N/A |
| Transaction Limit | No limit | 50,000 |
| Description Support | Yes | Yes |
| Supported Use Case | B2B | B2C |

## Supported Channels

Learn the different payout destinations that we support along with its destination-specific information in the table below:

[Embedded content](https://airtable.com/embed/appa8YthqtdBznm0k/shrUw1xDwbrrra1y5)

## Alipay

Alipay is a digital eWallet that allows users to make payments on their phone by storing their debit or credit card or bank account. In addition to that, Alipay allows users to receive money directly to their Chinese bank accounts (if successfully linked) for cross-border payout from abroad.

> [!NOTE]
> **Note:** A user must have a valid account with Alipay first before being able to receive a cross-border payout. However, Xendit still has the capability to reach more than 95% of bank accounts in China if the beneficiary has successfully linked his/her bank account.

#### Beneficiary Experience

1. A beneficiary receives a payment notification
2. The beneficiary accepts the payment
3. If the user has previously linked a bank account: Funds will arrive in the linked bank account
4. If the user has not previously linked a bank account: Beneficiary is given 72 hours to link a bank account

## B2B Bank Payout

(i) For sending B2B cross-border transactions into China, Xendit will return the completed result when the funds has already been cleared to the beneficiary bank side, but as of now there is no common practice regarding how and when in exact the beneficiary banks release the funds to beneficiary, and we won’t have visibility between the beneficiary and the beneficiary bank due to clearing system limitation

(ii) For most of the CNY transactions, the beneficiary banks may hold the fund themselves and contact the beneficiaries to provide supporting documents and transaction information before releasing the fund; This happens between beneficiary bank and beneficiary and hence Xendit has no visibility on when does the transaction released to the beneficiary; Please make sure the beneficiary is prepared for the providing supporting documents and explain the nature of the transaction with their own banks with the note on (iii)

(iii) The remitter of the transaction will be sent as "Thunes Hong Kong Limited" to the beneficiary banks, when the beneficiary banks ask the beneficiaries to provide more supporting documents, please indicate that the transaction is paid via POBO model and Thunes is the partnering payment service provider to process the transactions together with the required supporting documents of the transactions.

(iv) Due to clearing system limitation, the provided supporting documents could not be sent over to the beneficiary banks automatically, so please share the supporting documents to the beneficiaries and ask the beneficiary's registered bank contact person to be prepared for clarification.

### Supporting Documents

> [!NOTE]
> Disclaimer:
> 
> All CNY B2B payments to China require supporting documentation.

The supporting documentation required will differ depending on the purpose of your transaction. Below is a list with the `purpose_code` and the corresponding documentation that is required when making a CNY payment to China.

| **Purpose Code** | **Documentation Required** | **Required Attachment Type** |
| --- | --- | --- |
| `EXPORT` | **Pre-payment of goods:** - Purchase Order **Post-payment of goods:** - Logistics bill (Select type as delivery slip) - Customs declaration (Select type as delivery slip) - Purchase order/invoice/contract | **Pre-payment:** - `PURCHASE_ORDER` **Post-payment:** - `DELIVERY_SLIP` - `PURCHASE_ORDER` / `INVOICE` / `CONTRACT` |
| `DELIVERY` | - Bill of lading (Select type as delivery slip) - Contract/invoice | - `DELIVERY_SLIP` - `INVOICE` / `CONTRACT` |
| `TRAVEL` | - Flight tickets (Select type as purchase order) - Travel documents (Select type as purchase order) - Confirmation of hotel booking (Select type as purchase order) | - `PURCHASE ORDER` - `INVOICE` for flight ticket, visa, hotel booking |
| `HOTEL` | - Confirmation of hotel booking (Select type as purchase order) | - `PURCHASE_ORDER` |
| `OFFICE` | - Contract - Invoice | - `CONTRACT` - `INVOICE` |

**Note: While not validated, there is very huge chance that wrong document will not pass processing*

- Supporting documents must be stamped by the beneficiary (contracts need to be stamped by both parties), else it will lead to potential reversals of transactions due to improper supporting documents
- The invoice amount, sending business and receiving business registered name and address specified in the supporting doc must match the transaction information provided in API level, else it will lead to potential reversals of transactions due to improper supporting documents
- The receiving bank account needs to be a business account
- The payout currency must always match that of the invoice currency

## Payout Identifier

When creating a payout, you can also include a unique identifier (e.g. Order ID, your business name, etc.) in the `description` field. If your recipient's bank supports it, they'll see this in their transaction history. Note that actual display length limits vary by bank, so keep your identifier short.

What will be displayed is a combination of your `business_name` and `description`. Total length can only be up to 148 characters.

| **Destination Channel** | **Amount** | **Max. Characters** |
| --- | --- | --- |
| Any | Any | 148 characters (Including your Business Name) |
