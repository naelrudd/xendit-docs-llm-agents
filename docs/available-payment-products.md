---
title: "Choose your integration"
slug: "available-payment-products"
updated: 2026-07-20T12:33:17Z
published: 2026-07-20T12:33:17Z
canonical: "docs.xendit.co/available-payment-products"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Choose your integration

Xendit offers multiple payment products designed for different business needs, from no-code payment acceptance to fully customized checkout experiences.

Use the comparison below to identify the best integration based on your business needs, development resources, and desired customer experience.

## Integration comparison

All available payment integration from Xendit for you to use

|  | [Payments API](/v1/docs/how-payments-api-work) | [Subscriptions](/v1/docs/how-subscriptions-work) | [Plug-ins](/v1/docs/how-plug-ins-work) | [Payment Session](/v1/docs/how-payment-sessions-work) (Payment Link) | [Payment Session](/v1/docs/how-payment-sessions-work) (Component) |
| --- | --- | --- | --- | --- | --- |
| No-code solution (Create via Xendit Dashboard) | - | ***✓*** | ***✓*** | ***✓*** | - |
| API | [Payments API](/v1-api/apidocs/create-payment-request) | [Subscription API](/v1-api/apidocs/create-recurring-plan) | - | [Payment Session API](/v1-api/apidocs/create-session) | [Payment Session API](/v1-api/apidocs/create-session) |
| Support Xendit-hosted page | - | ***✓*** | ***✓*** | ***✓*** | ***✓*** |
| Development effort | ⏺⏺⏺ High | ⏺⏺⏺ Medium | ⏺⏺⏺ Low | ⏺⏺⏺ Low | ⏺⏺⏺ Medium |
| UI customization | ⏺⏺⏺ High customization on merchant’s own hosted page | ⏺⏺⏺ Limited customization (coming soon) | ⏺⏺⏺ Limited customization (coming soon) | ⏺⏺⏺ Limited customization (coming soon) | ⏺⏺⏺ High customization with component guideline |
| Speed to market | ⏺⏺⏺ Low | ⏺⏺⏺ Medium | ⏺⏺⏺ High | ⏺⏺⏺ High | ⏺⏺⏺ Medium |

## Payment Scenario

See how Xendit supports different payment scenarios by each use case

|  | [Payments API](/v1/docs/how-payments-api-work) | [Subscriptions](/v1/docs/how-subscriptions-work) | [Plug-ins](/v1/docs/how-plug-ins-work) | [Payment Session](/v1/docs/how-payment-sessions-work) (Payment Link) | [Payment Session](/v1/docs/how-payment-sessions-work) (Component) |
| --- | --- | --- | --- | --- | --- |
| One time payment flow | ***✓*** |  | ***✓*** | ***✓*** | ***✓*** |
| Saving payment information for future use (e.g. tokenized cards) | ***✓*** | ***✓*** | *-* | ***✓*** | ***✓*** |
| Making merchant initiated transactions (MIT) without user authentication | ***✓*** | ***✓*** | *-* | *-* | *-* |
| Holding a reserve amount and collecting up to full value of reserve as payment later (Auth & Capture) | ***✓*** | *-* | *-* | ***✓*** | ***✓*** |
