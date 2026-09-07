> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Submit evidence via multipart upload

> Submit one or more pieces of evidence to a dispute using multipart/form-data. Each form field name is the evidence category slug (from category.allowed_evidence[].name). For FILE evidence, the field value is the file binary. The server validates its detected MIME type against the configured allowlist, which defaults to image/png, image/jpeg, and application/pdf. For TEXT evidence, the field value is the text string. Maximum 10 evidence items per request. One submission per evidence category slug. Evidence can only be submitted while the dispute is in ACTION_REQUIRED status. Submitting evidence does not automatically trigger a challenge — call POST /v1/disputes/{dispute_id}/challenge to finalize and forward your case.

## OpenAPI

````json POST /v1/disputes/{dispute_id}/evidences
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
    "/v1/disputes/{dispute_id}/evidences": {
      "post": {
        "tags": [
          "Disputes"
        ],
        "operationId": "createDisputeEvidence",
        "summary": "Submit evidence via multipart upload",
        "description": "Submit one or more pieces of evidence to a dispute using multipart/form-data. Each form field name is the evidence category slug (from category.allowed_evidence[].name). For FILE evidence, the field value is the file binary. The server validates its detected MIME type against the configured allowlist, which defaults to image/png, image/jpeg, and application/pdf. For TEXT evidence, the field value is the text string. Maximum 10 evidence items per request. One submission per evidence category slug. Evidence can only be submitted while the dispute is in ACTION_REQUIRED status. Submitting evidence does not automatically trigger a challenge — call POST /v1/disputes/{dispute_id}/challenge to finalize and forward your case.",
        "parameters": [
          {
            "name": "dispute_id",
            "in": "path",
            "required": "true",
            "schema": {
              "type": "string"
            },
            "description": "Unique identifier of the dispute to submit evidence for. The dispute must be in ACTION_REQUIRED status."
          }
        ],
        "requestBody": {
          "required": "true",
          "content": {
            "multipart/form-data": {
              "schema": {
                "type": "object",
                "description": "Each field name is an evidence category slug. File fields contain the binary file. Text fields contain the text content string.",
                "additionalProperties": {
                  "oneOf": [
                    {
                      "type": "string",
                      "format": "binary",
                      "description": "File evidence (field name = category slug, value = file binary)."
                    },
                    {
                      "type": "string",
                      "description": "Text evidence (field name = category slug, value = text content)."
                    }
                  ]
                }
              },
              "examples": {
                "file_evidence": {
                  "summary": "Single file upload",
                  "value": {
                    "ITEMIZED_RECEIPTS": "(binary file content)"
                  }
                },
                "text_evidence": {
                  "summary": "Single text evidence",
                  "value": {
                    "OFFICIAL_MERCHANT_STATEMENT": "The customer completed the transaction at our store."
                  }
                },
                "mixed_evidence": {
                  "summary": "Multiple evidence items in one request",
                  "value": {
                    "ITEMIZED_RECEIPTS": "(binary file content)",
                    "OFFICIAL_MERCHANT_STATEMENT": "Customer was present at the store."
                  }
                }
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "Evidence submission result.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Merchant_Dispute_API_AddEvidenceResponse"
                }
              }
            }
          },
          "400": {
            "description": "Evidence submission not allowed.",
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
                  "category_not_allowed": {
                    "value": {
                      "error_code": "EVIDENCE_CATEGORY_NOT_ALLOWED",
                      "message": "Evidence category 'invalid_slug' is not allowed for this dispute's category."
                    }
                  },
                  "category_limit": {
                    "value": {
                      "error_code": "CATEGORY_LIMIT_REACHED",
                      "message": "Per-category evidence limit reached for category 'proof_of_delivery'."
                    }
                  },
                  "unsupported_type": {
                    "value": {
                      "error_code": "UNSUPPORTED_EVIDENCE_TYPE",
                      "message": "File type is not supported."
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
      "Merchant_Dispute_API_AddEvidenceResponse": {
        "type": "object",
        "description": "Response for multipart evidence submission.",
        "properties": {
          "dispute_id": {
            "type": "string",
            "description": "The dispute ID for which evidence was submitted.",
            "example": "mi-dspt-48e96517-9889-4e29-a93e-d1ffae1fa366"
          },
          "evidences_succeeded": {
            "type": "array",
            "description": "Evidence items that were successfully processed.",
            "items": {
              "type": "object",
              "properties": {
                "id": {
                  "type": "string",
                  "description": "Xendit-generated identifier for this evidence item.",
                  "example": "mi-dspt-evd-20d5cc8a-4ba0-4378-b96f-c4bcbb8a1d0e"
                },
                "category_slug": {
                  "type": "string",
                  "description": "The evidence category this item was filed under.",
                  "example": "ITEMIZED_RECEIPTS"
                },
                "filename": {
                  "type": "string",
                  "description": "Original filename. Only present for FILE evidence.",
                  "example": "receipt.pdf"
                },
                "mime_type": {
                  "type": "string",
                  "description": "Detected MIME type. Only present for FILE evidence.",
                  "example": "application/pdf"
                },
                "type": {
                  "type": "string",
                  "description": "FILE or TEXT.",
                  "enum": [
                    "FILE",
                    "TEXT"
                  ],
                  "example": "FILE"
                },
                "content_hash": {
                  "type": "string",
                  "description": "MD5 integrity hash prefixed with md5:. Only present for FILE evidence.",
                  "example": "md5:318d5cb8146d90b9f02a9fe5809583aa"
                }
              }
            }
          },
          "evidences_failed": {
            "type": "array",
            "description": "Evidence items that could not be processed. Only these items need to be resubmitted after correcting the issue.",
            "items": {
              "type": "object",
              "properties": {
                "filename": {
                  "type": "string",
                  "description": "The filename of the file that failed.",
                  "example": "receipt.pdf"
                },
                "reason": {
                  "type": "string",
                  "description": "Human-readable explanation of why this item failed.",
                  "example": "File type 'text/plain' is not supported for 'receipt.pdf'."
                },
                "category_slug": {
                  "type": "string",
                  "description": "The evidence category slug that was submitted.",
                  "example": "ITEMIZED_RECEIPTS"
                },
                "error_code": {
                  "type": "string",
                  "description": "Machine-readable failure code.",
                  "example": "UNSUPPORTED_EVIDENCE_TYPE"
                }
              }
            }
          },
          "message": {
            "type": "string",
            "description": "Human-readable summary of the overall submission result.",
            "example": "Evidence processed successfully."
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

