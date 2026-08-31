---
title: "Dispute guidelines: Cards"
slug: "dispute-guidelines-cards"
updated: 2026-08-28T05:11:27Z
published: 2026-08-28T05:11:27Z
canonical: "docs.xendit.co/dispute-guidelines-cards"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Dispute guidelines: Cards

## Overview of the Cards Dispute Process

When an account owner/cardholder raises a Cards dispute, the process typically follows a standard scenario as shown below :

![](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/base64-converted-image-1781495706291.png)

If you as a merchant are using your own acquirer to process Cards payments with Xendit (Xendit as Gateway), Acquiring Bank will forward the dispute directly to you and you will need to work the evidence together with the Acquiring Bank.

## Dispute Reasons

Account owner/cardholder may choose to contact their issuing bank/card issuer directly instead of the merchant for various reasons. These situations commonly involve concerns about unauthorized or disputed transactions.

Account owner/cardholder may initiate disputes for various reasons, including:

- **Fraudulent transactions**: Unauthorized purchases, stolen cards, or identity theft.
- **Product or service issues**: Item not received, defective products, or significantly different from the description.
- **Technical issues**: Duplicate charges, incorrect amounts, or uncredited refunds.
- **Friendly fraud**: When a cardholder intentionally raises a dispute in an attempt to keep the goods/purchase without paying for them, or the customer forgot about the purchase, or a family member made an unauthorized purchase.

When an account owner/cardholder raises a dispute to their issuing bank, Xendit will get a notification from the acquiring bank about the dispute. And we'll let you know about the dispute details.

## Understanding Your Liability

When you enter into an agreement to accept credit card payments, you also agree to abide by the rules and regulations set forth by the card networks (e.g Visa/Mastercard). These rules outline the rights, responsibilities, and procedures for handling disputes.

Dispute serves as a protective mechanism for account owner/cardholder, ensuring they can dispute unauthorized or problematic transactions. As a merchant, if a dispute is filed and validated, you are typically held liable for the disputed amount.

Here's a brief overview for clarity:

- **3D Secure (3DS) Transactions:**
  - 3DS is an additional security layer for online credit and debit card transactions. When a transaction is authenticated using 3DS, the cardholder is prompted to provide a password or other form of authentication, ensuring that they are the legitimate cardholder.
  - A successful authenticated 3DS transaction typically shifts liability from the merchant to the issuing bank in most fraudulent dispute cases (merchant can still be responsible for reasons such as good/services not delivered, etc).
  - This means that if a fraudulent transaction is successfully challenged by the cardholder, the issuing bank usually bears the loss instead of you (the merchant).
- **Non-3DS Transactions:**
  - Transactions not authenticated using 3DS lack this extra layer of security. As such, liability for any subsequent dispute will remain with the merchant as you have agreed to take on the risk of processing non-authenticated transactions. In other words, without the protection of 3DS, you have a higher risk of bearing the financial burden of fraudulent transactions.
  - Xendit's advice for merchants wary of these augmented risks is to eschew all non-3DS transactions henceforth.

For more information on Authentication, please refer [here](/v1/docs/cards-authentication-3ds2)

When using Xendit as Payment Facilitator, Xendit will place a hold* on the merchant’s balance responding to the chargeback amount related to the merchant (as stated in Xendit T&C**)

> [!WARNING]
> Xendit has the right to disable your cards channel
> 
> Upon receiving a high dispute count/ratio, Xendit has the right to temporarily or permanently stop merchants from processing Cards or payments altogether with Xendit, and merchants will also be responsible for any fines/penalty that is imposed by the card network.

* for QRIS, deduction will be made in bulk once the dispute is lost

**see table below

| Jurisdictions | T&C Link | Chargeback Clauses |
| --- | --- | --- |
| Indonesia | [https://www.xendit.co/en-id/terms-and-conditions/](https://www.xendit.co/en-id/terms-and-conditions/) | Clause 4A.9 Clause 4A.15 Clause 5.8 Clause 5.11 |
| Philippines | [https://www.xendit.co/en-ph/terms-and-conditions/](https://www.xendit.co/en-ph/terms-and-conditions/) | 5.3, 5.8 - 5.12, 5.16, 7.10, 14.2 |
| Thailand | [https://www.xendit.co/en-th/terms-and-conditions/](https://www.xendit.co/en-th/terms-and-conditions/) | 3.2.1, 4.10, 4.11, 4.12 |
| Regional (XSA) | [https://www.xendit.co/en/xendit-service-agreement/](https://www.xendit.co/en/xendit-service-agreement/) | Part 2: Service Terms COLLECTION AND SETTLEMENT SERVICES - General Clause 5,6,7 and 8 Part 2: Service Terms CARD PROCESSING SERVICES Clause 3, 5, and 6 |

## Dispute Reason Code and Defense Requirements

| **Dispute Category** | **Dispute Subcategory** | **Card Scheme** | **Description** | **Reason Code** | **Suggested Evidence** |
| --- | --- | --- | --- | --- | --- |
| Authorization | Authorization-related | Mastercard | Transaction was not properly authorized or exceeded authorization amount. | 4808 | • Valid authorization record showing approval code, matching amount/date • Terminal log or authorization message copy • Proof of split shipment authorization if applicable |
| Fraud | Unauthorized transaction | Mastercard | Cardholder claims they didn’t authorize or participate in the transaction. | 4837 | • 3-D Secure authentication record or AVS/CVV match • Signed sales receipt • Delivery confirmation or shipping tracking • Customer login/IP evidence showing participation • Record of prior undisputed transactions by same cardholder |
| Consumer Dispute | Not as Described/Defective | Mastercard | Buyer claims goods/services defective or not as described. | 4853 | • Copy of invoice or order details • Product/service description as displayed to buyer • Customer correspondence resolving or disputing issue • Proof of delivery or use • Refund or replacement evidence/ Proof that a refund was already processed before the dispute was filed. • Digital Goods: Proof of download, login timestamps, or IP logs showing the customer accessed the service. *For recurring: History of successful, undisputed purchases with your business. *Your Company's TnC |
| Consumer Dispute | Product / Service Not Received | Mastercard | Customer claims goods/service not received. | 4855 | • Proof of delivery (tracking or signed receipt) • Service completion or check-in logs • Access or usage records (e.g., digital service login) • Confirmation email or booking evidence |
| Consumer Dispute | Product / Service Not Received | Mastercard | Trip/event canceled or not delivered. | 4859 | • Booking confirmation • Merchant voucher disclosure and terms • Records showing service was available • Proof refund was processed if applicable *Your Company's TnC |
| Consumer Dispute | Credit Not Processed | Mastercard | Cardholder claims refund promised but not received. | 4860 | • Copy of refund transaction (DE 3 = 20 Purchase Return) • Settlement report showing refund posted • Timestamp proof refund occurred before chargeback • Customer communication confirming refund terms |
| Fraud | Fraudulent Transaction Claim | Mastercard | Merchant alleged to have engaged in fraud or coercion. | 4849 | • Evidence merchant not listed in QMAP • Proper fraud reporting records • Proof of legitimate transaction and fulfillment |
| Consumer Dispute | Incorrect Currency / Amount / Transaction Code | Mastercard | Dispute over number or amount of installments. | 4850 | • Signed customer agreement or contract • Documentation showing installment schedule and amounts • Proof correct billing sequence was followed |
| Consumer Dispute | General | Mastercard | Miscellaneous consumer complaint. | 4854 | • Copy of contract or purchase agreement • Refund/cancellation policy disclosure • Correspondence showing merchant tried to resolve issue |
| Processing Error | Duplicate Processing | Mastercard | Same transaction processed more than once. | 4806 | • POS/system logs showing single valid sale • Void or refund record for duplicate • Settlement audit showing correction applied |
| Fraud | Card not Present | Visa | Cardholder claims they did not authorize online or phone order. | 10.4 | • Compelling evidence of cardholder participation (3-D Secure authentication, CVV2 match, IP/device match) • Proof of product delivery or usage • Prior undisputed transactions from same account *Proof of download, login timestamps, or IP logs showing the customer accessed the service. *For recurring: History of successful, undisputed purchases with your business. *Your Company's TnC |
| Fraud | Visa Fraud Monitoring Program | Visa | Transaction identified as high-risk/fraudulent through Visa monitoring. | 10.5 | • Proof transaction validated through 3-D Secure • Fraud monitoring system evidence • Correspondence showing legitimate transaction |
| Authorization | Unauthorized transaction | Visa | Transaction completed without obtaining valid authorization. | 11.3 | • Authorization log showing approval before settlement • Reconciliation records • Proof that system automatically obtained auth prior to capture |
| Processing Error | Incorrect Account Number | Visa | The account number in the authorization does not match the account number used in the transaction. | 12.4 | • Invoice showing single valid payment • POS logs showing one completion • Proof refund or void issued for duplicate • Authorization logs |
| Processing Error | Duplicate Processing | Visa | A single transaction was processed two or more times. | 12.6.1 | • Invoice showing single valid payment • POS logs showing one completion • Proof refund or void issued for duplicate • Evidence of payment reconciliation |
| Processing Error | Paid by Other Means | Visa | You charged the customer’s card. But, the customer claims to have already paid for the transaction in question using another payment method, like cash, check, or another card. | 12.6.2 | • Invoice showing single valid payment • POS logs showing one completion • Proof refund or void issued for duplicate • Evidence of alternate payment reconciliation |
| Processing Error | Incorrect Currency / Amount / Transaction Code | Visa | Cardholder claims amount charged differs from agreed. | 12.5 | • Sales receipt showing correct transaction amount • Terminal or POS batch record • Customer communication confirming correct amount |
| Consumer Dispute | Product / Service Not Received | Visa | Customer claims goods/services not delivered or rendered. | 13.1 | • Delivery proof (signed courier receipt, tracking info) • Service completion logs • Refund proof if service canceled • Check-in or usage evidence (for digital services) *Proof of download, login timestamps, or IP logs showing the customer accessed the service. *For recurring: History of successful, undisputed purchases with your business. *Your Company's TnC |
| Consumer Dispute | Canceled Recurring | Visa | Merchant charged customer after cancellation request. | 13.2 | • Proof cancellation received after billing date • Terms of cancellation policy disclosed • Evidence service is still provided • Communication confirming customer agreement *Your Company's TnC |
| Consumer Dispute | Not as Described/Defective | Visa | Customer claims product/service not as described. | 13.3 | • Product listing and description proof • Correspondence resolving issue • Proof of repair, replacement, or satisfaction • Customer usage or access logs |
| Consumer Dispute | Counterfeit Merchandise | Visa | Customer alleges counterfeit goods. | 13.4 | • Manufacturer or brand authenticity certificate • Supplier invoice or product sourcing documents |
| Consumer Dispute | Misrepresentation | Visa | Cardholder claims merchant misled about terms, location, or merchant name. | 13.5 | • Screenshots or documentation of accurate representation • Contract or order confirmation with correct merchant name and terms |
| Consumer Dispute | Credit Not Processed | Visa | Refund promised but not posted. | 13.6 | • Refund record (credit transaction ID) • Settlement report showing refund posted before dispute • Communication with cardholder acknowledging refund |
| Consumer Dispute | Credit Not Processed | Visa | Cardholder canceled but was still billed. | 13.7 | • Documentation of cancellation policy • Proof cancellation received after nonrefundable cutoff • Evidence of service or delivery rendered prior to cancellation |
| Consumer Dispute | Original Credit Transaction Not Accepted | Visa | Credit transaction not properly processed or rejected. | 13.8 | • Processor or settlement logs confirming valid credit processed • Screenshot of merchant refund portal showing status |

## Arbitration

After the first two steps of evidence verification from the bank, there is a possibility that the issuing bank deems the evidence to still be not enough. If so, the issuing bank can then raise the dispute to arbitration.

Xendit will inform you about the arbitration step, and you'll need to make the decision whether you want to challenge the arbitration or not. If you want to challenge, then we'll require you to collect further evidence and submit it to us at the latest 7 calendar days from the 2nd chargeback / pre-arbitration notification, and we will send it to the acquiring bank, and then the issuing bank. If you win, you'll win the dispute. However, if you lose, the arbitration fee (USD 500 up to USD 600) on top of the amount of lost dispute.

The Card Scheme (i.e. VISA, Mastercard, etc) will be the deciding party of the final dispute status.

### Dispute Withdrawal

If your customer wishes to withdraw their dispute, please collect the following information and documents:

- Full name (must match the cardholder name)
- Transaction date
- Transaction amount
- Reason for withdrawal
- Confirmation from their issuing bank / Copy of Retract Letter from Issuing Bank / Copy of Official Form from the Issuing Bank (mandatory)

Please submit / advise the customer to submit these documents directly to [chargebacks@xendit.co](mailto:chargebacks@xendit.co).

### Cards Dispute and Fraud Monitoring Programs

Each network has its own fraud and dispute monitoring programs which are imposed to control and minimize disputes as they want account owner/cardholder to be comfortable opening credit card accounts and using them to make purchases both in person and online.

While these monitoring programs can provide merchants with specific assistance in identifying dispute root causes and developing effective prevention plans, the fines and penalties are quite severe. For example, if you’re enrolled in a program for a certain period of time without improvements in your chargeback/dispute rates, you will be eligible for disqualification from processing the network’s payments.

#### Visa Acquirer Monitoring Program (VAMP)

Visa launched the Visa Acquirer Monitoring Program (VAMP) on 1 April 2025, combining the former VDMP (Visa Dispute Monitoring Program) and VFMP (Visa Fraud Monitoring Program) frameworks into a single global program.

The VAMP measures performance based on two key metrics:

- VAMP ratio
- VAMP enumeration ratio

**VAMP Ratio and Threshold**

- Ratio Formula: Count of [Fraud (TC40) + Disputes (TC15)] ÷ Count of Settled Transactions (TC05)
- VAMP Ratio has additional criteria:
  - Excludes disputes resolved through pre-dispute solutions, contingent on the timing of the data extract.
  - Excludes TC 40 fraud qualified for Compelling Evidence 3.0, contingent on the timing of the data extract.
- Dispute with reason codes 10 (except 10.5), 11, 12, and 13
- A single fraudulent transaction may be reflected in both the TC40 and TC15 reports. If a transaction appears in both reports, it will be recorded twice in the VAMP count.

| Thresholds | VAMP Count | VAMP Ratio |
| --- | --- | --- |
| Non-compliant | 5 | 0.5% |
| Excessive | 150 in CEMEA 1,500 globally | 2.2% in CEMEA 1.5% globally Effective Apr 1, 2026 |

A fine of USD 10 may be applied for each transaction that is deemed fraudulent or disputed, particularly in cases where Merchant got into the Excessive threshold.

**VAMP Enumeration Ratio and Threshold**

- Ratio Formula: Total number of confirmed cards not present (CNP) enumerated transactions (approved plus declined) divided by the total number of CNP transactions (approved plus declined).
- Ratio Formula: [Count of Enumerated Authorization Transactions (Approved + Declined)] ÷ [Count of Authorization Transactions (Approved+ Declined)], ≥ 2000 bps
- VAMP Enumeration Transaction Count, defined as Enumerated Transactions (Approved + Declined), ≥ 300,000

| Threshold | VAMP Enumeration Count | VAMP Enumeration Ratio |
| --- | --- | --- |
| Excessive | Minimum of 300,000 | 20% |

#### Mastercard Excessive Chargeback Program (ECP)

Mastercard’s Excessive Chargeback Program (ECP) consists of two levels: Excessive Chargeback Merchant (ECM) and High Excessive Chargeback Merchant (HECM), and it applies to users in all supported countries. The program's purpose is to exercise oversight regarding eCommerce merchants and prevent too many chargebacks from occurring on the Mastercard network.

| Threshold | Dispute Count | Chargeback Rate | Fines |
| --- | --- | --- | --- |
| Excessive (ECM) | 100-299 | 1.5-2.99% | Fines begin in month two and continue at increasing rates in subsequent months |
| High Excessive (HECM) | 300+ | 3% | Fines begin in month two and continue at increasing rates in subsequent months |

#### Mastercard Excessive Fraud Merchant Program (EFM)

Mastercard EFM monitors fraud-related chargeback from e-commerce transactions at the merchant ID level. EFM is calculated based on dispute *reason code 4837 - No cardholder authorization* which indicates that the cardholder did not authorize the charge or *reason code 4863 - Cardholder Does Not Recognize—Potential Fraud* which indicates that the cardholder claims they don't recognize a card-not-present transaction.

A merchant will be identified as EFM if they meet or exceed all following four criteria:

| Threshold | Number of Electronic- Commerce Transactions | Chargeback Rate (fraud Reason code only) | Fraud Chargeback Amount | 3DS Mastercard payment |
| --- | --- | --- | --- | --- |
| Excessive | Minimum of 1,000 e-commerce Mastercard payments | 0.5% | Net fraud volume is greater than USD 50,000 | 10% of total Mastercard payment count (non-regulated countries) 50% of total Mastercard payment count (regulated countries) |
