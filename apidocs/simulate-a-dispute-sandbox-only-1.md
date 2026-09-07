> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Simulate a dispute (Sandbox Only)

> Create or resolve simulated disputes in the sandbox environment to test your integration. The workflow is two-phase: first create a simulated dispute using CREATE_DISPUTE or CREATE_DISPUTE_EXCEED_DEADLINE, then resolve it using DISPUTE_WON or DISPUTE_LOST.

## OpenAPI

````json POST /v1/disputes/simulate
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
    "/v1/disputes/simulate": {
      "post": {
        "tags": [
          "Disputes"
        ],
        "operationId": "simulateDispute",
        "summary": "Simulate a dispute (Sandbox Only)",
        "description": "Create or resolve simulated disputes in the sandbox environment to test your integration. The workflow is two-phase: first create a simulated dispute using CREATE_DISPUTE or CREATE_DISPUTE_EXCEED_DEADLINE, then resolve it using DISPUTE_WON or DISPUTE_LOST.",
        "requestBody": {
          "required": "true",
          "content": {
            "application/json": {
              "schema": {
                "oneOf": [
                  {
                    "$ref": "#/components/schemas/Merchant_Dispute_API_SimulateCreate"
                  },
                  {
                    "$ref": "#/components/schemas/Merchant_Dispute_API_SimulateResolve"
                  }
                ]
              },
              "examples": {
                "create_dispute": {
                  "summary": "Create a simulated dispute",
                  "value": {
                    "scenario": "CREATE_DISPUTE",
                    "payment_id": "py-59a3cf39-2a7d-4733-a3e3-8177c78090f7",
                    "amount": "100000",
                    "currency": "IDR",
                    "product_type": "CARDS",
                    "channel_code": "CARDS"
                  }
                },
                "create_dispute_exceed_deadline": {
                  "summary": "Create a simulated dispute that will exceed deadline",
                  "value": {
                    "scenario": "CREATE_DISPUTE_EXCEED_DEADLINE",
                    "payment_id": "py-59a3cf39-2a7d-4733-a3e3-8177c78090f7",
                    "amount": "100000",
                    "currency": "IDR",
                    "product_type": "CARDS",
                    "channel_code": "CARDS",
                    "deadline": "instant"
                  }
                },
                "resolve_won": {
                  "summary": "Resolve simulated dispute as WON",
                  "value": {
                    "scenario": "DISPUTE_WON",
                    "dispute_id": "mi-dspt-48e96517-9889-4e29-a93e-d1ffae1fa366"
                  }
                },
                "resolve_lost": {
                  "summary": "Resolve simulated dispute as LOST",
                  "value": {
                    "scenario": "DISPUTE_LOST",
                    "dispute_id": "mi-dspt-48e96517-9889-4e29-a93e-d1ffae1fa366"
                  }
                }
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "Simulation triggered successfully.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Merchant_Dispute_API_SimulateResponse"
                }
              }
            }
          },
          "202": {
            "description": "Simulation resolved successfully.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Merchant_Dispute_API_SimulateResponse"
                }
              }
            }
          },
          "400": {
            "description": "Bad request.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Merchant_Dispute_API_ErrorResponse"
                },
                "examples": {
                  "invalid_scenario": {
                    "value": {
                      "error_code": "INVALID_SCENARIO",
                      "message": "Invalid scenario."
                    }
                  },
                  "payment_not_found": {
                    "value": {
                      "error_code": "PAYMENT_NOT_FOUND",
                      "message": "The specified payment was not found."
                    }
                  },
                  "payment_not_settled": {
                    "value": {
                      "error_code": "PAYMENT_NOT_SETTLED",
                      "message": "The specified payment is not in a settled state."
                    }
                  },
                  "illegal_state": {
                    "value": {
                      "error_code": "ILLEGAL_STATE",
                      "message": "Evidence must be submitted before resolving a simulated dispute."
                    }
                  },
                  "invalid_request": {
                    "value": {
                      "error_code": "INVALID_REQUEST",
                      "message": "Invalid deadline value. Accepted values: instant, 1m, 2m, 3m, 5m."
                    }
                  }
                }
              }
            }
          },
          "403": {
            "description": "This endpoint is only available in sandbox environment.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Merchant_Dispute_API_ErrorResponse"
                },
                "example": {
                  "error_code": "UNAVAILABLE_IN_LIVE_MODE",
                  "message": "This endpoint is only available in test mode."
                }
              }
            }
          },
          "409": {
            "description": "Conflict. A resolve scenario has already been applied.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Merchant_Dispute_API_ErrorResponse"
                },
                "example": {
                  "error_code": "ILLEGAL_STATE",
                  "message": "A resolve scenario has already been applied to this simulated dispute."
                }
              }
            }
          },
          "429": {
            "description": "Too many requests. Maximum simulated disputes per time window exceeded.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Merchant_Dispute_API_ErrorResponse"
                },
                "example": {
                  "error_code": "TOO_MANY_REQUESTS",
                  "message": "Maximum of 5 simulated disputes per 24 hours exceeded."
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
      "Merchant_Dispute_API_SimulateCreate": {
        "type": "object",
        "required": [
          "scenario",
          "payment_id",
          "amount",
          "currency",
          "product_type",
          "channel_code"
        ],
        "properties": {
          "scenario": {
            "type": "string",
            "description": "CREATE_DISPUTE creates a dispute in ACTION_REQUIRED with a realistic deadline. CREATE_DISPUTE_EXCEED_DEADLINE creates a dispute that automatically expires.",
            "enum": [
              "CREATE_DISPUTE",
              "CREATE_DISPUTE_EXCEED_DEADLINE"
            ],
            "example": "CREATE_DISPUTE"
          },
          "payment_id": {
            "type": "string",
            "description": "Xendit payment ID of an existing settled payment to attach the simulated dispute to.",
            "example": "py-59a3cf39-2a7d-4733-a3e3-8177c78090f7"
          },
          "amount": {
            "type": "string",
            "description": "Dispute amount as a decimal string.",
            "example": "1000.00"
          },
          "currency": {
            "type": "string",
            "description": "Currency of the simulated dispute amount, in ISO-4217 format.",
            "example": "IDR"
          },
          "product_type": {
            "type": "string",
            "enum": [
              "CARDS",
              "QR"
            ],
            "description": "Product classification for the simulated dispute (e.g., CARDS, QR).",
            "example": "CARDS"
          },
          "channel_code": {
            "type": "string",
            "description": "Specific channel for the simulated dispute. Must be consistent with product_type.",
            "example": "CARDS"
          },
          "deadline": {
            "type": "string",
            "enum": [
              "instant",
              "1m",
              "2m",
              "3m",
              "5m"
            ],
            "description": "Optional deadline override for the simulated dispute. Only used with CREATE_DISPUTE_EXCEED_DEADLINE scenario.",
            "example": "instant"
          }
        }
      },
      "Merchant_Dispute_API_SimulateResolve": {
        "type": "object",
        "required": [
          "scenario",
          "dispute_id"
        ],
        "properties": {
          "scenario": {
            "type": "string",
            "description": "DISPUTE_WON resolves in the merchant's favor. DISPUTE_LOST resolves against the merchant.",
            "enum": [
              "DISPUTE_WON",
              "DISPUTE_LOST"
            ],
            "example": "DISPUTE_WON"
          },
          "dispute_id": {
            "type": "string",
            "description": "ID of the simulated dispute to resolve.",
            "example": "mi-dspt-48e96517-9889-4e29-a93e-d1ffae1fa366"
          },
          "amount": {
            "type": "string",
            "description": "Optional resolved amount. Defaults to the full initial amount. Provide a lower value to simulate a partial chargeback.",
            "example": "1000.00"
          }
        }
      },
      "Merchant_Dispute_API_SimulateResponse": {
        "type": "object",
        "properties": {
          "dispute_id": {
            "type": "string",
            "description": "ID of the dispute that was created or resolved by this simulation.",
            "example": "mi-dspt-f44d259f-fd9d-4de9-80de-1eef3f1506b7"
          },
          "created_at": {
            "type": "string",
            "description": "Timestamp when the simulated dispute was created, in ISO 8601 format.",
            "format": "date-time",
            "example": "2026-09-03T04:11:58.756Z"
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

