> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Quote

> Create a Quote for FX conversion or payout

## OpenAPI

````json POST /quotes
{
  "openapi": "3.0.3",
  "info": {
    "title": "Foreign Exchange",
    "version": "1.0",
    "description": "This Foreign Exchange API consists of quotes & conversion.\nA created quote returns a conversion rate that is active for a certain period of time. \nA created conversion acts on an active rate to convert from one currency  into another."
  },
  "servers": [
    {
      "url": "https://api.xendit.co",
      "description": "Xendit API"
    }
  ],
  "tags": [
    {
      "name": "Foreign Exchange"
    }
  ],
  "paths": {
    "/quotes": {
      "post": {
        "operationId": "Quotes_create",
        "summary": "Create Quote",
        "description": "Create a Quote for FX conversion or payout",
        "parameters": [
          {
            "name": "api-version",
            "in": "header",
            "required": "true",
            "description": "The version of the API. Value: \"2025-06-06\"",
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
                  "$ref": "#/components/schemas/Payouts_v3_Quote"
                },
                "examples": {
                  "Create Quote PHP to THB": {
                    "summary": "Create Quote PHP to THB",
                    "value": {
                      "quote_id": "qo-7c4d2e1f-a8b9-4f3e-9d6c-5a1b2c3d4e5f",
                      "reference_id": "a3f7c912-4e8b-4d1a-bc56-9f2e1a3d7b4c",
                      "source_amount": "78500",
                      "source_currency": "PHP",
                      "destination_amount": "500000",
                      "destination_currency": "THB",
                      "fx_rate": "0.637",
                      "type": "PAYOUT",
                      "created": "2025-06-03T09:15:00Z",
                      "updated": "2025-06-03T09:15:00Z",
                      "expires": "2025-06-03T09:15:30Z"
                    }
                  },
                  "Create Quote for Payout": {
                    "summary": "Create Quote for Payout",
                    "value": {
                      "quote_id": "qo-68b6ec19-4b83-46f0-aea5-e1f4a57966b1",
                      "reference_id": "51d9b583-717f-462b-834e-0fc523ae2894",
                      "source_amount": "100000",
                      "source_currency": "IDR",
                      "destination_amount": "627",
                      "destination_currency": "USD",
                      "fx_rate": "0.000063",
                      "type": "PAYOUT",
                      "created": "2025-06-02T15:58:16.97Z",
                      "updated": "2025-06-02T15:58:16.97Z",
                      "expires": "2025-06-02T15:58:46.952Z"
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
                  "$ref": "#/components/schemas/Payouts_v3_CreateQuote400Body"
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Payouts_v3_Http401InvalidApiKey"
                }
              }
            }
          },
          "403": {
            "description": "Forbidden",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Payouts_v3_CreateQuote403Body"
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Payouts_v3_Http500ServerError"
                }
              }
            }
          }
        },
        "tags": [
          "Foreign Exchange"
        ],
        "requestBody": {
          "required": "true",
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/Payouts_v3_CreateQuoteRequest"
              },
              "examples": {
                "Create Quote PHP to THB": {
                  "summary": "Create Quote PHP to THB",
                  "value": {
                    "reference_id": "a3f7c912-4e8b-4d1a-bc56-9f2e1a3d7b4c",
                    "type": "PAYOUT",
                    "source_currency": "PHP",
                    "destination_currency": "THB",
                    "destination_amount": "500000"
                  }
                },
                "Create Quote for Payout": {
                  "summary": "Create Quote for Payout",
                  "value": {
                    "reference_id": "51d9b583-717f-462b-834e-0fc523ae2894",
                    "type": "PAYOUT",
                    "source_currency": "IDR",
                    "destination_currency": "USD",
                    "source_amount": "100000"
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ForeignExchange_BasicAuth": []
          }
        ]
      }
    }
  },
  "components": {
    "schemas": {
      "Payouts_v3_Quote": {
        "type": "object",
        "required": [
          "quote_id",
          "reference_id",
          "source_currency",
          "source_amount",
          "destination_currency",
          "destination_amount",
          "fx_rate",
          "type",
          "created",
          "updated",
          "expires"
        ],
        "properties": {
          "quote_id": {
            "type": "string",
            "description": "Unique Quote ID in UUID format, prefixed with qo-"
          },
          "reference_id": {
            "type": "string",
            "description": "ID provided by merchant to identify the request"
          },
          "source_currency": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Payouts_v3_QuoteCurrency"
              }
            ],
            "description": "Source currency"
          },
          "source_amount": {
            "type": "integer",
            "description": "Source amount in minor units.\n\nA minor unit is the smallest unit of a currency. Most currencies have 2 decimals, others have 0.\nExamples: PHP 10.00 → `1000`, IDR 10 → `10`."
          },
          "destination_currency": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Payouts_v3_QuoteCurrency"
              }
            ],
            "description": "Destination currency"
          },
          "destination_amount": {
            "type": "integer",
            "description": "Destination amount in minor units.\n\nA minor unit is the smallest unit of a currency. Most currencies have 2 decimals, others have 0.\nExamples: PHP 10.00 → `1000`, IDR 10 → `10`."
          },
          "fx_rate": {
            "type": "number",
            "format": "double",
            "description": "Exchange rate"
          },
          "type": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Payouts_v3_QuoteType"
              }
            ],
            "description": "Type of transaction which the Quote will be used for"
          },
          "created": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when the quote was made. Format: ISO 8601, UTC+0"
          },
          "updated": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when the quote was last updated. Format: ISO 8601, UTC+0"
          },
          "expires": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when the quote will expire. Format: ISO 8601, UTC+0"
          }
        },
        "description": "Quote Object"
      },
      "Payouts_v3_CreateQuote400Body": {
        "oneOf": [
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400ApiValidationError"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400ApiValidationError_UnsupportedSourceCurrency"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400ApiValidationError_UnsupportedDestinationCurrency"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400ApiValidationError_BothAmounts"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400ApiValidationError_UnsupportedType"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400InvalidValueError_QuoteTooLow"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400InvalidValueError_QuoteTooHigh"
          }
        ]
      },
      "Payouts_v3_Http401InvalidApiKey": {
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
      "Payouts_v3_CreateQuote403Body": {
        "oneOf": [
          {
            "$ref": "#/components/schemas/Payouts_v3_Http403RequestForbiddenError"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http403InvalidMerchantSettings"
          }
        ]
      },
      "Payouts_v3_Http500ServerError": {
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
      "Payouts_v3_CreateQuoteRequest": {
        "type": "object",
        "required": [
          "reference_id",
          "type",
          "source_currency",
          "destination_currency"
        ],
        "properties": {
          "reference_id": {
            "type": "string",
            "description": "ID provided by merchant to identify the request"
          },
          "type": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Payouts_v3_QuoteType"
              }
            ],
            "description": "Type of transaction which the Quote will be used for"
          },
          "source_currency": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Payouts_v3_QuoteSourceCurrency"
              }
            ],
            "description": "Source currency"
          },
          "destination_currency": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Payouts_v3_QuoteDestCurrency"
              }
            ],
            "description": "Destination currency"
          },
          "source_amount": {
            "type": "integer",
            "description": "Source amount in minor units. Must be empty if destination_amount is filled.\n\nA minor unit is the smallest unit of a currency. Most currencies have 2 decimals, others have 0.\nExamples: PHP 10.00 → `1000`, IDR 10 → `10`."
          },
          "destination_amount": {
            "type": "integer",
            "description": "Destination amount in minor units. Must be empty if source_amount is filled.\n\nA minor unit is the smallest unit of a currency. Most currencies have 2 decimals, others have 0.\nExamples: PHP 10.00 → `1000`, IDR 10 → `10`."
          }
        }
      },
      "Payouts_v3_QuoteCurrency": {
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
          "CNY",
          "KRW",
          "AUD",
          "EUR",
          "MXN"
        ]
      },
      "Payouts_v3_QuoteType": {
        "type": "string",
        "enum": [
          "CONVERSION",
          "PAYOUT"
        ]
      },
      "Payouts_v3_Http400ApiValidationError": {
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
            "enum": [
              "Inputs are failing validation. The errors field contains details about which fields are violating validation."
            ]
          }
        }
      },
      "Payouts_v3_Http400ApiValidationError_UnsupportedSourceCurrency": {
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
            "enum": [
              "The source currency specified in the request is not supported. Please check our documentation for currencies available."
            ]
          }
        }
      },
      "Payouts_v3_Http400ApiValidationError_UnsupportedDestinationCurrency": {
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
            "enum": [
              "The destination currency specified in the request is not supported. Please check our documentation for currencies available."
            ]
          }
        }
      },
      "Payouts_v3_Http400ApiValidationError_BothAmounts": {
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
            "enum": [
              "Both source and destination amounts were specified. Please input only one of these amounts."
            ]
          }
        }
      },
      "Payouts_v3_Http400ApiValidationError_UnsupportedType": {
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
            "enum": [
              "The transaction type specified is not supported. Please check our documentation for supported transactions."
            ]
          }
        }
      },
      "Payouts_v3_Http400InvalidValueError_QuoteTooLow": {
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
            "enum": [
              "Quotes need to be at least US$1.00 or equivalent. Please retry the request with a higher source or destination quote amount."
            ]
          }
        }
      },
      "Payouts_v3_Http400InvalidValueError_QuoteTooHigh": {
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
            "enum": [
              "The value of the quote exceeds our limit of US$1,000,000. Please retry the request with a lower source or destination quote amount."
            ]
          }
        }
      },
      "Payouts_v3_Http403RequestForbiddenError": {
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
      "Payouts_v3_Http403InvalidMerchantSettings": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INVALID_MERCHANT_SETTINGS"
            ]
          },
          "message": {
            "type": "string",
            "enum": [
              "Quote failed because the source / destination currency has not been activated. Please reach out to Xendit to activate this currency before retrying."
            ]
          }
        }
      },
      "Payouts_v3_QuoteSourceCurrency": {
        "type": "string",
        "enum": [
          "USD",
          "SGD",
          "IDR",
          "PHP",
          "MYR",
          "THB",
          "HKD"
        ]
      },
      "Payouts_v3_QuoteDestCurrency": {
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
          "CNY",
          "KRW",
          "AUD",
          "EUR"
        ]
      }
    },
    "securitySchemes": {
      "ForeignExchange_BasicAuth": {
        "type": "http",
        "scheme": "basic"
      }
    }
  }
}
````

