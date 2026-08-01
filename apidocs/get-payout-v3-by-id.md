> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Payout by ID

> Retrieve a specific created Payout with a given ID

## OpenAPI

````json GET /v3/payouts/{payout_id}
{
  "openapi": "3.0.0",
  "info": {
    "title": "Payouts",
    "version": "3.0.0",
    "description": "Payouts enables businesses to send funds to anyone, anywhere in the world faster through a single seamless and highly-customizable API."
  },
  "servers": [
    {
      "url": "https://api.xendit.co",
      "description": "Xendit API",
      "variables": {}
    }
  ],
  "security": [
    {
      "SecretApiKeyAuth": []
    }
  ],
  "tags": [
    {
      "name": "Payout"
    }
  ],
  "paths": {
    "/v3/payouts/{payout_id}": {
      "get": {
        "operationId": "Payouts_read",
        "summary": "Get Payout by ID",
        "description": "Retrieve a specific created Payout with a given ID",
        "parameters": [
          {
            "name": "api-version",
            "in": "header",
            "required": "false",
            "description": "The version of the API. Value: \"2025-09-01\"",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "payout_id",
            "in": "path",
            "required": "true",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "The request has succeeded.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Payout"
                },
                "examples": {
                  "Get Failed Payout": {
                    "summary": "Get Failed Payout",
                    "value": {
                      "payout_id": "po-b2c3d4e5-f6a7-8901-bcde-f23456789012",
                      "status": "FAILED",
                      "reference_id": "payout-ref-002",
                      "type": "B2C",
                      "source_currency": "PHP",
                      "source_amount": "50000",
                      "destination_currency": "PHP",
                      "destination_amount": "50000",
                      "sender": {
                        "type": "BUSINESS",
                        "business_name": "Acme Corp"
                      },
                      "recipient": {
                        "type": "INDIVIDUAL",
                        "given_name": "Maria",
                        "surname": "Santos",
                        "relationship": "CUSTOMER",
                        "details": {
                          "personal_mobile_number": "+639171234567"
                        },
                        "address": {
                          "country": "PH",
                          "street_line_1": "123 Rizal Avenue",
                          "city": "Manila",
                          "province_state": "Metro Manila",
                          "postal_code": "1000"
                        },
                        "account_details": {
                          "currency": "PHP",
                          "account_country": "PH",
                          "account_holder_name": "Maria Santos",
                          "account_number": "09171234567",
                          "routing_type_1": "WALLET",
                          "routing_value_1": "PH_GCASH"
                        }
                      },
                      "source_of_fund": "BUSINESS_REVENUE",
                      "purpose_code": "SALARY",
                      "description": "Freelancer payment",
                      "failure_code": "INVALID_DESTINATION",
                      "created": "2025-06-11T08:00:00Z",
                      "updated": "2025-06-11T08:01:30Z",
                      "business_id": "6018306aa16ad90cb3c43ba7"
                    }
                  },
                  "Get Payout by ID": {
                    "summary": "Get Payout by ID",
                    "value": {
                      "payout_id": "po-a1b2c3d4-e5f6-7890-abcd-ef1234567890",
                      "status": "SUCCEEDED",
                      "reference_id": "payout-ref-001",
                      "type": "B2C",
                      "source_currency": "IDR",
                      "source_amount": "1000000",
                      "destination_currency": "USD",
                      "destination_amount": "63",
                      "sender": {
                        "type": "BUSINESS",
                        "business_name": "Acme Corp"
                      },
                      "recipient": {
                        "type": "INDIVIDUAL",
                        "given_name": "John",
                        "surname": "Doe",
                        "relationship": "CUSTOMER",
                        "account_details": {
                          "currency": "USD",
                          "account_country": "US",
                          "account_holder_name": "John Doe",
                          "account_number": "1234567890",
                          "routing_type_1": "ABA",
                          "routing_value_1": "021000021"
                        }
                      },
                      "source_of_fund": "BUSINESS_REVENUE",
                      "purpose_code": "SALARY",
                      "description": "Monthly salary payment",
                      "created": "2025-06-10T10:30:00Z",
                      "updated": "2025-06-10T11:45:00Z",
                      "estimated_arrival_time": "2025-06-10T12:00:00Z",
                      "business_id": "6018306aa16ad90cb3c43ba7"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Http401InvalidApiKey"
                }
              }
            }
          },
          "403": {
            "description": "Forbidden",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Http403RequestForbiddenError"
                }
              }
            }
          },
          "404": {
            "description": "Not found",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Http404DataNotFound_Payout"
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Http500ServerError"
                }
              }
            }
          }
        },
        "tags": [
          "Payout"
        ]
      }
    }
  },
  "components": {
    "schemas": {
      "Payout": {
        "type": "object",
        "required": [
          "payout_id",
          "status",
          "reference_id",
          "type",
          "destination_currency",
          "destination_amount",
          "sender",
          "recipient",
          "created",
          "updated",
          "business_id"
        ],
        "properties": {
          "payout_id": {
            "type": "string",
            "description": "Unique payout id in UUID format, prefixed with po-"
          },
          "status": {
            "allOf": [
              {
                "$ref": "#/components/schemas/PayoutStatus"
              }
            ],
            "description": "Status of the payout. See [Payout Status Lifecycle](https://docs.xendit.co/docs/payout-status-lifecycle)"
          },
          "reference_id": {
            "type": "string",
            "description": "ID provided by merchant to identify the request"
          },
          "type": {
            "allOf": [
              {
                "$ref": "#/components/schemas/PayoutType"
              }
            ],
            "description": "Payout type"
          },
          "processor_reference": {
            "type": "string",
            "description": "Payout reference from Xendit's processor"
          },
          "source_currency": {
            "allOf": [
              {
                "$ref": "#/components/schemas/PayoutCurrency"
              }
            ],
            "description": "Origin currency of the Payout"
          },
          "source_amount": {
            "type": "integer",
            "description": "Origin amount of the Payout in minor units.\n\nA minor unit is the smallest unit of a currency. Most currencies have 2 decimals, others have 0.\nExamples: PHP 10.00 → `1000`, IDR 10 → `10`."
          },
          "destination_currency": {
            "allOf": [
              {
                "$ref": "#/components/schemas/PayoutCurrency"
              }
            ],
            "description": "Destination currency of the Payout"
          },
          "destination_amount": {
            "type": "integer",
            "description": "Destination amount of the Payout in minor units.\n\nA minor unit is the smallest unit of a currency. Most currencies have 2 decimals, others have 0.\nExamples: PHP 10.00 → `1000`, IDR 10 → `10`."
          },
          "sender": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Sender"
              }
            ],
            "description": "Contains sender information"
          },
          "recipient": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Recipient"
              }
            ],
            "description": "Contains recipient information"
          },
          "source_of_fund": {
            "allOf": [
              {
                "$ref": "#/components/schemas/SourceOfFund"
              }
            ],
            "description": "Source of fund of the payout"
          },
          "purpose_code": {
            "allOf": [
              {
                "$ref": "#/components/schemas/PurposeCode"
              }
            ],
            "description": "Purpose of the payout"
          },
          "description": {
            "type": "string",
            "maxLength": "100",
            "description": "Free text description shown in recipient's bank statement, if supported"
          },
          "receipt_notification": {
            "allOf": [
              {
                "$ref": "#/components/schemas/ReceiptNotification"
              }
            ],
            "description": "Configuration for sending payout receipt notifications via email"
          },
          "underlying_documents": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/UnderlyingDocument"
            },
            "description": "Underlying document attachments"
          },
          "created": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when the payout was made. Format: ISO 8601, UTC+0"
          },
          "updated": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when the payout was last updated. Format: ISO 8601, UTC+0"
          },
          "estimated_arrival_time": {
            "type": "string",
            "format": "date-time",
            "description": "Estimated time of arrival of funds in destination account. UTC+0"
          },
          "failure_code": {
            "allOf": [
              {
                "$ref": "#/components/schemas/FailureCode"
              }
            ],
            "description": "Failure reason of the Payout. See [Payout Status Lifecycle](https://docs.xendit.co/docs/payout-status-lifecycle)"
          },
          "business_id": {
            "type": "string",
            "description": "Your Xendit Business ID"
          },
          "metadata": {
            "type": "object",
            "additionalProperties": {},
            "description": "Object of additional information the merchant may use"
          }
        },
        "description": "Payout Object"
      },
      "Http401InvalidApiKey": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INVALID_API_KEY"
            ]
          },
          "message": {
            "type": "string",
            "enum": [
              "API key format is invalid"
            ]
          }
        }
      },
      "Http403RequestForbiddenError": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "REQUEST_FORBIDDEN_ERROR"
            ]
          },
          "message": {
            "type": "string",
            "enum": [
              "The API key is forbidden to perform this request"
            ]
          }
        }
      },
      "Http404DataNotFound_Payout": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "DATA_NOT_FOUND"
            ]
          },
          "message": {
            "type": "string",
            "enum": [
              "Payout not found"
            ]
          }
        }
      },
      "Http500ServerError": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "SERVER_ERROR"
            ]
          },
          "message": {
            "type": "string",
            "enum": [
              "An unexpected error occurred"
            ]
          }
        }
      },
      "PayoutStatus": {
        "type": "string",
        "enum": [
          "ACCEPTED",
          "PENDING_COMPLIANCE_REVIEW",
          "REJECTED",
          "ROUTING",
          "REQUESTED",
          "READY",
          "LOCKED",
          "EXPIRED",
          "FAILED",
          "SUCCEEDED",
          "CANCELLED",
          "REVERSED"
        ]
      },
      "PayoutType": {
        "type": "string",
        "enum": [
          "B2B",
          "B2C",
          "C2C",
          "C2B"
        ]
      },
      "PayoutCurrency": {
        "type": "string",
        "enum": [
          "USD",
          "SGD",
          "IDR",
          "PHP",
          "MYR",
          "THB",
          "VND",
          "HKD",
          "MXN",
          "CNY",
          "KRW",
          "AUD",
          "EUR"
        ]
      },
      "Sender": {
        "type": "object",
        "required": [
          "type"
        ],
        "properties": {
          "type": {
            "allOf": [
              {
                "$ref": "#/components/schemas/EntityType"
              }
            ],
            "description": "Entity type of the sender"
          },
          "business_name": {
            "type": "string",
            "maxLength": "50",
            "description": "Name of the business sender. Required if type is BUSINESS"
          },
          "given_name": {
            "type": "string",
            "maxLength": "50",
            "description": "First name of the sender. Required if type is INDIVIDUAL"
          },
          "surname": {
            "type": "string",
            "maxLength": "50",
            "description": "Last name of the sender. Required if type is INDIVIDUAL"
          },
          "given_name_non_roman": {
            "type": "string",
            "maxLength": "50",
            "description": "First non-roman name of the sender"
          },
          "surname_non_roman": {
            "type": "string",
            "maxLength": "50",
            "description": "Last non-roman name of the sender"
          },
          "details": {
            "allOf": [
              {
                "$ref": "#/components/schemas/SenderDetails"
              }
            ],
            "description": "Details of the sender"
          },
          "address": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Address"
              }
            ],
            "description": "Address details of the sender"
          }
        },
        "description": "Contains sender information. Only allowed for FIs (Financial Institutions)."
      },
      "Recipient": {
        "type": "object",
        "required": [
          "type",
          "relationship",
          "account_details",
          "address"
        ],
        "properties": {
          "type": {
            "allOf": [
              {
                "$ref": "#/components/schemas/EntityType"
              }
            ],
            "description": "Entity type of the recipient"
          },
          "business_name": {
            "type": "string",
            "maxLength": "50",
            "description": "Name of the business recipient. Required if type is BUSINESS"
          },
          "given_name": {
            "type": "string",
            "maxLength": "50",
            "description": "First name of the recipient. Required if type is INDIVIDUAL"
          },
          "surname": {
            "type": "string",
            "maxLength": "50",
            "description": "Last name of the recipient. Required if type is INDIVIDUAL"
          },
          "given_name_non_roman": {
            "type": "string",
            "maxLength": "50",
            "description": "First non-roman name of the recipient"
          },
          "surname_non_roman": {
            "type": "string",
            "maxLength": "50",
            "description": "Last non-roman name of the recipient"
          },
          "relationship": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Relationship"
              }
            ],
            "description": "Recipient's relationship to the sender in the context of the transaction"
          },
          "details": {
            "allOf": [
              {
                "$ref": "#/components/schemas/RecipientDetails"
              }
            ],
            "description": "Details of the recipient"
          },
          "account_details": {
            "allOf": [
              {
                "$ref": "#/components/schemas/RecipientAccountDetails"
              }
            ],
            "description": "Recipient's account details where the payment will be credited"
          },
          "address": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Address"
              }
            ],
            "description": "Address details of the recipient"
          }
        },
        "description": "Contains recipient information"
      },
      "SourceOfFund": {
        "type": "string",
        "enum": [
          "INVESTMENT",
          "PERSONAL_SAVINGS",
          "BUSINESS_REVENUE",
          "LEGACY",
          "BUSINESS_ARRANGEMENT",
          "LOAN",
          "SALARY",
          "OTHER"
        ]
      },
      "PurposeCode": {
        "type": "string",
        "enum": [
          "SELF",
          "FAMILY",
          "EDUCATION",
          "MEDICAL",
          "HOTEL",
          "TRAVEL",
          "UTILITIES",
          "LOAN_REPAYMENT",
          "TAX_PAYMENT",
          "RESIDENCE_PURCHASE",
          "RESIDENCE_RENT",
          "INSURANCE",
          "MUTUAL_FUND",
          "SHARES_INVESTMENT",
          "DONATION",
          "ADVERTISING",
          "ROYALTY_FEES",
          "BROKER_FEES",
          "ADVISORS",
          "OFFICE",
          "CONSTRUCTION",
          "SHIPMENT",
          "EXPORT",
          "DELIVERY",
          "TRADES",
          "SALARY",
          "REFUND",
          "OTHER"
        ]
      },
      "ReceiptNotification": {
        "type": "object",
        "required": [
          "email_to"
        ],
        "properties": {
          "email_to": {
            "type": "array",
            "items": {
              "type": "string",
              "format": "email"
            },
            "description": "List of email addresses to send the payout receipt to"
          },
          "email_cc": {
            "type": "array",
            "items": {
              "type": "string",
              "format": "email"
            },
            "description": "List of email addresses to CC on the payout receipt"
          },
          "email_bcc": {
            "type": "array",
            "items": {
              "type": "string",
              "format": "email"
            },
            "description": "List of email addresses to BCC on the payout receipt"
          }
        }
      },
      "UnderlyingDocument": {
        "type": "object",
        "properties": {
          "type": {
            "allOf": [
              {
                "$ref": "#/components/schemas/UnderlyingDocumentType"
              }
            ],
            "description": "Type of the document"
          },
          "reference_no": {
            "type": "string",
            "maxLength": "100",
            "description": "Reference number of the document"
          },
          "file_id": {
            "type": "string",
            "description": "File ID of the document"
          }
        }
      },
      "FailureCode": {
        "type": "string",
        "enum": [
          "INSUFFICIENT_BALANCE",
          "INVALID_DESTINATION",
          "DESTINATION_MAXIMUM_LIMIT",
          "ACCOUNT_NAME_MISMATCH",
          "REJECTED_BY_CHANNEL",
          "TEMPORARY_TRANSFER_ERROR",
          "TRANSFER_ERROR",
          "SLS_SENDER",
          "SLS_RECIPIENT"
        ]
      },
      "EntityType": {
        "type": "string",
        "enum": [
          "INDIVIDUAL",
          "BUSINESS"
        ]
      },
      "SenderDetails": {
        "type": "object",
        "properties": {
          "date_of_birth": {
            "type": "string",
            "format": "date",
            "description": "Date of birth"
          },
          "country_of_birth": {
            "type": "string",
            "description": "Country of birth. Format: ISO 3166-2 Country Code"
          },
          "nationality": {
            "type": "string",
            "description": "Nationality. Format: ISO 3166-2 Country Code"
          },
          "personal_id_type": {
            "allOf": [
              {
                "$ref": "#/components/schemas/PersonalIdType"
              }
            ],
            "description": "Personal ID type"
          },
          "personal_id_value": {
            "type": "string",
            "maxLength": "255",
            "description": "Personal ID value"
          },
          "personal_id_expiration_date": {
            "type": "string",
            "format": "date",
            "description": "Personal ID expiration date"
          },
          "personal_id_country": {
            "type": "string",
            "description": "Personal ID country of issuance. Format: ISO 3166-2 Country Code"
          },
          "personal_email": {
            "type": "string",
            "maxLength": "50",
            "format": "email",
            "description": "Personal email"
          },
          "personal_mobile_number": {
            "type": "string",
            "minLength": "7",
            "maxLength": "15",
            "description": "Personal mobile number. Supports E.164 international format and local formats"
          },
          "gender": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Gender"
              }
            ],
            "description": "Gender"
          },
          "occupation": {
            "type": "string",
            "maxLength": "50",
            "description": "Occupation"
          },
          "date_of_incorporation": {
            "type": "string",
            "format": "date",
            "description": "Date of incorporation of the business sender"
          },
          "registration_number": {
            "type": "string",
            "maxLength": "50",
            "description": "Registration number of the business sender"
          },
          "business_phone_number": {
            "type": "string",
            "minLength": "7",
            "maxLength": "15",
            "description": "Phone number of the business sender"
          },
          "nature_of_business": {
            "type": "string",
            "maxLength": "50",
            "description": "Nature of business"
          }
        }
      },
      "Address": {
        "type": "object",
        "properties": {
          "country": {
            "type": "string",
            "description": "Country. Format: ISO 3166-2 Country Code"
          },
          "province_state": {
            "type": "string",
            "maxLength": "255",
            "description": "Province, state or region"
          },
          "city": {
            "type": "string",
            "maxLength": "255",
            "description": "City, village or town"
          },
          "street_line_1": {
            "type": "string",
            "maxLength": "255",
            "description": "Line 1 of street address e.g., building name and apartment number"
          },
          "street_line_2": {
            "type": "string",
            "maxLength": "255",
            "description": "Line 2 of street address e.g., street number and name"
          },
          "postal_code": {
            "type": "string",
            "maxLength": "255",
            "description": "ZIP/Postal Code"
          }
        }
      },
      "Relationship": {
        "type": "string",
        "enum": [
          "BRANCH_REPRESENTATIVE_OFFICE",
          "BUSINESS_PARTNER",
          "CHILDREN",
          "CREDITOR",
          "CUSTOMER",
          "DEBTOR",
          "EMPLOYEE",
          "EX_SPOUSE",
          "FRANCHISEE_FRANCHISOR",
          "GRANDPARENTS",
          "HOLDING_COMPANY",
          "MAID",
          "OWNSELF",
          "PARENTS",
          "RELATIVE",
          "SIBLING",
          "SPOUSE",
          "SUBSIDIARY_COMPANY",
          "SUPPLIER",
          "FRIEND",
          "GOVERNMENT_BODY",
          "EDUCATION_INSTITUTION",
          "NON_GOVERNMENT_BODY",
          "OTHER"
        ]
      },
      "RecipientDetails": {
        "type": "object",
        "properties": {
          "date_of_birth": {
            "type": "string",
            "format": "date",
            "description": "Date of birth"
          },
          "country_of_birth": {
            "type": "string",
            "description": "Country of birth. Format: ISO 3166-2 Country Code"
          },
          "nationality": {
            "type": "string",
            "description": "Nationality. Format: ISO 3166-2 Country Code"
          },
          "personal_id_type": {
            "allOf": [
              {
                "$ref": "#/components/schemas/PersonalIdType"
              }
            ],
            "description": "Personal ID type"
          },
          "personal_id_value": {
            "type": "string",
            "maxLength": "255",
            "description": "Personal ID value"
          },
          "personal_id_expiration_date": {
            "type": "string",
            "format": "date",
            "description": "Personal ID expiration date"
          },
          "personal_id_country": {
            "type": "string",
            "description": "Personal ID country of issuance. Format: ISO 3166-2 Country Code"
          },
          "personal_email": {
            "type": "string",
            "maxLength": "50",
            "format": "email",
            "description": "Personal email"
          },
          "personal_mobile_number": {
            "type": "string",
            "minLength": "7",
            "maxLength": "15",
            "description": "Personal mobile number. Supports E.164 international format and local formats"
          },
          "gender": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Gender"
              }
            ],
            "description": "Gender"
          },
          "occupation": {
            "type": "string",
            "maxLength": "50",
            "description": "Occupation"
          },
          "date_of_incorporation": {
            "type": "string",
            "format": "date",
            "description": "Date of incorporation of the business recipient"
          },
          "registration_number": {
            "type": "string",
            "maxLength": "50",
            "description": "Registration number of the business recipient"
          },
          "business_phone_number": {
            "type": "string",
            "minLength": "7",
            "maxLength": "15",
            "description": "Phone number of the business recipient"
          },
          "nature_of_business": {
            "type": "string",
            "maxLength": "50",
            "description": "Nature of business"
          }
        }
      },
      "RecipientAccountDetails": {
        "type": "object",
        "required": [
          "currency",
          "account_country",
          "account_holder_name",
          "account_number",
          "routing_type_1",
          "routing_value_1"
        ],
        "properties": {
          "currency": {
            "type": "string",
            "description": "Currency of the account. Format: ISO 4217 Currency Code"
          },
          "account_country": {
            "type": "string",
            "description": "Account country code. Format: ISO 3166-2 Country Code"
          },
          "account_holder_name": {
            "type": "string",
            "maxLength": "255",
            "description": "Account name of the recipient's account"
          },
          "account_number": {
            "type": "string",
            "description": "Account number"
          },
          "routing_type_1": {
            "allOf": [
              {
                "$ref": "#/components/schemas/RoutingType1"
              }
            ],
            "description": "Routing code type"
          },
          "routing_value_1": {
            "type": "string",
            "description": "Routing type value"
          },
          "routing_type_2": {
            "type": "string",
            "description": "Routing code subtype (reserved for future supported corridors)"
          },
          "routing_value_2": {
            "type": "string",
            "description": "Routing subtype value"
          },
          "account_type": {
            "allOf": [
              {
                "$ref": "#/components/schemas/AccountType"
              }
            ],
            "description": "Account type"
          }
        }
      },
      "UnderlyingDocumentType": {
        "type": "string",
        "enum": [
          "INVOICE",
          "PURCHASE_ORDER",
          "CONTRACT",
          "DELIVERY_SLIP",
          "CUSTOMS_DECLARATION",
          "BILL_OF_LADING",
          "OTHERS"
        ]
      },
      "PersonalIdType": {
        "type": "string",
        "enum": [
          "BIRTH_CERTIFICATE",
          "BANK_STATEMENT",
          "DRIVING_LICENSE",
          "IDENTITY_CARD",
          "PASSPORT",
          "VISA",
          "BUSINESS_REGISTRATION",
          "BUSINESS_LICENSE"
        ]
      },
      "Gender": {
        "type": "string",
        "enum": [
          "MALE",
          "FEMALE",
          "OTHER"
        ]
      },
      "RoutingType1": {
        "type": "string",
        "enum": [
          "SWIFT",
          "IBAN",
          "SORT_CODE",
          "ABA",
          "BSB",
          "WALLET",
          "CLABE",
          "MOBILE_NO",
          "BUSINESS_REG_NO",
          "NATIONAL_ID"
        ]
      },
      "AccountType": {
        "type": "string",
        "enum": [
          "CHECKING",
          "SAVINGS"
        ]
      }
    },
    "securitySchemes": {
      "SecretApiKeyAuth": {
        "type": "http",
        "scheme": "Basic",
        "description": "Secret API Key authentication. Required permission: MONEY-OUT"
      }
    }
  }
}
````

