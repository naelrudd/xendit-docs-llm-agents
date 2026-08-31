---
title: "Dispute & chargeback basics"
slug: "dispute-chargeback-basics"
status: "update"
updated: 2026-08-28T06:20:12Z
published: 2026-08-28T06:20:12Z
canonical: "docs.xendit.co/dispute-chargeback-basics"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Dispute & chargeback basics

<!--
RESTRUCTURE METADATA (remove before publishing — for CMS migration reference only)
Section: Disputes
Order: 2 of 5
Old title: Handling disputes and chargeback
Old slug: /docs/handling-disputes-and-chargeback
New slug: /docs/dispute-chargeback-basics
Change log: H1 renamed. The "Dispute Guidelines section" reference (previously
            unlinked plain text) now links to the two channel-specific
            guideline pages, since that single reference now maps to two pages.
            No wording, facts, or figures changed.

CAUTION: my source for this page's body was a JS-rendered fetch that stripped
heading levels and list formatting (no bullets/line breaks came through). I've
reconstructed the structure below based on the visible section titles and
table headers, but this should be diffed against the live CMS source before
publishing — I can't 100% guarantee heading levels, bullet grouping, or the
two embedded lifecycle diagrams (referenced below as images) match the
original exactly. Content/wording itself is unchanged from what was fetched.
-->

## Understanding disputes
### Dispute vs. chargeback
**Dispute:** the claim and the process. It starts when a customer raises a concern about a transaction, whether with you, a payment provider, or their bank, regardless of payment method or how far it has escalated.
 
**Chargeback:** the term for the fund movement within a dispute, used at Xendit for both Cards and other payment channels.
 
Not every payment channel has a dispute flow; see [Dispute guidelines: Cards](https://docs.xendit.co/docs/dispute-guidelines-cards) and [Dispute guidelines: QRIS](https://docs.xendit.co/docs/dispute-guidelines-qris) for a detailed explanation.
 
<!-- ^ link updated: previously a single unlinked reference to "the Dispute Guidelines section," now split since that section is two separate pages (Cards, QRIS) in the new structure -->
 
<!-- ^ this whole "Dispute vs. chargeback" definition was swapped in from manage-disputes-via-dashboard.md per instruction: this page is now the sole source of this definition, Dashboard's own copy was removed and replaced with a pointer link here. Original "What is a dispute?" text (the "forceful reversal of payments" framing) removed as superseded. -->

### Refund vs. dispute

Understanding the difference between a refund and a dispute is essential for your operations:

- **Who initiates:** Refunds are initiated by you (the merchant) directly to the account owner/cardholder. Disputes are initiated by the account owner/cardholder through their issuer, up to 540 days post transaction.
- **Processing time:** Refunds typically take 14 business days (depending on the issuer). Disputes processing time can take between 30–180 days or more.
- **Associated fees:** Refunds have no additional fees. Disputes can incur some cost.
- **Impact:** Refunds are a normal part of business. Disputes can affect your dispute-to-sales ratio and may result in enrollment in applicable monitoring programs.

## Dispute lifecycle and timeframe

| Stage | Cards | QRIS |
| --- | --- | --- |
| **Dispute raised** — deadline for an account owner/cardholder (through the issuer) to submit a dispute | 120 calendar days from transaction date, up to 540 calendar days from transaction date (for non-fraud reason code) | 90 calendar days from the transaction date |
| **Re-presentment** — deadline for you, the Merchant (through Xendit), to submit evidence to fight the dispute | 7 calendar days from the 1st dispute notification. *Failing to respond within this 7-day window typically results in an automatic loss of the dispute.* | Typically 7 calendar days from 1st dispute notification, or as stated on the email notification. *Failing to respond within this 7-day / due-date window typically results in an automatic loss of the dispute.* |
| **Dispute review & decision (2nd chargeback)** — deadline for the Issuer to reject the evidence provided by the Merchant (through Xendit) | 30 up to 45 calendar days after the representment date | 7 calendar days after the representment date |
| **Arbitration** — deadline for you, the Merchant (through Xendit), to re-challenge the Issuer at their discretion | 7 calendar days from 2nd Chargeback notification / re-presentment outcome. *Additional fee of USD 500–600 applies on top of the disputed amount for the losing party.* | 5 calendar days from 2nd Chargeback notification / re-presentment outcome. *Additional fee of IDR 500,000 applies on top of the disputed amount for the losing party. Eligibility for this stage applies to transactions starting from IDR 500,000 and above.* |

*"Calendar days" means every day as listed on a calendar, including weekends and holidays.*

Cards dispute lifecycle and timeline diagram
![cards_base64-converted-image-1787894684076.png](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/cards_base64-converted-image-1787894684076.png){height="" width=""}



QRIS dispute lifecycle and timeline diagram
![qris_base64-converted-image-1787894684078.png](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/qris_base64-converted-image-1787894684078.png){height="" width=""}


<!-- ^ two diagrams were embedded on the original page; re-embed the source images here, I only have the alt text from the fetch, not the image assets themselves -->

## What happens when a dispute is raised

This describes the process for payment channels other than Cards and QRIS, which are still handled by Xendit Ops over email. 

For Cards and QRIS disputes, evidence submission and the challenge/accept decision happen directly in the dashboard, see [Manage disputes via Dashboard](https://docs.xendit.co/docs/manage-disputes-via-dashboard).

When an account owner/cardholder disputes a charge to their issuing financial institution (issuer), Xendit will:

1. Send you an email containing information about the incoming dispute.
2. Show the reason for the dispute; you'll be able to submit evidence to fight the dispute by replying to the same email before the due date.
3. Hold the disputed amount from your Xendit Balance, as the payment network will pull funds for the disputed amount (the hold will be temporary if you win the dispute). For QRIS, the deduction will be made in bulk once the dispute is lost.
