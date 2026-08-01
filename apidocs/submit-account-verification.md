---
title: "Submit account verification"
slug: "submit-account-verification"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/submit-account-verification"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Submit account verification

Post/account_verification

Submits a sub-account's information for KYC verification. This lets you collect your merchant's verification data on your Platform's own interface and pass it to Xendit via API.

You may use this API for `OWNED` sub-accounts created with the `/v2/accounts` API, or for sub-accounts created in the Dashboard. Upload the referenced documents with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`) first, then reference them by `file_id`.

Include the `for-user-id` header with the sub-account's business ID to submit verification on its behalf.

Required fields, accepted document types, address fields and identification types vary by country of incorporation and entity type.

SecurityHTTPType basic

Header parametersfor-user-idstringRequired

The business ID of the sub-account to submit or retrieve verification for

Body parameters<select class='api-response-data' aria-label='Media type'><option value='62e118f6-83cc-4052-ae96-b7ddd0009fbd'>application/json</option>
</select>Expand Allobject  country_of_incorporationstring    Required

ISO 3166-1 alpha-2 country code of incorporation

ExampleHK
business_entity_typestring    Required

Business entity type, e.g. `CORPORATION` or `PARTNERSHIP`. Availability is country-specific.

ExampleCORPORATION
business_industry_codestring    Required

One of the accepted industry category codes for the country of incorporation

ExampleACCOUNTING_AUDITING_AND_BOOKKEEPING_SERVICES
kyc_detailsobject (AccountVerificationKycDetails)  Required

The KYC information of the business. Required fields, accepted document types and identification types vary by country of incorporation and entity type.

business_legal_namestring    Required
business_descriptionstring    Required
business_registration_numberstring    Required
business_tax_numberstring    

Indonesia only

business_establishment_datestring    Required

Format `YYYY-MM-DD`

business_average_monthly_basket_sizestring    RequiredExample$50K - $300K
business_intents Array of string   Requiredstring    Valid values[
  "PAYMENTS",
  "PAYOUT",
  "GLOBAL_PAYOUT",
  "BUSINESS_EXPENSES"
]
business_source_of_funds Array of string   Requiredstring    Valid values[
  "REVENUE",
  "INVESTOR_SHAREHOLDER_FUNDING",
  "INVESTMENT_INCOME",
  "BUSINESS_LOAN",
  "PERSONAL_FUNDING",
  "DONATIONS",
  "GRANTS",
  "OTHER"
]
business_registration_documents_amendedboolean    

Indonesia only

business_addressobject (AccountVerificationAddress)  Requiredstreet_line_1string    Required
street_line_2string    
citystring    Required
districtstring    

Required for ID, TH, VN

sub_districtstring    

Required for ID, TH

provincestring    

Required for ID, TH, PH, VN

statestring    

Required for PH, MY

wardstring    

Required for VN

postal_codestring    Required
country_codestring    Required

ISO 3166-1 alpha-2 country code

legal_entity_addressobject (AccountVerificationAddress)  Requiredstreet_line_1string    Required
street_line_2string    
citystring    Required
districtstring    

Required for ID, TH, VN

sub_districtstring    

Required for ID, TH

provincestring    

Required for ID, TH, PH, VN

statestring    

Required for PH, MY

wardstring    

Required for VN

postal_codestring    Required
country_codestring    Required

ISO 3166-1 alpha-2 country code

office_store_address_proof_documentobject  Required

Proof of the business's operating address. Required only when `business_address` differs from `legal_entity_address`. If the two addresses are the same, this document is not needed.

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

proof_of_business_websitesobject  

At least one of `proof_of_business_websites` or `proof_of_business_documents` must be provided.

websitestring    
website_staging_urlstring    
website_staging_usernamestring    
website_staging_passwordstring    
social_instagram_urlstring    
social_facebook_urlstring    
social_others_urlstring    
marketplace_urlstring    

proof_of_business_documents Array of object   

At least one of `proof_of_business_websites` or `proof_of_business_documents` must be provided.

object  file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603
typestring    Valid values[
  "POSTER_BROCHURE_PAMPHLET_DOCUMENT",
  "INVOICE_PURCHASE_ORDER_DOCUMENT",
  "OFFLINE_STORE_PHOTO_DOCUMENT",
  "OTHER_DOCUMENT"
]

business_registration_documents Array of object   Requiredobject  file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603
typestring    

Country-specific document type, e.g. `HK_CI`, `HK_NAR1`, `ID_NIB`, `ID_COMPANY_NPWP`, `ID_AKTA`, `ID_SKMENKEH`

business_license_documents Array of object (AccountVerificationFile)   Requiredobject  

A document uploaded with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`)

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

business_bank_account_documentobject  

A copy of the business bank account book or statement. Requirement varies by country of incorporation — optional for TH.

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

business_shareholding_chart_documentobject  Required

A chart of the business's shareholding structure. Only applies to corporate entity types (e.g. corporation, limited company, joint stock company). Required when `shareholders_include_corporate_entity` is `true`.

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

service_agreement_documentobject  

Signed service agreement. Optional — this is normally generated through the consent flow, but you may also provide it directly via this API.

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

business_bank_account_numberstring    

Indonesia only

business_bank_channel_codestring    

Indonesia only

business_bank_namestring    

Indonesia only

authorized_person_first_namestring    Required
authorized_person_last_namestring    Required
authorized_person_genderstring    RequiredExampleM
authorized_person_nationalitystring    Required

ISO 3166-1 alpha-2 country code

authorized_person_date_of_birthstring    Required

Format `YYYY-MM-DD`

authorized_person_rolestring    RequiredExampleFOUNDER
authorized_person_mobile_country_codestring    RequiredExample+852
authorized_person_mobile_number_onlystring    Required
authorized_person_email_addressstring    Required
authorized_person_addressobject (AccountVerificationAddress)  Requiredstreet_line_1string    Required
street_line_2string    
citystring    Required
districtstring    

Required for ID, TH, VN

sub_districtstring    

Required for ID, TH

provincestring    

Required for ID, TH, PH, VN

statestring    

Required for PH, MY

wardstring    

Required for VN

postal_codestring    Required
country_codestring    Required

ISO 3166-1 alpha-2 country code

authorized_person_selfie_documentobject (AccountVerificationFile)  Required

A document uploaded with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`)

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

authorized_person_identification Array of object (AccountVerificationIdentification)   Requiredobject  typestring    Required

Country-specific identification type, e.g. `PASSPORT`, `HK_NATIONAL_ID`, `ID_NATIONAL_ID_KTP`

numberstring    Required
document_frontobject (AccountVerificationFile)  Required

A document uploaded with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`)

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

document_backobject (AccountVerificationFile)  Required

A document uploaded with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`)

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

authorized_person_proof_of_residency_documentobject  

Proof of the authorized person's residential address. Required when the submitted `authorized_person_identification` document does not itself contain a residential address (e.g. a passport or Hong Kong ID).

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

authorized_person_board_resolution_documentobject  

Board resolution proving the authorized person is empowered to act for the business. Applies to corporation-type entities (e.g. SG/HK/ID corporation, TH limited company, VN joint stock company).

Required unless the authorized person is declared in `stakeholders` (with `is_authorized_person: true`) holding the `BOARD_DIRECTOR` role — in that case the document is not needed.

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

authorized_person_letter_of_authorization_documentobject  

Letter of authorization proving the authorized person is empowered to act for the business.

Required unless the authorized person is declared in `stakeholders` (with `is_authorized_person: true`) holding the governing role for the entity type. The role that waives this document depends on the entity type:

- Partnerships — `LEGAL_PARTNER`
- Sole proprietorships — `BUSINESS_OWNER`
- Mexico entities — `AUTHORIZED_SIGNATORY`
- Indonesia non-profit, Malaysia private limited — `BOARD_DIRECTOR`

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

contact_person_first_namestring    Required
contact_person_last_namestring    Required
contact_person_mobile_country_codestring    Required
contact_person_mobile_number_onlystring    Required
contact_person_email_addressstring    Required
stakeholders Array of object (AccountVerificationStakeholder)   Requiredobject  roles Array of string   Required

The stakeholder's role(s) in the business. When a stakeholder is the authorized person (`is_authorized_person: true`), their roles determine whether the `authorized_person_board_resolution_document` or `authorized_person_letter_of_authorization_document` is required — declaring the governing role for the entity type (e.g. `BOARD_DIRECTOR`, `LEGAL_PARTNER`, `BUSINESS_OWNER`, `AUTHORIZED_SIGNATORY`) waives that document.

string    Valid values[
  "BOARD_DIRECTOR",
  "BUSINESS_OWNER",
  "LEGAL_PARTNER",
  "AUTHORIZED_SIGNATORY"
]
first_namestring    Required
last_namestring    Required
nationalitystring    Required

ISO 3166-1 alpha-2 country code

date_of_birthstring    Required

Format `YYYY-MM-DD`

addressobject (AccountVerificationAddress)  Requiredstreet_line_1string    Required
street_line_2string    
citystring    Required
districtstring    

Required for ID, TH, VN

sub_districtstring    

Required for ID, TH

provincestring    

Required for ID, TH, PH, VN

statestring    

Required for PH, MY

wardstring    

Required for VN

postal_codestring    Required
country_codestring    Required

ISO 3166-1 alpha-2 country code

is_authorized_personboolean    Defaultfalse
identification Array of object (AccountVerificationIdentification)   Requiredobject  typestring    Required

Country-specific identification type, e.g. `PASSPORT`, `HK_NATIONAL_ID`, `ID_NATIONAL_ID_KTP`

numberstring    Required
document_frontobject (AccountVerificationFile)  Required

A document uploaded with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`)

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

document_backobject (AccountVerificationFile)  Required

A document uploaded with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`)

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

proof_of_residency_documentobject  

Proof of the stakeholder's residential address. Required when the stakeholder's `identification` document does not itself contain a residential address (e.g. a passport or Hong Kong ID).

file_namestring    RequiredExampleCertificate of Incorporation.pdf
file_idstring    RequiredExamplefile-c7bdf24b-738d-4c47-a919-55479daf7603

shareholders_include_corporate_entityboolean    Required

Whether any of the business's shareholders is a corporate entity (rather than an individual). When `true`, `business_shareholding_chart_document` is required.

third_party_verifications Array of object (AccountVerificationThirdParty)   

Results of verifications you have already performed through third parties

object  typestring    RequiredValid values[
  "SANCTION_SCREENING",
  "GOVT_DATABASE",
  "LIVENESS_VERIFICATION"
]
datestring    Required

Date the verification was performed, format `YYYY-MM-DD`

resultobject  Required

Free-form JSON object documenting the verification outcome

Responses200

Verification request created. Returns the KYC request with its current status.

<select class='api-response-data' aria-label='Media type'><option value='f46cd2b4-d283-4b8a-9400-5c4b35a73e9f'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='d40349ea-f55e-430b-85ff-3d6c5b935058'>Submitted</option>
</select>Submitted

```json
{
  "id": "kyc-request-id-12345",
  "status": "PENDING_VERIFICATION",
  "business_id": "sub-account-business-id",
  "country_of_incorporation": "HK",
  "business_entity_type": "CORPORATION"
}
```

Expand Allobject  idstring    

Unique ID of the KYC request

Examplekyc-request-id-12345
statusstring    

The KYC verification status of the sub-account

Valid values[
  "PENDING_VERIFICATION",
  "VERIFICATION_IN_PROGRESS",
  "AWAITING_RESUBMISSION",
  "PASSED",
  "FAILED"
]
business_idstring    

Business ID of the sub-account

country_of_incorporationstring    
business_entity_typestring    
kyc_detailsobject (AccountVerificationKycDetails)  

The KYC information of the business. Required fields, accepted document types and identification types vary by country of incorporation and entity type.

business_legal_namestring    
business_descriptionstring    
business_registration_numberstring    
business_tax_numberstring    

Indonesia only

business_establishment_datestring    

Format `YYYY-MM-DD`

business_average_monthly_basket_sizestring    Example$50K - $300K
business_intents Array of string   string    Valid values[
  "PAYMENTS",
  "PAYOUT",
  "GLOBAL_PAYOUT",
  "BUSINESS_EXPENSES"
]
business_source_of_funds Array of string   string    Valid values[
  "REVENUE",
  "INVESTOR_SHAREHOLDER_FUNDING",
  "INVESTMENT_INCOME",
  "BUSINESS_LOAN",
  "PERSONAL_FUNDING",
  "DONATIONS",
  "GRANTS",
  "OTHER"
]
business_registration_documents_amendedboolean    

Indonesia only

business_addressobject (AccountVerificationAddress)  street_line_1string    
street_line_2string    
citystring    
districtstring    

Required for ID, TH, VN

sub_districtstring    

Required for ID, TH

provincestring    

Required for ID, TH, PH, VN

statestring    

Required for PH, MY

wardstring    

Required for VN

postal_codestring    
country_codestring    

ISO 3166-1 alpha-2 country code

legal_entity_addressobject (AccountVerificationAddress)  street_line_1string    
street_line_2string    
citystring    
districtstring    

Required for ID, TH, VN

sub_districtstring    

Required for ID, TH

provincestring    

Required for ID, TH, PH, VN

statestring    

Required for PH, MY

wardstring    

Required for VN

postal_codestring    
country_codestring    

ISO 3166-1 alpha-2 country code

office_store_address_proof_documentobject  

Proof of the business's operating address. Required only when `business_address` differs from `legal_entity_address`. If the two addresses are the same, this document is not needed.

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

proof_of_business_websitesobject  

At least one of `proof_of_business_websites` or `proof_of_business_documents` must be provided.

websitestring    
website_staging_urlstring    
website_staging_usernamestring    
website_staging_passwordstring    
social_instagram_urlstring    
social_facebook_urlstring    
social_others_urlstring    
marketplace_urlstring    

proof_of_business_documents Array of object   

At least one of `proof_of_business_websites` or `proof_of_business_documents` must be provided.

object  file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603
typestring    Valid values[
  "POSTER_BROCHURE_PAMPHLET_DOCUMENT",
  "INVOICE_PURCHASE_ORDER_DOCUMENT",
  "OFFLINE_STORE_PHOTO_DOCUMENT",
  "OTHER_DOCUMENT"
]

business_registration_documents Array of object   object  file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603
typestring    

Country-specific document type, e.g. `HK_CI`, `HK_NAR1`, `ID_NIB`, `ID_COMPANY_NPWP`, `ID_AKTA`, `ID_SKMENKEH`

business_license_documents Array of object (AccountVerificationFile)   object  

A document uploaded with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`)

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

business_bank_account_documentobject  

A copy of the business bank account book or statement. Requirement varies by country of incorporation — optional for TH.

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

business_shareholding_chart_documentobject  

A chart of the business's shareholding structure. Only applies to corporate entity types (e.g. corporation, limited company, joint stock company). Required when `shareholders_include_corporate_entity` is `true`.

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

service_agreement_documentobject  

Signed service agreement. Optional — this is normally generated through the consent flow, but you may also provide it directly via this API.

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

business_bank_account_numberstring    

Indonesia only

business_bank_channel_codestring    

Indonesia only

business_bank_namestring    

Indonesia only

authorized_person_first_namestring    
authorized_person_last_namestring    
authorized_person_genderstring    ExampleM
authorized_person_nationalitystring    

ISO 3166-1 alpha-2 country code

authorized_person_date_of_birthstring    

Format `YYYY-MM-DD`

authorized_person_rolestring    ExampleFOUNDER
authorized_person_mobile_country_codestring    Example+852
authorized_person_mobile_number_onlystring    
authorized_person_email_addressstring    
authorized_person_addressobject (AccountVerificationAddress)  street_line_1string    
street_line_2string    
citystring    
districtstring    

Required for ID, TH, VN

sub_districtstring    

Required for ID, TH

provincestring    

Required for ID, TH, PH, VN

statestring    

Required for PH, MY

wardstring    

Required for VN

postal_codestring    
country_codestring    

ISO 3166-1 alpha-2 country code

authorized_person_selfie_documentobject (AccountVerificationFile)  

A document uploaded with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`)

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

authorized_person_identification Array of object (AccountVerificationIdentification)   object  typestring    

Country-specific identification type, e.g. `PASSPORT`, `HK_NATIONAL_ID`, `ID_NATIONAL_ID_KTP`

numberstring    
document_frontobject (AccountVerificationFile)  

A document uploaded with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`)

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

document_backobject (AccountVerificationFile)  

A document uploaded with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`)

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

authorized_person_proof_of_residency_documentobject  

Proof of the authorized person's residential address. Required when the submitted `authorized_person_identification` document does not itself contain a residential address (e.g. a passport or Hong Kong ID).

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

authorized_person_board_resolution_documentobject  

Board resolution proving the authorized person is empowered to act for the business. Applies to corporation-type entities (e.g. SG/HK/ID corporation, TH limited company, VN joint stock company).

Required unless the authorized person is declared in `stakeholders` (with `is_authorized_person: true`) holding the `BOARD_DIRECTOR` role — in that case the document is not needed.

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

authorized_person_letter_of_authorization_documentobject  

Letter of authorization proving the authorized person is empowered to act for the business.

Required unless the authorized person is declared in `stakeholders` (with `is_authorized_person: true`) holding the governing role for the entity type. The role that waives this document depends on the entity type:

- Partnerships — `LEGAL_PARTNER`
- Sole proprietorships — `BUSINESS_OWNER`
- Mexico entities — `AUTHORIZED_SIGNATORY`
- Indonesia non-profit, Malaysia private limited — `BOARD_DIRECTOR`

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

contact_person_first_namestring    
contact_person_last_namestring    
contact_person_mobile_country_codestring    
contact_person_mobile_number_onlystring    
contact_person_email_addressstring    
stakeholders Array of object (AccountVerificationStakeholder)   object  roles Array of string   

The stakeholder's role(s) in the business. When a stakeholder is the authorized person (`is_authorized_person: true`), their roles determine whether the `authorized_person_board_resolution_document` or `authorized_person_letter_of_authorization_document` is required — declaring the governing role for the entity type (e.g. `BOARD_DIRECTOR`, `LEGAL_PARTNER`, `BUSINESS_OWNER`, `AUTHORIZED_SIGNATORY`) waives that document.

string    Valid values[
  "BOARD_DIRECTOR",
  "BUSINESS_OWNER",
  "LEGAL_PARTNER",
  "AUTHORIZED_SIGNATORY"
]
first_namestring    
last_namestring    
nationalitystring    

ISO 3166-1 alpha-2 country code

date_of_birthstring    

Format `YYYY-MM-DD`

addressobject (AccountVerificationAddress)  street_line_1string    
street_line_2string    
citystring    
districtstring    

Required for ID, TH, VN

sub_districtstring    

Required for ID, TH

provincestring    

Required for ID, TH, PH, VN

statestring    

Required for PH, MY

wardstring    

Required for VN

postal_codestring    
country_codestring    

ISO 3166-1 alpha-2 country code

is_authorized_personboolean    Defaultfalse
identification Array of object (AccountVerificationIdentification)   object  typestring    

Country-specific identification type, e.g. `PASSPORT`, `HK_NATIONAL_ID`, `ID_NATIONAL_ID_KTP`

numberstring    
document_frontobject (AccountVerificationFile)  

A document uploaded with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`)

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

document_backobject (AccountVerificationFile)  

A document uploaded with the Upload File API (`POST /files`, purpose `KYC_DOCUMENT`)

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

proof_of_residency_documentobject  

Proof of the stakeholder's residential address. Required when the stakeholder's `identification` document does not itself contain a residential address (e.g. a passport or Hong Kong ID).

file_namestring    ExampleCertificate of Incorporation.pdf
file_idstring    Examplefile-c7bdf24b-738d-4c47-a919-55479daf7603

shareholders_include_corporate_entityboolean    

Whether any of the business's shareholders is a corporate entity (rather than an individual). When `true`, `business_shareholding_chart_document` is required.

400

| Error code | Description |
| --- | --- |
| `INVALID_DATA_SUBMITTED` | A field value is invalid or a required field is missing for the given country and entity type |

<select class='api-response-data' aria-label='Media type'><option value='6b6c5028-0f91-472b-b8a9-a8c6192b3d48'>application/json</option>
</select>object  error_codestring    
messagestring    

401

| Error code | Description |
| --- | --- |
| `INVALID_API_KEY` | The API key is missing or invalid |

<select class='api-response-data' aria-label='Media type'><option value='69e73021-790c-4c3f-94e2-21fe107f6415'>application/json</option>
</select>object  error_codestring    
messagestring    

403

| Error code | Description |
| --- | --- |
| `REQUEST_FORBIDDEN_ERROR` | The API key does not have permission to perform this request |

<select class='api-response-data' aria-label='Media type'><option value='32a016b1-98b8-4c1d-9f53-683c797da694'>application/json</option>
</select>object  error_codestring    
messagestring    

404

| Error code | Description |
| --- | --- |
| `XEN_PLATFORM_SUB_ACCOUNT_NOT_LIVE` | The sub-account referenced by `for-user-id` does not exist or is not live |

<select class='api-response-data' aria-label='Media type'><option value='cb50a9a7-e47b-4383-aa8e-beeb15563882'>application/json</option>
</select>object  error_codestring    
messagestring    

500

| Error code | Description |
| --- | --- |
| `SERVER_ERROR` | An unexpected error occurred — retry or contact support |

<select class='api-response-data' aria-label='Media type'><option value='824bd2db-b076-4491-8d15-87903819af04'>application/json</option>
</select>object  error_codestring    
messagestring
