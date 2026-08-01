> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Quote by ID

> Retrieve a specific Quote using its ID

## OpenAPI

````json GET /quotes/{quote_id}
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
    "/quotes/{quote_id}": {
      "get": {
        "operationId": "Quotes_read",
        "summary": "Get Quote by ID",
        "description": "Retrieve a specific Quote using its ID",
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
            "name": "quote_id",
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
                  "$ref": "#/components/schemas/Payouts_v3_Quote"
                },
                "examples": {
                  "Get Quote PHP to THB": {
                    "summary": "Get Quote PHP to THB",
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
                  "Get Quote by ID": {
                    "summary": "Get Quote by ID",
                    "value": {
                      "quote_id": "qo-e08492aa-d872-4c49-9fcf-c271480dbdc0",
                      "reference_id": "179d2fbc-e0c2-467d-8acd-b0b7cc4ee3f8",
                      "source_amount": "100000",
                      "source_currency": "IDR",
                      "destination_amount": "626",
                      "destination_currency": "USD",
                      "fx_rate": "0.000063",
                      "type": "PAYOUT",
                      "created": "2025-06-02T16:01:15.982Z",
                      "updated": "2025-06-02T16:01:15.982Z",
                      "expires": "2025-06-02T16:01:45.967Z"
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

