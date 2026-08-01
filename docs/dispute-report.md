---
title: "Dispute Report"
slug: "dispute-report"
status: "new"
updated: 2026-07-31T06:20:51Z
published: 2026-07-31T06:20:51Z
canonical: "docs.xendit.co/dispute-report"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Dispute Report

# Dispute report

The Dispute Report provides an itemized list of payment disputes raised against your account, including status, reason, amounts, and key dates. Use it to track the dispute lifecycle and reconcile dispute related deductions and reversals against your balance.

## Download Dispute Reports

- **On demand export**: Download directly from your dashboard's Disputes page.
- **Scheduled exports**: Currently not supported.
- **Export via API**: Currently not supported.

### Reports data

Column Header is the literal CSV header as it appears in the exported file.

| Column Name | Column Header | Description |
| --- | --- | --- |
| Dispute ID | `dispute_id` | Unique identifier for the dispute. |
| Payment ID | `payment_id` | ID of the original disputed payment. |
| Status | `status` | Current status of the dispute (single, most current value): `ACTION_REQUIRED`, `UNDER_REVIEW`, `WON`, or `LOST`. |
| Reason | `reason` | Category describing why the dispute was raised, such as fraud, product/service not received, duplicate processing, or billing error. Full list varies by payment channel. |
| Payment Method Type | `payment_method_type` | Broad category of the disputed payment method. Available at pilot: `QR`, `CARDS`. |
| Payment Channel | `payment_channel` | Specific channel within the payment method type. Available at pilot: `QRIS`, `CARDS`. |
| Card Brands | `card_brands` | Card network brand, applicable to CARDS disputes. Available at pilot: `MASTERCARD`, `VISA`. |
| Currency | `currency` | Currency of the disputed payment. |
| Dispute Amount | `dispute_amount` | Amount being disputed. |
| Payment Amount | `payment_amount` | Original full amount of the disputed payment. |
| Payment Reference | `payment_reference` | Your reference from the original payment, used to match the dispute against your own records. |
| Chargeback Transaction ID | `chargeback_transaction_id` | ID of the chargeback (deduction) transaction, as shown on the Transactions report. |
| Chargeback At | `chargeback_at` | Date the chargeback deduction occurred. |
| Chargeback Reversal Transaction ID | `chargeback_reversal_transaction_id` | ID of the chargeback reversal transaction, as shown on the Transactions report. |
| Chargeback Reversal At | `chargeback_reversal_at` | Date the disputed funds were reversed back to your balance. |
| Dispute Created On | `dispute_created_on` | Date the dispute was filed. |
| Last Update | `last_update` | Timestamp of the most recent update to the dispute record. |
