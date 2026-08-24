---
title: "Update account holder"
slug: "update-account-holder"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/update-account-holder"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Update account holder

Patch/account_holders/{id}

Use the Update Account Holder endpoint to:

1. Update your Account Holder information. This step may be needed when the your information and document submission is insufficient or invalid (e.g invalid website, blurry selfie, invalid ID, etc.).
2. Activate a payment channel Capability on an Account Holder object associated with a sub-account

You need to provide an URL to receive webhooks. Please specify your URL in [Webhook Settings](https://dashboard.xendit.co/settings/developers#callbacks) in the Xendit Dashboard.

> You will need the Account Holder `Write` API key permission to perform this request.

SecurityHTTPType basic

Path parametersidstringRequiredExample4376b7b0-1c44-46be-8640-828f79cdc8be

Body parameters<select class='api-response-data' aria-label='Media type'><option value='175baf1b-d53f-4e31-8618-2890f034ef3c'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='1d44aa91-2f93-4b49-ae72-ce195e2791bf'>Update Website</option>
<option value='efb89345-6ed0-4d4a-8226-bcf6755b4483'>Update KYC Document</option>
<option value='e88da3fd-d1de-4758-94e9-621744c9922b'>Activate Payment Channel Capabilities</option>
</select>Update Website

```json
{
  "website_url": "valid-marketplace.brand.com"
}
```

Update KYC Document

```json
{
  "kyc_documents": [
    {
      "country": "PH",
      "type": "LATEST_GIS_DOCUMENT",
      "file_id": "63f8719642f5856dc9feje7"
    }
  ]
}
```

Activate Payment Channel Capabilities

```json
{
  "capabilities": [
    {
      "type": "MONEY_IN",
      "channel_code": "PH_CARDS"
    },
    {
      "type": "MONEY_IN",
      "channel_code": "GCASH"
    }
  ]
}
```

Expand Allobject  business_detailobject (business_detail)  

An object containing the business detail of the Account Holder

typestring    

The entity type of the business

Valid values[
  "CORPORATION",
  "PARTNERSHIP",
  "SOLE_PROPRIETORSHIP",
  "INDIVIDUAL",
  "FOREIGN",
  "FOREIGN_SEC",
  "FOREIGN_NONSEC"
]
legal_namestring    

Legal name of the business. This must match the documentation submitted.

trading_namestring    

Trading or brand name of the business. This will be the name that appears to endpayer on payment page.

descriptionstring    

Description of the business. Please specify what business model or goods and services that the business provide. Max 1000 characters.

industry_categorystring    

One of our accepted Industry Category Codes depending on your entity type and country of operation.

Refer to the list of [accepted industry category codes here](https://docs.xendit.co/docs/create-verification-requests#list-of-accepted-industry-categories)

date_of_registrationstring  (date)    

Business registration date in YYYY-MM-DD

country_of_operationstring    

The country (based on ISO 3166-1 Alpha-2) of incorporation for a business, or the country of residence for an individual.

Valid values[
  "ID",
  "PH",
  "VN",
  "MY",
  "TH"
]

individual_details Array of object (individual_detail)   object  

An object containing the individual details of the Account Holder. This could be the details of the business owner, director etc.

typestring    Required

At least one individual with the type `PIC` (Person in Charge) is required. You may submit multiple PICs for your business in this object. A minimum 1 Incorporator and 1 PIC is required when they need to activate Cards capabilities.

Valid values[
  "PIC",
  "Incorporator"
]
rolestring    Required

This role specifies the role of the PIC or Incorporator. E.g. Owner, Director, Administrator.

given_namesstring    Required

First and middle name (if any) of the account holder

Max length255
surnamestring    Required

Surname or family name of the account holder

Max length255
phone_numberstring    Required

The contact number of the Account Holder in `E.164` format. This may also be a landline.

Max length30
emailstring    Required

The email address of the account holder

Max length255
nationalitystring    Required

Country code for customer's nationality (ISO 3166-2 Country Code)

place_of_birthstring    

City or other relevant location of the account holder's birth place

date_of_birthstring  (date)    

Date of birth of the customer in YYYY-MM-DD

genderstring    

The gender of the account holder

Valid values[
  "MALE",
  "FEMALE",
  "OTHER"
]
tax_identification_numberstring    

Tax Identification Number of the account holder. This parameter is required when they need to activate Cards capabilities with USD or recurring capabilities.

Please see more details [here](https://docs.xendit.co/docs/activate-payment-channels)

addressobject (address)  

An address object.

countrystring    Required

The country (based on ISO 3166-1 Alpha-2) of incorporation for a business, or the country of residence for an individual.

Valid values[
  "ID",
  "PH",
  "VN",
  "MY",
  "TH"
]
citystring    Required

City, village or town

province_statestring    Required

Province, state or region

street_line1string    Required

Line 1 of street address e.g street number and name

Max length255
street_line2string    Required

Line 2 of street address e.g building name or apartment number

Max length255
districtstring    Required

District

sub_districtstring    Required

Sub-district

postal_codestring    Required

Zip or postal code

addressobject (address)  

An address object.

countrystring    Required

The country (based on ISO 3166-1 Alpha-2) of incorporation for a business, or the country of residence for an individual.

Valid values[
  "ID",
  "PH",
  "VN",
  "MY",
  "TH"
]
citystring    Required

City, village or town

province_statestring    Required

Province, state or region

street_line1string    Required

Line 1 of street address e.g street number and name

Max length255
street_line2string    Required

Line 2 of street address e.g building name or apartment number

Max length255
districtstring    Required

District

sub_districtstring    Required

Sub-district

postal_codestring    Required

Zip or postal code

kyc_documents Array of object (kyc_document)   object  

A KYC document file for Account Holder verification

countrystring    

The country (based on ISO 3166-1 Alpha-2) of incorporation for a business, or the country of residence for an individual.

Valid values[
  "ID",
  "PH",
  "VN",
  "MY",
  "TH"
]
typestring    

The type of the legal or KYC requirements document

Refer to the list of [Required KYC Documents for all countries here](https://docs.xendit.co/docs/create-verification-requests#requirements-by-country-and-entity-type)

expires_atstring    

Expiry date of the document if relevant. Format `YYYY-MM-DD`

file_idstring    

The file ID returned by the Upload API

website_urlstring  (website)    

A valid website associated with the business

Max length255Examplemystore.com
phone_numberstring  (phone)    

A valid phone number associated with the business

Max length30Example62123456789
emailstring  (email)    

A valid email address associated with the object

Max length255Exampletest@example.co
capabilities Array of object   object  typestring    Valid values[
  "MONEY_IN"
]
channel_codestring    

Responses200<select class='api-response-data' aria-label='Media type'><option value='0847ec3a-b527-4c13-9cf6-0445c4653853'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='d0b4672c-f74e-402d-b893-2e72cb063646'>Philippines Corporation</option>
</select>Philippines Corporation

```json
{
  "id": "4376b7b0-1c44-46be-8640-828f79cdc8be",
  "business_detail": {
    "type": "CORPORATION",
    "legal_name": "My Store Inc.",
    "trading_name": "John's Store",
    "description": "description here",
    "industry_category": "ELECTRONICS_AND_ACCESSORIES",
    "date_of_registration": "2023-02-02",
    "country_of_operation": "PH"
  },
  "individual_details": [
    {
      "given_names": "John",
      "surname": "Doe",
      "phone_number": "+63021234567",
      "email": "test@xendit.co",
      "nationality": "PH",
      "place_of_birth": "PH",
      "date_of_birth": "2000-02-02",
      "gender": "MALE",
      "type": "PIC",
      "role": "owner"
    }
  ],
  "address": {
    "country": "PH",
    "city": "Caloocan",
    "street_line1": "9th St",
    "street_line2": "Building 101",
    "district": "1st district",
    "sub_district": "2nd subdistrict",
    "province_state": "Metro Manila",
    "postal_code": "1400"
  },
  "kyc_documents": [
    {
      "type": "SEC_CERTIFICATE_REGISTRATION_DOCUMENT",
      "country": "PH",
      "file_id": "63f8719642f5856dcb142bd2"
    },
    {
      "type": "ARTICLES_OF_INCORPORATION_DOCUMENT",
      "country": "PH",
      "file_id": "63f8719642f5856dcb142bd2"
    },
    {
      "type": "NOTARIZED_SECRETARY_CERTIFICATE_DOCUMENT",
      "country": "PH",
      "file_id": "63f8719642f5856dcb142bd2"
    },
    {
      "type": "LATEST_GIS_DOCUMENT",
      "country": "PH",
      "file_id": "63f8719642f5856dcb142bd2"
    },
    {
      "type": "ACR_OR_IMMIGRANT_COR_DOCUMENT",
      "country": "PH",
      "file_id": "63f8719642f5856dcb142bd2"
    },
    {
      "type": "SERVICE_AGREEMENT_DOCUMENT",
      "country": "PH",
      "file_id": "63f8719642f5856dcb142bd2"
    }
  ],
  "website_url": "https://xendit.co",
  "phone_number": "+6381234567",
  "email": "test@xendit.co",
  "kyc": {
    "status": "PASSED",
    "requested_at": "2021-01-01T10:00:00Z",
    "verified_at": "2021-01-02T10:00:00Z",
    "kyc_passed_at": "2021-01-03T10:00:00Z"
  },
  "capabilities": [
    {
      "type": "MONEY_IN",
      "channel_code": "GCASH",
      "requested_at": "2021-01-01T10:00:00Z",
      "verified_at": "2021-01-02T10:00:00Z",
      "activated_at": "2021-01-03T10:00:00Z",
      "status": "VERIFICATION_IN_PROGRESS"
    }
  ]
}
```

Expand Allobject  business_detailobject (business_detail)  

An object containing the business detail of the Account Holder

typestring    

The entity type of the business

Valid values[
  "CORPORATION",
  "PARTNERSHIP",
  "SOLE_PROPRIETORSHIP",
  "INDIVIDUAL",
  "FOREIGN",
  "FOREIGN_SEC",
  "FOREIGN_NONSEC"
]
legal_namestring    

Legal name of the business. This must match the documentation submitted.

trading_namestring    

Trading or brand name of the business. This will be the name that appears to endpayer on payment page.

descriptionstring    

Description of the business. Please specify what business model or goods and services that the business provide. Max 1000 characters.

industry_categorystring    

One of our accepted Industry Category Codes depending on your entity type and country of operation.

Refer to the list of [accepted industry category codes here](https://docs.xendit.co/docs/create-verification-requests#list-of-accepted-industry-categories)

date_of_registrationstring  (date)    

Business registration date in YYYY-MM-DD

country_of_operationstring    

The country (based on ISO 3166-1 Alpha-2) of incorporation for a business, or the country of residence for an individual.

Valid values[
  "ID",
  "PH",
  "VN",
  "MY",
  "TH"
]

individual_details Array of object (individual_detail)   object  

An object containing the individual details of the Account Holder. This could be the details of the business owner, director etc.

typestring    

At least one individual with the type `PIC` (Person in Charge) is required. You may submit multiple PICs for your business in this object. A minimum 1 Incorporator and 1 PIC is required when they need to activate Cards capabilities.

Valid values[
  "PIC",
  "Incorporator"
]
rolestring    

This role specifies the role of the PIC or Incorporator. E.g. Owner, Director, Administrator.

given_namesstring    

First and middle name (if any) of the account holder

Max length255
surnamestring    

Surname or family name of the account holder

Max length255
phone_numberstring    

The contact number of the Account Holder in `E.164` format. This may also be a landline.

Max length30
emailstring    

The email address of the account holder

Max length255
nationalitystring    

Country code for customer's nationality (ISO 3166-2 Country Code)

place_of_birthstring    

City or other relevant location of the account holder's birth place

date_of_birthstring  (date)    

Date of birth of the customer in YYYY-MM-DD

genderstring    

The gender of the account holder

Valid values[
  "MALE",
  "FEMALE",
  "OTHER"
]
tax_identification_numberstring    

Tax Identification Number of the account holder. This parameter is required when they need to activate Cards capabilities with USD or recurring capabilities.

Please see more details [here](https://docs.xendit.co/docs/activate-payment-channels)

addressobject (address)  

An address object.

countrystring    

The country (based on ISO 3166-1 Alpha-2) of incorporation for a business, or the country of residence for an individual.

Valid values[
  "ID",
  "PH",
  "VN",
  "MY",
  "TH"
]
citystring    

City, village or town

province_statestring    

Province, state or region

street_line1string    

Line 1 of street address e.g street number and name

Max length255
street_line2string    

Line 2 of street address e.g building name or apartment number

Max length255
districtstring    

District

sub_districtstring    

Sub-district

postal_codestring    

Zip or postal code

addressobject (address)  

An address object.

countrystring    

The country (based on ISO 3166-1 Alpha-2) of incorporation for a business, or the country of residence for an individual.

Valid values[
  "ID",
  "PH",
  "VN",
  "MY",
  "TH"
]
citystring    

City, village or town

province_statestring    

Province, state or region

street_line1string    

Line 1 of street address e.g street number and name

Max length255
street_line2string    

Line 2 of street address e.g building name or apartment number

Max length255
districtstring    

District

sub_districtstring    

Sub-district

postal_codestring    

Zip or postal code

kyc_documents Array of object (kyc_document)   object  

A KYC document file for Account Holder verification

countrystring    

The country (based on ISO 3166-1 Alpha-2) of incorporation for a business, or the country of residence for an individual.

Valid values[
  "ID",
  "PH",
  "VN",
  "MY",
  "TH"
]
typestring    

The type of the legal or KYC requirements document

Refer to the list of [Required KYC Documents for all countries here](https://docs.xendit.co/docs/create-verification-requests#requirements-by-country-and-entity-type)

expires_atstring    

Expiry date of the document if relevant. Format `YYYY-MM-DD`

file_idstring    

The file ID returned by the Upload API

website_urlstring  (website)    

A valid website associated with the business

Max length255Examplemystore.com
phone_numberstring  (phone)    

A valid phone number associated with the business

Max length30Example62123456789
emailstring  (email)    

A valid email address associated with the object

Max length255Exampletest@example.co
capabilities Array of object (account_holder_capability_response)   object  

An object containing the details of the Account Holder capabilities activation process

typestring    
channel_codestring    
statusstring    Valid values[
  "LIVE",
  "VERIFICATION_IN_PROGRESS",
  "RESUBMISSION_REQUIRED",
  "DECLINED"
]
failure_reasonstring    
activated_atstring  (date-time)    

Timestamp of when the object was updated

verified_atstring  (date-time)    

Timestamp of when the object was updated

requested_atstring  (date-time)    

Timestamp of when the object was updated

kycobject (account_holder_kyc_response)  statusstring    Valid values[
  "PASSED",
  "FAILED",
  "RESUBMISSION_REQUIRED"
]
requested_atstring  (date-time)    

Timestamp of when the object was updated

kyc_passed_atstring  (date-time)    

Timestamp of when the object was updated

verified_atstring  (date-time)    

Timestamp of when the object was updated

400<select class='api-response-data' aria-label='Media type'><option value='e2ba529e-d2c7-4260-8073-84d017886631'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='1d24a1c7-74cd-4014-bfa5-b76b709e206d'>INSUFFICIENT_ACCOUNT_HOLDER_DATA</option>
</select>INSUFFICIENT_ACCOUNT_HOLDER_DATA

```json
{
  "error_code": "INSUFFICIENT_ACCOUNT_HOLDER_DATA",
  "message": "The information in the Account Holder object is not sufficient to request activation for this payment channel. Please update the fields with the correct information.",
  "errors": [
    "Detailed description here"
  ]
}
```

object  

Inputs are failing validation. The errors field contains details about which fields are violating validation.

error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "INVALID_CONFIGURATION",
  "INVALID_JSON_FORMAT",
  "TYPE_AND_CONFIGURATION_CONFLICT",
  "INVALID_SOURCE_OR_DESTINATION_ERROR",
  "INSUFFICIENT_BALANCE",
  "INVALID_FEE_AMOUNT",
  "DUPLICATE_ERROR",
  "INVALID_AMOUNT",
  "INSUFFICIENT_ACCOUNT_HOLDER_DATA",
  "MISMATCH_PAYLOAD_FOR_REFERENCE",
  "INVALID_URL_FORMAT"
]
messagestring    
errors Array  OneOfstringstring
objectobject

403<select class='api-response-data' aria-label='Media type'><option value='be939cc5-8c4d-499b-a28d-e6ba4f51e039'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='d95a0569-eca9-4c34-93f9-6edf64e6ff11'>KYC_VERIFICATION_IN_PROGRESS</option>
<option value='fcb86d8a-dbef-4dcb-a522-47988489062d'>CHANNEL_HAS_BEEN_ACTIVATED</option>
</select>KYC_VERIFICATION_IN_PROGRESS

```json
{
  "error_code": "KYC_VERIFICATION_IN_PROGRESS",
  "message": "Account Holder cannot be updated while KYC verification is in progress, please try again when the verification process has been completed.",
  "errors": [
    "Detailed description here"
  ]
}
```

CHANNEL_HAS_BEEN_ACTIVATED

```json
{
  "error_code": "CHANNEL_HAS_BEEN_ACTIVATED",
  "message": "The payment channel requested has already been activated for this account holder.",
  "errors": [
    "Detailed description here"
  ]
}
```

object  

Forbidden request

error_codestring    Valid values[
  "REQUEST_FORBIDDEN_ERROR",
  "FEATURE_NOT_ACTIVATED",
  "DUPLICATE_REFERENCE",
  "XEN_PLATFORM_SUB_ACCOUNT_NOT_LIVE",
  "API_KEY_ENVIRONMENT_NOT_MATCH",
  "CHANNEL_ACTIVATION_IN_PROGRESS",
  "CHANNEL_HAS_BEEN_ACTIVATED",
  "KYC_VERIFICATION_IN_PROGRESS"
]
messagestring    
errors Array  OneOfstringstring
objectobject
