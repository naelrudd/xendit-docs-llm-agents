> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Get List of Subscription Cycles

> Retrieves all cycles for a specific subscription plan.

## OpenAPI

````json GET /recurring/plans/{id}/cycles
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
    }
  ],
  "paths": {
    "/recurring/plans/{id}/cycles": {
      "get": {
        "tags": [
          "Subscriptions"
        ],
        "summary": "Get List of Subscription Cycles",
        "description": "Retrieves all cycles for a specific subscription plan.",
        "operationId": "listRecurringCycles",
        "parameters": [
          {
            "name": "api-version",
            "in": "header",
            "schema": {
              "example": "2026-01-01",
              "type": "string",
              "enum": [
                "2026-01-01"
              ]
            }
          },
          {
            "name": "for-user-id",
            "in": "header",
            "required": "false",
            "schema": {
              "type": "string"
            },
            "description": "The sub-account user-id to make this transaction for. This header is only used if you have access to xenPlatform.  See xenPlatform for more information.\n"
          },
          {
            "name": "with-split-rule",
            "in": "header",
            "required": "false",
            "schema": {
              "type": "string"
            },
            "description": "The XenPlatform split rule ID that will be applied to this transaction. This header is only used if you have access to xenPlatform.\n"
          },
          {
            "name": "id",
            "in": "path",
            "required": "true",
            "description": "The ID of the recurring plan.",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "limit",
            "in": "query",
            "description": "Maximum number of entities to be returned in API response",
            "required": "false",
            "schema": {
              "type": "integer",
              "default": "10",
              "minimum": "1",
              "maximum": "100"
            }
          },
          {
            "name": "before_id",
            "in": "query",
            "description": "Fetch cycles created before the creation of the cycle with this ID",
            "required": "false",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "after_id",
            "in": "query",
            "description": "Fetch cycles created after the creation of the cycle with this ID",
            "required": "false",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Successfully retrieved the recurring cycles.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "required": [
                    "data",
                    "has_more"
                  ],
                  "properties": {
                    "data": {
                      "type": "array",
                      "items": {
                        "$ref": "#/components/schemas/Xendit_Subscriptions_API_RecurringCycle"
                      }
                    },
                    "has_more": {
                      "type": "boolean"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Validation errors occurred. Safe to retry.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "error_code": {
                      "type": "string",
                      "description": "Error code identifying the issue."
                    },
                    "message": {
                      "type": "string",
                      "description": "Description of the error."
                    }
                  }
                },
                "examples": {
                  "API_VALIDATION_ERROR": {
                    "summary": "Fields or values in the payload body does not comply with our API specification.",
                    "value": {
                      "error_code": "API_VALIDATION_ERROR",
                      "message": "Check the specific error message for debugging."
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Invalid API key or unauthorized access. Safe to retry.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "error_code": {
                      "type": "string"
                    },
                    "message": {
                      "type": "string"
                    }
                  },
                  "example": {
                    "error_code": "INVALID_API_KEY",
                    "message": "API key format is invalid."
                  }
                }
              }
            }
          },
          "403": {
            "description": "Request forbidden error. Safe to retry.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "error_code": {
                      "type": "string"
                    },
                    "message": {
                      "type": "string"
                    }
                  },
                  "example": {
                    "error_code": "REQUEST_FORBIDDEN_ERROR",
                    "message": "The request is forbidden."
                  }
                }
              }
            }
          },
          "500": {
            "description": "Server error.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "error_code": {
                      "type": "string"
                    },
                    "message": {
                      "type": "string"
                    }
                  },
                  "example": {
                    "error_code": "SERVER_ERROR",
                    "message": "An unexpected error occurred. Our team has been notified and will troubleshoot the issue."
                  }
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
      "Xendit_Subscriptions_API_RecurringCycle": {
        "type": "object",
        "properties": {
          "id": {
            "type": "string",
            "description": "Xendit-generated recurring cycle ID.",
            "example": "recy_4e66b458-00b7-4ddd-9859-cce153dda097"
          },
          "type": {
            "type": "string",
            "description": "Indicates whether the cycle was charged as part of plan creation",
            "enum": [
              "SCHEDULED",
              "IMMEDIATE"
            ]
          },
          "reference_id": {
            "type": "string",
            "description": "Inherited from Plan reference_id"
          },
          "plan_id": {
            "type": "string",
            "description": "ID of the associated recurring plan.",
            "example": "repl_4e66b458-00b7-4ddd-9859-cce153dda097"
          },
          "customer_id": {
            "type": "string",
            "description": "Xendit-generated customer ID."
          },
          "cycle_number": {
            "type": "integer",
            "description": "The order of the current cycle within the plan"
          },
          "status": {
            "type": "string",
            "enum": [
              "SCHEDULED",
              "PENDING",
              "RETRYING",
              "FAILED",
              "SUCCEEDED",
              "CANCELLED"
            ],
            "description": "Status of the recurring cycle."
          },
          "attempt_details": {
            "type": "array",
            "description": "Details of any attempt actions made on the cycle.",
            "items": {
              "type": "object",
              "required": [
                "attempt_number",
                "action_number",
                "type",
                "created",
                "payment_id",
                "status",
                "failure_code",
                "next_retry_timestamp"
              ],
              "properties": {
                "attempt_number": {
                  "type": "integer",
                  "description": "Order of the attempt within the cycle. The current action belongs to this attempt.\n"
                },
                "action_number": {
                  "type": "integer",
                  "description": "Order of the action within an attempt. An attempt can have multiple actions.\nIn general, one action corresponds to one unique payment token within the same attempt.\n"
                },
                "type": {
                  "type": "string",
                  "description": "The type of payment attempt made on the cycle.\nINITIAL represents the first system generated attempt on the cycle.\nRETRY represents all subsequent system generated attempt after first attempt failed.\nFORCED represents explicit request made by the merchant to perform a payment attempt on the cycle.\nPAYMENT_LINK represents a payment link sent to the end user to solicit payment.\n",
                  "enum": [
                    "INITIAL",
                    "RETRY",
                    "FORCED",
                    "PAYMENT_LINK"
                  ]
                },
                "created": {
                  "type": "string",
                  "description": "The date time that the payment action was performed.",
                  "format": "date-time"
                },
                "payment_id": {
                  "type": "string",
                  "description": "This field used to indicate the payment ID created from cycle",
                  "example": "py-5cd39c23-89da-45f9-b316-f1e865b71b46",
                  "nullable": "true"
                },
                "payment_token_id": {
                  "type": "string",
                  "description": "The payment token ID used for this payment action.",
                  "example": "pt-f8429206-f3ea-49f0-abb4-eaa89064056e",
                  "nullable": "true"
                },
                "status": {
                  "type": "string",
                  "description": "The status of the action",
                  "enum": [
                    "SUCCEEDED",
                    "FAILED",
                    "PENDING"
                  ]
                },
                "failure_code": {
                  "type": "string",
                  "description": "If payment action encounters an error, the failure reason will be shown here.",
                  "nullable": "true"
                },
                "next_retry_timestamp": {
                  "nullable": "true",
                  "type": "string",
                  "description": "The date time that the next RETRY attempt should be created for this cycle.",
                  "format": "date-time"
                },
                "payment_session": {
                  "nullable": "true",
                  "type": "object",
                  "description": "Contains details of payment links sent to the end user.",
                  "properties": {
                    "session_id": {
                      "type": "string",
                      "description": "Payment session id created when the cycle attempt failed",
                      "example": "ps-661f87c614802d6c402cd82d"
                    },
                    "payment_link_url": {
                      "type": "string",
                      "description": "This URL will lead the end user to a checkout page to complete the payment."
                    }
                  }
                }
              }
            }
          },
          "attempt_count": {
            "type": "integer",
            "description": "number of attempts made on the cycle so far"
          },
          "forced_attempt_count": {
            "type": "integer",
            "description": "number of forced attempts made on the cycle so far"
          },
          "scheduled_timestamp": {
            "type": "string",
            "format": "date-time",
            "description": "The scheduled date and time that the cycle will be executed. Always in UTC zero.",
            "example": "2020-11-20T16:23:52Z"
          },
          "currency": {
            "type": "string",
            "description": "ISO 4217 currency code (e.g., IDR, PHP).",
            "example": "IDR"
          },
          "amount": {
            "type": "number",
            "description": "Amount charged in the cycle.",
            "minimum": "0"
          },
          "metadata": {
            "type": "object",
            "nullable": "true"
          },
          "created": {
            "type": "string",
            "format": "date-time",
            "description": "ISO 8601 date time format",
            "example": "2017-07-21T17:32:28Z"
          },
          "updated": {
            "type": "string",
            "format": "date-time",
            "description": "ISO 8601 date time format",
            "example": "2017-07-21T17:32:28Z"
          }
        }
      }
    }
  }
}
````

