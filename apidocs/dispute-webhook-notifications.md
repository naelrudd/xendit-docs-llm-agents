> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Dispute Webhook Notifications

> Xendit sends a POST request to your configured endpoint whenever a dispute status changes. The payload includes the event name alongside the dispute object.

## OpenAPI

````json POST /your_dispute_webhook_url
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
    "/your_dispute_webhook_url": {
      "post": {
        "tags": [
          "Disputes"
        ],
        "operationId": "disputeWebhook",
        "summary": "Dispute Webhook Notifications",
        "description": "Xendit sends a POST request to your configured endpoint whenever a dispute status changes. The payload includes the event name alongside the dispute object.",
        "parameters": [
          {
            "$ref": "#/components/parameters/Merchant_Dispute_API_XCallbackToken"
          }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/Merchant_Dispute_API_WebhookEvent"
              },
              "examples": {
                "dispute_action_required": {
                  "summary": "New Dispute - Action Required",
                  "value": {
                    "event": "dispute.action_required",
                    "id": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7",
                    "channel_code": "CARDS",
                    "card_brands": "VISA",
                    "status": "ACTION_REQUIRED",
                    "currency": "USD",
                    "amount": {
                      "initial": "1000.00",
                      "terminal": null
                    },
                    "created_at": "2026-03-01T19:50:51.724Z",
                    "updated_at": "2026-03-01T19:50:51.724Z",
                    "due_date": "2026-03-15T19:50:51.724Z",
                    "note": "Please provide evidence of delivery.",
                    "category": {
                      "name": "fraud",
                      "allowed_evidence": [
                        {
                          "name": "proof_of_delivery",
                          "type": "FILE",
                          "max_length": "5242880",
                          "is_recommended": "true",
                          "max_evidences": "3"
                        },
                        {
                          "name": "explanation",
                          "type": "TEXT",
                          "max_length": "255",
                          "is_recommended": "false",
                          "max_evidences": "3"
                        }
                      ]
                    },
                    "related_disputes": [],
                    "payment_id": "py-59a3cf39-2a7d-4733-a3e3-8177c78090f7",
                    "reference_id": "ref-123456"
                  }
                },
                "dispute_under_review": {
                  "summary": "Dispute Under Review",
                  "value": {
                    "event": "dispute.under_review",
                    "id": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7",
                    "channel_code": "CARDS",
                    "card_brands": "VISA",
                    "status": "UNDER_REVIEW",
                    "currency": "USD",
                    "amount": {
                      "initial": "1000.00",
                      "terminal": null
                    },
                    "created_at": "2026-03-01T19:50:51.724Z",
                    "updated_at": "2026-03-05T10:30:00Z",
                    "due_date": "2026-03-15T19:50:51.724Z",
                    "note": "Please provide evidence of delivery.",
                    "category": {
                      "name": "fraud",
                      "allowed_evidence": [
                        {
                          "name": "proof_of_delivery",
                          "type": "FILE",
                          "max_length": "5242880",
                          "is_recommended": "true",
                          "max_evidences": "3"
                        },
                        {
                          "name": "explanation",
                          "type": "TEXT",
                          "max_length": "255",
                          "is_recommended": "false",
                          "max_evidences": "3"
                        }
                      ]
                    },
                    "evidences": [
                      {
                        "id": "mi-dspt-evd-12345",
                        "type": "FILE",
                        "category_slug": "proof_of_delivery",
                        "filename": "delivery_receipt.pdf",
                        "mime_type": "application/pdf"
                      }
                    ],
                    "related_disputes": [],
                    "payment_id": "py-59a3cf39-2a7d-4733-a3e3-8177c78090f7",
                    "reference_id": "ref-123456"
                  }
                },
                "dispute_won": {
                  "summary": "Dispute Won",
                  "value": {
                    "event": "dispute.won",
                    "id": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7",
                    "channel_code": "CARDS",
                    "card_brands": "VISA",
                    "status": "WON",
                    "status_reason": "CHALLENGED",
                    "currency": "USD",
                    "amount": {
                      "initial": "1000.00",
                      "terminal": null
                    },
                    "created_at": "2026-03-01T19:50:51.724Z",
                    "updated_at": "2026-03-20T14:00:00Z",
                    "due_date": "2026-03-15T19:50:51.724Z",
                    "category": {
                      "name": "fraud",
                      "allowed_evidence": [
                        {
                          "name": "proof_of_delivery",
                          "type": "FILE",
                          "max_length": "5242880",
                          "is_recommended": "true",
                          "max_evidences": "3"
                        },
                        {
                          "name": "explanation",
                          "type": "TEXT",
                          "max_length": "255",
                          "is_recommended": "false",
                          "max_evidences": "3"
                        }
                      ]
                    },
                    "evidences": [
                      {
                        "id": "mi-dspt-evd-12345",
                        "type": "FILE",
                        "category_slug": "proof_of_delivery",
                        "filename": "delivery_receipt.pdf",
                        "mime_type": "application/pdf"
                      }
                    ],
                    "related_disputes": [],
                    "payment_id": "py-59a3cf39-2a7d-4733-a3e3-8177c78090f7",
                    "reference_id": "ref-123456"
                  }
                },
                "dispute_lost": {
                  "summary": "Dispute Lost",
                  "value": {
                    "event": "dispute.lost",
                    "id": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7",
                    "channel_code": "CARDS",
                    "card_brands": "VISA",
                    "status": "LOST",
                    "status_reason": "EXCEEDED_DEADLINE",
                    "currency": "USD",
                    "amount": {
                      "initial": "1000.00",
                      "terminal": null
                    },
                    "created_at": "2026-03-01T19:50:51.724Z",
                    "updated_at": "2026-03-20T14:00:00Z",
                    "due_date": "2026-03-15T19:50:51.724Z",
                    "note": "Please provide evidence of delivery.",
                    "category": {
                      "name": "fraud",
                      "allowed_evidence": [
                        {
                          "name": "proof_of_delivery",
                          "type": "FILE",
                          "max_length": "5242880",
                          "is_recommended": "true",
                          "max_evidences": "3"
                        },
                        {
                          "name": "explanation",
                          "type": "TEXT",
                          "max_length": "255",
                          "is_recommended": "false",
                          "max_evidences": "3"
                        }
                      ]
                    },
                    "evidences": [
                      {
                        "id": "mi-dspt-evd-12345",
                        "type": "FILE",
                        "category_slug": "proof_of_delivery",
                        "filename": "delivery_receipt.pdf",
                        "mime_type": "application/pdf"
                      }
                    ],
                    "related_disputes": [],
                    "payment_id": "py-59a3cf39-2a7d-4733-a3e3-8177c78090f7",
                    "reference_id": "ref-123456"
                  }
                },
                "dispute_due_date_approaching": {
                  "summary": "Dispute Due Date Approaching",
                  "value": {
                    "event": "dispute.due_date_approaching",
                    "id": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7",
                    "channel_code": "CARDS",
                    "card_brands": "VISA",
                    "status": "ACTION_REQUIRED",
                    "currency": "USD",
                    "amount": {
                      "initial": "1000.00",
                      "terminal": null
                    },
                    "created_at": "2026-03-01T19:50:51.724Z",
                    "updated_at": "2026-03-13T08:00:00Z",
                    "due_date": "2026-03-15T19:50:51.724Z",
                    "category": {
                      "name": "fraud",
                      "allowed_evidence": [
                        {
                          "name": "proof_of_delivery",
                          "type": "FILE",
                          "max_length": "5242880",
                          "is_recommended": "true",
                          "max_evidences": "3"
                        },
                        {
                          "name": "explanation",
                          "type": "TEXT",
                          "max_length": "255",
                          "is_recommended": "false",
                          "max_evidences": "3"
                        }
                      ]
                    },
                    "related_disputes": [],
                    "payment_id": "py-59a3cf39-2a7d-4733-a3e3-8177c78090f7",
                    "reference_id": "ref-123456"
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OK. The webhook was received and processed."
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
    "parameters": {
      "Merchant_Dispute_API_XCallbackToken": {
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
      "Merchant_Dispute_API_WebhookEvent": {
        "type": "object",
        "x-callback-object": "true",
        "required": [
          "event",
          "id",
          "channel_code",
          "status",
          "currency",
          "amount",
          "created_at",
          "updated_at",
          "due_date",
          "related_disputes"
        ],
        "properties": {
          "event": {
            "type": "string",
            "enum": [
              "dispute.action_required",
              "dispute.under_review",
              "dispute.won",
              "dispute.lost",
              "dispute.due_date_approaching"
            ],
            "description": "The specific lifecycle event. dispute.action_required: dispute raised, response required. dispute.under_review: challenge submitted. dispute.won: ruled in your favor. dispute.lost: ruled against you. dispute.due_date_approaching: deadline is near.",
            "example": "dispute.action_required"
          },
          "id": {
            "type": "string",
            "description": "Unique dispute identifier.",
            "example": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7"
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
            "description": "Dispute status at the time this webhook was fired.",
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
          "created_at": {
            "type": "string",
            "format": "date-time",
            "example": "2026-09-03T04:11:58.756Z"
          },
          "updated_at": {
            "type": "string",
            "format": "date-time",
            "example": "2026-09-03T04:14:53.499Z"
          },
          "due_date": {
            "type": "string",
            "description": "Response deadline for this dispute.",
            "format": "date-time",
            "example": "2026-09-10T04:11:54.917Z"
          },
          "note": {
            "type": "string",
            "description": "Optional guidance message from Xendit explaining the dispute.",
            "nullable": "true",
            "example": null
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
            }
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
          "evidences": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Merchant_Dispute_API_EvidenceItem"
            },
            "description": "Flat list of evidence items (not grouped)."
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

