---
title: "Migrating to new subscription version"
slug: "migrate-from-legacy-subscriptions-to-new-subscriptions"
updated: 2026-07-08T06:57:03Z
published: 2026-07-09T10:00:12Z
canonical: "docs.xendit.co/migrate-from-legacy-subscriptions-to-new-subscriptions"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Migrating to new subscription version

If you are currently using the legacy Subscriptions version, you can migrate to the new version by updating your API endpoints, payload parameters, and webhook configurations as outlined below.

This new version consolidates your subscription workflows with our **Payment Sessions** product, delivering a smoother UI, modernized checkout experiences, and a more uniform integration lifecycle.

## Feature comparison

| Feature | Legacy Subscription | New Subscription |
| --- | --- | --- |
| Payment Link and Component Support | Limited only on Payment Link | Both Payment Link and Component |
| Payment Channels Availability | Limited to legacy payment methods and specific regions | Availability for all existing channels and new channels in all regions Xendit supported |
| New design for hosted page | Old design style, payment channel categorization is outdated | Fresh new design with improvement in user experience |
| Uniform experiences on payment interfaces | Separate payment lifecycle overview on `payment_method` and UI experiences | One integration principle on each lifecycle on payment interfaces and payment object |
| Support on initial payment | Only available via legacy parameter `immediate_action_type` | Recommended to use `PAY_AND_SAVE` flow (learn more) with also backward compatibility with parameter `immediate_payment` |
| Subscription Dashboard | The current dashboard will show the transaction created on legacy subscription | The current dashboard will show the transaction created on legacy subscription. Creation on current dashboard will use the new subscription version |

## How to migrate

1. **Update your integration flow**
  - **Update your API Version Header:** To access the new features, update your `api-version` header from the legacy `2022-04-10` to the new `2026-01-01` version.
  - **Migrate plans using Xendit hosted URLs:** Instead of calling `POST /recurring/plans` (which returned `actions.url`), call `POST /sessions` with `session_type: "SUBSCRIPTION"`. The response will now return a `payment_link_url` or `components_sdk_key` depending on your integration mode.
  - **Migrate plans using existing payment tokens:** Continue using `POST /recurring/plans`, but replace the legacy `payment_methods` parameter with the new, unified `payment_tokens` parameter.
2. **Convert your parameters**

The new version supports most functionalities of the legacy system but introduces a simplified payload structure. Use this mapping table to update your API requests (refer to the API Reference for the full schema):

| Legacy Subscription | New Subscription | Notes |
| --- | --- | --- |
| `payment_methods` | `payment_tokens` | Support the new payment tokens object |
| `immediate_action_type` | `immediate_payment` | Simplified into a boolean type to easily trigger immediate payments |
| `recurring_action` | - | Streamlined flow; defaults exclusively to `PAYMENT` |
| `notification_config.recurring_created, notification_config.recurring_created and notification_config.recurring_failed` | `notification_channels` | Consolidated into a single parameter to configure your notification channels |
3. **Handle new error responses**

Ensure your server's error-handling logic is updated to catch and process the [new error structures](https://docs.xendit.co/apidocs/create-session) returned by the [**Payment Sessions** API](https://docs.xendit.co/apidocs/create-session) (upon session creation) and the upgraded [**Subscriptions** API](https://docs.xendit.co/apidocs/create-recurring-plan).
4. **Adjust your webhook setup**

The new version utilizes Xendit's upgraded **Payment v3** and **Payment Tokens v3** webhook infrastructure. We highly recommend updating your webhook URL endpoints to cleanly capture and process updates across your subscription lifecycles.
  - **Legacy Setup:** Managed via the legacy webhook configuration page.

![](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/Screenshot 2026-04-08 at 1.50.01 AM(1).png)
  - **New Setup:** Configured via the new unified webhook dashboard.

![](https://cdn.document360.io/217abc43-8677-41fb-a81d-fceeb1fa0358/Images/Documentation/Screenshot 2026-04-08 at 1.50.19 AM.png)

- **Optional but recommended:** Adjust the webhook URL to receive the information upon your subscription lifecycle.
  - **Payment v3 – Payment Status**

Xendit sends webhooks whenever there is a status update on a Payment object.
    - `payment.succeeded` Identifies successful payments and includes full payment details.
    - `payment.failure` Identifies failed payment attempts, including failures that occur on the Xendit hosted page.
  - **Payment Tokens v3 – Payment Token Status**

Xendit sends webhooks whenever there is a status update on a Payment Token object.
