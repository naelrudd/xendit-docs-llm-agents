---
title: "Retrieve account verification"
slug: "retrieve-account-verification"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/retrieve-account-verification"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve account verification

Get/account_verification

Retrieves the KYC verification request and current verification status of a sub-account. Include the `for-user-id` header with the sub-account's business ID.

SecurityHTTPType basic

Header parametersfor-user-idstringRequired

The business ID of the sub-account to submit or retrieve verification for

Responses200

The sub-account's verification request and status.

<select class='api-response-data' aria-label='Media type'><option value='5bfeb634-0495-4544-956c-3d6ac05c6e84'>application/json</option>
</select>Expand Allobject  idstring    

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

401

Invalid API key

<select class='api-response-data' aria-label='Media type'><option value='f9b1dd37-9b87-4f74-a700-48944e6c4cd5'>application/json</option>
</select>object  error_codestring    
messagestring    

404

No verification request found for the sub-account

<select class='api-response-data' aria-label='Media type'><option value='5ebb7722-2ec1-423e-bbe3-4013420d97d3'>application/json</option>
</select>object  error_codestring    
messagestring
