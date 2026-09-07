> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Delete a submitted evidence

> Remove a previously submitted evidence item from a dispute. The dispute must still be in ACTION_REQUIRED status. Deleted evidence cannot be recovered.

## OpenAPI

````json DELETE /v1/disputes/{dispute_id}/evidences/{evidence_id}
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
      "delete": {
        "tags": [
          "Disputes"
        ],
        "operationId": "deleteDisputeEvidence",
        "summary": "Delete a submitted evidence",
        "description": "Remove a previously submitted evidence item from a dispute. The dispute must still be in ACTION_REQUIRED status. Deleted evidence cannot be recovered.",
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
            "description": "Unique identifier of the evidence item to delete."
          }
        ],
        "responses": {
          "204": {
            "description": "Evidence deleted successfully."
          },
          "400": {
            "description": "Action not allowed in current state.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Merchant_Dispute_API_ErrorResponse"
                },
                "example": {
                  "error_code": "ILLEGAL_STATE",
                  "message": "The requested action is not allowed in the current dispute state."
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

