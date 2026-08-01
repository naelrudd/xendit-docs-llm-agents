---
title: "Merchant initiated and recurring flagging"
slug: "merchant-initiated-transaction-2"
updated: 2025-10-02T05:57:11Z
published: 2025-10-02T05:57:11Z
canonical: "docs.xendit.co/merchant-initiated-transaction-2"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Merchant initiated and recurring flagging

> [!WARNING]
> Merchant initiated transactions require additional approval from our risk team
> 
> Due to the high risk of fraud, we by default do not allow merchant initiated transactions to take place. To enable merchant initiated transactions, request recurring payments from from the [Xendit Dashboard](https://dashboard.xendit.co/settings/payment-methods/cards-configuration).

This guide describes how to charge merchant initiated transactions (with recurring indicators) **without using Xendit issued tokens**.

## Merchant initiated transaction indicators

There are several fields that can be used for recurring flagging:

### Card on file type

```json
"channel_properties": {
    "card_on_file_type": "RECURRING", "MERCHANT_UNSCHEDULED", "CUSTOMER_UNSCHEDULED"
}
```

`card_on_file_type` - can have the following values:

**RECURRING** - This transaction is expected to happen on a recurring basis, subscriptions to a service, for example.

**MERCHANT_UNSCHEDULED** - This transaction can happen any time, at different amounts, whenever the merchant initiates the transaction.

**CUSTOMER_UNSCHEDULED** - Use for tokenized cards ([Pay and save](/docs/create-a-token))

### Transaction sequence

```json
"channel_properties": {
     "transaction_sequence": "INITIAL", "SUBSEQUENT"
```

`transaction_sequence` - can have the following values:

**INITIAL** - first time transaction

**SUBSEQUENT** - any follow up transaction, also used when switching between providers

### Recurring configuration

For recurring transactions, additional configuration is required, both `recurring_expiry` and `recurring_frequency` are scheme mandated fields

```json
"channel_properties": {
    "recurring_configuration" : {
        "recurring_expiry": "YYYY-MM-DD", // The expiry date of the contract
        "recurring_frequency": 30 // The days in between each charge, for unscheduled pass "1"
    }
}
```

## Initial unscheduled merchant initiated transaction

The first transaction of a merchant initiated transaction requires the transaction to be flagged as **INITIAL**:

`transaction_sequence : "INITIAL"` - the first time we are setting up the “contract” between the shopper and your product.

**Perform the payment request:**

Set up an unscheduled merchant initiated transaction (customer initiated, first time):

Request - POST /v3/payment_requests

```json
{
  "reference_id": "UNIQUE_REFERENCE_ID",
  "type": "PAY",
  "country": "ID",
  "currency": "IDR",
  "request_amount": 10000,
  "capture_method": "AUTOMATIC",
  "channel_code": "CARDS",
  "customer": {
        "reference_id": "UNIQUE_CUSTOMER_REFERENCE_ID",
        "type": "INDIVIDUAL",
        "email": "test@yourdomain.com",
        "mobile_number": "+6212345678",
        "individual_detail": {
            "given_names": "Lorem",
            "surname": "Ipsum"
        }
    },
    "channel_properties": {
        "card_details": {
                "card_number": "4000000000001091",
                "cvn": "123",
                "cardholder_first_name": "shopperFirstName",
                "cardholder_last_name": "shopperLastName",
                "cardholder_email": "shopper@shopper.co",
                "expiry_month": "12",
                "expiry_year": "2029"
        },
        "card_on_file_type": "MERCHANT_UNSCHEDULED",
        "transaction_sequence":"INITIAL",
        "skip_three_ds": false // We recommend not to skip 3DS (risk and liability)
    },
    "failure_return_url": "https://xendit.co/failure",
    "success_return_url": "https://xendit.co/success",
    "statement_descriptor": "New PC",
    "description": "Your description",
    "metadata": {
        "metametadata": "Any meta data"
    }
}
```

## Subsequent transactions

Follow up transactions has to be flagged **SUBSEQUENT**

We have created a “contract” between the shopper and the merchant and are now charing a previously stored card.

For subsequent transactions make sure to pass the `card_on_file_type` , `network_transaction_id` in the `channel_properties` object

```json
 "channel_properties": {
        "success_return_url": null,
        "failure_return_url": null,
        "card_on_file_type": "RECURRING",
        "network_transaction_id": "1251251511"
...
```

> [!NOTE]
> **Alphanumeric Network transaction ID resulting in error**
> 
> On test, the returned network_transaction_id is alphanumeric. This reflects actual network_transaction_id’s.
> 
> When using this network_transaction_id, it will result in processor error.
> 
> To circumvent this issue on test, pass a numeric character (can be random); 12123456789012

**Merchant unscheduled transaction sample**

Sample request to follow up the merchant unscheduled transaction:

Request - POST /v3/payment_requests

```json
{
  "reference_id": "UNIQUE_REFERENCE_ID",
  "type": "PAY",
  "country": "ID",
  "currency": "IDR",
  "request_amount": 115100,
  "capture_method": "AUTOMATIC",
  "channel_code": "CARDS",
  "customer": {
        "reference_id": "UNIQUE_CUSTOMER_REFERENCE_ID",
        "type": "INDIVIDUAL",
        "email": "test@yourdomain.com",
        "mobile_number": "+6212345678",
        "individual_detail": {
            "given_names": "Lorem",
            "surname": "Ipsum"
        }
    },
    "channel_properties": {
        "card_details": {
                "card_number": "4000000000001091",
                "cardholder_first_name": "shopperFirstName",
                "cardholder_last_name": "shopperLastName",
                "cardholder_email": "shopper@shopper.co",
                "expiry_month": "12",
                "expiry_year": "2029"
        },
        "card_on_file_type": "MERCHANT_UNSCHEDULED",
        "transaction_sequence":"SUBSEQUENT",
        "network_transaction_id": "1251251511", // numerical on test
    },
    "failure_return_url": "https://xendit.co/failure",
    "success_return_url": "https://xendit.co/success",
    "statement_descriptor": "testing goodds",
    "description": "this should have the proper ntid",
    "metadata": {
        "metametadata": "metametametadata"
    }
}
```

## Initial recurring transaction

First time recurring transaction. Ideally we do request 3DS2 for a first time recurring contract:

1. **Create the payment request with the** [**recurring configuration**](/docs/merchant-initiated-transaction-2#recurring-configuration) **in place** Request - POST /v3/payment_requests

```json
{
  "reference_id": "UNIQUE_REFERENCE_ID",
  "type": "PAY",
  "country": "ID",
  "currency": "IDR",
  "request_amount": 10000,
  "capture_method": "AUTOMATIC",
  "channel_code": "CARDS",
  "customer": {
        "reference_id": "UNIQUE_CUSTOMER_REFERENCE_ID",
        "type": "INDIVIDUAL",
        "email": "test@yourdomain.com",
        "mobile_number": "+6212345678",
        "individual_detail": {
            "given_names": "Lorem",
            "surname": "Ipsum"
        }
    },
    "channel_properties": {
        "recurring_configuration": {
            "recurring_expiry": "2028-12-10",
            "recurring_frequency" : 30
        },
        "card_details": {
                "card_number": "4000000000001091",
                "cvn": "123",
                "cardholder_first_name": "Shopper",
                "cardholder_last_name": "LastName",
                "cardholder_email": "example@shopper.com",
                "expiry_month": "12",
                "expiry_year": "2029"
        },
        "card_on_file_type": "RECURRING",
        "transaction_sequence":"INITIAL",
        "failure_return_url": "https://xendit.co/failure",
        "success_return_url": "https://xendit.co/success"
    },
    "statement_descriptor": "30 day subscription",
    "description": "Recurring sample"
}
```

1. **Redirect to the authentication page**

Redirect your customer to the [authentication page](/docs/authentication-3ds2) provided by the `action_url` from the response object. This is where the cardholder completes the 3D Secure authentication.
2. **Fetch the transaction details and store the** `network_transaction id`

Follow [this guide](/docs/retrieving-authorization-and-decline-details) to retrieve the payment details.

> [!NOTE]
> **Alphanumeric Network transaction ID resulting in error**
> 
> On test, the returned network_transaction_id is alphanumeric. This reflects actual network_transaction_id’s.
> 
> When using this network_transaction_id, it will result in processor error.
> 
> To circumvent this issue on test, pass a numeric character (can be random); 12123456789012

## Follow up recurring transaction

The follow up transaction would (in this case) be expected to be charged 30 days later.

1. **Create the follow up payment request with the network_transaction_id field** Request - POST /v3/payment_requests

```json
{
  "reference_id": "UNIQUE_REFERENCE_ID",
  "type": "PAY",
  "country": "ID",
  "currency": "IDR",
  "request_amount": 50000,
  "capture_method": "AUTOMATIC",
  "channel_code": "CARDS",
  "customer": {
        "reference_id": "UNIQUE_CUSTOMER_REFERENCE_ID",
        "type": "INDIVIDUAL",
        "email": "test@yourdomain.com",
        "mobile_number": "+6212345678",
        "individual_detail": {
            "given_names": "Lorem",
            "surname": "Ipsum"
        }
    },
    "channel_properties": {
        "card_details": {
                "card_number": "4000000000001091",
                "cardholder_first_name": "Shopper",
                "cardholder_last_name": "Name",
                "cardholder_email": "example@shopper.com",
                "expiry_month": "12",
                "expiry_year": "2029"
        },
        "card_on_file_type": "RECURRING",
        "transaction_sequence":"SUBSEQUENT",
        "skip_three_ds": true,
        "network_transaction_id": "12123456789012"
    },
    "statement_descriptor": "Your subscription",
    "description": "Recurring MIT follow up transaction"
}
```

1. **This transaction has now been authorized.** Make sure to receive the [webhook or fetch the transaction details](/docs/retrieving-authorization-and-decline-details)
