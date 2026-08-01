> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Webhook notification that will be sent to your defined webhook url for updates to payment session status

> Webhook notification that will be sent to your defined webhook url for updates to payment session status.

## OpenAPI

````json POST /your_payment_session_webhook_url
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
    "/your_payment_session_webhook_url": {
      "post": {
        "security": [
          {
            "Payment_Session_BasicAuth": []
          }
        ],
        "operationId": "processPaymentSessionWebhook",
        "summary": "Webhook notification that will be sent to your defined webhook url for updates to payment session status.",
        "description": "Webhook notification that will be sent to your defined webhook url for updates to payment session status.",
        "tags": [
          "Session"
        ],
        "requestBody": {
          "required": "true",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "description": "Payment session status webhook",
                "properties": {
                  "event": {
                    "type": "string",
                    "enum": [
                      "payment_session.completed",
                      "payment_session.expired"
                    ],
                    "description": "Webhook event names for payment session status updates.\nApplies to all session types including SUBSCRIPTION.\n"
                  },
                  "business_id": {
                    "type": "string",
                    "description": "Business ID of the merchant",
                    "example": "661f87c614802d6c402cd82d"
                  },
                  "created": {
                    "type": "string",
                    "format": "date-time",
                    "description": "Timestamp of webhook delivery attempt in ISO 8601 date-time format.\n",
                    "example": "2021-12-31T23:59:59Z"
                  },
                  "data": {
                    "$ref": "#/components/schemas/Payment_Session_SessionWebhookSchema"
                  }
                }
              },
              "examples": {
                "PaymentSession_CompletedExample": {
                  "value": {
                    "event": "payment_session.completed",
                    "business_id": "661f87c614802d6c402cd82d",
                    "created": "2026-12-31T23:59:59Z",
                    "data": {
                      "payment_session_id": "ps-661f87c614802d6c402cd82d",
                      "created": "2026-12-30T23:59:59Z",
                      "updated": "2026-12-31T23:59:59Z",
                      "reference_id": "order_12345_PAY",
                      "customer_id": "cust-e2878b4c-d57e-4a2c-922d-c0313c2800a3",
                      "session_type": "PAY",
                      "allow_save_payment_method": "OPTIONAL",
                      "currency": "PHP",
                      "amount": "10000",
                      "country": "PH",
                      "mode": "PAYMENT_LINK",
                      "expires_at": "2027-12-31T23:59:59Z",
                      "locale": "en",
                      "description": "Insurance Plan Registration",
                      "success_return_url": "https://yourcompany.com/success/example_item=my_item",
                      "cancel_return_url": "https://yourcompany.com/cancel/example_item=my_item",
                      "status": "COMPLETED",
                      "payment_link_url": "https://xen.to/kGxPCi60",
                      "payment_token_id": "pt-661f87c614802d6c402cd82d",
                      "payment_request_id": "pr-661f87c614802d6c402cd82d",
                      "payment_id": "py-661f87c614802d6c402cd82d",
                      "business_id": "661f87c614802d6c402cd82d"
                    }
                  }
                },
                "PaymentSession_ExpiredExample": {
                  "value": {
                    "event": "payment_session.expired",
                    "business_id": "661f87c614802d6c402cd82d",
                    "created": "2021-12-31T23:59:59Z",
                    "data": {
                      "payment_session_id": "ps-661f87c614802d6c402cd82d",
                      "created": "2021-12-31T23:59:59Z",
                      "updated": "2021-12-31T23:59:59Z",
                      "reference_id": "order_12345_PAY",
                      "customer_id": "cust-e2878b4c-d57e-4a2c-922d-c0313c2800a3",
                      "session_type": "PAY",
                      "currency": "PHP",
                      "amount": "10000",
                      "country": "PH",
                      "mode": "PAYMENT_LINK",
                      "expires_at": "2021-12-31T23:59:59Z",
                      "locale": "en",
                      "description": "Insurance Plan Registration",
                      "success_return_url": "https://yourcompany.com/success/example_item=my_item",
                      "cancel_return_url": "https://yourcompany.com/cancel/example_item=my_item",
                      "status": "EXPIRED",
                      "payment_link_url": "https://xen.to/kGxPCi60"
                    }
                  }
                },
                "PaymentSession_SubscriptionCompletedExample": {
                  "value": {
                    "event": "payment_session.completed",
                    "business_id": "661f87c614802d6c402cd82d",
                    "created": "2026-12-31T23:59:59Z",
                    "data": {
                      "payment_session_id": "ps-661f87c614802d6c402cd82d",
                      "created": "2026-12-30T23:59:59Z",
                      "updated": "2026-12-31T23:59:59Z",
                      "reference_id": "subscription_12345",
                      "customer_id": "cust-e2878b4c-d57e-4a2c-922d-c0313c2800a3",
                      "session_type": "SUBSCRIPTION",
                      "currency": "PHP",
                      "amount": "50000",
                      "country": "PH",
                      "mode": "PAYMENT_LINK",
                      "expires_at": "2027-12-31T23:59:59Z",
                      "locale": "en",
                      "description": "Monthly subscription plan",
                      "success_return_url": "https://yourcompany.com/success/example_item=my_item",
                      "cancel_return_url": "https://yourcompany.com/cancel/example_item=my_item",
                      "status": "COMPLETED",
                      "payment_link_url": "https://xen.to/kGxPCi60",
                      "payment_token_id": "pt-661f87c614802d6c402cd82d",
                      "payment_request_id": "pr-661f87c614802d6c402cd82d",
                      "payment_id": "py-661f87c614802d6c402cd82d",
                      "business_id": "661f87c614802d6c402cd82d"
                    }
                  }
                }
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
  },
  "components": {
    "schemas": {
      "Payment_Session_SessionWebhookSchema": {
        "type": "object",
        "properties": {
          "customer_id": {
            "$ref": "#/components/schemas/Payment_Session_CustomerId"
          },
          "reference_id": {
            "$ref": "#/components/schemas/Payment_Session_ReferenceId"
          },
          "payment_session_id": {
            "$ref": "#/components/schemas/Payment_Session_SessionId"
          },
          "payment_request_id": {
            "$ref": "#/components/schemas/Payment_Session_PaymentRequestId"
          },
          "session_type": {
            "$ref": "#/components/schemas/Payment_Session_SessionTypeEnum"
          },
          "mode": {
            "$ref": "#/components/schemas/Payment_Session_SessionModeEnum"
          },
          "status": {
            "$ref": "#/components/schemas/Payment_Session_SessionStatus"
          },
          "updated": {
            "$ref": "#/components/schemas/Payment_Session_UpdatedDateTime"
          },
          "created": {
            "$ref": "#/components/schemas/Payment_Session_CreatedDateTime"
          },
          "expires_at": {
            "$ref": "#/components/schemas/Payment_Session_ExpiresAt"
          },
          "locale": {
            "$ref": "#/components/schemas/Payment_Session_Locale"
          },
          "description": {
            "$ref": "#/components/schemas/Payment_Session_Description"
          },
          "items": {
            "$ref": "#/components/schemas/Payment_Session_XenditStandardItemBasket"
          },
          "success_return_url": {
            "$ref": "#/components/schemas/Payment_Session_GenericReturnUrl"
          },
          "cancel_return_url": {
            "$ref": "#/components/schemas/Payment_Session_GenericReturnUrl"
          },
          "payment_link_url": {
            "$ref": "#/components/schemas/Payment_Session_PaymentLinkUrl"
          },
          "payment_token_id": {
            "$ref": "#/components/schemas/Payment_Session_PaymentTokenId"
          },
          "payment_id": {
            "$ref": "#/components/schemas/Payment_Session_PaymentId"
          },
          "business_id": {
            "type": "string",
            "description": "Business ID of the merchant"
          },
          "components_sdk_key": {
            "$ref": "#/components/schemas/Payment_Session_ComponentsSDKKey"
          },
          "components_configuration": {
            "$ref": "#/components/schemas/Payment_Session_ComponentsConfiguration"
          }
        }
      },
      "Payment_Session_CustomerId": {
        "type": "string",
        "minLength": "41",
        "maxLength": "41",
        "description": "A unique identifier automatically generated by Xendit to represent an end customer. This ID can be used as a consistent reference across multiple transactions or payment activities for the same user. You can create a customer object in advance through the Create Customer API here: https://xendit-docs.document360.io/apidocs/create-customer-request",
        "example": "cust-b98d6f63-d240-44ec-9bd5-aa42954c4f48"
      },
      "Payment_Session_ReferenceId": {
        "type": "string",
        "minLength": "1",
        "maxLength": "64",
        "description": "Your reference to uniquely identify the Payment Session. This is commonly used to identify your order or transaction."
      },
      "Payment_Session_SessionId": {
        "type": "string",
        "minLength": "27",
        "maxLength": "27",
        "description": "A unique identifier for the Payment Session",
        "example": "ps-661f87c614802d6c402cd82d"
      },
      "Payment_Session_PaymentRequestId": {
        "type": "string",
        "nullable": "true",
        "description": "Xendit Payment Request ID used to reference the payment made during this Session.",
        "example": "pr-0800fe40-bb79-47ae-9d1e-e69394d3949c"
      },
      "Payment_Session_SessionTypeEnum": {
        "type": "string",
        "enum": [
          "SAVE",
          "PAY",
          "SUBSCRIPTION",
          "AUTHORIZATION"
        ],
        "description": "The use case for Payment Session.\nSAVE: save the payment details from a customer for future payments.\nPAY: collects a one-time payment from a customer.\nSUBSCRIPTION: register a subscription payment for your customer using Xendit Subscription product, see here https://docs.xendit.co/docs/subscriptions-overview.\nAUTHORIZATION: authorize a card payment for a future capture.\n"
      },
      "Payment_Session_SessionModeEnum": {
        "type": "string",
        "enum": [
          "PAYMENT_LINK",
          "COMPONENTS",
          "CARDS_SESSION_JS"
        ],
        "description": "The frontend integration mode for Payment Session.\nPAYMENT_LINK: redirect the customer to the Xendit Hosted Checkout page.\nCOMPONENTS: collect the payment details directly from the customer on your own page using Xendit Components.\nCARDS_SESSION_JS: collect payment details from customer with cards-session Javascript library.\nOnly supported PAYMENT_LINK and CARDS_SESSION_JS as mode for now.\n"
      },
      "Payment_Session_SessionStatus": {
        "type": "string",
        "enum": [
          "ACTIVE",
          "COMPLETED",
          "EXPIRED",
          "CANCELED"
        ],
        "description": "The status of the Payment Session."
      },
      "Payment_Session_UpdatedDateTime": {
        "type": "string",
        "format": "date-time",
        "example": "2021-12-31T23:59:59Z"
      },
      "Payment_Session_CreatedDateTime": {
        "type": "string",
        "format": "date-time",
        "example": "2021-12-31T23:59:59Z"
      },
      "Payment_Session_ExpiresAt": {
        "type": "string",
        "format": "date-time",
        "description": "ISO 8601 date-time format.\nBy default the Session will expire 30 minutes after creation.\nWe recommend you to keep Sessions short-lived and create a new Session again only when the customer is ready to make payment.\n",
        "example": "2021-12-31T23:59:59Z"
      },
      "Payment_Session_Locale": {
        "type": "string",
        "default": "en",
        "description": "ISO 639-1 two-letter language code for Hosted Checkout page.",
        "example": "en"
      },
      "Payment_Session_Description": {
        "type": "string",
        "minLength": "1",
        "maxLength": "1000",
        "description": "A custom description for the Session. This text will be displayed on the Xendit Hosted Checkout page.",
        "example": "Payment for your order #123"
      },
      "Payment_Session_XenditStandardItemBasket": {
        "type": "array",
        "nullable": "true",
        "description": "Array of objects describing the item/s attached to the session.\n",
        "items": {
          "$ref": "#/components/schemas/Payment_Session_XenditStandardItem"
        }
      },
      "Payment_Session_GenericReturnUrl": {
        "type": "string",
        "description": "Specify the URL to redirect the customer after the session is completed or expired,\nor if the customer decide to stop the payment process.\nMust be HTTPS.\nFor example: \"https://yourcompany.com/example_item=my_example_item\"\n",
        "example": "https://yourcompany.com/example_item"
      },
      "Payment_Session_PaymentLinkUrl": {
        "type": "string",
        "nullable": "true",
        "description": "The URL for Xendit Hosted Checkout page. Redirect your customer to this URL to complete the payment.",
        "example": "https://checkout.xendit.co/sessions/ps-661f87c614802d6c402cd82d0 or https://xen.to/kGxPCi60. For test mode, https://checkout-staging.xendit.co/sessions/ps-661f87c614802d6c402cd82d0 or https://dev.xen.to/kGxPCi76"
      },
      "Payment_Session_PaymentTokenId": {
        "type": "string",
        "nullable": "true",
        "description": "Xendit Payment Token ID used to reference the saved payment details from the customer.",
        "example": "ptkn-cc3938dc-c2a5-43c4-89d7-7570793348c2"
      },
      "Payment_Session_PaymentId": {
        "type": "string",
        "nullable": "true",
        "description": "Xendit Payment ID used to reference the captured payment details from the customer.",
        "example": "py-ac1fcd3e-21c5-4c70-bb06-fa3c34e19e0c"
      },
      "Payment_Session_ComponentsSDKKey": {
        "type": "string",
        "nullable": "true",
        "description": "key will be used for sessions flows with mode COMPONENT",
        "example": "f5RBHw4S3SeZV8KGlBxjy8tyN2Vg4klA5Bww7"
      },
      "Payment_Session_ComponentsConfiguration": {
        "type": "object",
        "nullable": "true",
        "properties": {
          "origins": {
            "$ref": "#/components/schemas/Payment_Session_Origins"
          },
          "return_url": {
            "type": "string",
            "nullable": "true",
            "description": "Optional HTTPS URL to redirect the user to after payment completes or fails via a hard redirect channel. If not provided, users are redirected to the default Xendit page.\n",
            "example": "https://yourcompany.com/checkout/done"
          }
        }
      },
      "Payment_Session_XenditStandardItem": {
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
          "reference_id": {
            "type": "string",
            "description": "Merchant provided identifier for the item",
            "minLength": "1",
            "maxLength": "255"
          },
          "type": {
            "enum": [
              "DIGITAL_PRODUCT",
              "PHYSICAL_PRODUCT",
              "DIGITAL_SERVICE",
              "PHYSICAL_SERVICE",
              "FEE"
            ],
            "description": "Type of item"
          },
          "name": {
            "type": "string",
            "description": "Name of item",
            "minLength": "1",
            "maxLength": "255"
          },
          "net_unit_amount": {
            "type": "number",
            "description": "Net amount to be charged per unit"
          },
          "quantity": {
            "type": "integer",
            "description": "Number of units of this item in the basket",
            "minimum": "1"
          },
          "url": {
            "type": "string",
            "description": "URL of the item. Must be HTTPS or HTTP"
          },
          "image_url": {
            "type": "string",
            "description": "URL of the image of the item. Must be HTTPS or HTTP"
          },
          "category": {
            "type": "string",
            "description": "Category for item",
            "maxLength": "255"
          },
          "subcategory": {
            "type": "string",
            "description": "Sub-category for item",
            "maxLength": "255"
          },
          "description": {
            "type": "string",
            "description": "Description of item",
            "maxLength": "255"
          },
          "metadata": {
            "$ref": "#/components/schemas/Payment_Session_MerchantMetadata"
          }
        }
      },
      "Payment_Session_Origins": {
        "type": "array",
        "items": {
          "type": "string"
        },
        "description": "Origins will be used for sessions flows with mode COMPONENT to validate CORS",
        "example": [
          "https://yourcompany.com"
        ]
      },
      "Payment_Session_MerchantMetadata": {
        "type": "object",
        "nullable": "true",
        "description": "Key-value entries for your custom data/information.\nYou can specify up to 50 keys, with key names up to 40 characters and values up to 500 characters.\nThis is commonly used for your internal reference or reconciliation purposes. Xendit will not use this data for any processing.\n",
        "example": {
          "my_custom_id": "merchant-123",
          "my_custom_order_id": "order-123"
        }
      }
    },
    "securitySchemes": {
      "Payment_Session_BasicAuth": {
        "type": "http",
        "scheme": "basic"
      }
    }
  }
}
````

