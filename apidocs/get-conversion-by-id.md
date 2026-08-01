> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Conversion by ID

> Retrieve a specific Conversion using its ID

## OpenAPI

````json GET /conversions/{conversion_id}
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
    "/conversions/{conversion_id}": {
      "get": {
        "operationId": "Conversions_read",
        "summary": "Get Conversion by ID",
        "description": "Retrieve a specific Conversion using its ID",
        "parameters": [
          {
            "name": "api-version",
            "in": "header",
            "required": "true",
            "description": "The version of the API. Value: \"2025-06-06\"",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "conversion_id",
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
                  "$ref": "#/components/schemas/Payouts_v3_Conversion"
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
                  "$ref": "#/components/schemas/Payouts_v3_Http403RequestForbiddenError"
                }
              }
            }
          },
          "404": {
            "description": "Not found",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Payouts_v3_Http404DataNotFound_Quote"
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
      "Payouts_v3_Http404DataNotFound_Quote": {
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
              "Quote not found"
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

