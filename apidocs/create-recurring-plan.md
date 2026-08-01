> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Subscription Plan

> Creates a new subscription plan for managing subscription payments.

## OpenAPI

````json POST /recurring/plans
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
    "/recurring/plans": {
      "post": {
        "tags": [
          "Subscriptions"
        ],
        "summary": "Create Subscription Plan",
        "description": "Creates a new subscription plan for managing subscription payments.",
        "operationId": "createRecurringPlan",
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
          }
        ],
        "requestBody": {
          "description": "JSON object containing recurring plan details.",
          "required": "true",
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/Xendit_Subscriptions_API_RecurringPlan"
              }
            }
          }
        },
        "responses": {
          "202": {
            "description": "Successfully created a recurring plan. A webhook will follow to confirm plan activation.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Xendit_Subscriptions_API_RecurringPlanResponse"
                }
              }
            }
          },
          "400": {
            "description": "Validation errors occurred.",
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
                  },
                  "INVALID_PAYMENT_TOKEN_ID": {
                    "summary": "Payment token ID is not in eligible status for plan creation.",
                    "value": {
                      "error_code": "INVALID_PAYMENT_TOKEN_ID",
                      "message": "The payment_token_id provided has a mismatched currency or it is not \"ACTIVE\" because it has expired/ been unlinked/ linking has not been completed. Please retry with a valid payment_token_id."
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Invalid API key or unauthorized access.",
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
            "description": "Request forbidden error.",
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
          "404": {
            "description": "Resource not found.",
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
                  }
                },
                "examples": {
                  "CUSTOMER_NOT_FOUND": {
                    "summary": "Customer not found.",
                    "value": {
                      "error_code": "CUSTOMER_NOT_FOUND_ERROR",
                      "message": "customer_id is invalid or not found. Please try again with a valid customer_id."
                    }
                  }
                }
              }
            }
          },
          "409": {
            "description": "Idempotency error.",
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
                    "error_code": "IDEMPOTENCY_ERROR",
                    "message": "Idempotency key has been used before."
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
          },
          "503": {
            "description": "Payment server error.",
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
                    "error_code": "CHANNEL_UNAVAILABLE",
                    "message": "The payment channel is currently unavailable. Please try again later."
                  }
                }
              }
            }
          }
        },
        "callbacks": {
          "recurringPlan": {
            "/{merchant defined callback url}": {
              "post": {
                "summary": "Recurring Plan Webhook",
                "description": "Webhooks sent for recurring plan status updates:\n- `recurring.plan.activated`: Sent when a recurring plan is successfully activated. This webhook includes both the plan and the first cycle details.\n- `recurring.plan.inactivated`: Sent when a recurring plan is deactivated, either by merchant request or due to failed cycles when failed_cycle_action is STOP.\n",
                "requestBody": {
                  "description": "Recurring plan webhook payload",
                  "content": {
                    "application/json": {
                      "schema": {
                        "$ref": "#/components/schemas/Xendit_Subscriptions_API_RecurringPlanWebhook"
                      }
                    }
                  }
                },
                "responses": {
                  "200": {
                    "description": "OK"
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
      "Xendit_Subscriptions_API_RecurringPlan": {
        "type": "object",
        "required": [
          "reference_id",
          "customer_id",
          "currency",
          "amount",
          "payment_tokens",
          "schedule"
        ],
        "properties": {
          "reference_id": {
            "type": "string",
            "description": "Merchant-provided identifier for the recurring plan.",
            "minLength": "1",
            "example": "my-plan-01"
          },
          "customer_id": {
            "type": "string",
            "description": "Xendit-generated customer ID."
          },
          "currency": {
            "type": "string",
            "description": "ISO 4217 currency code (e.g., IDR, PHP).",
            "example": "IDR"
          },
          "amount": {
            "type": "number",
            "description": "Amount to be charged in each recurring cycle.",
            "minimum": "0"
          },
          "schedule": {
            "$ref": "#/components/schemas/Xendit_Subscriptions_API_RecurringScheduleCreate"
          },
          "payment_tokens": {
            "type": "array",
            "minItems": "0",
            "maxItems": "5",
            "items": {
              "type": "object",
              "required": [
                "payment_token_id",
                "rank"
              ],
              "properties": {
                "payment_token_id": {
                  "type": "string",
                  "description": "ID for payment token.",
                  "example": "pt-f8429206-f3ea-49f0-abb4-eaa89064056e"
                },
                "rank": {
                  "type": "integer",
                  "description": "Order in which payment tokens will be attempted (1 to 5).",
                  "minimum": "1",
                  "maximum": "5"
                }
              }
            }
          },
          "immediate_payment": {
            "type": "boolean",
            "default": "false",
            "description": "Payment taken upon recurring plan creation. Failing the payment will inactivate the plan."
          },
          "failed_cycle_action": {
            "type": "string",
            "enum": [
              "RESUME",
              "STOP"
            ],
            "description": "Determines if the plan should be terminated when a cycle fails. RESUME continues, STOP inactivates the plan.",
            "default": "RESUME"
          },
          "notification_channels": {
            "type": "array",
            "items": {
              "type": "string",
              "enum": [
                "WHATSAPP",
                "EMAIL"
              ]
            },
            "description": "Channels to notify end user."
          },
          "locale": {
            "type": "string",
            "description": "ISO 639-1 two-letter codes for language of notifications to be sent to end user",
            "default": "en"
          },
          "payment_link_for_failed_attempt": {
            "type": "boolean",
            "description": "Whether a payment link is generated for failed cycle attempts.",
            "default": "false"
          },
          "metadata": {
            "type": "object",
            "nullable": "true",
            "additionalProperties": {
              "type": "string"
            },
            "description": "Additional JSON properties. Max 20 keys, with key names up to 40 characters and values up to 80 characters.",
            "example": {
              "customKey": "customValue"
            }
          },
          "description": {
            "type": "string",
            "description": "Custom description of the recurring plan.",
            "example": "My newspaper subscription 01",
            "nullable": "true",
            "maxLength": "1000"
          },
          "items": {
            "type": "array",
            "nullable": "true",
            "description": "Details of items included in the recurring plan.",
            "items": {
              "$ref": "#/components/schemas/Xendit_Subscriptions_API_BasketItem"
            }
          }
        }
      },
      "Xendit_Subscriptions_API_RecurringPlanResponse": {
        "allOf": [
          {
            "$ref": "#/components/schemas/Xendit_Subscriptions_API_RecurringPlan"
          },
          {
            "type": "object",
            "properties": {
              "id": {
                "type": "string",
                "description": "Xendit-generated recurring plan ID.",
                "example": "repl_4e66b458-00b7-4ddd-9859-cce153dda097"
              },
              "status": {
                "type": "string",
                "enum": [
                  "ACTIVE",
                  "INACTIVE",
                  "PENDING",
                  "REQUIRES_ACTION"
                ],
                "description": "Status of the recurring plan."
              },
              "failure_code": {
                "type": "string",
                "nullable": "true",
                "description": "Failure code for failed plan creation",
                "example": "UNPROCESSABLE_ENTITY_ERROR"
              },
              "country": {
                "type": "string",
                "nullable": "true",
                "description": "Country code for the plan",
                "example": "ID"
              },
              "payment_session_id": {
                "type": "string",
                "nullable": "true",
                "description": "Payment session ID for plans that require account linking",
                "example": "ps-661f87c614802d6c402cd82d"
              },
              "recurring_cycle_count": {
                "type": "integer",
                "description": "Number of cycles generated for this plan."
              },
              "schedule": {
                "$ref": "#/components/schemas/Xendit_Subscriptions_API_RecurringSchedule"
              },
              "payment_tokens": {
                "type": "array",
                "minItems": "0",
                "maxItems": "5",
                "items": {
                  "type": "object",
                  "required": [
                    "payment_token_id",
                    "rank"
                  ],
                  "properties": {
                    "payment_token_id": {
                      "type": "string",
                      "example": "pt-f8429206-f3ea-49f0-abb4-eaa89064056e"
                    },
                    "rank": {
                      "type": "integer",
                      "minimum": "1",
                      "maximum": "5"
                    }
                  }
                }
              },
              "actions": {
                "type": "array",
                "description": "Array of objects containing URLs for end users to complete the recurring plan.",
                "items": {
                  "type": "object",
                  "required": [
                    "action"
                  ],
                  "properties": {
                    "action": {
                      "type": "string",
                      "description": "Describes the purpose of the action. `AUTH` triggers payment account linking."
                    },
                    "url_type": {
                      "type": "string",
                      "enum": [
                        "WEB"
                      ],
                      "description": "Type of URL, optimized for desktop or web interface."
                    },
                    "url": {
                      "type": "string",
                      "format": "uri",
                      "description": "Generated URL to perform the action."
                    },
                    "method": {
                      "type": "string",
                      "enum": [
                        "GET",
                        "POST"
                      ],
                      "description": "HTTP method for calling the URL."
                    }
                  }
                }
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
        ]
      },
      "Xendit_Subscriptions_API_RecurringPlanWebhook": {
        "type": "object",
        "required": [
          "event",
          "business_id",
          "created",
          "data"
        ],
        "description": "Webhook payload sent for recurring plan status updates.\n- `recurring.plan.activated`: Sent when a recurring plan is successfully activated.\n- `recurring.plan.inactivated`: Sent when a recurring plan is deactivated.\n\nNote: When a plan is activated, a separate `recurring.cycle.created` webhook is also sent for the first cycle.\n",
        "properties": {
          "event": {
            "type": "string",
            "enum": [
              "recurring.plan.activated",
              "recurring.plan.inactivated"
            ],
            "description": "Webhook event names for recurring plan status updates.\n",
            "example": "recurring.plan.activated"
          },
          "business_id": {
            "type": "string",
            "description": "Business ID of Xendit.",
            "example": "62440e322008e87fb29c1fd0"
          },
          "created": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp of webhook delivery attempt in ISO 8601 date-time format.",
            "example": "2021-12-31T23:59:59Z"
          },
          "api_version": {
            "type": "string",
            "description": "API version used for this webhook.",
            "example": "2026-01-01"
          },
          "data": {
            "$ref": "#/components/schemas/Xendit_Subscriptions_API_RecurringPlanResponse"
          }
        }
      },
      "Xendit_Subscriptions_API_RecurringScheduleCreate": {
        "type": "object",
        "required": [
          "interval",
          "interval_count",
          "anchor_date"
        ],
        "properties": {
          "interval": {
            "type": "string",
            "enum": [
              "DAY",
              "WEEK",
              "MONTH",
              "YEAR"
            ],
            "description": "Frequency of the recurring cycles."
          },
          "interval_count": {
            "type": "integer",
            "description": "Number of intervals between consecutive cycles.",
            "minimum": "1",
            "maximum": "365"
          },
          "total_recurrence": {
            "type": "integer",
            "nullable": "true",
            "description": "Total number of cycles (optional; runs indefinitely if null).",
            "minimum": "1",
            "maximum": "32000"
          },
          "anchor_date": {
            "type": "string",
            "format": "date-time",
            "description": "Start date for the recurring schedule (ISO 8601 format), max allowed day of the month is 28. Supports time offset and UTC zero.",
            "example": "2020-11-20T16:23:52+00:00"
          },
          "retry_interval": {
            "type": "string",
            "nullable": "true",
            "description": "Interval between retry attempts for failed payments.",
            "enum": [
              "DAY",
              null
            ]
          },
          "retry_interval_count": {
            "type": "integer",
            "nullable": "true",
            "description": "Number of retry intervals between consecutive retries.",
            "minimum": "1",
            "maximum": "365"
          },
          "total_retry": {
            "type": "integer",
            "nullable": "true",
            "description": "Maximum number of retries for failed cycles.",
            "minimum": "1",
            "maximum": "10"
          },
          "failed_attempt_notifications": {
            "type": "array",
            "items": {
              "type": "integer",
              "minimum": "1",
              "maximum": "10"
            },
            "description": "Notifications triggered at specific retry attempts.",
            "example": [
              "1",
              "3",
              "5"
            ]
          }
        }
      },
      "Xendit_Subscriptions_API_BasketItem": {
        "type": "object",
        "required": [
          "reference_id",
          "type",
          "name",
          "net_unit_amount",
          "quantity",
          "category"
        ],
        "properties": {
          "type": {
            "type": "string",
            "enum": [
              "DIGITAL_PRODUCT",
              "PHYSICAL_PRODUCT",
              "DIGITAL_SERVICE",
              "PHYSICAL_SERVICE",
              "FEE"
            ],
            "description": "Type of item."
          },
          "reference_id": {
            "type": "string",
            "minLength": "1",
            "maxLength": "255",
            "example": "my-plan-01"
          },
          "name": {
            "type": "string",
            "description": "Name of the item.",
            "example": "Granny Smith Apple",
            "minLength": "1",
            "maxLength": "255"
          },
          "net_unit_amount": {
            "type": "number",
            "description": "Net amount charged per unit. Negative values for discounts."
          },
          "quantity": {
            "type": "integer",
            "description": "Number of units of the item."
          },
          "url": {
            "type": "string",
            "nullable": "true",
            "description": "URL of the item, must be HTTPS or HTTP.",
            "pattern": "^https?:\\/\\/.+"
          },
          "category": {
            "type": "string",
            "description": "Merchant category for the item.",
            "example": "Food",
            "maxLength": "255"
          },
          "subcategory": {
            "type": "string",
            "description": "Subcategory for the item.",
            "example": "Fruits",
            "nullable": "true",
            "maxLength": "255"
          },
          "description": {
            "type": "string",
            "description": "Description of the item.",
            "example": "Green apple that is a little sour.",
            "nullable": "true",
            "maxLength": "255"
          },
          "metadata": {
            "type": "object",
            "description": "Additional JSON properties. Max 20 keys, with key names up to 40 characters and values up to 80 characters.",
            "nullable": "true",
            "additionalProperties": {
              "type": "string"
            }
          }
        }
      },
      "Xendit_Subscriptions_API_RecurringSchedule": {
        "type": "object",
        "required": [
          "interval",
          "interval_count",
          "total_recurrence",
          "anchor_date",
          "retry_interval",
          "retry_interval_count",
          "total_retry",
          "failed_attempt_notifications",
          "created",
          "updated"
        ],
        "properties": {
          "interval": {
            "type": "string",
            "enum": [
              "DAY",
              "WEEK",
              "MONTH",
              "YEAR"
            ],
            "description": "Frequency of the recurring cycles."
          },
          "interval_count": {
            "type": "integer",
            "description": "Number of intervals between consecutive cycles.",
            "minimum": "1",
            "maximum": "365"
          },
          "total_recurrence": {
            "type": "integer",
            "nullable": "true",
            "description": "Total number of cycles (optional; runs indefinitely if null).",
            "minimum": "1",
            "maximum": "32000"
          },
          "anchor_date": {
            "type": "string",
            "format": "date-time",
            "description": "Start date for the recurring schedule (ISO 8601 format), max allowed day of the month is 28. Supports time offset and UTC zero.",
            "example": "2020-11-20T16:23:52+00:00"
          },
          "retry_interval": {
            "type": "string",
            "nullable": "true",
            "description": "Interval between retry attempts for failed payments."
          },
          "retry_interval_count": {
            "type": "integer",
            "nullable": "true",
            "description": "Number of retry intervals between consecutive retries.",
            "minimum": "1",
            "maximum": "365"
          },
          "total_retry": {
            "type": "integer",
            "nullable": "true",
            "description": "Maximum number of retries for failed cycles.",
            "minimum": "1",
            "maximum": "10"
          },
          "failed_attempt_notifications": {
            "type": "array",
            "items": {
              "type": "integer",
              "minimum": "1",
              "maximum": "10"
            },
            "description": "Notifications triggered at specific retry attempts.",
            "example": [
              "1",
              "3",
              "5"
            ]
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

