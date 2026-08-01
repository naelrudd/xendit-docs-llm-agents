---
title: "Create customer request"
slug: "create-customer-request"
updated: 2026-04-01T03:43:19Z
published: 2026-04-01T03:43:19Z
canonical: "docs.xendit.co/create-customer-request"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create customer request

Post/customers

Make a POST request to this endpoint to create a customer for later use with a payments endpoint.

The Customer Object is a standard data structure to hold information relating to one of your customers. It has the following major components:

- A Type of customer (Individual or Business)
- Basic descriptive details of that customer
- Addresses of the customer
- Identity accounts and KYC documents to prove the legitimacy of the customer
- Other metadata

SecurityHTTPType Basic

Header parametersidempotency-keystring

A unique key to prevent processing duplicate requests. Can be your reference_id or any GUID. Must be unique across development & production environments. Idempotency keys are stored on the request layer; it expires after 24 hours from the first request

Min length1Max length100
api-versionstring

API version in date semantic. Attach this parameter when calling a specific API version. List of API versions can be found here.

Valid values[
  "2020-10-31",
  "2020-05-19"
]
for-user-idstring

The sub-account user-id that you want to make this transaction for.

This header is only used if you have access to xenPlatform. See xenPlatform for more information

Body parameters<select class='api-response-data' aria-label='Media type'><option value='5a00bba5-23fa-44f4-9f07-f2f742ca1b53'>application/json</option>
</select>Expand Allobject  

Patch body request

individual_detailobject (XenditStandardIndividualDetail)  

JSON object containing details of the Individual. Required if type is `INDIVIDUAL`

given_namesstring    Required

Primary or first name/s of customer. Alphanumeric. No special characters is allowed.

Min length1Max length50
surnamestring   | null  

Last or family name of customer. Alphanumeric. No special characters is allowed.

Min length1Max length50
nationalitystring   | null  

Country code for customer nationality. ISO 3166-1 alpha-2 Country Code

Min length2Max length2
place_of_birthstring   | null  

City or other relevant location for the customer birth place. Alphanumeric. No special characters is allowed.

Min length1Max length60
date_of_birthstring   | null  

Date of birth of the customer. Format: YYYY-MM-DD

Min length10Max length10
genderstring   | null  

Gender of customer

Valid values[
  "MALE",
  "FEMALE",
  "OTHER"
]
employmentobject | null  employer_namestring    

Name of the employer

Min length1Max length50
nature_of_businessstring    

Industry or nature of business

Min length1Max length50
role_descriptionstring    

Occupation or title

Min length1Max length50

business_detailobject (XenditStandardBusinessDetail)  

JSON object containing details of the business. Required if type is `BUSINESS`

business_namestring    Required

Name of business

Min length1Max length50
trading_namestring   | null  

Trading name

Min length1Max length50
business_typestring    

Legal entity type of the business

Valid values[
  "SOLE_PROPRIETOR",
  "PARTNERSHIP",
  "COOPERATIVE",
  "TRUST",
  "NON_PROFIT",
  "GOVERNMENT",
  "CORPORATION"
]
nature_of_businessstring   | null  

Free text description of the type of business this entity pursues

Min length1Max length50ExampleEcommerce, Travel
business_domicilestring   | null  

Registered country of the business. ISO 3166 format

date_of_registrationstring  (date)   | null  

Business registration date

mobile_numberstring   | null  

Supports both E.164 international format (+<country code=""><subscriber number="">) and local formats with or without a leading zero.</subscriber></country>

Min length7Max length15
phone_numberstring   | null  

Supports both E.164 international format (+<country code=""><subscriber number="">) and local formats with or without a leading zero.</subscriber></country>

Min length7Max length15
emailstring  (email)   | null  

E-mail address of customer

Min length1Max length50
addressesobject (XenditStandardAddress)  countrystring    Required

ISO 3166-1 alpha-2 Country Code

Min length2Max length2
street_line1string    

Line 1 of street address e.g., building name and apartment number

Min length1Max length255
street_line2string    

Line 2 of street address e.g., building name and apartment number

Min length1Max length255
citystring    

City, village or town of residence of customer

Min length1Max length255
province_statestring    

Province, state or region of residence of customer

Min length1Max length255
postal_codestring    

ZIP/Postal Code of customer

Min length1Max length255
categorystring    

Address type

Valid values[
  "HOME",
  "WORK",
  "PROVINCIAL"
]
is_primaryboolean    

Defaults to false. Indicates that the information provided refers to the customer's primary address

Defaultfalse

kyc_documents Array of object (XenditKYCDocumentsObject)   object  countrystring    Required

ISO 3166-1 alpha-2 Country Code

Min length2Max length2
typestring    

Generic ID type

Valid values[
  "BIRTH_CERTIFICATE",
  "BANK_STATEMENT",
  "DRIVING_LICENSE",
  "IDENTITY_CARD",
  "PASSPORT",
  "VISA",
  "BUSINESS_REGISTRATION",
  "BUSINESS_LICENSE"
]
sub_typestring    

Specific ID type for IDENTITY_CARD types

Valid values[
  "NATIONAL_ID",
  "CONSULAR_ID",
  "VOTER_ID",
  "POSTAL_ID",
  "RESIDENCE_PERMIT",
  "TAX_ID",
  "STUDENT_ID",
  "MILITARY_ID",
  "MEDICAL_ID",
  "OTHERS"
]
document_namestring    

Free text description of the type of document (e.g., NIB, SIUP, AKTA). `Characters` alphanumeric. No special characters is allowed.

Max length255
document_numberstring    

Unique alphanumeric identity document number or code. `Characters` alphanumeric. No special characters is allowed.

Max length255
expires_atstring   | null  

Expiry date, if relevant

Example2024-11-11
holder_namestring    

Free text to capture the full name(s) of the individual or business as defined on the document, if relevant. `Characters` alphanumeric. No special characters is allowed.

Max length255
document_images Array of string   

Array of file ids returned from uploads to the files endpoint, representing images of the front/back of the document, in png/jpg/jpeg/pdf format

string    

descriptionstring   | null  

Merchant-provided description for the customer. `Characters` alphanumeric. No special characters is allowed.

Min length2Max length500
date_of_registrationstring  (date)    

Business registration date

domicile_of_registrationstring    

Country within which the account that the shopper had to create/sign up on the merchant's website resides (e.g. accounts created on Shopee SG have `SG` as the value for this field. ISO 3166-2 Country Code

Min length2Max length2
metadataobject  

Object of additional information related to the customer. Define the JSON properties and values as required to pass information through the APIs. You can specify up to 50 keys, with key names up to 40 characters long and values up to 500 characters long. This is only for your use and will not be used by Xendit.

Responses200

Successful operation

<select class='api-response-data' aria-label='Media type'><option value='7d07c084-4b9e-45e0-905f-d76357f7811d'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='2df8e1ac-34b6-4d54-8887-cdf8a1e74b5d'>getIndividualCustomer</option>
<option value='80508024-5603-494e-ba89-2b5365ff5b7c'>getBusinessCustomer</option>
</select>getIndividualCustomer

```json
{
  "id": "cust-239c16f4-866d-43e8-9341-7badafbc019f",
  "reference_id": "demo_1475801962607",
  "type": "INDIVIDUAL",
  "individual_detail": {
    "given_names": "John",
    "surname": "Doe",
    "nationality": "ID",
    "place_of_birth": "Jakarta",
    "date_of_birth": "1980-01-01",
    "gender": "MALE",
    "employment": {
      "employer_name": "Xendit",
      "nature_of_business": "Payment Gateway",
      "role_description": "Test dummy"
    }
  },
  "email": "customer@website.com",
  "mobile_number": "+62812123456",
  "phone_number": "+62812123456",
  "hashed_phone_number": "+628#######56",
  "addresses": [
    {
      "street_line1": "Panglima Polim IV",
      "street_line2": "Ruko Grand Panglima Polim, Blok E",
      "city": "Jakarta Selatan",
      "province_state": "DKI Jakarta",
      "postal_code": "993448",
      "country": "ID",
      "category": "HOME",
      "is_primary": true
    }
  ],
  "kyc_documents": [
    {
      "type": "IDENTITY_CARD",
      "sub_type": "NATIONAL_ID",
      "country": "ID",
      "document_name": "KTP",
      "document_number": "12356789012456",
      "expires_at": null,
      "holder_name": "John Doe",
      "document_images": [
        "file-ec700c1c-db17-4496-b1fb-04ebe551b412"
      ]
    }
  ],
  "description": "My first customer",
  "date_of_registration": "2020-03-30",
  "domicile_of_registration": "ID",
  "metadata": {
    "foo": "bar"
  },
  "created": "2020-03-30T06:12:47.212Z",
  "updated": "2020-03-30T06:12:47.212Z"
}
```

getBusinessCustomer

```json
{
  "id": "cust-239c16f4-866d-43e8-9341-7badafbc019f",
  "reference_id": "demo_1475801962607",
  "type": "BUSINESS",
  "business_detail": {
    "business_name": "ACME Corp",
    "trading_name": null,
    "business_type": "CORPORATION",
    "nature_of_business": null,
    "business_domicile": null,
    "date_of_registration": null
  },
  "email": "customer@website.com",
  "mobile_number": null,
  "phone_number": null,
  "hashed_phone_number": null,
  "addresses": [],
  "kyc_documents": [],
  "description": null,
  "date_of_registration": "2020-03-30",
  "domicile_of_registration": "ID",
  "metadata": {},
  "created": "2020-03-30T06:12:47.212Z",
  "updated": "2020-03-30T06:12:47.212Z"
}
```

Expand Allobject  

Customer Object

idstring    

Xendit unique Capture ID generated as reference for the end user

Max length41Examplecust-b98d6f63-d240-44ec-9bd5-aa42954c4f48
reference_idstring    

A Reference ID from merchants to identify their request.

Min length1Max length255
typestring    

Type of customer

Valid values[
  "INDIVIDUAL",
  "BUSINESS"
]
individual_detailobject  given_namesstring    

Primary or first name/s of customer. Alphanumeric. No special characters is allowed.

Min length1Max length50
surnamestring   | null  

Last or family name of customer. Alphanumeric. No special characters is allowed.

Min length1Max length50
nationalitystring   | null  

Country code for customer nationality. ISO 3166-1 alpha-2 Country Code

Min length2Max length2
place_of_birthstring   | null  

City or other relevant location for the customer birth place. Alphanumeric. No special characters is allowed.

Min length1Max length60
date_of_birthstring   | null  

Date of birth of the customer. Format: YYYY-MM-DD

Min length10Max length10
genderstring   | null  

Gender of customer

Valid values[
  "MALE",
  "FEMALE",
  "OTHER"
]
employmentobject | null  employer_namestring    

Name of the employer

Min length1Max length50
nature_of_businessstring    

Industry or nature of business

Min length1Max length50
role_descriptionstring    

Occupation or title

Min length1Max length50

business_detailobject  business_namestring    

Name of business

Min length1Max length50
trading_namestring   | null  

Trading name

Min length1Max length50
business_typestring    

Legal entity type of the business

Valid values[
  "SOLE_PROPRIETOR",
  "PARTNERSHIP",
  "COOPERATIVE",
  "TRUST",
  "NON_PROFIT",
  "GOVERNMENT",
  "CORPORATION"
]
nature_of_businessstring   | null  

Free text description of the type of business this entity pursues

Min length1Max length50ExampleEcommerce, Travel
business_domicilestring   | null  

Registered country of the business. ISO 3166 format

date_of_registrationstring  (date)   | null  

Business registration date

mobile_numberstring   | null  

Supports both E.164 international format (+<country code=""><subscriber number="">) and local formats with or without a leading zero.</subscriber></country>

Min length7Max length15
phone_numberstring   | null  

Supports both E.164 international format (+<country code=""><subscriber number="">) and local formats with or without a leading zero.</subscriber></country>

Min length7Max length15
hashed_phone_numberstring   | null  

Hashed phone number

Min length1Max length250
emailstring  (email)   | null  

E-mail address of customer

Min length1Max length50
addresses Array of object (XenditStandardAddress)   object  countrystring    

ISO 3166-1 alpha-2 Country Code

Min length2Max length2
street_line1string    

Line 1 of street address e.g., building name and apartment number

Min length1Max length255
street_line2string    

Line 2 of street address e.g., building name and apartment number

Min length1Max length255
citystring    

City, village or town of residence of customer

Min length1Max length255
province_statestring    

Province, state or region of residence of customer

Min length1Max length255
postal_codestring    

ZIP/Postal Code of customer

Min length1Max length255
categorystring    

Address type

Valid values[
  "HOME",
  "WORK",
  "PROVINCIAL"
]
is_primaryboolean    

Defaults to false. Indicates that the information provided refers to the customer's primary address

Defaultfalse

identity_accounts Array of object (IdentityAccount)   object  typestring    

Type of identity account

Valid values[
  "CREDIT_CARD",
  "DEBIT_CARD",
  "BANK_ACCOUNT"
]
companystring    

Financial institution or company name

descriptionstring    

Description of the account

countrystring    

ISO 3166-1 alpha-2 Country Code

Min length2Max length2
propertiesobject  

Additional properties specific to the account type

kyc_documents Array of object (XenditKYCDocumentsObject)   object  countrystring    

ISO 3166-1 alpha-2 Country Code

Min length2Max length2
typestring    

Generic ID type

Valid values[
  "BIRTH_CERTIFICATE",
  "BANK_STATEMENT",
  "DRIVING_LICENSE",
  "IDENTITY_CARD",
  "PASSPORT",
  "VISA",
  "BUSINESS_REGISTRATION",
  "BUSINESS_LICENSE"
]
sub_typestring    

Specific ID type for IDENTITY_CARD types

Valid values[
  "NATIONAL_ID",
  "CONSULAR_ID",
  "VOTER_ID",
  "POSTAL_ID",
  "RESIDENCE_PERMIT",
  "TAX_ID",
  "STUDENT_ID",
  "MILITARY_ID",
  "MEDICAL_ID",
  "OTHERS"
]
document_namestring    

Free text description of the type of document (e.g., NIB, SIUP, AKTA). `Characters` alphanumeric. No special characters is allowed.

Max length255
document_numberstring    

Unique alphanumeric identity document number or code. `Characters` alphanumeric. No special characters is allowed.

Max length255
expires_atstring   | null  

Expiry date, if relevant

Example2024-11-11
holder_namestring    

Free text to capture the full name(s) of the individual or business as defined on the document, if relevant. `Characters` alphanumeric. No special characters is allowed.

Max length255
document_images Array of string   

Array of file ids returned from uploads to the files endpoint, representing images of the front/back of the document, in png/jpg/jpeg/pdf format

string    

descriptionstring   | null  

Merchant-provided description for the customer. `Characters` alphanumeric. No special characters is allowed.

Min length2Max length500
date_of_registrationstring  (date)    

Date of which the account that the shopper had to create/sign up on the merchant's website

domicile_of_registrationstring    

Country within which the account that the shopper had to create/sign up on the merchant's website resides (e.g. accounts created on Shopee SG have `SG` as the value for this field. ISO 3166-2 Country Code

Min length2Max length2
metadataobject  

Object of additional information related to the customer. Define the JSON properties and values as required to pass information through the APIs. You can specify up to 50 keys, with key names up to 40 characters long and values up to 500 characters long. This is only for your use and will not be used by Xendit.

createdstring  (date-time)    

Customer creation timestamp

updatedstring  (date-time)    

Customer last update timestamp

409

Conflict

<select class='api-response-data' aria-label='Media type'><option value='5ffe5694-d87f-41cd-87ba-d01a235120d8'>application/json</option>
</select>object  error_codestring    Valid values[
  "DUPLICATE_ERROR",
  "IDEMPOTENCY_ERROR"
]
messagestring    
errors Array  OneOfstringstring
objectobject
