---
title: "Optimizing operations"
slug: "optimizing-operations"
updated: 2026-07-08T15:39:43Z
published: 2026-07-08T15:39:43Z
canonical: "docs.xendit.co/optimizing-operations"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Optimizing operations

Learn how to reduce your customer complaints and help your customer inquiries. This page will guide you through some best practices that would allow you to achieve operational excellence.

## Common operation issues

### Funds not received

Due to messaging issues, your recipient might get back to you saying that the funds have not been received. To help with this process, we recommend that you:

- Subscribe to payout webhooks for latest status updates and auto recovery
- Send Payout receipt to your recipient for them to track and log an issue with their bank
- Utilize `description` to send identifiers to your recipient’s app or statement

### Funds bounced back

Sometimes we cannot pay the funds out or the funds are returned to us due to processing limitations (e.g. the recipient’s details were incorrect or their account is closed). We recommend that you:

- Subscribe to reversed/failed webhooks for latest status updates

## Tool for reducing operations issues

### Payout receipts

Payout receipts is a simple yet powerful tool to assure your recipient that the funds has been processed, and if not yet received, is on its way to their account. If utilized, we will send this on behalf of you directly to your recipient on successful payout processing.

### Resend payout receipts

Easily resend payout receipts from your dashboard to share with recipients as proof of transfer.

#### Batch Payouts

1. Go to [Payouts](https://dashboard.xendit.co/payouts)
2. Click on your selected batch payout
3. Click the checkboxes to select your preferred transaction
4. Click **Download All Receipts**
5. A download link (valid for 7 days) will be emailed to you
6. Open the email and click to download your receipt(s)
