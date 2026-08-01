> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Conversion

> Our Create Conversion APIs allow you to execute a conversion between two different currency balances

## OpenAPI

````json POST /conversions
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
    "/conversions": {
      "post": {
        "operationId": "Conversions_create",
        "summary": "Create Conversion",
        "description": "Our Create Conversion APIs allow you to execute a conversion between two different currency balances",
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
                  "$ref": "#/components/schemas/Payouts_v3_Conversion"
                },
                "examples": {
                  "Create Conversion Example": {
                    "summary": "Create Conversion IDR to USD",
                    "value": {
                      "conversion_id": "cnv-ded92b17-fd82-4951-898f-d88c4267436f",
                      "quote_id": "qo-b3b7b4da-75d3-4367-b69f-ddd92b368a09",
                      "reference_id": "5296b95d-5cd1-4dd9-84f6-12cffd9682e1",
                      "source_amount": "100000",
                      "source_currency": "IDR",
                      "destination_amount": "626",
                      "destination_currency": "USD",
                      "fx_rate": "0.000063",
                      "status": "PENDING",
                      "created": "2025-06-02T16:07:21.457368Z",
                      "updated": "2025-06-02T16:07:21.457368Z"
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
                  "$ref": "#/components/schemas/Payouts_v3_CreatePayout400Body"
                },
                "examples": {
                  "Create Conversion Example": {
                    "summary": "Quote Expired",
                    "value": {
                      "error_code": "QUOTE_EXPIRED",
                      "message": "The Quote ID qo-bf27b6f2-2e8f-4c12-a301-99b4738fd6f2 has expired. Please retry with a valid Quote ID.",
                      "http_status": "400"
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
                  "$ref": "#/components/schemas/Payouts_v3_CreatePayout403Body"
                }
              }
            }
          },
          "404": {
            "description": "Not found",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Payouts_v3_Http404DataNotFound_QuoteId"
                }
              }
            }
          },
          "409": {
            "description": "Conflict",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Payouts_v3_Http409DuplicateError"
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
                "$ref": "#/components/schemas/Payouts_v3_CreateConversionRequest"
              },
              "examples": {
                "Create Conversion Example": {
                  "summary": "Create Conversion IDR to USD",
                  "value": {
                    "reference_id": "5296b95d-5cd1-4dd9-84f6-12cffd9682e1",
                    "quote_id": "qo-bf27b6f2-2e8f-4c12-a301-99b4738fd6f2"
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
      "Payouts_v3_Conversion": {
        "type": "object",
        "required": [
          "conversion_id",
          "quote_id",
          "reference_id",
          "source_amount",
          "source_currency",
          "destination_amount",
          "destination_currency",
          "fx_rate",
          "status",
          "created",
          "updated"
        ],
        "properties": {
          "conversion_id": {
            "$ref": "#/components/schemas/payouts_v3_ConversionID"
          },
          "quote_id": {
            "$ref": "#/components/schemas/payouts_v3_QuoteID"
          },
          "reference_id": {
            "type": "string",
            "example": "REF123456789"
          },
          "source_amount": {
            "type": "number",
            "example": "1000.00"
          },
          "source_currency": {
            "$ref": "#/components/schemas/Payouts_v3_PayoutCurrency",
            "example": "USD"
          },
          "destination_amount": {
            "type": "number",
            "example": "14650000.00"
          },
          "destination_currency": {
            "$ref": "#/components/schemas/Payouts_v3_PayoutCurrency",
            "example": "IDR"
          },
          "fx_rate": {
            "type": "number",
            "format": "float",
            "example": "0.000065"
          },
          "status": {
            "type": "string",
            "enum": [
              "PENDING",
              "SUCCEEDED",
              "FAILED"
            ]
          },
          "created": {
            "type": "string",
            "format": "date-time",
            "example": "2024-03-20T08:30:00Z"
          },
          "updated": {
            "type": "string",
            "format": "date-time",
            "example": "2024-03-20T08:30:00Z"
          },
          "failure_code": {
            "type": "string",
            "enum": [
              "INSUFFICIENT_BALANCE"
            ],
            "example": "INSUFFICIENT_BALANCE"
          }
        }
      },
      "Payouts_v3_CreatePayout400Body": {
        "oneOf": [
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400ApiValidationError"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400ApiValidationError_BothAmounts"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400InvalidValueError_UnsupportedSourceCurrency"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400InvalidValueError_UnsupportedDestinationCurrency"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400InvalidValueError_AmountTooLow"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400InvalidValueError_AmountTooHigh"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http400InvalidQuote"
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
      "Payouts_v3_CreatePayout403Body": {
        "oneOf": [
          {
            "$ref": "#/components/schemas/Payouts_v3_Http403RequestForbiddenError"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http403RequestForbiddenError_Account"
          },
          {
            "$ref": "#/components/schemas/Payouts_v3_Http403InvalidMerchantSettings_Payout"
          }
        ]
      },
      "Payouts_v3_Http404DataNotFound_QuoteId": {
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
              "The Quote ID specified cannot be found"
            ]
          }
        }
      },
      "Payouts_v3_Http409DuplicateError": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "DUPLICATE_ERROR"
            ]
          },
          "message": {
            "type": "string",
            "enum": [
              "A payout with this idempotency key already exists. If you meant to execute a different request, please use another idempotency key."
            ]
          }
        }
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
      "Payouts_v3_CreateConversionRequest": {
        "type": "object",
        "required": [
          "quote_id",
          "reference_id"
        ],
        "properties": {
          "quote_id": {
            "$ref": "#/components/schemas/payouts_v3_QuoteID"
          },
          "reference_id": {
            "type": "string",
            "example": "REF123456789"
          }
        }
      },
      "payouts_v3_ConversionID": {
        "type": "string",
        "pattern": "^cnv-[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
        "description": "Conversion ID in format 'cnv-<UUID>', e.g. cnv-4b2e58ca-4a75-4a83-b503-40501ee1d87e",
        "example": "cnv-123e4567-e89b-12d3-a456-426614174000"
      },
      "payouts_v3_QuoteID": {
        "type": "string",
        "pattern": "^qo-[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
        "description": "Quote ID in format 'qo-<UUID>', e.g. qo-4b2e58ca-4a75-4a83-b503-40501ee1d87e",
        "example": "qo-123e4567-e89b-12d3-a456-426614174000"
      },
      "Payouts_v3_PayoutCurrency": {
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
      "Payouts_v3_Http400InvalidValueError_UnsupportedSourceCurrency": {
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
              "The source currency specified in the request is not supported. Please check our documentation for currencies available."
            ]
          }
        }
      },
      "Payouts_v3_Http400InvalidValueError_UnsupportedDestinationCurrency": {
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
              "The destination currency specified in the request is not supported. Please check our documentation for currencies available."
            ]
          }
        }
      },
      "Payouts_v3_Http400InvalidValueError_AmountTooLow": {
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
              "The transfer amount requested is lower than the prescribed minimum for the region. Amend the transfer amount before retrying."
            ]
          }
        }
      },
      "Payouts_v3_Http400InvalidValueError_AmountTooHigh": {
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
              "The transfer amount requested is higher than the prescribed maximum for the region. Amend the transfer amount before retrying."
            ]
          }
        }
      },
      "Payouts_v3_Http400InvalidQuote": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INVALID_QUOTE"
            ]
          },
          "message": {
            "type": "string",
            "enum": [
              "This quote was created for a different transaction type. Please create a new Quote with the correct transaction type."
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
      "Payouts_v3_Http403RequestForbiddenError_Account": {
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
              "Your account is forbidden to perform this request"
            ]
          }
        }
      },
      "Payouts_v3_Http403InvalidMerchantSettings_Payout": {
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
              "Payout failed because the source currency has not been activated. Please reach out to Xendit to activate this currency before retrying."
            ]
          }
        }
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

