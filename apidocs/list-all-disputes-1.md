> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# List all disputes

> Retrieve a paginated list of disputes associated with the Business ID.

## OpenAPI

````json GET /v1/disputes
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
    "/v1/disputes": {
      "get": {
        "tags": [
          "Disputes"
        ],
        "operationId": "listDisputes",
        "summary": "List all disputes",
        "description": "Retrieve a paginated list of disputes associated with the Business ID.",
        "parameters": [
          {
            "name": "limit",
            "in": "query",
            "description": "Number of disputes to return per page. Defaults to 10, maximum 100.",
            "schema": {
              "type": "integer",
              "default": "10",
              "maximum": "100"
            }
          },
          {
            "name": "cursor",
            "in": "query",
            "description": "Dispute ID from pagination.next_cursor for fetching the next page.",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "status",
            "in": "query",
            "description": "Filter disputes by lifecycle status. Use ACTION_REQUIRED to find disputes requiring your response.",
            "schema": {
              "type": "string",
              "enum": [
                "ACTION_REQUIRED",
                "UNDER_REVIEW",
                "WON",
                "LOST"
              ]
            }
          },
          {
            "name": "payment_id",
            "in": "query",
            "description": "Filter disputes by a specific Payment ID.",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "channel_code",
            "in": "query",
            "description": "Filter disputes by payment channel (e.g., CARDS, QRIS).",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "card_brands",
            "in": "query",
            "description": "Filter card disputes by card network (e.g., VISA, MASTERCARD). Only applicable when channel_code is CARDS.",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "currency",
            "in": "query",
            "description": "Filter disputes by currency using ISO-4217 currency code (e.g., IDR, PHP, USD).",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "created_after",
            "in": "query",
            "description": "Return only disputes created after this timestamp (ISO 8601 format).",
            "schema": {
              "type": "string",
              "format": "date-time"
            }
          },
          {
            "name": "created_before",
            "in": "query",
            "description": "Return only disputes created before this timestamp (ISO 8601 format).",
            "schema": {
              "type": "string",
              "format": "date-time"
            }
          },
          {
            "name": "due_date_after",
            "in": "query",
            "description": "Return only disputes with a response deadline after this timestamp (ISO 8601 format).",
            "schema": {
              "type": "string",
              "format": "date-time"
            }
          },
          {
            "name": "due_date_before",
            "in": "query",
            "description": "Return only disputes with a response deadline before this timestamp. Use this to surface disputes expiring soon.",
            "schema": {
              "type": "string",
              "format": "date-time"
            }
          },
          {
            "name": "search",
            "in": "query",
            "description": "Full-text search across dispute ID, payment ID, and reference ID.",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "A list of disputes.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "data": {
                      "type": "array",
                      "items": {
                        "$ref": "#/components/schemas/Merchant_Dispute_API_DisputeListItem"
                      }
                    },
                    "pagination": {
                      "$ref": "#/components/schemas/Merchant_Dispute_API_Pagination"
                    }
                  }
                }
              }
            }
          },
          "403": {
            "description": "Access not allowed for this business.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Merchant_Dispute_API_ErrorResponse"
                },
                "example": {
                  "error_code": "RESTRICTED_ACCESS",
                  "message": "Access to this resource is restricted."
                }
              }
            }
          }
        },
        "security": [
          {
            "Merchant_Dispute_API_BasicAuth": []
          }
        ]
      }
    }
  },
  "components": {
    "schemas": {
      "Merchant_Dispute_API_DisputeListItem": {
        "type": "object",
        "required": [
          "id",
          "status",
          "status_reason",
          "channel_code",
          "currency",
          "amount",
          "due_date",
          "category",
          "note",
          "payment_id",
          "reference_id",
          "created_at",
          "updated_at"
        ],
        "description": "Minimal dispute representation for list responses.",
        "properties": {
          "id": {
            "type": "string",
            "description": "Xendit-generated unique dispute identifier.",
            "example": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7"
          },
          "status": {
            "type": "string",
            "description": "Current lifecycle state. ACTION_REQUIRED means a response is needed before due_date.",
            "enum": [
              "ACTION_REQUIRED",
              "UNDER_REVIEW",
              "WON",
              "LOST"
            ],
            "example": "ACTION_REQUIRED"
          },
          "status_reason": {
            "type": "string",
            "description": "Reason for the terminal outcome. Only populated when status is WON or LOST.",
            "nullable": "true",
            "enum": [
              "EXCEEDED_DEADLINE",
              "ACCEPTED",
              "CHALLENGED",
              "WITHDRAWN",
              "ARBITRATION",
              "NEED_MORE_INFORMATION"
            ],
            "example": "EXCEEDED_DEADLINE"
          },
          "channel_code": {
            "type": "string",
            "description": "Payment channel through which the original transaction was made (e.g., CARDS, QRIS).",
            "example": "CARDS"
          },
          "card_brands": {
            "type": "string",
            "description": "Card network associated with the dispute. Only present when channel_code is CARDS.",
            "example": "VISA"
          },
          "currency": {
            "type": "string",
            "description": "Currency of the disputed amount, in ISO-4217 format.",
            "example": "USD"
          },
          "amount": {
            "$ref": "#/components/schemas/Merchant_Dispute_API_DisputeAmount"
          },
          "due_date": {
            "type": "string",
            "description": "Deadline by which you must respond to avoid an automatic LOST outcome.",
            "format": "date-time",
            "example": "2026-09-10T04:11:54.917Z"
          },
          "note": {
            "type": "string",
            "description": "Optional message from Xendit providing guidance on the dispute.",
            "nullable": "true",
            "example": null
          },
          "category": {
            "type": "string",
            "description": "Slug identifier of the dispute category. The full category object with allowed evidence types is available in GET /v1/disputes/{dispute_id}.",
            "example": "fraudulent"
          },
          "payment_id": {
            "type": "string",
            "description": "Xendit payment identifier for the original disputed transaction.",
            "nullable": "true",
            "example": "py-59a3cf39-2a7d-4733-a3e3-8177c78090f7"
          },
          "reference_id": {
            "type": "string",
            "nullable": "true",
            "description": "Your reference ID for the original transaction.",
            "example": "dispute-test-1788408708890"
          },
          "created_at": {
            "type": "string",
            "description": "Timestamp when the dispute was created, in ISO 8601 format.",
            "format": "date-time",
            "example": "2026-09-03T04:11:58.756Z"
          },
          "updated_at": {
            "type": "string",
            "description": "Timestamp of the most recent update, in ISO 8601 format.",
            "format": "date-time",
            "example": "2026-09-03T04:14:53.499Z"
          }
        }
      },
      "Merchant_Dispute_API_Pagination": {
        "type": "object",
        "properties": {
          "next_cursor": {
            "type": "string",
            "nullable": "true",
            "description": "The ID of the last dispute in the current page. Pass as the `cursor` query parameter to fetch the next page. Null when there are no more results.",
            "example": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7"
          },
          "has_more": {
            "type": "boolean",
            "description": "Whether there are more results beyond this page.",
            "example": "true"
          }
        }
      },
      "Merchant_Dispute_API_ErrorResponse": {
        "type": "object",
        "properties": {
          "error_code": {
            "type": "string",
            "example": "ILLEGAL_STATE"
          },
          "message": {
            "type": "string",
            "example": "The requested action is not allowed in the current dispute state."
          }
        }
      },
      "Merchant_Dispute_API_DisputeAmount": {
        "type": "object",
        "properties": {
          "initial": {
            "type": "string",
            "description": "The amount when the dispute was first raised.",
            "example": "1000.00"
          },
          "terminal": {
            "type": "string",
            "nullable": "true",
            "description": "The final resolved amount. May differ from initial for partial disputes. Null while unresolved.",
            "example": "1000.00"
          }
        }
      }
    },
    "securitySchemes": {
      "Merchant_Dispute_API_BasicAuth": {
        "type": "http",
        "scheme": "basic"
      }
    }
  }
}
````

