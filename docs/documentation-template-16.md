---
title: "Reconciling your Xendit Invoice"
slug: "documentation-template-16"
updated: 2026-01-06T09:26:27Z
published: 2026-01-06T09:26:27Z
canonical: "docs.xendit.co/documentation-template-16"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Reconciling your Xendit Invoice

To match transactions to your Xendit Invoice, use our Billing Report.

The Billing Report shows the full list of individual transactions and associated fees that were charged in the monthly Invoice.

## **Available columns in the Billing Report**

The table below provides the definition of every column available in the Billing Report:

| Title | Description |
| --- | --- |
| id | The transaction_id used in balance history and transactions tab reports or an ID that uniquely defines a billable event |
| reference | The unique identifier you input for the transaction. Usually the external_id or reference_id in your transaction request |
| transaction_type | The product such as VA_PAYMENT, EWALLET_PAYMENT, etc |
| transaction_channel | The subcategory of transaction_type used such as DANA, BNI, BCA, etc |
| transaction_label | The subcategory of transaction_channel used such as QR, Installments 3 Months, etc |
| is_switcher | Whether a transaction_type was a switcher transaction. Only relevant for Virtual Account and Cards transactions |
| calculation_method | The identifier of refund fee calculation of refund transactions. DEFAULT = Full refund. VARIABLE_FEE_REFUND = Partial refund. NO_FEE_REFUND = Refund transaction with no fee refunded |
| business_id | The unique identifier used to identify a Xendit merchant |
| billed_at | The timestamp of a transaction being billed based on your registered country timezone. For example, Indonesian merchants will have GMT+7 while Philippines merchants will have GMT+8 as the timestamp timezone |
| fee_pricing_currency | The currency in which the flat fees are denominated |
| tier | The pricing tier applicable to the transaction |
| flat_fee | The flat fee billing rate used for the transaction to calculate the transaction fee |
| fee_percentage | The percentage billing rate used for the transaction to calculate the transaction fee |
| net_currency | The currency of settlement of the transaction |
| gross_amount | Transaction amount expressed in net currency |
| transaction_currency | The customer facing currency for money-in and the balance currency for money-out |
| fee_amount | The amount of fees for the transaction |
| vat_amount | The amount of VAT charged to the transaction |
| deduction | Indicates if the fee is directly or indirectly deducted. Values: DIRECT (fee deducted from the transaction amount), INDIRECT (fee invoiced separately) |

##
