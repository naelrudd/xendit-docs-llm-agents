> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Update a payment request

> Update payment request only allowed for VA channel. Update can only be done on the payment request with status REQUIRES_ACTION and ACCEPTING_PAYMENTS


## OpenAPI

````json PATCH /v3/payment_requests/{payment_request_id}
{
  "openapi": "3.0.0",
  "info": {
    "title": "Payments",
    "version": "3.0.0",
    "description": "Payments API enables businesses to integrate seamless and secure payment processing into their platforms, \nsupporting key features like a customizable checkout page for user-friendly payment experiences, \ndirect payments through API for tailored and flexible transaction flows, \nand recurring subscriptions to automate billing for memberships or SaaS. \nThese APIs streamline payment processing by supporting multiple payment channels, \nensuring PCI compliance, and offering features like tokenization, real-time transactions, \nand automated retries for subscription payments, making them essential for modern, scalable businesses.\n"
  },
  "servers": [
    {
      "url": "https://api.xendit.co",
      "description": "Xendit API"
    }
  ],
  "tags": [
    {
      "name": "Payment Request",
      "x-displayName": "Payment Request"
    },
    {
      "name": "Refund",
      "x-displayName": "Refund"
    },
    {
      "name": "Payment",
      "x-displayName": "Payment"
    },
    {
      "name": "Payment Token",
      "x-displayName": "Payment Token"
    },
    {
      "name": "Subscriptions",
      "description": "Manage recurring plans and cycles",
      "x-displayName": "Subscriptions"
    },
    {
      "name": "Session",
      "x-displayName": "Session"
    },
    {
      "name": "Disputes",
      "description": "Core dispute management endpoints",
      "x-displayName": "Disputes"
    }
  ],
  "paths": {
    "/v3/payment_requests/{payment_request_id}": {
      "patch": {
        "security": [
          {
            "Payments_API_BasicAuth": []
          }
        ],
        "operationId": "UpdatePaymentRequest",
        "summary": "Update a payment request",
        "description": "Update payment request only allowed for VA channel. Update can only be done on the payment request with status REQUIRES_ACTION and ACCEPTING_PAYMENTS\n",
        "tags": [
          "Payment Request"
        ],
        "parameters": [
          {
            "$ref": "#/components/parameters/Payments_API_APIVersionHeaderExternal"
          },
          {
            "$ref": "#/components/parameters/Payments_API_PaymentRequestIdPathParam"
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/Payments_API_UpdatePaymentRequestSchema"
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Update a Payment Request",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Payments_API_PaymentRequestPublicSchema"
                },
                "examples": {
                  "updatePaymentResponsePresentToCustomer": {
                    "value": {
                      "business_id": "5f27a14a9bf05c73dd040bc8",
                      "reference_id": "90392f42-d98a-49ef-a7f3-abcezas123",
                      "payment_request_id": "pr-90392f42-d98a-49ef-a7f3-abcezas123",
                      "customer_id": "cust-90392f42-d98a-49ef-a7f3-abcezas123",
                      "type": "REUSABLE_PAYMENT_CODE",
                      "country": "ID",
                      "currency": "IDR",
                      "request_amount": 10000,
                      "capture_method": "AUTOMATIC",
                      "channel_code": "BRI_VIRTUAL_ACCOUNT",
                      "channel_properties": {
                        "expires_at": "2026-09-24T03:15:18Z",
                        "display_name": "xenCommerce Shop"
                      },
                      "actions": [
                        {
                          "type": "PRESENT_TO_CUSTOMER",
                          "descriptor": "VIRTUAL_ACCOUNT_NUMBER",
                          "value": "1251255"
                        }
                      ],
                      "status": "ACCEPTING_PAYMENTS",
                      "description": "Payment for your order #123",
                      "metadata": {
                        "invoice_id": "INV-2025-001",
                        "customer_type": "business"
                      },
                      "created": "2021-12-31T23:59:59Z",
                      "updated": "2021-12-31T23:59:59Z"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Bad request",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400InactivePaymentRequest"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400InvalidValueError"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400ApiValidationError"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400TemporarilyUnavailable"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400IneligibleTransactionStatus"
                    }
                  ]
                }
              }
            }
          },
          "404": {
            "description": "Not found",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/Payments_API_Http404DataNotFound"
                    }
                  ]
                }
              }
            }
          },
          "409": {
            "description": "Conflict",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/Payments_API_Http409DuplicateError"
                    }
                  ]
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/Payments_API_Http500ServerError"
                    }
                  ]
                }
              }
            }
          },
          "503": {
            "description": "Service unavailable",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/Payments_API_Http503ChannelUnavailable"
                    }
                  ]
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "parameters": {
      "Payments_API_APIVersionHeaderExternal": {
        "in": "header",
        "name": "api-version",
        "schema": {
          "example": "2024-11-11",
          "type": "string",
          "enum": [
            "2024-11-11"
          ]
        }
      },
      "Payments_API_PaymentRequestIdPathParam": {
        "in": "path",
        "name": "payment_request_id",
        "required": true,
        "schema": {
          "type": "string",
          "minLength": 39,
          "maxLength": 39
        },
        "example": "pr-8877c08a-740d-4153-9816-3d744ed197a5"
      }
    },
    "schemas": {
      "Payments_API_UpdatePaymentRequestSchema": {
        "type": "object",
        "properties": {
          "channel_properties": {
            "$ref": "#/components/schemas/Payments_API_PRPatchRequestChannelProperties"
          },
          "description": {
            "$ref": "#/components/schemas/Payments_API_Description"
          },
          "request_amount": {
            "$ref": "#/components/schemas/Payments_API_RequestAmount"
          }
        }
      },
      "Payments_API_PaymentRequestPublicSchema": {
        "type": "object",
        "description": "Payment request object",
        "properties": {
          "business_id": {
            "$ref": "#/components/schemas/Payments_API_BusinessId"
          },
          "reference_id": {
            "$ref": "#/components/schemas/Payments_API_PaymentRequestReferenceId"
          },
          "payment_request_id": {
            "$ref": "#/components/schemas/Payments_API_PaymentRequestId"
          },
          "payment_token_id": {
            "$ref": "#/components/schemas/Payments_API_PaymentTokenId"
          },
          "customer_id": {
            "$ref": "#/components/schemas/Payments_API_CustomerId"
          },
          "latest_payment_id": {
            "$ref": "#/components/schemas/Payments_API_LatestPaymentId"
          },
          "latest_payment": {
            "$ref": "#/components/schemas/Payments_API_LatestPayment"
          },
          "type": {
            "$ref": "#/components/schemas/Payments_API_PaymentRequestType"
          },
          "country": {
            "$ref": "#/components/schemas/Payments_API_Country"
          },
          "currency": {
            "$ref": "#/components/schemas/Payments_API_Currency"
          },
          "request_amount": {
            "$ref": "#/components/schemas/Payments_API_RequestAmount"
          },
          "capture_method": {
            "$ref": "#/components/schemas/Payments_API_CaptureMethod"
          },
          "channel_code": {
            "$ref": "#/components/schemas/Payments_API_ChannelCode"
          },
          "channel_properties": {
            "$ref": "#/components/schemas/Payments_API_ChannelProperties"
          },
          "actions": {
            "$ref": "#/components/schemas/Payments_API_ArrayOfActions"
          },
          "status": {
            "$ref": "#/components/schemas/Payments_API_PaymentRequestStatus"
          },
          "failure_code": {
            "$ref": "#/components/schemas/Payments_API_PaymentFailureCodes"
          },
          "description": {
            "$ref": "#/components/schemas/Payments_API_Description"
          },
          "metadata": {
            "$ref": "#/components/schemas/Payments_API_MerchantMetadata"
          },
          "created": {
            "$ref": "#/components/schemas/Payments_API_CreatedDateTime"
          },
          "updated": {
            "$ref": "#/components/schemas/Payments_API_UpdatedDateTime"
          }
        }
      },
      "Payments_API_Http400InactivePaymentRequest": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INACTIVE_PAYMENT_REQUEST"
            ]
          },
          "message": {
            "type": "string",
            "description": "Payment request is already inactive."
          }
        }
      },
      "Payments_API_Http400InvalidValueError": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INVALID_VALUE_ERROR"
            ]
          },
          "message": {
            "type": "string",
            "description": "Values in the payment request is not within expected range or expected configurations. Check the specific error message for debugging."
          }
        }
      },
      "Payments_API_Http400ApiValidationError": {
        "description": "Api Validation Error",
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "API_VALIDATION_ERROR"
            ]
          },
          "message": {
            "type": "string",
            "description": "Fields or values in the payment request does not comply with our API specification. Check the specific error message for debugging."
          }
        }
      },
      "Payments_API_Http400TemporarilyUnavailable": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "TEMPORARILY_UNAVAILABLE"
            ]
          },
          "message": {
            "type": "string",
            "description": "Requested feature is unavailable during this timing."
          }
        }
      },
      "Payments_API_Http400IneligibleTransactionStatus": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INELIGIBLE_TRANSACTION_STATUS"
            ]
          },
          "message": {
            "type": "string",
            "description": "Feature is not allowed for the payment request because of its current status. Check the specific error message for debugging."
          }
        }
      },
      "Payments_API_Http404DataNotFound": {
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
            "description": "ID specified in request cannot be found."
          }
        }
      },
      "Payments_API_Http409DuplicateError": {
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
            "description": "Duplication is not allowed. Check specific error message for debugging."
          }
        }
      },
      "Payments_API_Http500ServerError": {
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
            "description": "An unexpected error occured, our team has been notified and will troubleshoot the issue"
          }
        }
      },
      "Payments_API_Http503ChannelUnavailable": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "CHANNEL_UNAVAILABLE"
            ]
          },
          "message": {
            "type": "string",
            "description": "The channel requested is currently experiencing unexpected issues. The provider will be notified to resolve this issue."
          }
        }
      },
      "Payments_API_PRPatchRequestChannelProperties": {
        "anyOf": [
          {
            "$ref": "#/components/schemas/Payments_API_VirtualAccountPatchPrRequest"
          }
        ]
      },
      "Payments_API_Description": {
        "type": "string",
        "minLength": 1,
        "maxLength": 1000,
        "description": "A custom description for the Payment Request.",
        "example": "Payment for your order #123"
      },
      "Payments_API_RequestAmount": {
        "type": "number",
        "minimum": 0,
        "description": "The intended payment amount to be collected from the end user.\n",
        "example": 10000
      },
      "Payments_API_BusinessId": {
        "type": "string",
        "description": "Xendit-generated identifier for the business that owns the transaction",
        "example": "5f27a14a9bf05c73dd040bc8"
      },
      "Payments_API_PaymentRequestReferenceId": {
        "type": "string",
        "minLength": 1,
        "maxLength": 255,
        "description": "A reference ID from merchants to identify their request. For \"CARDS\" channel code, reference ID must be unique."
      },
      "Payments_API_PaymentRequestId": {
        "type": "string",
        "description": "Xendit unique Payment Request ID generated as reference after creation of payment request.",
        "example": "pr-1102feb0-bb79-47ae-9d1e-e69394d3949c"
      },
      "Payments_API_PaymentTokenId": {
        "type": "string",
        "description": "Xendit unique Payment Token ID generated as a reference for saved payment token of an end user.",
        "example": "pt-cc3938dc-c2a5-43c4-89d7-7570793348c2"
      },
      "Payments_API_CustomerId": {
        "type": "string",
        "maxLength": 41,
        "description": "Xendit unique Customer ID generated as reference for the end user",
        "example": "cust-b98d6f63-d240-44ec-9bd5-aa42954c4f48"
      },
      "Payments_API_LatestPaymentId": {
        "type": "string",
        "description": "Latest Payment ID linked to the payment request.",
        "example": "py-1402feb0-bb79-47ae-9d1e-e69394d3949c"
      },
      "Payments_API_LatestPayment": {
        "allOf": [
          {
            "$ref": "#/components/schemas/Payments_API_PaymentSchema"
          }
        ],
        "description": "Latest payment information provided by the payment method provider. Fields returned are dependent on what is made available by the provider.\nCurrently only available for \"CARDS\" channel code and only shown once the transaction reaches a terminal state (e.g. non 3DS transaction or MIT transaction).\n"
      },
      "Payments_API_PaymentRequestType": {
        "type": "string",
        "enum": [
          "PAY",
          "PAY_AND_SAVE",
          "REUSABLE_PAYMENT_CODE"
        ],
        "description": "The payment collection intent type for the payment request.\n\nPAY: Create a payment request that is able to receive one payment.\n\nPAY_AND_SAVE: Create a payment request that is able to receive one payment. If the payment is successful, a reusable payment token will be returned for subsequent payment requests.\n\nREUSABLE_PAYMENT_CODE: Create a payment request that is able to receive multiple payments. This is only used for repeat use payment method like a static QR, a predefined OTC payment code or a predefined Virtual Account number.\n"
      },
      "Payments_API_Country": {
        "type": "string",
        "enum": [
          "ID",
          "PH",
          "VN",
          "TH",
          "SG",
          "MY",
          "HK",
          "MX"
        ],
        "description": "ISO 3166-1 alpha-2 two-letter country code for the country of transaction.",
        "example": "ID"
      },
      "Payments_API_Currency": {
        "type": "string",
        "enum": [
          "IDR",
          "PHP",
          "VND",
          "THB",
          "SGD",
          "MYR",
          "USD",
          "HKD",
          "AUD",
          "GBP",
          "EUR",
          "JPY",
          "MXN",
          "AED",
          "AFN",
          "ALL",
          "AMD",
          "AOA",
          "ARS",
          "AWG",
          "AZN",
          "BAM",
          "BBD",
          "BDT",
          "BGN",
          "BHD",
          "BIF",
          "BMD",
          "BND",
          "BOB",
          "BOV",
          "BRL",
          "BSD",
          "BTN",
          "BWP",
          "BYN",
          "BZD",
          "CAD",
          "CDF",
          "CHF",
          "CLF",
          "CLP",
          "CNY",
          "COP",
          "COU",
          "CRC",
          "CUC",
          "CUP",
          "CVE",
          "CZK",
          "DJF",
          "DKK",
          "DOP",
          "DZD",
          "EGP",
          "ERN",
          "ETB",
          "FJD",
          "FKP",
          "GEL",
          "GHS",
          "GIP",
          "GMD",
          "GNF",
          "GTQ",
          "GYD",
          "HNL",
          "HTG",
          "HUF",
          "ILS",
          "INR",
          "IQD",
          "IRR",
          "ISK",
          "JMD",
          "JOD",
          "KES",
          "KGS",
          "KHR",
          "KMF",
          "KPW",
          "KRW",
          "KWD",
          "KYD",
          "KZT",
          "LAK",
          "LBP",
          "LKR",
          "LRD",
          "LSL",
          "LYD",
          "MAD",
          "MDL",
          "MGA",
          "MKD",
          "MMK",
          "MNT",
          "MOP",
          "MRU",
          "MUR",
          "MVR",
          "MWK",
          "MZN",
          "NAD",
          "NGN",
          "NIO",
          "NOK",
          "NPR",
          "NZD",
          "OMR",
          "PAB",
          "PEN",
          "PGK",
          "PKR",
          "PLN",
          "PYG",
          "QAR",
          "RON",
          "RSD",
          "RUB",
          "RWF",
          "SAR",
          "SBD",
          "SCR",
          "SDG",
          "SEK",
          "SHP",
          "SLE",
          "SOS",
          "SRD",
          "SSP",
          "STN",
          "SVC",
          "SYP",
          "SZL",
          "TJS",
          "TMT",
          "TND",
          "TOP",
          "TRY",
          "TTD",
          "TWD",
          "TZS",
          "UAH",
          "UGX",
          "UYU",
          "UZS",
          "VEF",
          "VES",
          "VUV",
          "WST",
          "XAF",
          "XCD",
          "XCG",
          "XOF",
          "XPF",
          "YER",
          "ZAR",
          "ZMW",
          "ZWG",
          "ZWL"
        ],
        "description": "ISO 4217 three-letter currency code for the payment.",
        "example": "IDR"
      },
      "Payments_API_CaptureMethod": {
        "type": "string",
        "enum": [
          "AUTOMATIC",
          "MANUAL"
        ],
        "default": "AUTOMATIC",
        "description": "AUTOMATIC: payment capture will be processed immediately after payment request is created.\nMANUAL: payment capture requires merchant's trigger via payment capture endpoint before being processed\n",
        "example": "AUTOMATIC"
      },
      "Payments_API_ChannelCode": {
        "type": "string",
        "description": "Channel code used to select the payment method provider.\n\n<iframe src=\"https://doc-widget.xendit.co/channel-data-finder/?iframe_id=channel-code-iframe\" frameborder=\"0\" allowfullscreen=\"\" allow=\"accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture\" title=\"\" style=\"border:1px solid #ccc;width:100%;display:flex;margin-right:auto;max-height:800px;\" width=\"100%\" loading=\"lazy\" referrerpolicy=\"no-referrer-when-downgrade\"></iframe>\n"
      },
      "Payments_API_ChannelProperties": {
        "type": "object",
        "description": "Data required to initiate transaction with payment method provider. Refer to the Payment Method Options information in the channel_code field above for the full list of required properties for each payment method.\n"
      },
      "Payments_API_ArrayOfActions": {
        "type": "array",
        "items": {
          "$ref": "#/components/schemas/Payments_API_Actions"
        }
      },
      "Payments_API_PaymentRequestStatus": {
        "type": "string",
        "enum": [
          "ACCEPTING_PAYMENTS",
          "REQUIRES_ACTION",
          "AUTHORIZED",
          "CANCELED",
          "EXPIRED",
          "SUCCEEDED",
          "FAILED"
        ],
        "description": "Status of the payment request.",
        "example": "SUCCEEDED"
      },
      "Payments_API_PaymentFailureCodes": {
        "type": "string",
        "enum": [
          "ACCOUNT_ACCESS_BLOCKED",
          "INVALID_MERCHANT_SETTINGS",
          "INVALID_ACCOUNT_DETAILS",
          "PAYMENT_ATTEMPT_COUNTS_EXCEEDED",
          "USER_DEVICE_UNREACHABLE",
          "CHANNEL_UNAVAILABLE",
          "INSUFFICIENT_BALANCE",
          "ACCOUNT_NOT_ACTIVATED",
          "INVALID_TOKEN",
          "SERVER_ERROR",
          "PARTNER_TIMEOUT_ERROR",
          "TIMEOUT_ERROR",
          "USER_DECLINED_PAYMENT",
          "USER_DID_NOT_AUTHORIZE",
          "PAYMENT_REQUEST_EXPIRED",
          "FAILURE_DETAILS_UNAVAILABLE",
          "EXPIRED_OTP",
          "INVALID_OTP",
          "PAYMENT_AMOUNT_LIMITS_EXCEEDED",
          "OTP_ATTEMPT_COUNTS_EXCEEDED",
          "CARD_DECLINED",
          "DECLINED_BY_ISSUER",
          "ISSUER_UNAVAILABLE",
          "INVALID_CVV",
          "DECLINED_BY_PROCESSOR",
          "CAPTURE_AMOUNT_EXCEEDED ",
          "AUTHENTICATION_FAILED",
          "PROCESSOR_ERROR",
          "EXPIRED_CARD",
          "STOLEN_CARD",
          "INACTIVE_OR_UNAUTHORIZED_CARD",
          "INVALID_MERCHANT_CREDENTIALS",
          "SUSPECTED_FRAUDULENT"
        ],
        "description": "Failure codes for payments.",
        "example": "CARD_DECLINED"
      },
      "Payments_API_MerchantMetadata": {
        "type": "object",
        "description": "Key-value entries for your custom data.\nXendit supports up to 50 key-value pairs, with key names up to 40 characters and primitive values of up to 500 characters in length.\nXendit will not use this data for any processing.\n",
        "example": {
          "my_custom_id": "merchant-123",
          "my_custom_order_id": "order-123"
        }
      },
      "Payments_API_CreatedDateTime": {
        "type": "string",
        "format": "date-time",
        "description": "ISO 8601 date-time format.\n",
        "example": "2021-12-31T23:59:59Z"
      },
      "Payments_API_UpdatedDateTime": {
        "type": "string",
        "format": "date-time",
        "description": "ISO 8601 date-time format.\n",
        "example": "2021-12-31T23:59:59Z"
      },
      "Payments_API_VirtualAccountPatchPrRequest": {
        "type": "object",
        "properties": {
          "expires_at": {
            "$ref": "#/components/schemas/Payments_API_ExpiresAt"
          }
        }
      },
      "Payments_API_PaymentSchema": {
        "type": "object",
        "description": "Payment object",
        "properties": {
          "payment_id": {
            "$ref": "#/components/schemas/Payments_API_PaymentId"
          },
          "business_id": {
            "$ref": "#/components/schemas/Payments_API_BusinessId"
          },
          "reference_id": {
            "$ref": "#/components/schemas/Payments_API_ReferenceId"
          },
          "payment_request_id": {
            "$ref": "#/components/schemas/Payments_API_PaymentRequestId"
          },
          "payment_token_id": {
            "$ref": "#/components/schemas/Payments_API_PaymentTokenId"
          },
          "customer_id": {
            "$ref": "#/components/schemas/Payments_API_CustomerId"
          },
          "type": {
            "$ref": "#/components/schemas/Payments_API_PaymentRequestType"
          },
          "country": {
            "$ref": "#/components/schemas/Payments_API_Country"
          },
          "currency": {
            "$ref": "#/components/schemas/Payments_API_Currency"
          },
          "request_amount": {
            "$ref": "#/components/schemas/Payments_API_RequestAmount"
          },
          "capture_method": {
            "$ref": "#/components/schemas/Payments_API_CaptureMethod"
          },
          "channel_code": {
            "$ref": "#/components/schemas/Payments_API_ChannelCode"
          },
          "captures": {
            "$ref": "#/components/schemas/Payments_API_ArrayOfCaptures"
          },
          "status": {
            "$ref": "#/components/schemas/Payments_API_PaymentStatus"
          },
          "payment_details": {
            "$ref": "#/components/schemas/Payments_API_PaymentDetails"
          },
          "failure_code": {
            "$ref": "#/components/schemas/Payments_API_PaymentFailureCodes"
          },
          "metadata": {
            "$ref": "#/components/schemas/Payments_API_MerchantMetadata"
          },
          "created": {
            "$ref": "#/components/schemas/Payments_API_CreatedDateTime"
          },
          "updated": {
            "$ref": "#/components/schemas/Payments_API_UpdatedDateTime"
          }
        }
      },
      "Payments_API_Actions": {
        "description": "Actions object contains possible next steps merchants can take to proceed with payment collection from end user",
        "type": "object",
        "properties": {
          "type": {
            "enum": [
              "PRESENT_TO_CUSTOMER",
              "REDIRECT_CUSTOMER",
              "API_POST_REQUEST"
            ],
            "description": "The type of action that merchant system will need to handle to complete payment."
          },
          "descriptor": {
            "enum": [
              "CAPTURE_PAYMENT",
              "PAYMENT_CODE",
              "QR_STRING",
              "VIRTUAL_ACCOUNT_NUMBER",
              "WEB_URL",
              "DEEPLINK_URL",
              "VALIDATE_OTP",
              "RESEND_OTP"
            ],
            "description": "The type of action that merchant system will need to handle to complete payment."
          },
          "value": {
            "type": "string",
            "description": "The specific value that will be used by merchant to complete the action"
          }
        }
      },
      "Payments_API_ExpiresAt": {
        "type": "string",
        "format": "date-time"
      },
      "Payments_API_PaymentId": {
        "type": "string",
        "description": "Xendit unique Payment ID generated as reference for a payment.",
        "example": "py-1402feb0-bb79-47ae-9d1e-e69394d3949c"
      },
      "Payments_API_ReferenceId": {
        "type": "string",
        "minLength": 1,
        "maxLength": 255,
        "description": "A Reference ID from merchants to identify their request."
      },
      "Payments_API_ArrayOfCaptures": {
        "type": "array",
        "items": {
          "$ref": "#/components/schemas/Payments_API_Capture"
        }
      },
      "Payments_API_PaymentStatus": {
        "type": "string",
        "enum": [
          "AUTHORIZED",
          "CANCELED",
          "SUCCEEDED",
          "FAILED",
          "EXPIRED",
          "PENDING"
        ],
        "description": "Status of the payment.",
        "example": "SUCCEEDED"
      },
      "Payments_API_PaymentDetails": {
        "type": "object",
        "description": "Payment information provided by the payment method provider. Fields returned are dependent on what is made available by the provider.\n<iframe src=\"https://doc-widget.xendit.co/channel-details/payment?iframe_id=channel-payment-iframe\" frameborder=\"0\" allowfullscreen=\"\" allow=\"accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture\" title=\"\" style=\"border:1px solid #ccc;width:100%;display:flex;margin-right:auto;max-height:800px;\" width=\"100%\" loading=\"lazy\" referrerpolicy=\"no-referrer-when-downgrade\"></iframe>\n",
        "properties": {
          "authorization_data": {
            "$ref": "#/components/schemas/Payments_API_AuthorizationData"
          },
          "authentication_data": {
            "$ref": "#/components/schemas/Payments_API_AuthenticationData"
          },
          "digital_wallet": {
            "type": "string",
            "description": "Name of the digital wallet used by the end user.\n"
          },
          "issuer_name": {
            "type": "string",
            "description": "Name of the payment method provider used by the end user.\n"
          },
          "payer_account_number": {
            "type": "string",
            "description": "Account number of the end user making the payment from the payment method provider's records.\n"
          },
          "payer_name": {
            "type": "string",
            "description": "Name of the end user making the payment from the payment method provider's records.\n"
          },
          "receipt_id": {
            "type": "string",
            "description": "Receipt reference number communicated to the end user by their payment method provider for this specific payment. This a commonly used reference number for the end users to raise tickets.\n"
          },
          "remark": {
            "type": "string",
            "description": "Remarks about this specific payment from the payment method provider's records.\n"
          },
          "network": {
            "type": "string",
            "description": "Payment network which the payment was processed over.\n"
          },
          "fund_source": {
            "type": "string",
            "description": "Information about what was used by the end user to complete the payment. e.g. balance, installment, credit.\n"
          }
        }
      },
      "Payments_API_Capture": {
        "description": "Capture object contains information about the capture that was performed",
        "type": "object",
        "properties": {
          "capture_timestamp": {
            "type": "string",
            "format": "date-time",
            "description": "ISO 8601 date-time format.\n",
            "example": "2021-12-31T23:59:59Z"
          },
          "capture_id": {
            "$ref": "#/components/schemas/Payments_API_CaptureId"
          },
          "capture_amount": {
            "$ref": "#/components/schemas/Payments_API_CaptureAmount"
          }
        }
      },
      "Payments_API_AuthorizationData": {
        "type": "object",
        "description": "Specific to cards transaction only. Details about the card authorization processing.\n",
        "properties": {
          "authorization_code": {
            "type": "string",
            "description": "Authorization approval code from the scheme. 6 alphanumeric characters."
          },
          "cvn_verification_result": {
            "type": "string",
            "enum": [
              "M",
              "N"
            ],
            "description": "Whether CVN input matches with the issuer's data."
          },
          "address_verification_result": {
            "type": "string",
            "enum": [
              "M",
              "N"
            ],
            "description": "Whether the end user's address input matches with the issuer's data."
          },
          "retrieval_reference_number": {
            "type": "string",
            "description": "Receipt reference number communicated to the end user by their card issuer for this specific payment. This a commonly used reference number for the end users to raise tickets."
          },
          "network_response_code": {
            "type": "string",
            "description": "The response code returned by the scheme (Visa, Mastercard, JCB, China Unionpay or Amex)."
          },
          "network_response_code_descriptor": {
            "type": "string",
            "description": "Description of the response code."
          },
          "network_transaction_id": {
            "type": "string",
            "description": "Transaction ID received from the card scheme. Only available for merchants on switcher model."
          },
          "transaction_link_id": {
            "type": "string",
            "description": "Mastercard Transaction Link Identifier (TLID) received from the card scheme. Returned for Mastercard transactions only."
          },
          "acquirer_merchant_id": {
            "type": "string",
            "description": "Acquirer's record of the MID that was used to process this transaction. Only available for merchants on switcher model."
          },
          "reconciliation_id": {
            "type": "string",
            "description": "Acquirer's transaction record of the payment on their settlement statement. Only available for merchants on switcher model."
          }
        }
      },
      "Payments_API_AuthenticationData": {
        "type": "object",
        "description": "Specific to cards transaction only. Details about the card authentication.\n",
        "properties": {
          "flow": {
            "type": "string",
            "enum": [
              "FULL_AUTH",
              "FRICTIONLESS"
            ],
            "description": "Indicates the flow that was used for the 3DS authentication."
          },
          "a_res": {
            "type": "object",
            "description": "Details about the card authentication response from the 3DS server.\n",
            "properties": {
              "eci": {
                "type": "string",
                "description": "Payment system-specific value provided by the ACS or DS to indicate the results of the attempt to authenticate the Cardholder."
              },
              "message_version": {
                "type": "string",
                "description": "The 3DS protocol version which has been used to perform 3DS."
              },
              "authentication_value": {
                "type": "string",
                "description": "The result value from the 3DS transaction received from the ACS. This value is no longer present on responses after 45 days have passed after the authentication. Note that Mastercard and Visa use a different underlying format."
              },
              "ds_trans_id": {
                "type": "string",
                "description": "Universally unique transaction identifier assigned by the DS to identify a single transaction."
              }
            }
          }
        }
      },
      "Payments_API_CaptureId": {
        "type": "string",
        "description": "Xendit unique Capture ID generated as reference for a single capture.",
        "example": "cap-1502feb0-bb79-47ae-9d1e-e69394d3949c"
      },
      "Payments_API_CaptureAmount": {
        "type": "number",
        "minimum": 0,
        "description": "The payment amount captured for this payment. Maximum capture amount can only be equal or lesser than the authorized amount value.\n",
        "example": 10000
      }
    },
    "securitySchemes": {
      "Payments_API_BasicAuth": {
        "type": "http",
        "scheme": "basic"
      }
    }
  }
}
````

