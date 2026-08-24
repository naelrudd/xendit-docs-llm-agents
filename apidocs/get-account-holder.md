---
title: "Get account holder"
slug: "get-account-holder"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/get-account-holder"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Get account holder

Get/account_holders/{id}

This endpoint retrieves a single Account Holder that was previously created. This is often used for checking the verification status of a Account Holder using the id from the Account Holder Object.

> Use API key permission Account Holder `Read` to perform this request

SecurityHTTPType basic

Path parametersidstringRequiredExample4376b7b0-1c44-46be-8640-828f79cdc8be

Responses200<select class='api-response-data' aria-label='Media type'><option value='7e7004a7-cff0-4cac-9713-d0ec0dc471b6'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='c35846ba-f59f-42b6-be5e-676900fbed29'>Philippines Corporation</option>
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

401

Not found error

<select class='api-response-data' aria-label='Media type'><option value='23830aba-d539-46a1-94d8-886ac0f67eca'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='98bf8244-e476-4623-bb8a-aea8b1d6ff56'>INVALID_API_KEY</option>
</select>INVALID_API_KEY

```json
{
  "error_code": "INVALID_API_KEY",
  "message": "The API key is invalid",
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

Forbidden error

<select class='api-response-data' aria-label='Media type'><option value='811d2401-a3cb-40d3-81c2-c020c58faf56'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='0350fdc5-785b-4576-8629-cbd89781e79e'>REQUEST_FORBIDDEN_ERROR</option>
</select>REQUEST_FORBIDDEN_ERROR

```json
{
  "error_code": "REQUEST_FORBIDDEN_ERROR",
  "message": "API key in use does not have necessary permissions to perform the request. Please assign the xenPlatform Account Holder Read permission for the key.",
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

<select class='api-response-data' aria-label='Media type'><option value='6aa68cad-b58b-4e9e-97e7-d1860f30426b'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='a76f6958-852b-4ee2-8be4-9e4cdb8bd286'>DATA_NOT_FOUND</option>
</select>DATA_NOT_FOUND

```json
{
  "error_code": "DATA_NOT_FOUND",
  "message": "Could not find an account holder with the corresponding ID. Please try again with a valid ID.",
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
