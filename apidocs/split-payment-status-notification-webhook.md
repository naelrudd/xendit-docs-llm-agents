---
title: "Split payment status notification webhook"
slug: "split-payment-status-notification-webhook"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/split-payment-status-notification-webhook"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Split payment status notification webhook

Post/your_split_payment_webhook_url

These events will be sent when a split payment is completed or has failed to execute

Body parameters<select class='api-response-data' aria-label='Media type'><option value='2290dc85-2dac-424a-a155-37637f897a45'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='a58e0c2a-b328-4f93-8ee1-e15c889c4ef8'>Split Payment Completed</option>
<option value='aebf411e-5e6b-4584-a1d7-1f50d85890b4'>Split Payment Failed</option>
</select>Split Payment Completed

```json
{
  "event": "split.payment",
  "created": "2021-01-01T10:00:00Z",
  "business_id": "5fe2b0137b7d62542fe6d7de",
  "data": {
    "id": "57fb4e076fa3fa296b7f5a97",
    "split_rule_id": "splitru_d9e069f2-4da7-4562-93b7-ded87023d749",
    "reference_id": "my_unique_route_reference_12345",
    "payment_id": "py-1402feb0-bb79-47ae-9d1e-e69394d3949c",
    "payment_reference_id": "my_unique_payment_reference_12345",
    "source_account_id": "5fe2b0137b7d62542fe6d7de",
    "destination_account_id": "67514ce3b045c2ebade1d94e",
    "status": "COMPLETED",
    "amount": 150.45,
    "currency": "PHP"
  }
}
```

Split Payment Failed

```json
{
  "event": "split.payment",
  "created": "2021-01-01T10:00:00Z",
  "business_id": "5fe2b0137b7d62542fe6d7de",
  "data": {
    "id": "57fb4e076fa3fa296b7f5a97",
    "split_rule_id": "splitru_d9e069f2-4da7-4562-93b7-ded87023d749",
    "reference_id": "my_unique_route_reference_12345",
    "payment_id": "py-1402feb0-bb79-47ae-9d1e-e69394d3949c",
    "payment_reference_id": "my_unique_payment_reference_12345",
    "source_account_id": "5fe2b0137b7d62542fe6d7de",
    "destination_account_id": "67514ce3b045c2ebade1d94e",
    "status": "FAILED",
    "amount": 150.45,
    "currency": "PHP",
    "failure_code": "INSUFFICIENT_BALANCE"
  }
}
```

Expand Allobject  eventstring    

Event that occurred for this webhook

Valid values[
  "split.payment"
]Examplesplit.payment
business_idstring    

ID of your Account, use this in the for-user-id header to create transactions on behalf of your Account

createdstring    

Timestamp of when the webhook was sent

dataobject  idstring    

The unique Split Payment ID created for every split

split_rule_idstring    

The unique Split Rule ID

reference_idstring    

Reference ID which acts as an identifier of the route itself. This is used to distinguish in case one split rule has multiple routes of the same destinations. Its value must be unique and case sensitive for every route object under the same Split Rule.

payment_idstring    

The original payment ID that the Split payment was processed for, or that the Split Rule was linked to using the with-split-rule header. The payment ID is the unique identifier for the payment. Its prefix varies based on the payment method type.

payment_reference_idstring    

Reference ID of the Payment object

source_account_idstring    

Business ID of the account where the split was sent from. This is also the account that received the original payment.

destination_account_idstring    

Business ID of the destination account where the amount is routed to.This could be the Business ID of your Master or Sub-account.

statusstring    

The status of the split payment.

Valid values[
  "COMPLETED",
  "FAILED"
]
amountnumber    

The total currency amount that is sent to the destination_account_id

currencystring    

ISO 4217 Currency Code

Valid values[
  "IDR",
  "PHP",
  "VND",
  "MYR",
  "THB",
  "SGD",
  "USD"
]
failure_codestring    

The failure code for FAILED events

ExampleINSUFFICIENT_BALANCE

Responses200

OK

400

Bad Request - Invalid webhook payload
