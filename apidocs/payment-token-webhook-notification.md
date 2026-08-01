> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Payment token webhook notification

> Webhook notification that will be sent to your defined webhook url for updates to payment token status.


## OpenAPI

````json POST /your_payment_token_webhook_url
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
    }
  ],
  "paths": {
    "/your_payment_token_webhook_url": {
      "post": {
        "operationId": "PaymentTokenWebhook",
        "summary": "Payment token webhook notification",
        "description": "Webhook notification that will be sent to your defined webhook url for updates to payment token status.\n",
        "parameters": [
          {
            "$ref": "#/components/parameters/Payments_API_XCallbackToken"
          }
        ],
        "tags": [
          "Payment Token"
        ],
        "requestBody": {
          "description": "Payment Token status callback",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "description": "Payment Token status callback for binding",
                "properties": {
                  "event": {
                    "type": "string",
                    "enum": [
                      "payment_token.activation",
                      "payment_token.failure",
                      "payment_token.expiry"
                    ],
                    "description": "Webhook event names for payment token status updates.\n"
                  },
                  "business_id": {
                    "$ref": "#/components/schemas/Payments_API_BusinessId"
                  },
                  "created": {
                    "type": "string",
                    "format": "date-time",
                    "description": "Timestamp of webhook delivery attempt in ISO 8601 date-time format.\n",
                    "example": "2021-12-31T23:59:59Z"
                  },
                  "data": {
                    "$ref": "#/components/schemas/Payments_API_PaymentTokenSchema"
                  }
                }
              },
              "example": {
                "tokenActivation": {
                  "value": {
                    "event": "payment_token.activation",
                    "business_id": "6094fa76c2fd53701b8e079c",
                    "created": "2021-12-02T14:52:21.566Z",
                    "data": {
                      "payment_token_id": "pt-1402feb0-bb79-47ae-9d1e-e69394d3949c",
                      "business_id": "5f27a14a9bf05c73dd040bc8",
                      "reference_id": "90392f42-d98a-49ef-a7f3-abcezas123",
                      "customer_id": "cust-b98d6f63-d240-44ec-9bd5-aa42954c4f48",
                      "country": "ID",
                      "currency": "IDR",
                      "channel_code": "OVO",
                      "channel_properties": {
                        "failure_return_url": "https://xendit.co/failure",
                        "success_return_url": "https://xendit.co/success"
                      },
                      "actions": [
                        {
                          "type": "REDIRECT_CUSTOMER",
                          "descriptor": "WEB_URL",
                          "value": "https://xendit.co/"
                        }
                      ],
                      "status": "ACTIVE",
                      "token_details": {
                        "account_name": "John Doe",
                        "account_balance": "1000001",
                        "account_point_balance": "50000"
                      },
                      "metadata": {
                        "invoice_id": "INV-2025-001",
                        "customer_type": "business"
                      },
                      "created": "2029-12-31T23:59:59Z",
                      "updated": "2029-12-31T23:59:59Z"
                    }
                  }
                },
                "tokenFailure": {
                  "value": {
                    "event": "payment_token.failure",
                    "business_id": "6094fa76c2fd53701b8e079c",
                    "created": "2021-12-02T14:52:21.566Z",
                    "data": {
                      "payment_token_id": "pt-1402feb0-bb79-47ae-9d1e-e69394d3949c",
                      "business_id": "5f27a14a9bf05c73dd040bc8",
                      "reference_id": "90392f42-d98a-49ef-a7f3-abcezas123",
                      "customer_id": "cust-b98d6f63-d240-44ec-9bd5-aa42954c4f48",
                      "country": "ID",
                      "currency": "IDR",
                      "channel_code": "OVO",
                      "channel_properties": {
                        "failure_return_url": "https://xendit.co/failure",
                        "success_return_url": "https://xendit.co/success"
                      },
                      "actions": [
                        {
                          "type": "REDIRECT_CUSTOMER",
                          "descriptor": "WEB_URL",
                          "value": "https://xendit.co/"
                        }
                      ],
                      "status": "FAILED",
                      "metadata": {
                        "invoice_id": "INV-2025-001",
                        "customer_type": "business"
                      },
                      "created": "2029-12-31T23:59:59Z",
                      "updated": "2029-12-31T23:59:59Z"
                    }
                  }
                },
                "tokenExpiry": {
                  "value": {
                    "event": "payment_token.expiry",
                    "business_id": "6094fa76c2fd53701b8e079c",
                    "created": "2021-12-02T14:52:21.566Z",
                    "data": {
                      "payment_token_id": "pt-1402feb0-bb79-47ae-9d1e-e69394d3949c",
                      "business_id": "5f27a14a9bf05c73dd040bc8",
                      "reference_id": "90392f42-d98a-49ef-a7f3-abcezas123",
                      "customer_id": "cust-b98d6f63-d240-44ec-9bd5-aa42954c4f48",
                      "country": "ID",
                      "currency": "IDR",
                      "channel_code": "OVO",
                      "channel_properties": {
                        "failure_return_url": "https://xendit.co/failure",
                        "success_return_url": "https://xendit.co/success"
                      },
                      "actions": [
                        {
                          "type": "REDIRECT_CUSTOMER",
                          "descriptor": "WEB_URL",
                          "value": "https://xendit.co/"
                        }
                      ],
                      "status": "EXPIRED",
                      "token_details": {
                        "account_name": "John Doe",
                        "account_balance": "1000001",
                        "account_point_balance": "50000"
                      },
                      "metadata": {
                        "invoice_id": "INV-2025-001",
                        "customer_type": "business"
                      },
                      "created": "2029-12-31T23:59:59Z",
                      "updated": "2029-12-31T23:59:59Z"
                    }
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OK"
          }
        }
      }
    }
  },
  "components": {
    "parameters": {
      "Payments_API_XCallbackToken": {
        "in": "header",
        "name": "x-callback-token",
        "required": "false",
        "schema": {
          "type": "string"
        },
        "description": "Your Xendit unique webhook token to verify the origin of the webhook. It is highly recommended for your integration to verify this value."
      }
    },
    "schemas": {
      "Payments_API_BusinessId": {
        "type": "string",
        "description": "Xendit-generated identifier for the business that owns the transaction",
        "example": "5f27a14a9bf05c73dd040bc8"
      },
      "Payments_API_PaymentTokenSchema": {
        "type": "object",
        "description": "Payment Token object",
        "properties": {
          "payment_token_id": {
            "$ref": "#/components/schemas/Payments_API_PaymentTokenId"
          },
          "channel_code": {
            "$ref": "#/components/schemas/Payments_API_ChannelCode"
          },
          "country": {
            "$ref": "#/components/schemas/Payments_API_Country"
          },
          "business_id": {
            "$ref": "#/components/schemas/Payments_API_BusinessId"
          },
          "customer_id": {
            "$ref": "#/components/schemas/Payments_API_CustomerId"
          },
          "reference_id": {
            "$ref": "#/components/schemas/Payments_API_ReferenceId"
          },
          "currency": {
            "$ref": "#/components/schemas/Payments_API_Currency"
          },
          "channel_properties": {
            "$ref": "#/components/schemas/Payments_API_ChannelProperties"
          },
          "actions": {
            "$ref": "#/components/schemas/Payments_API_ArrayOfActions"
          },
          "status": {
            "$ref": "#/components/schemas/Payments_API_PaymentTokenStatus"
          },
          "token_details": {
            "$ref": "#/components/schemas/Payments_API_TokenDetails"
          },
          "failure_code": {
            "$ref": "#/components/schemas/Payments_API_PaymentTokenFailureCodes"
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
      "Payments_API_PaymentTokenId": {
        "type": "string",
        "description": "Xendit unique Payment Token ID generated as reference for reusable payment details of the end user.",
        "example": "pt-cc3938dc-c2a5-43c4-89d7-7570793348c2"
      },
      "Payments_API_ChannelCode": {
        "type": "string",
        "description": "Channel code used to select the payment method provider.\n\n<iframe src=\"https://doc-widget.xendit.co/channel-data-finder/?iframe_id=channel-code-iframe\" frameborder=\"0\" allowfullscreen=\"\" allow=\"accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture\" title=\"\" style=\"border:1px solid #ccc;width:100%;display:flex;margin-right:auto;max-height:800px;\" width=\"100%\" loading=\"lazy\" referrerpolicy=\"no-referrer-when-downgrade\"></iframe>\n"
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
      "Payments_API_CustomerId": {
        "type": "string",
        "maxLength": "41",
        "description": "Xendit unique Capture ID generated as reference for the end user",
        "example": "cust-b98d6f63-d240-44ec-9bd5-aa42954c4f48"
      },
      "Payments_API_ReferenceId": {
        "type": "string",
        "minLength": "1",
        "maxLength": "255",
        "description": "A Reference ID from merchants to identify their request."
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
      "Payments_API_ChannelProperties": {
        "type": "object",
        "description": "Data required to initiate transaction with payment method provider. Refer to the Channel Data Finder widget in the channel_code field above for the full list of required properties for each channel.\n"
      },
      "Payments_API_ArrayOfActions": {
        "type": "array",
        "items": {
          "$ref": "#/components/schemas/Payments_API_Actions"
        }
      },
      "Payments_API_PaymentTokenStatus": {
        "type": "string",
        "enum": [
          "REQUIRES_ACTION",
          "PENDING",
          "ACTIVE",
          "FAILED",
          "EXPIRED",
          "CANCELED"
        ],
        "description": "Status of the payment token.",
        "example": "ACTIVE"
      },
      "Payments_API_TokenDetails": {
        "type": "object",
        "description": "Account information provided by the payment method provider. Fields returned are dependent on what is made available by the provider.\n<iframe src=\"https://doc-widget.xendit.co/channel-details/token?type=pay-with-token,pay-and-save,save&iframe_id=channel-token-iframe\" frameborder=\"0\" allowfullscreen=\"\" allow=\"accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture\" title=\"\" style=\"border:1px solid #ccc;width:100%;display:flex;margin-right:auto;max-height:800px;\" width=\"100%\" loading=\"lazy\" referrerpolicy=\"no-referrer-when-downgrade\"></iframe>\n",
        "properties": {
          "authorization_data": {
            "$ref": "#/components/schemas/Payments_API_AuthorizationData"
          },
          "authentication_data": {
            "$ref": "#/components/schemas/Payments_API_AuthenticationData"
          },
          "account_name": {
            "type": "string",
            "description": "Name of the owner of the account bound to the token.\n"
          },
          "account_balance": {
            "type": "string",
            "description": "Balance of the account bound to the token.\n"
          },
          "account_point_balance": {
            "type": "string",
            "description": "Point balance of the account bound to the token.\n"
          },
          "account_number": {
            "type": "string",
            "description": "Account number bound to the token.\n"
          }
        }
      },
      "Payments_API_PaymentTokenFailureCodes": {
        "type": "string",
        "enum": [
          "ACCOUNT_ALREADY_LINKED",
          "INVALID_ACCOUNT_DETAILS",
          "AUTHENTICATION_FAILED",
          "CARD_DECLINED",
          "CAPTURE_AMOUNT_EXCEEDED ",
          "INSUFFICIENT_BALANCE",
          "ISSUER_UNAVAILABLE",
          "CHANNEL_UNAVAILABLE",
          "INVALID_MERCHANT_SETTINGS"
        ],
        "description": "Failure codes for payment tokens.",
        "example": "AUTHENTICATION_FAILED"
      },
      "Payments_API_Description": {
        "type": "string",
        "minLength": "1",
        "maxLength": "1000",
        "description": "A custom description for the Payment Request.",
        "example": "Payment for your order #123"
      },
      "Payments_API_MerchantMetadata": {
        "type": "object",
        "description": "Key-value entries for your custom data.\nYou can specify up to 50 keys, with key names up to 40 characters and values up to 500 characters.\nThis is for your convenience. Xendit will not use this data for any processing.\n",
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
      }
    }
  }
}
````

