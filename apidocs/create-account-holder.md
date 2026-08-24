---
title: "Create account holder"
slug: "create-account-holder"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/create-account-holder"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create account holder

Post/account_holders

An Account Holder represents the legal entity that holds the Xendit Account that is created in your Platform. You will need to [Create an Account](/apidocs/create-account-holder#create-account) to link the account holder with. The details that you need to provide in the request depend on the Account holders' legal entity type. Please refer to [this guide](https://docs.xendit.co/docs/xenplatform-account-holder-api) for a comprehensive step-by-step as well as requirements for each country and entity type.

You will need to use [Update Account](/update-a-xenplatform-account) API to link the Account Holder to the xenPlatform Account before the verification can begin.

> You will need the Account Holder `Write` API key permission to perform this request

SecurityHTTPType basic

Body parameters<select class='api-response-data' aria-label='Media type'><option value='a7e37ec8-c888-41ea-96fa-a486d9228ca5'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='bfb7aec5-dbc6-4f18-9fd8-6199de9fb9ec'>Philippines Corporation</option>
</select>Philippines Corporation

```json
{
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
  "email": "test@xendit.co"
}
```

Expand Allobject  business_detailobject (business_detail)  Required

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

individual_details Array of object (individual_detail)   Requiredobject  

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

addressobject (address)  Required

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

kyc_documents Array of object (kyc_document)   Requiredobject  

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

website_urlstring  (website)    Required

A valid website associated with the business

Max length255Examplemystore.com
phone_numberstring  (phone)    Required

A valid phone number associated with the business

Max length30Example62123456789
emailstring  (email)    Required

A valid email address associated with the object

Max length255Exampletest@example.co

Responses200<select class='api-response-data' aria-label='Media type'><option value='9f196e4c-d0e2-49f9-894f-f78ae04bcf97'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='0dc85921-0201-4e18-be16-20a9eac6f849'>Philippines Corporation</option>
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
    "status": "NOT_VERIFIED"
  },
  "created_at": "2023-03-30T11:41:57.881Z",
  "updated_at": "2023-03-30T11:44:01.122Z"
}
```

Expand Allobject  idstring    

The unique ID of an Account Holder object

business_detailobject (business_detail)  

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
kycobject  statusstring    Valid values[
  "NOT_VERIFIED",
  "VERIFIED"
]

created_atstring  (date-time)    

Timestamp of when the object was created

updated_atstring  (date-time)    

Timestamp of when the object was updated

400

Validation error

<select class='api-response-data' aria-label='Media type'><option value='71d444f9-84be-44bc-8122-214c34220467'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='1fd960ec-1fff-492e-8f7d-798a15592387'>API_VALIDATION_ERROR</option>
</select>API_VALIDATION_ERROR

```json
{
  "error_code": "API_VALIDATION_ERROR",
  "message": "Inputs are failing validation. The errors field contains details about which fields are violating validation.",
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

401

Validation error

<select class='api-response-data' aria-label='Media type'><option value='80a9615d-077b-4466-8f1e-a65e991b9e9c'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='7e6946e4-43f0-4175-b40c-6311b030210d'>INVALID_API_KEY</option>
</select>INVALID_API_KEY

```json
{
  "error_code": "INVALID_API_KEY",
  "message": "The API key format is invalid",
  "errors": [
    "Detailed description here"
  ]
}
```

object  

Invalid API key

error_codestring    Valid values[
  "INVALID_API_KEY"
]
messagestring    
errors Array  OneOfstringstring
objectobject

403

Validation error

<select class='api-response-data' aria-label='Media type'><option value='c3cafe6e-922c-4b08-8b2f-51b95ba206b8'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='f36888db-b4c3-4487-a697-a023c2c14c6d'>REQUEST_FORBIDDEN_ERROR</option>
<option value='c17eb3c5-0be9-4b14-ac42-9b33841b4ff0'>FEATURE_NOT_ACTIVATED</option>
</select>REQUEST_FORBIDDEN_ERROR

```json
{
  "error_code": "REQUEST_FORBIDDEN_ERROR",
  "message": "The API key in use does not have the necessary permissions to perform the request. Please assign the xenPlatform Account Holder Write permission for the key.",
  "errors": [
    "Detailed description here"
  ]
}
```

FEATURE_NOT_ACTIVATED

```json
{
  "error_code": "FEATURE_NOT_ACTIVATED",
  "message": "This feature has not been activated for your account",
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

404

Not found error

<select class='api-response-data' aria-label='Media type'><option value='b729a03b-230c-49c9-9c56-916bdfb23cec'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='6ca8708d-c9a9-44bf-a993-7b26259c531b'>DATA_NOT_FOUND</option>
</select>DATA_NOT_FOUND

```json
{
  "error_code": "DATA_NOT_FOUND",
  "message": "Could not find payout with the corresponding ID. Please try again with a valid ID.",
  "errors": [
    "Detailed description here"
  ]
}
```

object  

The object being referenced does not exist

error_codestring    Valid values[
  "DESTINATION_ACCOUNT_NOT_FOUND",
  "DATA_NOT_FOUND",
  "CALLBACK_AUTHENTICATION_TOKEN_NOT_FOUND_ERROR"
]
messagestring    
errors Array  OneOfstringstring
objectobject

500

Validation error

<select class='api-response-data' aria-label='Media type'><option value='0daa9bf6-4fb4-4a82-b457-50950fdcbc65'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='8cb5be29-c124-4e4b-8da0-47a58cfb667a'>SERVER_ERROR</option>
</select>SERVER_ERROR

```json
{
  "error_code": "SERVER_ERROR",
  "message": "Something unexpected, our developers have been notified to troubleshoot the issue",
  "errors": [
    "Detailed description here"
  ]
}
```

object  

Server error

error_codestring    Valid values[
  "SERVER_ERROR"
]
messagestring    
errors Array  OneOfstringstring
objectobject
