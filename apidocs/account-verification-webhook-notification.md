---
title: "Account verification webhook notification"
slug: "account-verification-webhook-notification"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/account-verification-webhook-notification"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Account verification webhook notification

Post/your_account_verification_webhook_url

A webhook event sent to your Platform when the KYC verification status of one of your sub-accounts changes.

Configure the **Account Verification Status** webhook URL on your master account to receive these events. If no URL is set, the webhook service logs `CALLBACK_URL_NOT_SET` (this is not a delivery failure). There is no master-initiated resend — if you miss an event, poll the [Retrieve account verification](/apidocs/account-verification-webhook-notification#operation/getAccountVerification) API as a fallback. Webhook delivery logs appear on the sub-account's dashboard, not the master's, even when the event is routed to the master URL.

When the status is `AWAITING_RESUBMISSION`, the `kyc.failure_reasons` array lists each field that needs correcting so you know exactly what to re-upload. `field` uses dot-notation; for array document fields the specific document type is appended (e.g. `business_registration_documents.id_company_npwp`). `message` is a human-readable explanation.

Body parameters<select class='api-response-data' aria-label='Media type'><option value='7ee4a547-e53d-4244-a71f-b5077ef2b67e'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='b4da65c6-4c94-4a18-a616-bcdc175cf0a6'>Awaiting resubmission</option>
</select>Awaiting resubmission

```json
{
  "event": "account.verification",
  "created": "2026-06-19T04:52:35.291Z",
  "business_id": "68b65fa5c2d38abe0de734ce",
  "data": {
    "id": "6a34caaa8a9c47963f1b7abc",
    "created": "2026-06-19T04:51:02.634Z",
    "updated": "2026-06-19T04:52:33.723Z",
    "kyc": {
      "status": "AWAITING_RESUBMISSION",
      "verified_at": "2026-06-19T04:52:33.723Z",
      "requested_at": "2026-06-19T04:51:03.517Z",
      "failure_reasons": [
        {
          "field": "business_license_documents",
          "reason": "NEW_DOCUMENT",
          "message": "We need to verify this additional document for your business type."
        },
        {
          "field": "business_registration_documents.id_skmenkeh_latest",
          "reason": "WRONG_DOCUMENT",
          "message": "This document is not valid. Make sure you upload the correct one."
        },
        {
          "field": "business_registration_documents.id_company_npwp",
          "reason": "NEW_INFORMATION",
          "message": "We need to collect this additional information for your business type."
        },
        {
          "field": "authorized_person_identification.id_national_id_ktp",
          "reason": "WRONG_DOCUMENT",
          "message": "This document is not valid. Make sure you upload the correct one."
        },
        {
          "field": "authorized_person_selfie_document",
          "reason": "BLURRY_IMAGE",
          "message": "This document is blurry. Please try uploading again and make sure all of your details can be read clearly."
        }
      ]
    }
  },
  "api_version": null
}
```

Expand Allobject  eventstring    

The KYC verification status of your sub-account has changed

Valid values[
  "account.verification"
]Exampleaccount.verification
business_idstring    

ID of your Account, use this in the for-user-id header to create transactions on behalf of your Account

createdstring    

Timestamp of when the webhook was sent

api_versionstring   | null  

API version of the webhook payload. May be `null`.

dataobject  idstring    

ID of the sub-account whose verification status changed

createdstring    

Timestamp of when the KYC request was created

updatedstring    

Timestamp of when the KYC request was last updated

kycobject  statusstring    

The KYC verification status of the sub-account

Valid values[
  "VERIFICATION_IN_PROGRESS",
  "PASSED",
  "AWAITING_RESUBMISSION",
  "FAILED"
]
requested_atstring    

Timestamp of the last KYC submission

verified_atstring    

Timestamp of when the verification status was last updated

kyc_passed_atstring    

Timestamp of when KYC passed. Only present when `status` is `PASSED`

failure_reasons Array of object   

Present when `status` is `AWAITING_RESUBMISSION`. One entry per field that needs correcting.

object  fieldstring    

The KYC field that needs correcting, in dot-notation. For array document fields the specific document type is appended, e.g. `business_registration_documents.id_company_npwp`.

reasonstring    

Machine-readable reason the field needs correcting

Valid values[
  "NEW_DOCUMENT",
  "WRONG_DOCUMENT",
  "NEW_INFORMATION",
  "BLURRY_IMAGE"
]
messagestring    

Human-readable explanation. May be reviewer free-text or a templated message.

Responses200

OK

400

Bad Request - Invalid webhook payload
