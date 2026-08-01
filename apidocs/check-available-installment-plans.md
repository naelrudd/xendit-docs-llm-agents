> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Check available installment plans

> Check the available installment plans for the specific transaction.


## OpenAPI

````json POST /v3/payment_options
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
    "/v3/payment_options": {
      "post": {
        "security": [
          {
            "Payments_API_BasicAuth": []
          }
        ],
        "operationId": "PaymentOptions",
        "summary": "Check available installment plans",
        "description": "Check the available installment plans for the specific transaction.\n",
        "parameters": [
          {
            "$ref": "#/components/parameters/Payments_API_APIVersionHeader"
          },
          {
            "$ref": "#/components/parameters/Payments_API_BusinessIdHeader"
          }
        ],
        "requestBody": {
          "required": "true",
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/Payments_API_PaymentOptionsRequestSchema"
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Installment options available",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Payments_API_PaymentOptionsSchema"
                }
              }
            }
          },
          "4XX": {
            "$ref": "#/components/responses/Payments_API_Generic4XXResponse"
          },
          "5XX": {
            "$ref": "#/components/responses/Payments_API_Generic5XXResponse"
          }
        },
        "tags": [
          "Payment Request"
        ]
      }
    }
  },
  "components": {
    "parameters": {
      "Payments_API_APIVersionHeader": {
        "in": "header",
        "name": "api-version",
        "schema": {
          "example": "2024-11-11",
          "type": "string",
          "enum": [
            "2024-10-31",
            "2024-11-11"
          ]
        }
      },
      "Payments_API_BusinessIdHeader": {
        "in": "header",
        "name": "business-id",
        "required": "true",
        "schema": {
          "example": "629db55f8378f3f47acd1ef1",
          "type": "string"
        }
      }
    },
    "schemas": {
      "Payments_API_PaymentOptionsRequestSchema": {
        "type": "object",
        "properties": {
          "channel_code": {
            "type": "string",
            "description": "Channel code of the transactions. Installment now only available for: \n  CARDS, \n  BAY_CARD_INSTALLMENT,\n  BBL_CARD_INSTALLMENT, \n  KBANK_CARD_INSTALLMENT, \n  KTB_CARD_INSTALLMENT, \n  SCB_CARD_INSTALLMENT,\n  TTB_CARD_INSTALLMENT\n"
          },
          "country": {
            "$ref": "#/components/schemas/Payments_API_Country"
          },
          "amount": {
            "type": "number",
            "format": "double"
          },
          "currency": {
            "$ref": "#/components/schemas/Payments_API_Currency"
          },
          "customer_id": {
            "$ref": "#/components/schemas/Payments_API_CustomerId"
          },
          "channel_properties": {
            "description": "Channel properties only required for CARDS",
            "$ref": "#/components/schemas/Payments_API_PaymentOptionChannelProperties"
          }
        },
        "required": [
          "channel_code",
          "country",
          "amount",
          "currency"
        ]
      },
      "Payments_API_PaymentOptionsSchema": {
        "type": "object",
        "properties": {
          "channel_code": {
            "$ref": "#/components/schemas/Payments_API_ChannelCode"
          },
          "country": {
            "$ref": "#/components/schemas/Payments_API_Country"
          },
          "amount": {
            "type": "number",
            "format": "double"
          },
          "currency": {
            "$ref": "#/components/schemas/Payments_API_Currency"
          },
          "installment_plans": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Payments_API_InstallmentPlan"
            }
          }
        }
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
      "Payments_API_CustomerId": {
        "type": "string",
        "maxLength": "41",
        "description": "Xendit unique Capture ID generated as reference for the end user",
        "example": "cust-b98d6f63-d240-44ec-9bd5-aa42954c4f48"
      },
      "Payments_API_PaymentOptionChannelProperties": {
        "type": "object",
        "properties": {
          "card_number": {
            "type": "string",
            "nullable": "true",
            "description": "Only PCI-DSS compliant merchants can check installment options through this endpoint. Non PCI-DSS merchants should use Xendit Components or Payment Session integration."
          }
        }
      },
      "Payments_API_ChannelCode": {
        "type": "string",
        "description": "Channel code used to select the payment method provider.\n\n<iframe src=\"https://doc-widget.xendit.co/channel-data-finder/?iframe_id=channel-code-iframe\" frameborder=\"0\" allowfullscreen=\"\" allow=\"accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture\" title=\"\" style=\"border:1px solid #ccc;width:100%;display:flex;margin-right:auto;max-height:800px;\" width=\"100%\" loading=\"lazy\" referrerpolicy=\"no-referrer-when-downgrade\"></iframe>\n"
      },
      "Payments_API_InstallmentPlan": {
        "type": "object",
        "properties": {
          "interval": {
            "type": "string"
          },
          "interval_count": {
            "type": "number"
          },
          "terms": {
            "type": "number"
          },
          "installment_amount": {
            "type": "number",
            "format": "double"
          },
          "total_amount": {
            "type": "number",
            "format": "double"
          },
          "interest_rate": {
            "type": "number",
            "format": "double",
            "nullable": "true"
          },
          "description": {
            "type": "string",
            "nullable": "true"
          },
          "code": {
            "type": "string",
            "nullable": "true"
          }
        },
        "required": [
          "interval",
          "interval_count",
          "terms",
          "installment_amount",
          "total_amount"
        ]
      }
    },
    "responses": {
      "Payments_API_Generic4XXResponse": {
        "description": "Client Side Bad Request Error"
      },
      "Payments_API_Generic5XXResponse": {
        "description": "Server Side Error"
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

