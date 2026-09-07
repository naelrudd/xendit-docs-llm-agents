> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Get dispute details

> Retrieve full details of a single dispute, including category, allowed evidence types, and submitted evidences. Use include_timeline=true to also receive the audit trail of state transitions.

## OpenAPI

````json GET /v1/disputes/{dispute_id}
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
    "/v1/disputes/{dispute_id}": {
      "get": {
        "tags": [
          "Disputes"
        ],
        "operationId": "getDispute",
        "summary": "Get dispute details",
        "description": "Retrieve full details of a single dispute, including category, allowed evidence types, and submitted evidences. Use include_timeline=true to also receive the audit trail of state transitions.",
        "parameters": [
          {
            "name": "dispute_id",
            "in": "path",
            "required": "true",
            "schema": {
              "type": "string"
            },
            "description": "Unique identifier of the dispute. Returned in the id field from GET /disputes or in webhook payloads."
          },
          {
            "name": "include_timeline",
            "in": "query",
            "schema": {
              "type": "boolean",
              "default": "false"
            },
            "description": "If true, embeds timeline events inside the dispute response."
          }
        ],
        "responses": {
          "200": {
            "description": "Detailed information about the dispute.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Merchant_Dispute_API_Dispute"
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
          },
          "404": {
            "description": "Dispute not found."
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
      "Merchant_Dispute_API_Dispute": {
        "type": "object",
        "required": [
          "id",
          "created_at",
          "updated_at",
          "channel_code",
          "status",
          "currency",
          "amount",
          "due_date",
          "evidences",
          "related_disputes",
          "note",
          "category",
          "payment_id",
          "reference_id"
        ],
        "properties": {
          "id": {
            "type": "string",
            "description": "Xendit-generated unique dispute identifier.",
            "example": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7"
          },
          "created_at": {
            "type": "string",
            "description": "Timestamp when the dispute was created, in ISO 8601 format.",
            "format": "date-time",
            "example": "2026-09-03T04:11:58.756Z"
          },
          "updated_at": {
            "type": "string",
            "description": "Timestamp of the last status change, in ISO 8601 format.",
            "format": "date-time",
            "example": "2026-09-03T04:14:53.499Z"
          },
          "channel_code": {
            "type": "string",
            "description": "Payment channel through which the original transaction was made.",
            "example": "CARDS"
          },
          "card_brands": {
            "type": "string",
            "description": "Card network associated with the dispute. Only present when channel_code is CARDS.",
            "example": "VISA"
          },
          "status": {
            "type": "string",
            "description": "Current lifecycle state.",
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
            "enum": [
              "EXCEEDED_DEADLINE",
              "ACCEPTED",
              "CHALLENGED",
              "WITHDRAWN",
              "ARBITRATION",
              "NEED_MORE_INFORMATION"
            ],
            "description": "Reason for the dispute outcome.",
            "example": "EXCEEDED_DEADLINE"
          },
          "currency": {
            "type": "string",
            "description": "Currency of the disputed amount, in ISO-4217 format.",
            "example": "USD"
          },
          "amount": {
            "$ref": "#/components/schemas/Merchant_Dispute_API_DisputeAmount"
          },
          "note": {
            "type": "string",
            "description": "Optional guidance message from Xendit explaining the dispute reason.",
            "nullable": "true",
            "example": "Please provide evidence of delivery."
          },
          "due_date": {
            "type": "string",
            "format": "date-time",
            "description": "The deadline to take action on this dispute.",
            "example": "2026-09-10T04:11:54.917Z"
          },
          "evidences": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Merchant_Dispute_API_EvidenceItem"
            },
            "description": "Flat list of evidence items (not grouped)."
          },
          "category": {
            "allOf": [
              {
                "$ref": "#/components/schemas/Merchant_Dispute_API_PublicDisputeCategory"
              }
            ],
            "nullable": "true",
            "description": "Dispute category with the evidence categories allowed for it. Null when the category is not set or could not be resolved."
          },
          "related_disputes": {
            "type": "array",
            "items": {
              "type": "string"
            },
            "description": "IDs of other disputes linked to the same original transaction."
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
          "timeline": {
            "type": "array",
            "description": "Only included when `include_timeline=true` query param is passed.",
            "items": {
              "$ref": "#/components/schemas/Merchant_Dispute_API_TimelineEvent"
            }
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
      },
      "Merchant_Dispute_API_EvidenceItem": {
        "type": "object",
        "required": [
          "id",
          "type",
          "category_slug",
          "created_at"
        ],
        "properties": {
          "id": {
            "type": "string",
            "description": "Xendit-generated unique identifier for this evidence item. Use in PATCH and DELETE evidence endpoints.",
            "example": "mi-dspt-evd-20d5cc8a-4ba0-4378-b96f-c4bcbb8a1d0e"
          },
          "type": {
            "type": "string",
            "description": "Evidence type. FILE indicates a file attachment. TEXT indicates inline text content.",
            "enum": [
              "FILE",
              "TEXT"
            ],
            "example": "FILE"
          },
          "category_slug": {
            "type": "string",
            "description": "Slug of the evidence category this belongs to.",
            "example": "proof_of_delivery"
          },
          "text_content": {
            "type": "string",
            "description": "The text content of this evidence item. Only present when type is TEXT.",
            "example": "The customer completed the transaction at our store."
          },
          "mime_type": {
            "type": "string",
            "description": "MIME type of the uploaded file (e.g., application/pdf, image/jpeg). Only present when type is FILE.",
            "example": "application/pdf"
          },
          "filename": {
            "type": "string",
            "description": "Original filename of the uploaded file. Only present when type is FILE.",
            "example": "receipt.pdf"
          },
          "content_hash": {
            "type": "string",
            "description": "MD5 hash of the file content, prefixed with md5:. Only present when type is FILE.",
            "example": "md5:318d5cb8146d90b9f02a9fe5809583aa"
          },
          "created_at": {
            "type": "string",
            "description": "Timestamp when this evidence item was submitted, in ISO 8601 format.",
            "format": "date-time",
            "example": "2026-09-03T04:14:53.499Z"
          }
        }
      },
      "Merchant_Dispute_API_PublicDisputeCategory": {
        "type": "object",
        "required": [
          "name",
          "allowed_evidence"
        ],
        "properties": {
          "name": {
            "type": "string",
            "description": "Slug of the dispute category.",
            "example": "fraud"
          },
          "allowed_evidence": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Merchant_Dispute_API_PublicAllowedEvidenceCategory"
            }
          }
        }
      },
      "Merchant_Dispute_API_TimelineEvent": {
        "type": "object",
        "properties": {
          "status": {
            "type": "string",
            "description": "Dispute status at the time of this event.",
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
            "description": "Reason associated with this status transition. Only populated for WON or LOST transitions.",
            "nullable": "true",
            "enum": [
              "EXCEEDED_DEADLINE",
              "ACCEPTED",
              "CHALLENGED",
              "WITHDRAWN",
              "ARBITRATION",
              "NEED_MORE_INFORMATION"
            ],
            "example": null
          },
          "actor": {
            "type": "string",
            "description": "Entity that triggered this event. MERCHANT_VIA_DASHBOARD or MERCHANT_VIA_API for merchant actions. XENDIT for internal system actions.",
            "enum": [
              "MERCHANT_VIA_DASHBOARD",
              "MERCHANT_VIA_API",
              "XENDIT"
            ],
            "example": "XENDIT"
          },
          "action": {
            "type": "string",
            "description": "Internal action name describing what occurred at this step. Provided for informational and debugging purposes.",
            "example": "SEND_TO_MERCHANT"
          },
          "note": {
            "type": "string",
            "description": "Optional message associated with this timeline event.",
            "nullable": "true",
            "example": null
          },
          "due_date": {
            "type": "string",
            "description": "Response deadline applicable at this point in the timeline.",
            "format": "date-time",
            "nullable": "true",
            "example": "2026-09-10T04:11:54.917Z"
          },
          "amount": {
            "$ref": "#/components/schemas/Merchant_Dispute_API_DisputeAmount"
          },
          "evidences": {
            "type": "array",
            "items": {
              "type": "string"
            },
            "description": "Evidence IDs associated with this event."
          },
          "timestamp": {
            "type": "string",
            "description": "When this event occurred, in ISO 8601 format.",
            "format": "date-time",
            "example": "2026-09-03T04:11:58.756Z"
          }
        }
      },
      "Merchant_Dispute_API_PublicAllowedEvidenceCategory": {
        "type": "object",
        "required": [
          "name",
          "type",
          "max_length",
          "is_recommended",
          "max_evidences"
        ],
        "properties": {
          "name": {
            "type": "string",
            "description": "Evidence category slug. Use this exact value as the multipart form field name when calling POST /v1/disputes/{dispute_id}/evidences.",
            "example": "receipt"
          },
          "type": {
            "type": "string",
            "enum": [
              "FILE",
              "TEXT"
            ],
            "description": "FILE requires a file upload; TEXT accepts inline text content.",
            "example": "FILE"
          },
          "max_length": {
            "type": "integer",
            "format": "int64",
            "description": "Maximum size for this evidence category. For FILE: maximum file size in bytes. For TEXT: maximum character count.",
            "example": "10485760"
          },
          "is_recommended": {
            "type": "boolean",
            "description": "When true, Xendit recommends submitting this evidence type to strengthen your challenge.",
            "example": "true"
          },
          "max_evidences": {
            "type": "integer",
            "description": "Maximum number of evidence items accepted for this evidence category.",
            "example": "1"
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

