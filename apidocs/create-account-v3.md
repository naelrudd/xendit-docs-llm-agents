---
title: "Create account (v3)"
slug: "create-account-v3"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/create-account-v3"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create account (v3)

Post/v3/accounts

Creates a new sub-account linked to your master account.

The v3 Accounts API provides richer sub-account management with explicit identity and configuration options. It supersedes the v2 `/v2/accounts` endpoint.

**Key changes from v2:**

- `email` is now required on create
- Sub-account identity (country + entity type) is now required on create
- `configuration` replaces `configurations` with a new shape
- Webhook recipient values changed: `MASTER` → `MASTER_ACCOUNT`, `SUB` → `SUB_ACCOUNT`
- Response includes `identity` and `configuration` objects instead of top-level
`legal_name` / `country_of_incorporation`

The API key used for the request determines which master account the sub-account is linked to — you do not need to pass a business ID or environment mode explicitly.

> Use an API key with **Account Write** permission to perform this request.

**Country of incorporation**

By default, `identity.country_of_incorporation` must match your master account's country of operation. Cross-country sub-accounts are only allowed if explicitly enabled for your account — contact your account manager to enable this.

**Entity types by country**

Available `identity.entity_type` values depend on `identity.country_of_incorporation`:

| Country | Available entity types |
| --- | --- |
| ID | `CORPORATION`, `SOLE_PROPRIETORSHIP`, `PARTNERSHIP`, `NON_PROFIT`, `INDIVIDUAL`, `COOPERATIVE` |
| PH | `CORPORATION`, `SOLE_PROPRIETORSHIP`, `PARTNERSHIP`, `INDIVIDUAL`, `ONE_PERSON_CORPORATION` |
| VN | `CORPORATION`, `SOLE_PROPRIETORSHIP`, `PARTNERSHIP`, `LIMITED_LIABILITY_COMPANY` |
| TH | `CORPORATION`, `PARTNERSHIP`, `NON_PROFIT`, `INDIVIDUAL` |
| MY | `CORPORATION`, `SOLE_PROPRIETORSHIP`, `PARTNERSHIP`, `NON_PROFIT` |
| SG | `CORPORATION`, `PARTNERSHIP` |
| HK | `CORPORATION`, `PARTNERSHIP` |
| MX | `CORPORATION`, `SOLE_PROPRIETORSHIP`, `PARTNERSHIP`, `NON_PROFIT` |

Any other country of incorporation follows the SG entity type list.

**Test mode restrictions**

When using a Test API key, the following constraints apply:

| Field | Restriction |
| --- | --- |
| `identity.entity_type` | Must be `CORPORATION` |
| `identity.country_of_incorporation` | Must match your master account's country |
| `configuration.users.send_email_invite` | Must be `false` or omitted |
| `configuration.webhooks.recipient` | Must be `MASTER_ACCOUNT` or omitted |

Sub-accounts created in Test mode are provisioned immediately with status `LIVE`, and their `identity` and `configuration` are returned with default values. They are only available in Test mode and will never go live.

SecurityHTTPType basic

Body parameters<select class='api-response-data' aria-label='Media type'><option value='f2fefbab-a098-4d90-a005-7ca120ea5100'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='d5ca6bc6-76b2-4cfd-9cb1-3d8c0ce02483'>Corporation (SG)</option>
<option value='6facba7e-58fc-418d-ad2d-e1204d8cda6e'>Minimal request (ID, defaults)</option>
<option value='06b24773-3906-4f5e-8737-a4da308f1697'>Test mode</option>
</select>Corporation (SG)

```json
{
  "name": "Acme Corp",
  "email": "owner@acme.com",
  "identity": {
    "country_of_incorporation": "SG",
    "entity_type": "CORPORATION"
  },
  "configuration": {
    "users": {
      "send_email_invite": true
    },
    "webhooks": {
      "recipient": "MASTER_ACCOUNT"
    }
  }
}
```

Minimal request (ID, defaults)

The entire `configuration` block is optional for every entity type. When omitted, no email invite is sent (`send_email_invite: false`) and webhooks default to `MASTER_ACCOUNT`.

```json
{
  "name": "Toko Berkah",
  "email": "owner@tokoberkah.co.id",
  "identity": {
    "country_of_incorporation": "ID",
    "entity_type": "INDIVIDUAL"
  }
}
```

Test mode

With a Test API key, `entity_type` must be `CORPORATION`, the country must match your master account's country, and `configuration` must be omitted or use the default values.

```json
{
  "name": "Acme Corp (Test)",
  "email": "owner@acme.com",
  "identity": {
    "country_of_incorporation": "SG",
    "entity_type": "CORPORATION"
  }
}
```

Expand Allobject  namestring    Required

Sub-account display name

emailstring  (email)    Required

Email address for the sub-account owner. This becomes the sub-account's default email address, and is the first email to receive the invitation (when `configuration.users.send_email_invite` is `true`) to access the dashboard and continue filling in the sub-account's KYC information.

identity

The legal identity of the sub-account's business.

`country_of_incorporation` is an ISO 3166-1 alpha-2 country code. It must match your master account's country of operation unless cross-country sub-accounts are explicitly enabled for your account.

The available `entity_type` values depend on `country_of_incorporation` — see the per-country variants below. Any country not listed follows the Singapore (SG) entity type list.

OneOfIndonesia (ID)object (Indonesia (ID))country_of_incorporationstring    RequiredValid values[
  "ID"
]
entity_typestring    RequiredValid values[
  "CORPORATION",
  "SOLE_PROPRIETORSHIP",
  "PARTNERSHIP",
  "NON_PROFIT",
  "INDIVIDUAL",
  "COOPERATIVE"
]

Philippines (PH)object (Philippines (PH))country_of_incorporationstring    RequiredValid values[
  "PH"
]
entity_typestring    RequiredValid values[
  "CORPORATION",
  "SOLE_PROPRIETORSHIP",
  "PARTNERSHIP",
  "INDIVIDUAL",
  "ONE_PERSON_CORPORATION"
]

Vietnam (VN)object (Vietnam (VN))country_of_incorporationstring    RequiredValid values[
  "VN"
]
entity_typestring    RequiredValid values[
  "CORPORATION",
  "SOLE_PROPRIETORSHIP",
  "PARTNERSHIP",
  "LIMITED_LIABILITY_COMPANY"
]

Thailand (TH)object (Thailand (TH))country_of_incorporationstring    RequiredValid values[
  "TH"
]
entity_typestring    RequiredValid values[
  "CORPORATION",
  "PARTNERSHIP",
  "NON_PROFIT",
  "INDIVIDUAL"
]

Malaysia (MY)object (Malaysia (MY))country_of_incorporationstring    RequiredValid values[
  "MY"
]
entity_typestring    RequiredValid values[
  "CORPORATION",
  "SOLE_PROPRIETORSHIP",
  "PARTNERSHIP",
  "NON_PROFIT"
]

Singapore (SG)object (Singapore (SG))country_of_incorporationstring    RequiredValid values[
  "SG"
]
entity_typestring    RequiredValid values[
  "CORPORATION",
  "PARTNERSHIP"
]

Hong Kong (HK)object (Hong Kong (HK))country_of_incorporationstring    RequiredValid values[
  "HK"
]
entity_typestring    RequiredValid values[
  "CORPORATION",
  "PARTNERSHIP"
]

Mexico (MX)object (Mexico (MX))country_of_incorporationstring    RequiredValid values[
  "MX"
]
entity_typestring    RequiredValid values[
  "CORPORATION",
  "SOLE_PROPRIETORSHIP",
  "PARTNERSHIP",
  "NON_PROFIT"
]

configurationobject (AccountConfigurationV3)  

Optional behaviour configuration for the sub-account

usersobject  send_email_inviteboolean    Required

If `true`, sends an email invitation to `email` on account creation so the owner can access the sub-account dashboard and continue filling in the sub-account's KYC information. Available for every entity type. Only applies in Live mode.

Defaultfalse

webhooksobject  recipientstring    Required

Where webhooks for the sub-account's transactions are delivered:

- `MASTER_ACCOUNT` — webhooks are sent to the URLs configured in the master account's settings (default)
- `SUB_ACCOUNT` — webhooks are sent to the URLs configured in the sub-account's own settings

Valid values[
  "MASTER_ACCOUNT",
  "SUB_ACCOUNT"
]Default"MASTER_ACCOUNT"

Responses200

Sub-account created successfully. Returns a Sub-Account V3 object.

<select class='api-response-data' aria-label='Media type'><option value='f841d9de-4272-4902-81fa-bb03ccf28ed6'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='8bf3e2ab-45a9-4b20-a276-1fa41f098952'>Corporation (SG)</option>
<option value='0ce59886-f264-4b06-bf94-fa1c3fc43a19'>Minimal request (ID, defaults)</option>
<option value='d7f3a25c-3df1-4e6f-9526-ec4fc0667a57'>Test mode</option>
</select>Corporation (SG)

```json
{
  "id": "5cafeb170a2b18519b1b8761",
  "name": "Acme Corp",
  "email": "owner@acme.com",
  "status": "REGISTERED",
  "identity": {
    "country_of_incorporation": "SG",
    "entity_type": "CORPORATION"
  },
  "configuration": {
    "users": {
      "send_email_invite": true
    },
    "webhooks": {
      "recipient": "MASTER_ACCOUNT"
    }
  },
  "created_at": "2026-07-07T10:00:00Z",
  "updated_at": "2026-07-07T10:00:00Z"
}
```

Minimal request (ID, defaults)

```json
{
  "id": "5cafeb170a2b18519b1b8762",
  "name": "Toko Berkah",
  "email": "owner@tokoberkah.co.id",
  "status": "REGISTERED",
  "identity": {
    "country_of_incorporation": "ID",
    "entity_type": "INDIVIDUAL"
  },
  "configuration": {
    "users": {
      "send_email_invite": false
    },
    "webhooks": {
      "recipient": "MASTER_ACCOUNT"
    }
  },
  "created_at": "2026-07-07T10:00:00Z",
  "updated_at": "2026-07-07T10:00:00Z"
}
```

Test mode

Test mode sub-accounts are provisioned immediately with status `LIVE`, and `identity` and `configuration` are returned with default values.

```json
{
  "id": "5cafeb170a2b18519b1b8763",
  "name": "Acme Corp (Test)",
  "email": "owner@acme.com",
  "status": "LIVE",
  "identity": {
    "country_of_incorporation": "SG",
    "entity_type": "CORPORATION"
  },
  "configuration": {
    "users": {
      "send_email_invite": false
    },
    "webhooks": {
      "recipient": "MASTER_ACCOUNT"
    }
  },
  "created_at": "2026-07-07T10:00:00Z",
  "updated_at": "2026-07-07T10:00:00Z"
}
```

Expand Allobject  

A Sub-Account V3 object

idstring    

ID of the sub-account. Use this in the `for-user-id` header to create transactions on behalf of the sub-account.

Example5cafeb170a2b18519b1b8761
namestring    

Sub-account display name

emailstring  (email)    

Email address of the sub-account owner

statusstring    

Status of the sub-account. Sub-accounts created in Test mode always report `LIVE`.

Valid values[
  "REGISTERED",
  "AWAITING_DOCS",
  "PENDING_VERIFICATION",
  "AWAITING_RESUBMISSION",
  "LIVE",
  "DECLINED",
  "DORMANT",
  "SUSPENDED",
  "CLOSED"
]
identity

The legal identity of the sub-account's business.

`country_of_incorporation` is an ISO 3166-1 alpha-2 country code. It must match your master account's country of operation unless cross-country sub-accounts are explicitly enabled for your account.

The available `entity_type` values depend on `country_of_incorporation` — see the per-country variants below. Any country not listed follows the Singapore (SG) entity type list.

OneOfIndonesia (ID)object (Indonesia (ID))country_of_incorporationstring    Valid values[
  "ID"
]
entity_typestring    Valid values[
  "CORPORATION",
  "SOLE_PROPRIETORSHIP",
  "PARTNERSHIP",
  "NON_PROFIT",
  "INDIVIDUAL",
  "COOPERATIVE"
]

Philippines (PH)object (Philippines (PH))country_of_incorporationstring    Valid values[
  "PH"
]
entity_typestring    Valid values[
  "CORPORATION",
  "SOLE_PROPRIETORSHIP",
  "PARTNERSHIP",
  "INDIVIDUAL",
  "ONE_PERSON_CORPORATION"
]

Vietnam (VN)object (Vietnam (VN))country_of_incorporationstring    Valid values[
  "VN"
]
entity_typestring    Valid values[
  "CORPORATION",
  "SOLE_PROPRIETORSHIP",
  "PARTNERSHIP",
  "LIMITED_LIABILITY_COMPANY"
]

Thailand (TH)object (Thailand (TH))country_of_incorporationstring    Valid values[
  "TH"
]
entity_typestring    Valid values[
  "CORPORATION",
  "PARTNERSHIP",
  "NON_PROFIT",
  "INDIVIDUAL"
]

Malaysia (MY)object (Malaysia (MY))country_of_incorporationstring    Valid values[
  "MY"
]
entity_typestring    Valid values[
  "CORPORATION",
  "SOLE_PROPRIETORSHIP",
  "PARTNERSHIP",
  "NON_PROFIT"
]

Singapore (SG)object (Singapore (SG))country_of_incorporationstring    Valid values[
  "SG"
]
entity_typestring    Valid values[
  "CORPORATION",
  "PARTNERSHIP"
]

Hong Kong (HK)object (Hong Kong (HK))country_of_incorporationstring    Valid values[
  "HK"
]
entity_typestring    Valid values[
  "CORPORATION",
  "PARTNERSHIP"
]

Mexico (MX)object (Mexico (MX))country_of_incorporationstring    Valid values[
  "MX"
]
entity_typestring    Valid values[
  "CORPORATION",
  "SOLE_PROPRIETORSHIP",
  "PARTNERSHIP",
  "NON_PROFIT"
]

configurationobject (AccountConfigurationV3)  

Optional behaviour configuration for the sub-account

usersobject  send_email_inviteboolean    

If `true`, sends an email invitation to `email` on account creation so the owner can access the sub-account dashboard and continue filling in the sub-account's KYC information. Available for every entity type. Only applies in Live mode.

Defaultfalse

webhooksobject  recipientstring    

Where webhooks for the sub-account's transactions are delivered:

- `MASTER_ACCOUNT` — webhooks are sent to the URLs configured in the master account's settings (default)
- `SUB_ACCOUNT` — webhooks are sent to the URLs configured in the sub-account's own settings

Valid values[
  "MASTER_ACCOUNT",
  "SUB_ACCOUNT"
]Default"MASTER_ACCOUNT"

created_atstring  (date-time)    

Timestamp of when the sub-account was created

updated_atstring  (date-time)    

Timestamp of when the sub-account was last updated

400

Invalid request.

| Error code | Description |
| --- | --- |
| `API_VALIDATION_ERROR` | Inputs are failing validation — a required field is missing or malformed |
| `INVALID_DATA_PROVIDED` | A field value is invalid — unsupported entity type for the given country, cross-country sub-account not allowed, or Test mode restriction violated |
| `MAXIMUM_ACCOUNT_REACHED` | You have reached the Test mode sub-account limit (500). This limit does not apply in Live mode. |

<select class='api-response-data' aria-label='Media type'><option value='268da9a1-7bbf-403e-835b-926b5967b699'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='fb839fca-4323-4ea8-94dc-b8a9bb1e9210'>InvalidDataProvided</option>
<option value='6a61548b-0775-447e-a26a-043d2dff9b99'>InvalidDataProvidedTestMode</option>
<option value='613089e3-27a0-44f1-bf8e-aaeab2b9bed5'>MaximumAccountReached</option>
</select>InvalidDataProvided

```json
{
  "error_code": "INVALID_DATA_PROVIDED",
  "message": "Invalid 'identity.entity_type' provided. Check allowed entity types for the provided country."
}
```

InvalidDataProvidedTestMode

```json
{
  "error_code": "INVALID_DATA_PROVIDED",
  "message": "Invalid 'identity.entity_type' provided. Only CORPORATION is supported in TEST mode."
}
```

MaximumAccountReached

```json
{
  "error_code": "MAXIMUM_ACCOUNT_REACHED",
  "message": "You may only create 500 Accounts in TEST mode. Contact help@xendit.co if you need a higher limit"
}
```

object  error_codestring    
messagestring    

401

Unauthorized.

| Error code | Description |
| --- | --- |
| `INVALID_CREDENTIALS` | The API key is missing/invalid, or the account it belongs to is not enabled for xenPlatform |

<select class='api-response-data' aria-label='Media type'><option value='f27cb068-0e6c-4f4d-bcdd-3741a19f1e8e'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='4dc12f3b-2f16-4d68-9d56-4da56d818f15'>InvalidCredentials</option>
</select>InvalidCredentials

```json
{
  "error_code": "INVALID_CREDENTIALS",
  "message": "Your credentials are not valid to make this request"
}
```

object  error_codestring    
messagestring    

403

Forbidden.

| Error code | Description |
| --- | --- |
| `DISALLOWED_OPERATION` | Operation not permitted for your account |

<select class='api-response-data' aria-label='Media type'><option value='156b3edc-3d35-497e-9986-f6f29349c930'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='e007fd68-9105-45ab-a097-848e96ebfa60'>DisallowedOperation</option>
</select>DisallowedOperation

```json
{
  "error_code": "DISALLOWED_OPERATION",
  "message": "You are not authorized to create accounts"
}
```

object  error_codestring    
messagestring    

404

Not found.

| Error code | Description |
| --- | --- |
| `BUSINESS_NOT_FOUND_ERROR` | Master account not found |

<select class='api-response-data' aria-label='Media type'><option value='1e36be9a-1fd8-43ac-a4c5-8fe8f2eb00af'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='f70a4435-60d3-4195-97f3-4f079136af50'>BusinessNotFound</option>
</select>BusinessNotFound

```json
{
  "error_code": "BUSINESS_NOT_FOUND_ERROR",
  "message": "Business not found"
}
```

object  error_codestring    
messagestring
