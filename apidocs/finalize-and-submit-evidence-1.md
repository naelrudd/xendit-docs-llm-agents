> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Finalize and submit evidence

> Finalize and submit all uploaded evidence to contest the dispute. Once submitted, the dispute moves to UNDER_REVIEW status and evidence can no longer be added, modified, or deleted. The outcome (WON or LOST) is determined asynchronously and delivered via webhook. The dispute must be in ACTION_REQUIRED status and must have at least one evidence item.

## OpenAPI

````json POST /v1/disputes/{dispute_id}/challenge
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
    "/v1/disputes/{dispute_id}/challenge": {
      "post": {
        "tags": [
          "Disputes"
        ],
        "operationId": "challengeDispute",
        "summary": "Finalize and submit evidence",
        "description": "Finalize and submit all uploaded evidence to contest the dispute. Once submitted, the dispute moves to UNDER_REVIEW status and evidence can no longer be added, modified, or deleted. The outcome (WON or LOST) is determined asynchronously and delivered via webhook. The dispute must be in ACTION_REQUIRED status and must have at least one evidence item.",
        "parameters": [
          {
            "name": "dispute_id",
            "in": "path",
            "required": "true",
            "schema": {
              "type": "string"
            },
            "description": "Unique identifier of the dispute."
          }
        ],
        "responses": {
          "202": {
            "description": "Challenge accepted. The dispute will be processed asynchronously.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "dispute_id": {
                      "type": "string"
                    },
                    "message": {
                      "type": "string"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Action not allowed in current state.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Merchant_Dispute_API_ErrorResponse"
                },
                "examples": {
                  "illegal_state": {
                    "value": {
                      "error_code": "ILLEGAL_STATE",
                      "message": "The requested action is not allowed in the current dispute state."
                    }
                  },
                  "no_evidence": {
                    "value": {
                      "error_code": "INVALID_REQUEST",
                      "message": "No evidence items provided."
                    }
                  }
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

