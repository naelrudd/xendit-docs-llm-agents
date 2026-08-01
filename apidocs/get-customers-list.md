---
title: "Get customers list"
slug: "get-customers-list"
updated: 2026-04-01T03:43:19Z
published: 2026-04-01T03:43:19Z
canonical: "docs.xendit.co/get-customers-list"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Get customers list

Get/customers

Retrieves an array with a customer object that matches the provided reference_id - the identifier provided by you

The Customer Object is a standard data structure to hold information relating to one of your customers. It has the following major components:

- A Type of customer (Individual or Business)
- Basic descriptive details of that customer
- Addresses of the customer
- Identity accounts and KYC documents to prove the legitimacy of the customer
- Other metadata

SecurityHTTPType Basic

Header parametersapi-versionstring

API version in date semantic. Attach this parameter when calling a specific API version. List of API versions can be found here.

Valid values[
  "2020-10-31",
  "2020-05-19"
]
for-user-idstring

The sub-account user-id that you want to make this transaction for.

This header is only used if you have access to xenPlatform. See xenPlatform for more information

Query parametersreference_idstringRequired

Your identifier for the customer

Min length1Max length255

Responses200

Successful operation

<select class='api-response-data' aria-label='Media type'><option value='d460b732-2718-4252-be59-676ea668e9de'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='004728d2-29e8-49a7-a111-5c3ea391a3a6'>getCustomerByReferenceId</option>
</select>getCustomerByReferenceId

```json
{
  "data": [
    {
      "id": "cust-239c16f4-866d-43e8-9341-7badafbc019f",
      "reference_id": "demo_1475801962607",
      "type": "INDIVIDUAL",
      "individual_detail": {
        "given_names": "John",
        "surname": "Doe",
        "nationality": null,
        "place_of_birth": null,
        "date_of_birth": null,
        "gender": "MALE",
        "employment": null
      },
      "email": "customer@website.com",
      "mobile_number": null,
      "phone_number": null,
      "hashed_phone_number": null,
      "addresses": [],
      "identity_accounts": [],
      "kyc_documents": [],
      "description": null,
      "metadata": {},
      "created": "2020-03-30T06:12:47.212Z",
      "updated": "2020-03-30T06:12:47.212Z"
    }
  ],
  "has_more": false
}
```

Expand Allobject  

List of customer object

data Array of object (CustomerObject)   object  

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

has_moreboolean    

404

The provided `id` does not exist. Please review the `id` and try again

<select class='api-response-data' aria-label='Media type'><option value='db524d8c-3a5d-480e-9289-80ab03511920'>application/json</option>
</select>object  error_codestring    Valid values[
  "RATE_LIMIT_EXCEEDED"
]
messagestring    
errors Array  OneOfstringstring
objectobject
