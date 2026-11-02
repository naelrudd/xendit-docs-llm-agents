> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create a refund

> Refund a payment using its `payment_id`. Refunds are available for eligible card,
e-wallet, direct debit, and QR code payments, subject to channel support.

Provide `amount` for a specific refund amount, or omit it to request a full refund.
The amount uses the original payment's currency. Partial refunds depend on channel support.
Use a new `reference_id` to identify each refund in your system.

Check `status` in the response. If it is `PENDING`, wait for the refund status
webhook or retrieve the refund by its `refund_id` to check for a final status.


## OpenAPI

````json POST /v3/refunds
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
    "/v3/refunds": {
      "post": {
        "security": [
          {
            "Payments_API_BasicAuth": []
          }
        ],
        "operationId": "CreateRefund",
        "summary": "Create a refund",
        "description": "Refund a payment using its `payment_id`. Refunds are available for eligible card,\ne-wallet, direct debit, and QR code payments, subject to channel support.\n\nProvide `amount` for a specific refund amount, or omit it to request a full refund.\nThe amount uses the original payment's currency. Partial refunds depend on channel support.\nUse a new `reference_id` to identify each refund in your system.\n\nCheck `status` in the response. If it is `PENDING`, wait for the refund status\nwebhook or retrieve the refund by its `refund_id` to check for a final status.\n",
        "tags": [
          "Refund"
        ],
        "parameters": [
          {
            "$ref": "#/components/parameters/Payments_API_RefundAPIVersionHeader"
          },
          {
            "$ref": "#/components/parameters/Payments_API_ForUserIdHeaderParam"
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/Payments_API_RefundRequestSchema"
              },
              "examples": {
                "Refund_With_Amount": {
                  "summary": "Refund a specified amount",
                  "value": {
                    "reference_id": "refund-order-123",
                    "payment_id": "py-1402feb0-8b79-85ae-9d1e-e69394d3949c",
                    "amount": 10000,
                    "reason": "REQUESTED_BY_CUSTOMER",
                    "metadata": {
                      "order_id": "1234567890"
                    }
                  }
                },
                "Refund_Without_Amount": {
                  "summary": "Request a full refund",
                  "value": {
                    "reference_id": "refund-order-124",
                    "payment_id": "py-1402feb0-8b79-85ae-9d1e-e69394d3949c",
                    "reason": "REQUESTED_BY_CUSTOMER"
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Refund request processed. Check status to determine whether the refund is pending, succeeded, or failed.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Payments_API_V3RefundSchema"
                },
                "examples": {
                  "RefundSucceeded": {
                    "value": {
                      "refund_id": "rfd-1402feb0-8b79-85ae-9d1e-e69394d3949c",
                      "reference_id": "refund-order-123",
                      "business_id": "62440e322008e87fb29c1fd0",
                      "payment_id": "py-1402feb0-8b79-85ae-9d1e-e69394d3949c",
                      "status": "SUCCEEDED",
                      "amount": 10000,
                      "currency": "IDR",
                      "channel_code": "CARDS",
                      "reason": "REQUESTED_BY_CUSTOMER",
                      "created": "2024-10-28T05:29:07Z",
                      "updated": "2024-10-28T05:29:07Z",
                      "metadata": {
                        "order_id": "1234567890"
                      }
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Bad request",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400InvalidValueError"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400ApiValidationError"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400RefundNotSupported"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400RefundAmountExceeded"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400RefundInProgress"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400InsufficientBalance"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400PartialRefundCountsExceeded"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400IneligibleTransactionStatus"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400MaximumRefundAmountReached"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400MaximumRefundTransactionReached"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400PartialRefundNotSupported"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http400RefundTemporarilyUnavailable"
                    }
                  ]
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/Payments_API_Http401InvalidApiKey"
                    }
                  ]
                }
              }
            }
          },
          "403": {
            "description": "Forbidden",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/Payments_API_Http403IneligibleTransactionStatus"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http403InvalidMerchantSettings"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http403RefundNotSupported"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http403PartialRefundNotSupported"
                    },
                    {
                      "$ref": "#/components/schemas/Payments_API_Http403IneligibleTransaction"
                    }
                  ]
                }
              }
            }
          },
          "404": {
            "description": "Not found",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/Payments_API_Http404DataNotFound"
                    }
                  ]
                }
              }
            }
          },
          "409": {
            "description": "Conflict",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/Payments_API_Http409DuplicateError"
                    }
                  ]
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/Payments_API_Http500ServerError"
                    }
                  ]
                }
              }
            }
          },
          "503": {
            "description": "Service unavailable",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/Payments_API_Http503ChannelUnavailable"
                    }
                  ]
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "parameters": {
      "Payments_API_RefundAPIVersionHeader": {
        "in": "header",
        "name": "api-version",
        "required": true,
        "description": "API version required for V3 refund operations.",
        "schema": {
          "type": "string",
          "enum": [
            "2024-11-11"
          ],
          "example": "2024-11-11"
        }
      },
      "Payments_API_ForUserIdHeaderParam": {
        "in": "header",
        "name": "for-user-id",
        "required": false,
        "schema": {
          "type": "string"
        },
        "description": "The XenPlatform subaccount user id that will perform this transaction."
      }
    },
    "schemas": {
      "Payments_API_RefundRequestSchema": {
        "type": "object",
        "description": "Request a refund for an existing payment.",
        "required": [
          "reference_id",
          "payment_id",
          "reason"
        ],
        "properties": {
          "reference_id": {
            "$ref": "#/components/schemas/Payments_API_ReferenceId"
          },
          "payment_id": {
            "$ref": "#/components/schemas/Payments_API_RefundPaymentId"
          },
          "amount": {
            "type": "number",
            "minimum": 0,
            "exclusiveMinimum": true,
            "description": "Amount to refund in the original payment's currency. Must be greater than zero.\nOmit to request a full refund. Partial refunds depend on channel support.\n",
            "example": 10000
          },
          "reason": {
            "$ref": "#/components/schemas/Payments_API_V3RefundReason"
          },
          "metadata": {
            "$ref": "#/components/schemas/Payments_API_RefundMetadata"
          }
        }
      },
      "Payments_API_V3RefundSchema": {
        "type": "object",
        "description": "Details and current status of a V3 refund.",
        "properties": {
          "refund_id": {
            "$ref": "#/components/schemas/Payments_API_RefundId"
          },
          "reference_id": {
            "$ref": "#/components/schemas/Payments_API_ReferenceId"
          },
          "business_id": {
            "$ref": "#/components/schemas/Payments_API_BusinessId"
          },
          "payment_id": {
            "$ref": "#/components/schemas/Payments_API_PaymentId"
          },
          "status": {
            "$ref": "#/components/schemas/Payments_API_V3RefundStatus"
          },
          "amount": {
            "$ref": "#/components/schemas/Payments_API_RefundAmount"
          },
          "currency": {
            "$ref": "#/components/schemas/Payments_API_Currency"
          },
          "channel_code": {
            "$ref": "#/components/schemas/Payments_API_ChannelCode"
          },
          "reason": {
            "$ref": "#/components/schemas/Payments_API_V3RefundReason"
          },
          "created": {
            "$ref": "#/components/schemas/Payments_API_CreatedDateTime"
          },
          "updated": {
            "$ref": "#/components/schemas/Payments_API_UpdatedDateTime"
          },
          "failure_code": {
            "$ref": "#/components/schemas/Payments_API_RefundFailureCode"
          },
          "refund_details": {
            "$ref": "#/components/schemas/Payments_API_RefundDetails"
          },
          "metadata": {
            "$ref": "#/components/schemas/Payments_API_RefundMetadata"
          }
        }
      },
      "Payments_API_Http400InvalidValueError": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INVALID_VALUE_ERROR"
            ]
          },
          "message": {
            "type": "string",
            "description": "Values in the payment request is not within expected range or expected configurations. Check the specific error message for debugging."
          }
        }
      },
      "Payments_API_Http400ApiValidationError": {
        "description": "Api Validation Error",
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "API_VALIDATION_ERROR"
            ]
          },
          "message": {
            "type": "string",
            "description": "Fields or values in the payment request does not comply with our API specification. Check the specific error message for debugging."
          }
        }
      },
      "Payments_API_Http400RefundNotSupported": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "REFUND_NOT_SUPPORTED"
            ]
          },
          "message": {
            "type": "string",
            "description": "Refund feature is not available for this payment channel."
          }
        }
      },
      "Payments_API_Http400RefundAmountExceeded": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "REFUND_AMOUNT_EXCEEDED"
            ]
          },
          "message": {
            "type": "string",
            "description": "Refund amount specified in refund request must be less than or equal to unrefunded capture amount."
          }
        }
      },
      "Payments_API_Http400RefundInProgress": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "REFUND_IN_PROGRESS"
            ]
          },
          "message": {
            "type": "string",
            "description": "Please wait for the pending refund request to be completed before initiating a new one."
          }
        }
      },
      "Payments_API_Http400InsufficientBalance": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INSUFFICIENT_BALANCE"
            ]
          },
          "message": {
            "type": "string",
            "description": "There is insufficient balance in your account to perform a refund. Please top up your balance with a sufficient amount before retrying the refund."
          }
        }
      },
      "Payments_API_Http400PartialRefundCountsExceeded": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "PARTIAL_REFUND_COUNTS_EXCEEDED"
            ]
          },
          "message": {
            "type": "string",
            "description": "Number of partial refunds for this payment request has exceeded what is allowed by payment channel. Please check our documentations for refund limitations."
          }
        }
      },
      "Payments_API_Http400IneligibleTransactionStatus": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INELIGIBLE_TRANSACTION_STATUS"
            ]
          },
          "message": {
            "type": "string",
            "description": "Feature is not allowed for the payment request because of its current status. Check the specific error message for debugging."
          }
        }
      },
      "Payments_API_Http400MaximumRefundAmountReached": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "MAXIMUM_REFUND_AMOUNT_REACHED"
            ]
          },
          "message": {
            "type": "string",
            "description": "The maximum refundable amount for this payment has been reached."
          }
        }
      },
      "Payments_API_Http400MaximumRefundTransactionReached": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "MAXIMUM_REFUND_TRANSACTION_REACHED"
            ]
          },
          "message": {
            "type": "string",
            "description": "The maximum number of refunds allowed for this payment has been reached."
          }
        }
      },
      "Payments_API_Http400PartialRefundNotSupported": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "PARTIAL_REFUND_NOT_SUPPORTED"
            ]
          },
          "message": {
            "type": "string",
            "description": "Partial refunds are not supported for this payment or channel."
          }
        }
      },
      "Payments_API_Http400RefundTemporarilyUnavailable": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "REFUND_TEMPORARILY_UNAVAILABLE"
            ]
          },
          "message": {
            "type": "string",
            "description": "Refunds are temporarily unavailable for this payment or channel. Try again later."
          }
        }
      },
      "Payments_API_Http401InvalidApiKey": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INVALID_API_KEY"
            ]
          },
          "message": {
            "type": "string",
            "description": "The API key is missing or invalid. Use a valid secret API key to authenticate the request."
          }
        }
      },
      "Payments_API_Http403IneligibleTransactionStatus": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INELIGIBLE_TRANSACTION_STATUS"
            ]
          },
          "message": {
            "type": "string",
            "description": "Feature is not allowed for the payment request because of its current status. Check the specific error message for debugging."
          }
        }
      },
      "Payments_API_Http403InvalidMerchantSettings": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INVALID_MERCHANT_SETTINGS"
            ]
          },
          "message": {
            "type": "string",
            "description": "Merchant credentials met with an error with the provider. Please contact Xendit customer support to resolve this issue."
          }
        }
      },
      "Payments_API_Http403RefundNotSupported": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "REFUND_NOT_SUPPORTED"
            ]
          },
          "message": {
            "type": "string",
            "description": "Refund feature is not available for this payment channel."
          }
        }
      },
      "Payments_API_Http403PartialRefundNotSupported": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "PARTIAL_REFUND_NOT_SUPPORTED"
            ]
          },
          "message": {
            "type": "string",
            "description": "Partial Refund feature is not available for this payment channel."
          }
        }
      },
      "Payments_API_Http403IneligibleTransaction": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "INELIGIBLE_TRANSACTION"
            ]
          },
          "message": {
            "type": "string",
            "description": "This payment is not eligible for a refund. Check the error message for details."
          }
        }
      },
      "Payments_API_Http404DataNotFound": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "DATA_NOT_FOUND"
            ]
          },
          "message": {
            "type": "string",
            "description": "ID specified in request cannot be found."
          }
        }
      },
      "Payments_API_Http409DuplicateError": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "DUPLICATE_ERROR"
            ]
          },
          "message": {
            "type": "string",
            "description": "Duplication is not allowed. Check specific error message for debugging."
          }
        }
      },
      "Payments_API_Http500ServerError": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "SERVER_ERROR"
            ]
          },
          "message": {
            "type": "string",
            "description": "An unexpected error occured, our team has been notified and will troubleshoot the issue"
          }
        }
      },
      "Payments_API_Http503ChannelUnavailable": {
        "type": "object",
        "required": [
          "error_code",
          "message"
        ],
        "properties": {
          "error_code": {
            "type": "string",
            "enum": [
              "CHANNEL_UNAVAILABLE"
            ]
          },
          "message": {
            "type": "string",
            "description": "The channel requested is currently experiencing unexpected issues. The provider will be notified to resolve this issue."
          }
        }
      },
      "Payments_API_ReferenceId": {
        "type": "string",
        "minLength": 1,
        "maxLength": 255,
        "description": "A Reference ID from merchants to identify their request."
      },
      "Payments_API_RefundPaymentId": {
        "type": "string",
        "minLength": 1,
        "description": "ID of the original payment to refund. Accepts V3 payment IDs (`py-`) and\nsupported legacy payment IDs: card IDs (`ca_`, `cc_`, or a 24-character\nhexadecimal ID), e-wallet IDs (`ewc_`), direct debit IDs (`ddpy_`), and QR IDs (`qrpy_`).\nUse the payment ID, not the payment request ID.\n",
        "example": "py-1402feb0-bb79-47ae-9d1e-e69394d3949c"
      },
      "Payments_API_V3RefundReason": {
        "type": "string",
        "enum": [
          "FRAUDULENT",
          "DUPLICATE",
          "REQUESTED_BY_CUSTOMER",
          "CANCELLATION",
          "OTHERS"
        ],
        "description": "Reason for requesting the refund."
      },
      "Payments_API_RefundMetadata": {
        "type": "object",
        "maxProperties": 50,
        "description": "Custom data attached to the refund. Supports up to 50 entries. Keys must be\nno longer than 40 characters. Values may be strings (up to 500 characters),\nfinite numbers, booleans, or null. Nested objects and arrays are not supported.\n",
        "additionalProperties": {
          "anyOf": [
            {
              "type": "string",
              "maxLength": 500,
              "nullable": true
            },
            {
              "type": "number"
            },
            {
              "type": "boolean"
            }
          ]
        },
        "example": {
          "order_id": "1234567890"
        }
      },
      "Payments_API_RefundId": {
        "type": "string",
        "pattern": "^rfd-[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
        "description": "Xendit-generated identifier for a refund.",
        "example": "rfd-1402feb0-8b79-85ae-9d1e-e69394d3949c"
      },
      "Payments_API_BusinessId": {
        "type": "string",
        "description": "Xendit-generated identifier for the business that owns the transaction",
        "example": "5f27a14a9bf05c73dd040bc8"
      },
      "Payments_API_PaymentId": {
        "type": "string",
        "description": "Xendit unique Payment ID generated as reference for a payment.",
        "example": "py-1402feb0-bb79-47ae-9d1e-e69394d3949c"
      },
      "Payments_API_V3RefundStatus": {
        "type": "string",
        "enum": [
          "SUCCEEDED",
          "FAILED",
          "PENDING"
        ],
        "description": "`PENDING`: the refund is still processing.\n`SUCCEEDED`: the refund completed successfully.\n`FAILED`: the refund could not be completed; check `failure_code` for details.\n"
      },
      "Payments_API_RefundAmount": {
        "type": "number",
        "minimum": 0,
        "exclusiveMinimum": true,
        "description": "The intended payment amount to be refunded to the end user.\n",
        "example": 10000
      },
      "Payments_API_Currency": {
        "type": "string",
        "enum": [
          "IDR",
          "PHP",
          "VND",
          "THB",
          "SGD",
          "MYR",
          "USD",
          "HKD",
          "AUD",
          "GBP",
          "EUR",
          "JPY",
          "MXN",
          "AED",
          "AFN",
          "ALL",
          "AMD",
          "AOA",
          "ARS",
          "AWG",
          "AZN",
          "BAM",
          "BBD",
          "BDT",
          "BGN",
          "BHD",
          "BIF",
          "BMD",
          "BND",
          "BOB",
          "BOV",
          "BRL",
          "BSD",
          "BTN",
          "BWP",
          "BYN",
          "BZD",
          "CAD",
          "CDF",
          "CHF",
          "CLF",
          "CLP",
          "CNY",
          "COP",
          "COU",
          "CRC",
          "CUC",
          "CUP",
          "CVE",
          "CZK",
          "DJF",
          "DKK",
          "DOP",
          "DZD",
          "EGP",
          "ERN",
          "ETB",
          "FJD",
          "FKP",
          "GEL",
          "GHS",
          "GIP",
          "GMD",
          "GNF",
          "GTQ",
          "GYD",
          "HNL",
          "HTG",
          "HUF",
          "ILS",
          "INR",
          "IQD",
          "IRR",
          "ISK",
          "JMD",
          "JOD",
          "KES",
          "KGS",
          "KHR",
          "KMF",
          "KPW",
          "KRW",
          "KWD",
          "KYD",
          "KZT",
          "LAK",
          "LBP",
          "LKR",
          "LRD",
          "LSL",
          "LYD",
          "MAD",
          "MDL",
          "MGA",
          "MKD",
          "MMK",
          "MNT",
          "MOP",
          "MRU",
          "MUR",
          "MVR",
          "MWK",
          "MZN",
          "NAD",
          "NGN",
          "NIO",
          "NOK",
          "NPR",
          "NZD",
          "OMR",
          "PAB",
          "PEN",
          "PGK",
          "PKR",
          "PLN",
          "PYG",
          "QAR",
          "RON",
          "RSD",
          "RUB",
          "RWF",
          "SAR",
          "SBD",
          "SCR",
          "SDG",
          "SEK",
          "SHP",
          "SLE",
          "SOS",
          "SRD",
          "SSP",
          "STN",
          "SVC",
          "SYP",
          "SZL",
          "TJS",
          "TMT",
          "TND",
          "TOP",
          "TRY",
          "TTD",
          "TWD",
          "TZS",
          "UAH",
          "UGX",
          "UYU",
          "UZS",
          "VEF",
          "VES",
          "VUV",
          "WST",
          "XAF",
          "XCD",
          "XCG",
          "XOF",
          "XPF",
          "YER",
          "ZAR",
          "ZMW",
          "ZWG",
          "ZWL"
        ],
        "description": "ISO 4217 three-letter currency code for the payment.",
        "example": "IDR"
      },
      "Payments_API_ChannelCode": {
        "type": "string",
        "description": "Channel code used to select the payment method provider.\n\n<iframe src=\"https://doc-widget.xendit.co/channel-data-finder/?iframe_id=channel-code-iframe\" frameborder=\"0\" allowfullscreen=\"\" allow=\"accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture\" title=\"\" style=\"border:1px solid #ccc;width:100%;display:flex;margin-right:auto;max-height:800px;\" width=\"100%\" loading=\"lazy\" referrerpolicy=\"no-referrer-when-downgrade\"></iframe>\n"
      },
      "Payments_API_CreatedDateTime": {
        "type": "string",
        "format": "date-time",
        "description": "ISO 8601 date-time format.\n",
        "example": "2021-12-31T23:59:59Z"
      },
      "Payments_API_UpdatedDateTime": {
        "type": "string",
        "format": "date-time",
        "description": "ISO 8601 date-time format.\n",
        "example": "2021-12-31T23:59:59Z"
      },
      "Payments_API_RefundFailureCode": {
        "type": "string",
        "nullable": true,
        "description": "Channel-specific failure code if the refund fails; otherwise null or omitted."
      },
      "Payments_API_RefundDetails": {
        "type": "object",
        "description": "Additional refund information, when available from the channel.",
        "properties": {
          "acquirer_reference_id": {
            "type": "string",
            "nullable": true,
            "description": "Reference provided by the acquirer to help trace the refund."
          }
        }
      }
    },
    "securitySchemes": {
      "Payments_API_BasicAuth": {
        "type": "http",
        "scheme": "basic"
      }
    }
  }
}
````

