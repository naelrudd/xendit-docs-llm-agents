---
title: "Create sub-accounts"
slug: "xenplatform-global-accounts-setup"
updated: 2026-07-09T01:57:47Z
published: 2026-07-09T01:57:47Z
canonical: "docs.xendit.co/xenplatform-global-accounts-setup"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create sub-accounts

If you have xenPlatform activated, you can start creating sub-accounts to accept payments on their behalf and route funds between all your accounts.

## How to create and verify sub-accounts

1. On your sub-accounts page, click **Create Sub-Account**
2. Fill in the sub-account’s **business name**
3. Select whether you want to:
  1. Verify the sub-account yourself, if you are the Authorized Representative;
  2. or invite an Authorized Representative who legally represents the business to submit the verification information
4. Click **Create**

**Note:** Only the Authorized Representative can submit the business verification form once it’s filled in. They are also required to complete a [Face Verification](/v1/docs/authorized-representative-requirements#liveness-verification-test) test. The person creating the sub-account can also access the verification form at any time.

### Additional Configurations

You will also need to specify how webhooks are sent for events occurring in your sub-accounts. You can set this to either use the Master account’s configured webhook URLs (synchronized), or use the sub-account’s configured webhook URLs.

### Using the API

Our [Create Account API](https://docs.xendit.co/apidocs/create-account) can also be used to automate the sub-account creation process. You can refer to [this guide](/docs/create-sub-accounts#creating-subaccounts-via-api) for more details.

To pass on KYC information and verify sub-accounts using the API, refer to [this guide](/docs/xenplatform-verification-api).

## Next steps

After your sub-accounts have gone Live, you can follow our [guide](/docs/accepting-payments-for-sub-accounts) to start accepting payments or [create Split Rules](/docs/split-payments) to transfer a portion of the payment amounts to different accounts.

### Account Verification

You can invite your merchants to [sign up and submit](https://docs.xendit.co/docs/create-account) their information for verification. Note that you may invite your own users to submit on the merchants’ behalf.

##
