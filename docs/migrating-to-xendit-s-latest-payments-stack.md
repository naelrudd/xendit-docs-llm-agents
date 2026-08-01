---
title: "Migrate to Xendit's latest integration stack"
slug: "migrating-to-xendit-s-latest-payments-stack"
updated: 2026-07-27T05:36:07Z
published: 2026-07-27T05:36:07Z
canonical: "docs.xendit.co/migrating-to-xendit-s-latest-payments-stack"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Migrate to Xendit's latest integration stack

Xendit is improving its integrations — across both Payments and Payouts — into one stack: a single, consistent object model, working the same way across every payment channel and every supported region. This page covers what's legacy, what to move to, and which detailed guide to follow, product by product.

## Overview

Migrating to latest integration stack will bring a host of improvements to your existing payment integrations, such as:

- **Built to scale across regions.** New countries and channels will only get added to the current stack.

**Built for the long run.** The legacy APIs below are still functional but are no longer where new channels, regions, or features ship. The current stack is where Xendit's roadmap is heading.

The table below will help you identify migration guideline per each product

### Payments

| If you're using... | Move to... | Migration Guideline |
| --- | --- | --- |
| Direct per-channel APIs (`/ewallets`, `/callback_virtual_accounts`, `/direct_debits`, `/qr_codes`, `/fixed_payment_code`, `/credit_card_charges`) | **Payments API v3** — `/payment_requests` + `/payment_tokens` | [Migrate Direct per-Channel API to v3](/v1/docs/migrate-direct-per-channel-apis-to-v3) |
| Payment API v2 (`payment_methods` / `payment_requests`) | **Payments API v3** — `/v3/payment_requests` + `/v3/payment_tokens` | [Migrate Payment API v2 to v3](/v1/docs/migrate-payment-api-v2-to-v3) |
| Payment Links / Invoices (`/v2/invoices`) | **Payment Sessions** — `/sessions` (`PAYMENT_LINK` mode) | [Migrate Payment Links/Invoice → Payment Session](https://docs.xendit.co/docs/migrate-to-payment-session) |
| Subscriptions v1 (`/recurring/plans`, `api-version 2022-04-10`) | **Subscriptions v2** (`api-version 2026-01-01`) | [Migrate Subscriptions v1 → v2](https://docs.xendit.co/docs/migrate-from-legacy-subscriptions-to-new-subscriptions) |
| Cards Client App SDK ([xendit.js](https://js.xendit.co/v1/xendit.min.js)) | Xendit Components | [Refer to our Xendit Components guideline](/v1/docs/components-overview) |

##
