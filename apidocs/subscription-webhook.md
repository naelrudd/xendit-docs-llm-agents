> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Subscription Webhook

> Endpoint to receive webhook notifications for subscription events. 
Xendit will send webhooks to this URL when plan or cycle status changes occur.

**Plan Events:**
- `recurring.plan.activated` - Plan successfully activated
- `recurring.plan.inactivated` - Plan deactivated

**Cycle Events:**
- `recurring.cycle.created` - New cycle created
- `recurring.cycle.retrying` - Cycle payment failed, retry scheduled
- `recurring.cycle.succeeded` - Cycle payment completed
- `recurring.cycle.failed` - Cycle payment failed after all retries
- `recurring.cycle.force_attempt_failed` - Forced payment attempt failed


## OpenAPI

````json POST /your_subscription_webhook_url
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
    "/your_subscription_webhook_url": {
      "post": {
        "tags": [
          "Subscriptions"
        ],
        "summary": "Subscription Webhook",
        "description": "Endpoint to receive webhook notifications for subscription events. \nXendit will send webhooks to this URL when plan or cycle status changes occur.\n\n**Plan Events:**\n- `recurring.plan.activated` - Plan successfully activated\n- `recurring.plan.inactivated` - Plan deactivated\n\n**Cycle Events:**\n- `recurring.cycle.created` - New cycle created\n- `recurring.cycle.retrying` - Cycle payment failed, retry scheduled\n- `recurring.cycle.succeeded` - Cycle payment completed\n- `recurring.cycle.failed` - Cycle payment failed after all retries\n- `recurring.cycle.force_attempt_failed` - Forced payment attempt failed\n",
        "operationId": "receiveSubscriptionWebhook",
        "requestBody": {
          "description": "Webhook payload containing either a plan or cycle event.",
          "required": "true",
          "content": {
            "application/json": {
              "schema": {
                "oneOf": [
                  {
                    "$ref": "#/components/schemas/Xendit_Subscriptions_API_RecurringPlanWebhook"
                  },
                  {
                    "$ref": "#/components/schemas/Xendit_Subscriptions_API_RecurringCycleWebhook"
                  }
                ],
                "discriminator": {
                  "propertyName": "event",
                  "mapping": {
                    "recurring.plan.activated": "#/components/schemas/Xendit_Subscriptions_API_RecurringPlanWebhook",
                    "recurring.plan.inactivated": "#/components/schemas/Xendit_Subscriptions_API_RecurringPlanWebhook",
                    "recurring.cycle.created": "#/components/schemas/Xendit_Subscriptions_API_RecurringCycleWebhook",
                    "recurring.cycle.retrying": "#/components/schemas/Xendit_Subscriptions_API_RecurringCycleWebhook",
                    "recurring.cycle.succeeded": "#/components/schemas/Xendit_Subscriptions_API_RecurringCycleWebhook",
                    "recurring.cycle.failed": "#/components/schemas/Xendit_Subscriptions_API_RecurringCycleWebhook",
                    "recurring.cycle.force_attempt_failed": "#/components/schemas/Xendit_Subscriptions_API_RecurringCycleWebhook"
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Webhook received successfully. Return 200 to acknowledge receipt."
          },
          "500": {
            "description": "Server error - webhook will be retried."
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
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
      "Xendit_Subscriptions_API_RecurringCycleWebhook": {
        "type": "object",
        "required": [
          "event",
          "business_id",
          "created",
          "data"
        ],
        "description": "Webhook payload sent for recurring cycle status updates.\n- `recurring.cycle.created`: Sent when a new recurring cycle is created for a plan.\n- `recurring.cycle.retrying`: Sent when a cycle payment fails and a retry is scheduled.\n- `recurring.cycle.succeeded`: Sent when a cycle payment is completed successfully.\n- `recurring.cycle.failed`: Sent when a cycle payment fails after all retry attempts are exhausted.\n- `recurring.cycle.force_attempt_failed`: Sent when a forced payment attempt on a cycle fails.\n",
        "properties": {
          "event": {
            "type": "string",
            "enum": [
              "recurring.cycle.created",
              "recurring.cycle.retrying",
              "recurring.cycle.succeeded",
              "recurring.cycle.failed",
              "recurring.cycle.force_attempt_failed"
            ],
            "description": "Webhook event names for recurring cycle status updates.\n",
            "example": "recurring.cycle.succeeded"
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
            "$ref": "#/components/schemas/Xendit_Subscriptions_API_RecurringCycle"
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
      },
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
      }
    }
  }
}
````

