> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Update text evidence

> Replace the text content of a previously submitted TEXT evidence item. Only TEXT evidence can be modified; FILE evidence must be deleted and re-uploaded. The dispute must still be in ACTION_REQUIRED status.

## OpenAPI

````json PATCH /v1/disputes/{dispute_id}/evidences/{evidence_id}
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
    "/v1/disputes/{dispute_id}/evidences/{evidence_id}": {
      "patch": {
        "tags": [
          "Disputes"
        ],
        "operationId": "updateDisputeEvidence",
        "summary": "Update text evidence",
        "description": "Replace the text content of a previously submitted TEXT evidence item. Only TEXT evidence can be modified; FILE evidence must be deleted and re-uploaded. The dispute must still be in ACTION_REQUIRED status.",
        "parameters": [
          {
            "name": "dispute_id",
            "in": "path",
            "required": "true",
            "schema": {
              "type": "string"
            },
            "description": "Unique identifier of the dispute that owns this evidence."
          },
          {
            "name": "evidence_id",
            "in": "path",
            "required": "true",
            "schema": {
              "type": "string"
            },
            "description": "Unique identifier of the evidence item to update."
          }
        ],
        "requestBody": {
          "required": "true",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "required": [
                  "text_content"
                ],
                "properties": {
                  "text_content": {
                    "type": "string",
                    "description": "Updated text content."
                  }
                }
              }
            }
          }
        },
        "responses": {
          "204": {
            "description": "Evidence text content updated successfully."
          },
          "422": {
            "description": "Evidence is not a text type.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "error_code": {
                      "type": "string",
                      "enum": [
                        "EVIDENCE_NOT_TEXT"
                      ]
                    },
                    "message": {
                      "type": "string"
                    }
                  }
                },
                "example": {
                  "error_code": "EVIDENCE_NOT_TEXT",
                  "message": "Only TEXT evidence can be updated. This evidence is of type FILE."
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
    "securitySchemes": {
      "Merchant_Dispute_API_BasicAuth": {
        "type": "http",
        "scheme": "basic"
      }
    }
  }
}
````

