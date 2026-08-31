---
title: "Manage disputes via Dashboard"
slug: "manage-disputes-via-dashboard"
status: "new"
updated: 2026-08-28T05:30:48Z
published: 2026-08-28T05:30:48Z
canonical: "docs.xendit.co/manage-disputes-via-dashboard"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Manage disputes via Dashboard

<!--
RESTRUCTURE METADATA (remove before publishing — for CMS migration reference only)
Section: Disputes
Order: 1 of 5
Old title: Dispute Management
Old slug: /docs/dispute-management
New slug: /docs/manage-disputes-via-dashboard
Change log: H1 renamed to match "Manage disputes via API" naming convention.
            One internal anchor link updated to the new slug (was pointing at
            the old /docs/dispute-management URL). No other content changed.
-->
 
Dispute Management gives you a single place to track, manage, and respond to disputes on your transactions, directly from your dashboard.
 
> New to disputes? See [Dispute & chargeback basics](https://docs.xendit.co/docs/dispute-chargeback-basics#dispute-vs-chargeback) for what "dispute" and "chargeback" mean.

## Supported payment channels

Dispute Management is available for the following payment channels. Both are fully defendable, you can challenge any dispute raised by your shopper.

| Payment channel | Supported | Defendable |
| --------------- | --------- | ---------- |
| CARDS           | ✓         | ✓          |
| QRIS            | ✓         | ✓          |

## Other payment channels

Disputes on payment channels other than Cards and QRIS are not on the new Dispute Management dashboard yet, and continue to be handled by Xendit Ops over email: Ops notifies you by email when a dispute is raised, and you respond (accept, challenge, and submit evidence if challenging) via that same email thread. Ops then relays evidence to the payment partner and follows up on the outcome. If the dispute is lost, a `chargeback_deduction` transaction is booked and the disputed amount is deducted from your balance. Dashboard statuses such as Won and Lost do not apply here.

## What is changing

|                                  | Before                                                             | Now                                                                                                                  |
| -------------------------------- | ------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------- |
| Finding out about a dispute      | Xendit emails your registered business or dispute operations email | Xendit emails your configured dispute notification address. Dispute appears in your Disputes dashboard.              |
| Managing disputes                | Via email with Xendit                                              | Directly in your Disputes dashboard                                                                                  |
| Responding to a dispute          | Emailing Xendit to accept or challenge the dispute                 | Challenge or accept the dispute directly in the dispute detail view. Evidence upload happens as part of a Challenge. |
| Tracking status                  | Via email updates from Xendit                                      | Directly in your Disputes dashboard                                                                                  |
| Transaction type in your balance | `chargeback_deduction`                                             | `CHARGEBACK` when raised. `CHARGEBACK_REVERSAL` if won.                                                              |

During the transition period, disputes raised before your cutoff date will continue to be resolved via the existing email flow and will appear as `chargeback_deduction` in your transaction history. Net new disputes from your cutoff date onwards will appear as `CHARGEBACK` and `CHARGEBACK_REVERSAL`. You may see both transaction types in your balance and transaction history during this period.

## Set up your dispute notification email

This applies if you manage disputes through the Dispute Management dashboard.

By default, dispute notifications are sent to your registered business email. This may not be the email your ops or finance team monitors for disputes, which means notifications could be missed.

To make sure the right people are alerted when a dispute is raised or updated:

1. Log in to your [Xendit Dashboard](https://dashboard.xendit.co/dispute)
2. Go to [**Disputes**](https://dashboard.xendit.co/dispute)
3. Select **Dispute Settings** in the top right corner
4. Add the email address(es) where dispute notifications should be sent

Do this before disputes go live on your account. A missed notification is a missed deadline.

## Who can do what: user permissions

Not all dashboard users have the same access to Dispute Management. Make sure the right people have the right permissions before disputes go live. Users must have at least one of the permissions listed for each action.

| Action                | Required permission  |
| --------------------- | -------------------- |
| View disputes         | All users            |
| Challenge or Accept   | Edit, Approve, Admin |
| Edit Dispute Settings | Edit, Admin          |
| Export dispute data   | Edit, Approve, Admin |

> **Important:** Users who can only view disputes cannot challenge or accept them. If your ops or finance team needs to respond to disputes, confirm they have the appropriate permissions before disputes go live. For more on user permissions, see [Users & Permissions](https://docs.xendit.co/docs/users-permissions).

## When you receive a dispute

When a dispute is raised on one of your transactions, it appears in the Disputes tab of your dashboard. A `CHARGEBACK` transaction is recorded and the disputed amount is deducted from your balance while the dispute is in progress.

### Your three options

When a dispute needs a response, you have three options:

**1. Accept**
Return the disputed amount to your customer. This cannot be undone and the dispute is marked Lost. Use this if you do not intend to fight the dispute.

**2. Challenge**
Submit evidence to prove the transaction is valid. If you win, the amount (in full or in part, depending on payment channel and dispute outcome) is returned to your balance.

**3. No action taken**
> **Note:** Deadlines are strict. If no action is taken before the response deadline, the dispute is automatically marked Lost, whether or not you intended to challenge. This cannot be reversed.

### How to respond to a dispute

Same path for both Cards and QRIS disputes.

**To Accept:**

1. Go to [**Disputes**](https://dashboard.xendit.co/dispute) in the sidebar
2. Click the dispute
3. On **Dispute Details**, click **Action** (top right)
4. Choose **Accept**
5. Confirm in the popup

**To Challenge:**

1. Go to [**Disputes**](https://dashboard.xendit.co/dispute) in the sidebar
2. Click the dispute
3. On **Dispute Details**, click **Action** (top right)
4. Choose **Challenge**
5. Upload your evidence, following the guidance shown for your case
6. Click **Submit Challenge**
7. Confirm in the popup

The dispute moves to Under Review while your evidence is reviewed by the relevant party.
> **Note:** Evidence is not saved until you submit. If you leave before completing step 7 of Challenge (confirming in the popup), your uploads are lost and you will need to start over. The deadline keeps running in the meantime.

Once evidence is submitted, it cannot be changed. Review carefully before submitting.

If the dispute is resolved in your favour, the amount (in full or in part) is returned to your balance via a `CHARGEBACK_REVERSAL` transaction, subject to a processing window that varies by payment channel. The Chargeback Fee still applies and is not refunded.

## Dispute statuses

See [How disputes affect your balance](https://docs.xendit.co/docs/manage-disputes-via-dashboard#how-disputes-affect-your-balance) for how each status impacts your funds.

<!-- ^ link updated: was #how-disputes-affect-your-balance on the old /docs/dispute-management slug -->

| Status          | What it means                                             |
| --------------- | ----------------------------------------------------------|
| Action required | Dispute received. Review and respond before the deadline. |
| Under review    | You have responded. Under review with the relevant party. |
| Won             | Resolved in your favour.\*                                 |
| Lost            | Resolved against you.\*                                    |

*Amounts may be partially adjusted depending on payment channel and dispute outcome.

## How disputes affect your balance

Every dispute creates two potential transaction entries, visible under your Balance and Transactions tabs:

| Transaction type      | When it appears                    | What it means                                                                                                                              |
| --------------------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `CHARGEBACK`          | When a dispute is raised           | The disputed amount is deducted from your balance. The Chargeback Fee is included in this deduction and is not refundable.                 |
| `CHARGEBACK_REVERSAL` | When you win, in full or in part\* | The amount is returned to your balance, subject to a processing window that varies by payment channel. The Chargeback Fee is not refunded. |
