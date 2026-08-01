---
title: "Guest checkout"
slug: "guest-checkout-1"
updated: 2026-07-09T06:53:17Z
published: 2026-07-09T06:53:17Z
canonical: "docs.xendit.co/guest-checkout-1"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Guest checkout

## Guest Checkout (Without Storing Card)

Guest checkout allows users to complete purchases without creating an account. By explicitly disabling card storage, the payment details are used solely to authorize the immediate transaction. The system does not vault the credentials or generate a reusable payment token, minimizing your data retention footprint and simplifying PCI compliance scope.

To implement this workflow, create a payment session with the `allow_save_payment_method` parameter set to `DISABLED`.

## 1. Create a Payment Session

`POST - https://api.xendit.co/sessions`

### Request Payload

```
{
    "reference_id": "pay-save-test-2",
    "session_type": "PAY",
    "mode": "COMPONENTS",
    "amount": 20.00,
    "currency": "SGD",
    "country": "SG",
    "customer": {
        "reference_id": "c83b8791-2a6c-4b68-809c-e6fc1f7a08e7",
        "type": "INDIVIDUAL",
        "email": "customer@yourdomain.com",
        "mobile_number": "+628123456789",
        "individual_detail": {
            "given_names": "John",
            "surname": "Doe"
        }
    },
    "components_configuration": {
        "origins": ["https://localhost:4443"]
    },
    "allow_save_payment_method" : "DISABLED",
    "allowed_payment_channels": ["CARDS"]
}
```

### Response Payload

```
{
    "payment_session_id": "ps-6a4ef5ced5b7f3721c195a48",
    "created": "2026-07-09T01:13:50.197Z",
    "updated": "2026-07-09T01:13:50.197Z",
    "status": "ACTIVE",
    "reference_id": "pay-save-test-2",
    "currency": "SGD",
    "amount": 20,
    "country": "SG",
    "expires_at": "2026-07-09T01:43:49.454Z",
    "session_type": "PAY",
    "mode": "COMPONENTS",
    "locale": "en",
    "business_id": "6943ca3xxxx2cfa43",
    "customer_id": "cust-65d2eb1b-2021-4450-a0cb-2a323ecdb82e",
    "capture_method": "AUTOMATIC",
    "allowed_payment_channels": [
        "CARDS"
    ],
    "allow_save_payment_method": "DISABLED",
    "components_sdk_key": "session-40d9fb9cf9af4397ea64c5679cda35c3-pd-MHYwEAYHKoZIzj0CAQYFK4EEACIDYgAEkqsQxgGJ7xxX6xWfEQL0vux1Mqk8CU5j75ZEgtdFF9sRwymt4a+1kNsQIDRs8PLf7/QPP/MW09mAjwfHjBmOZqZOGKiFbdYHLxXjK2nFYcDEyvAIOZWXwLf+DNhQZdr5-sDFidO4VZ4verVWOPaqngVgENamW/W/cVYNYRsVMwkx1vU9AZL5xt5Eth3Xg8PrsGExt/ONYfzfXW33xA6WQIVZSuMxeAqsGFxYH+YwAytoZv1PY0a5qCgicEPNQQG4i",
    "components_configuration": {
        "origins": [
            "https://localhost:4443"
        ]
    }
}
```

---

## Next Steps: Initialize UI Components

Once you have successfully generated the session, pass the `components_sdk_key` returned in the response payload to your frontend application.

To render the secure card input fields and complete the guest checkout flow, proceed to the [Component Integration Guide](/components-overview)
