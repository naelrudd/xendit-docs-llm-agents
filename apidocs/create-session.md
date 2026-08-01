> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# Create a session

> Initiate the process of collecting payments from your customer.
We recommend creating a new Session from your server and redirect the customer to the Session Hosted Checkout page.
Once payment has succeeded, Session will contain a reference Payment ID or the Payment Token ID.
You get the outcome asynchronously in a Session webhook.


## OpenAPI

````json POST /sessions
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
    "/sessions": {
      "post": {
        "security": [
          {
            "Payment_Session_BasicAuth": []
          }
        ],
        "operationId": "createSession",
        "summary": "Create a session",
        "description": "Initiate the process of collecting payments from your customer.\nWe recommend creating a new Session from your server and redirect the customer to the Session Hosted Checkout page.\nOnce payment has succeeded, Session will contain a reference Payment ID or the Payment Token ID.\nYou get the outcome asynchronously in a Session webhook.\n",
        "tags": [
          "Session"
        ],
        "parameters": [
          {
            "$ref": "#/components/parameters/Payment_Session_ForUserIdHeaderParam"
          },
          {
            "$ref": "#/components/parameters/Payment_Session_SplitRuleHeaderParam"
          }
        ],
        "requestBody": {
          "required": "true",
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/Payment_Session_CreateSessionRequestPublicSchema"
              },
              "examples": {
                "PaymentLink_OneTimePaymentExample": {
                  "value": {
                    "reference_id": "order_12345_PAY",
                    "session_type": "PAY",
                    "mode": "PAYMENT_LINK",
                    "amount": "10000",
                    "currency": "PHP",
                    "country": "PH",
                    "customer": {
                      "reference_id": "cust_Lorem_Ipsum",
                      "type": "INDIVIDUAL",
                      "email": "test@yourdomain.com",
                      "mobile_number": "+6212345678",
                      "individual_detail": {
                        "given_names": "Lorem",
                        "surname": "Ipsum"
                      }
                    },
                    "items": [
                      {
                        "reference_id": "item_001",
                        "name": "Clothes",
                        "description": "Red clothes",
                        "type": "PHYSICAL_PRODUCT",
                        "category": "CLOTHES",
                        "net_unit_amount": "5000",
                        "quantity": "1",
                        "currency": "PHP",
                        "url": "https://example.com/item"
                      },
                      {
                        "reference_id": "item_002",
                        "name": "Pants",
                        "description": "Black pants",
                        "type": "PHYSICAL_PRODUCT",
                        "category": "CLOTHES",
                        "net_unit_amount": "5000",
                        "quantity": "1",
                        "currency": "PHP",
                        "url": "https://example.com/item"
                      }
                    ],
                    "capture_method": "AUTOMATIC",
                    "locale": "en",
                    "description": "Sample one-time payment using Payment Session",
                    "success_return_url": "https://yourcompany.com/success/example_item=my_item",
                    "cancel_return_url": "https://yourcompany.com/cancel/example_item=my_item"
                  }
                },
                "PaymentLink_PayandSaveExample": {
                  "value": {
                    "reference_id": "order_123456_SAVE",
                    "customer": {
                      "reference_id": "cust_Lorem_Ipsum",
                      "type": "INDIVIDUAL",
                      "email": "test@yourdomain.com",
                      "mobile_number": "+6212345678",
                      "individual_detail": {
                        "given_names": "Lorem",
                        "surname": "Ipsum"
                      }
                    },
                    "items": [
                      {
                        "reference_id": "item_001",
                        "name": "Clothes",
                        "description": "Red clothes",
                        "type": "PHYSICAL_PRODUCT",
                        "category": "CLOTHES",
                        "net_unit_amount": "5000",
                        "quantity": "1",
                        "currency": "PHP",
                        "url": "https://example.com/item"
                      },
                      {
                        "reference_id": "item_002",
                        "name": "Pants",
                        "description": "Black pants",
                        "type": "PHYSICAL_PRODUCT",
                        "category": "CLOTHES",
                        "net_unit_amount": "5000",
                        "quantity": "1",
                        "currency": "PHP",
                        "url": "https://example.com/item"
                      }
                    ],
                    "session_type": "PAY",
                    "currency": "PHP",
                    "amount": "10000",
                    "mode": "PAYMENT_LINK",
                    "allow_save_payment_method": "OPTIONAL",
                    "country": "PH",
                    "locale": "en",
                    "description": "Sample of pay and save flow using Payment Session",
                    "success_return_url": "https://yourcompany.com/success/example_item=my_item",
                    "cancel_return_url": "https://yourcompany.com/cancel/example_item=my_item"
                  }
                },
                "PaymentLink_SavePaymentMethodExample": {
                  "value": {
                    "reference_id": "order_123456_SAVE",
                    "customer": {
                      "reference_id": "cust_Lorem_Ipsum",
                      "type": "INDIVIDUAL",
                      "email": "test@yourdomain.com",
                      "mobile_number": "+6212345678",
                      "individual_detail": {
                        "given_names": "Lorem",
                        "surname": "Ipsum"
                      }
                    },
                    "session_type": "SAVE",
                    "currency": "IDR",
                    "amount": "0",
                    "mode": "PAYMENT_LINK",
                    "country": "ID",
                    "locale": "en",
                    "description": "Insurance Plan Registration",
                    "success_return_url": "https://yourcompany.com/success/example_item=my_item",
                    "cancel_return_url": "https://yourcompany.com/cancel/example_item=my_item"
                  }
                },
                "PaymentLink_ManualCaptureExample": {
                  "value": {
                    "reference_id": "order_12345_PAY",
                    "session_type": "PAY",
                    "mode": "PAYMENT_LINK",
                    "amount": "10000",
                    "currency": "PHP",
                    "country": "PH",
                    "customer": {
                      "reference_id": "cust_Lorem_Ipsum",
                      "type": "INDIVIDUAL",
                      "email": "test@yourdomain.com",
                      "mobile_number": "+6212345678",
                      "individual_detail": {
                        "given_names": "Lorem",
                        "surname": "Ipsum"
                      }
                    },
                    "capture_method": "MANUAL",
                    "locale": "en",
                    "description": "Sample of authorization and manual capture flow using Payment Session",
                    "success_return_url": "https://yourcompany.com/success/example_item=my_item",
                    "cancel_return_url": "https://yourcompany.com/cancel/example_item=my_item"
                  }
                },
                "XenditComponents_OneTimePaymentExample": {
                  "value": {
                    "reference_id": "order_12345_PAY",
                    "session_type": "PAY",
                    "mode": "COMPONENTS",
                    "amount": "10000",
                    "currency": "PHP",
                    "country": "PH",
                    "locale": "en",
                    "customer": {
                      "reference_id": "cust_Lorem_Ipsum",
                      "type": "INDIVIDUAL",
                      "email": "test@yourdomain.com",
                      "mobile_number": "+6212345678",
                      "individual_detail": {
                        "given_names": "Lorem",
                        "surname": "Ipsum"
                      }
                    },
                    "items": [
                      {
                        "reference_id": "item_001",
                        "name": "Clothes",
                        "description": "Red clothes",
                        "type": "PHYSICAL_PRODUCT",
                        "category": "CLOTHES",
                        "net_unit_amount": "5000",
                        "quantity": "1",
                        "currency": "PHP",
                        "url": "https://example.com/item"
                      },
                      {
                        "reference_id": "item_002",
                        "name": "Pants",
                        "description": "Black pants",
                        "type": "PHYSICAL_PRODUCT",
                        "category": "CLOTHES",
                        "net_unit_amount": "5000",
                        "quantity": "1",
                        "currency": "PHP",
                        "url": "https://example.com/item"
                      }
                    ],
                    "description": "Sample one-time payment using Xendit Components",
                    "components_configuration": {
                      "origins": [
                        "https://yourcompany.com"
                      ],
                      "return_url": "https://yourcompany.com/checkout/done"
                    }
                  }
                },
                "XenditComponents_PayandSaveExample": {
                  "value": {
                    "reference_id": "order_123456_SAVE",
                    "customer": {
                      "reference_id": "cust_Lorem_Ipsum",
                      "type": "INDIVIDUAL",
                      "email": "test@yourdomain.com",
                      "mobile_number": "+6212345678",
                      "individual_detail": {
                        "given_names": "Lorem",
                        "surname": "Ipsum"
                      }
                    },
                    "items": [
                      {
                        "reference_id": "item_001",
                        "name": "Clothes",
                        "description": "Red clothes",
                        "type": "PHYSICAL_PRODUCT",
                        "category": "CLOTHES",
                        "net_unit_amount": "5000",
                        "quantity": "1",
                        "currency": "PHP",
                        "url": "https://example.com/item"
                      },
                      {
                        "reference_id": "item_002",
                        "name": "Pants",
                        "description": "Black pants",
                        "type": "PHYSICAL_PRODUCT",
                        "category": "CLOTHES",
                        "net_unit_amount": "5000",
                        "quantity": "1",
                        "currency": "PHP",
                        "url": "https://example.com/item"
                      }
                    ],
                    "session_type": "PAY",
                    "currency": "PHP",
                    "amount": "10000",
                    "mode": "COMPONENTS",
                    "allow_save_payment_method": "OPTIONAL",
                    "country": "PH",
                    "locale": "en",
                    "description": "Sample of pay and save flow using Payment Session",
                    "components_configuration": {
                      "origins": [
                        "https://yourcompany.com"
                      ],
                      "return_url": "https://yourcompany.com/checkout/done"
                    }
                  }
                },
                "XenditComponents_SavePaymentMethodExample": {
                  "value": {
                    "reference_id": "registration_123456_SAVE",
                    "session_type": "SAVE",
                    "mode": "COMPONENTS",
                    "amount": "0",
                    "currency": "PHP",
                    "country": "PH",
                    "customer": {
                      "reference_id": "cust_Lorem_Ipsum",
                      "type": "INDIVIDUAL",
                      "email": "test@yourdomain.com",
                      "mobile_number": "+6212345678",
                      "individual_detail": {
                        "given_names": "Lorem",
                        "surname": "Ipsum"
                      }
                    },
                    "locale": "en",
                    "description": "Insurance Plan Registration",
                    "components_configuration": {
                      "origins": [
                        "https://yourcompany.com"
                      ],
                      "return_url": "https://yourcompany.com/checkout/done"
                    }
                  }
                },
                "XenditComponents_ManualCaptureExample": {
                  "value": {
                    "reference_id": "order_12345_PAY",
                    "session_type": "PAY",
                    "mode": "COMPONENTS",
                    "amount": "10000",
                    "currency": "PHP",
                    "country": "PH",
                    "locale": "en",
                    "customer": {
                      "reference_id": "cust_Lorem_Ipsum",
                      "type": "INDIVIDUAL",
                      "email": "test@yourdomain.com",
                      "mobile_number": "+6212345678",
                      "individual_detail": {
                        "given_names": "Lorem",
                        "surname": "Ipsum"
                      }
                    },
                    "capture_method": "MANUAL",
                    "description": "Sample of authorization and manual capture flow using Xendit Components",
                    "components_configuration": {
                      "origins": [
                        "https://yourcompany.com"
                      ],
                      "return_url": "https://yourcompany.com/checkout/done"
                    }
                  }
                },
                "PaymentLink_SubscriptionExample": {
                  "value": {
                    "reference_id": "subscription_12345",
                    "session_type": "SUBSCRIPTION",
                    "mode": "PAYMENT_LINK",
                    "amount": "50000",
                    "currency": "PHP",
                    "country": "PH",
                    "customer": {
                      "reference_id": "cust_Lorem_Ipsum",
                      "type": "INDIVIDUAL",
                      "email": "test@yourdomain.com",
                      "mobile_number": "+6212345678",
                      "individual_detail": {
                        "given_names": "Lorem",
                        "surname": "Ipsum"
                      }
                    },
                    "locale": "en",
                    "description": "Monthly subscription plan",
                    "subscription": {
                      "schedule": {
                        "interval": "MONTH",
                        "interval_count": "1",
                        "total_recurrence": "12",
                        "anchor_date": "2026-05-01T00:00:00Z",
                        "retry_interval": "DAY",
                        "retry_interval_count": "1",
                        "total_retry": "3",
                        "failed_attempt_notifications": [
                          "1",
                          "2",
                          "3"
                        ]
                      },
                      "failed_cycle_action": "RESUME"
                    },
                    "success_return_url": "https://yourcompany.com/success/example_item=my_item",
                    "cancel_return_url": "https://yourcompany.com/cancel/example_item=my_item"
                  }
                },
                "XenditComponents_SubscriptionExample": {
                  "value": {
                    "reference_id": "subscription_12345",
                    "session_type": "SUBSCRIPTION",
                    "mode": "COMPONENTS",
                    "amount": "50000",
                    "currency": "PHP",
                    "country": "PH",
                    "customer": {
                      "reference_id": "cust_Lorem_Ipsum",
                      "type": "INDIVIDUAL",
                      "email": "test@yourdomain.com",
                      "mobile_number": "+6212345678",
                      "individual_detail": {
                        "given_names": "Lorem",
                        "surname": "Ipsum"
                      }
                    },
                    "locale": "en",
                    "description": "Monthly subscription plan",
                    "subscription": {
                      "schedule": {
                        "interval": "MONTH",
                        "interval_count": "1",
                        "total_recurrence": "12",
                        "anchor_date": "2026-05-01T00:00:00Z",
                        "retry_interval": "DAY",
                        "retry_interval_count": "1",
                        "total_retry": "3",
                        "failed_attempt_notifications": [
                          "1",
                          "2",
                          "3"
                        ]
                      },
                      "failed_cycle_action": "RESUME"
                    },
                    "components_configuration": {
                      "origins": [
                        "https://yourcompany.com"
                      ],
                      "return_url": "https://yourcompany.com/checkout/done"
                    }
                  }
                }
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "Session Created",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Payment_Session_StandardSessionResponsePublicSchema"
                },
                "examples": {
                  "createSessionResponseExample": {
                    "value": {
                      "payment_session_id": "ps-661f87c614802d6c402cd82d",
                      "created": "2021-12-31T23:59:59Z",
                      "updated": "2021-12-31T23:59:59Z",
                      "reference_id": "Alice",
                      "customer_id": "cust-e2878b4c-d57e-4a2c-922d-c0313c2800a3",
                      "session_type": "SAVE",
                      "currency": "IDR",
                      "amount": "0",
                      "country": "ID",
                      "mode": "PAYMENT_LINK",
                      "channel_properties": {},
                      "allowed_payment_channels": [
                        "OVO",
                        "DANA"
                      ],
                      "expires_at": "2021-12-31T23:59:59Z",
                      "locale": "en",
                      "description": "Insurance Plan Registration",
                      "success_return_url": "https://yourcompany.com/success/example_item=my_item",
                      "cancel_return_url": "https://yourcompany.com/cancel/example_item=my_item",
                      "items": null,
                      "metadata": null,
                      "status": "ACTIVE",
                      "payment_link_url": "https://xen.to/kGxPCi60",
                      "payment_token_id": null,
                      "payment_request_id": null,
                      "business_id": "661f87c614802d6c402cd82d"
                    }
                  }
                }
              }
            }
          },
          "4XX": {
            "$ref": "#/components/responses/Payment_Session_CreateSessionError"
          },
          "5XX": {
            "$ref": "#/components/responses/Payment_Session_Generic5XXResponse"
          }
        }
      }
    }
  },
  "components": {
    "parameters": {
      "Payment_Session_ForUserIdHeaderParam": {
        "in": "header",
        "name": "for-user-id",
        "required": "false",
        "schema": {
          "type": "string"
        },
        "description": "The XenPlatform subaccount user id that will perform this transaction."
      },
      "Payment_Session_SplitRuleHeaderParam": {
        "in": "header",
        "name": "with-split-rule",
        "required": "false",
        "schema": {
          "type": "string"
        },
        "description": "The XenPlatform split rule id that will be applied to this transaction."
      }
    },
    "schemas": {
      "Payment_Session_CreateSessionRequestPublicSchema": {
        "type": "object",
        "required": [
          "reference_id",
          "currency",
          "amount",
          "country",
          "session_type",
          "mode"
        ],
        "properties": {
          "reference_id": {
            "$ref": "#/components/schemas/Payment_Session_ReferenceId"
          },
          "customer_id": {
            "$ref": "#/components/schemas/Payment_Session_CustomerId"
          },
          "customer": {
            "$ref": "#/components/schemas/Payment_Session_CustomerDetails"
          },
          "session_type": {
            "$ref": "#/components/schemas/Payment_Session_SessionTypePublicEnum"
          },
          "allow_save_payment_method": {
            "$ref": "#/components/schemas/Payment_Session_AllowSavePaymentMethodEnum"
          },
          "currency": {
            "$ref": "#/components/schemas/Payment_Session_CurrencyPublic"
          },
          "amount": {
            "$ref": "#/components/schemas/Payment_Session_Amount"
          },
          "mode": {
            "$ref": "#/components/schemas/Payment_Session_SessionModePublicEnum"
          },
          "capture_method": {
            "$ref": "#/components/schemas/Payment_Session_CaptureMethodEnum"
          },
          "country": {
            "$ref": "#/components/schemas/Payment_Session_CountryPublic"
          },
          "channel_properties": {
            "$ref": "#/components/schemas/Payment_Session_ChannelProperties"
          },
          "allowed_payment_channels": {
            "$ref": "#/components/schemas/Payment_Session_AllowedPaymentChannels"
          },
          "expires_at": {
            "$ref": "#/components/schemas/Payment_Session_ExpiresAt"
          },
          "locale": {
            "$ref": "#/components/schemas/Payment_Session_Locale"
          },
          "metadata": {
            "$ref": "#/components/schemas/Payment_Session_MerchantMetadata"
          },
          "description": {
            "$ref": "#/components/schemas/Payment_Session_Description"
          },
          "items": {
            "$ref": "#/components/schemas/Payment_Session_XenditStandardItemBasket"
          },
          "notification_channels": {
            "$ref": "#/components/schemas/Payment_Session_NotificationChannels"
          },
          "subscription": {
            "$ref": "#/components/schemas/Payment_Session_SubscriptionPublic"
          },
          "success_return_url": {
            "$ref": "#/components/schemas/Payment_Session_GenericReturnUrl"
          },
          "cancel_return_url": {
            "$ref": "#/components/schemas/Payment_Session_GenericReturnUrl"
          }
        }
      },
      "Payment_Session_StandardSessionResponsePublicSchema": {
        "type": "object",
        "properties": {
          "payment_session_id": {
            "$ref": "#/components/schemas/Payment_Session_SessionId"
          },
          "created": {
            "$ref": "#/components/schemas/Payment_Session_CreatedDateTime"
          },
          "updated": {
            "$ref": "#/components/schemas/Payment_Session_UpdatedDateTime"
          },
          "reference_id": {
            "$ref": "#/components/schemas/Payment_Session_ReferenceId"
          },
          "customer_id": {
            "$ref": "#/components/schemas/Payment_Session_CustomerId"
          },
          "session_type": {
            "$ref": "#/components/schemas/Payment_Session_SessionTypePublicEnum"
          },
          "allow_save_payment_method": {
            "$ref": "#/components/schemas/Payment_Session_AllowSavePaymentMethodEnum"
          },
          "currency": {
            "$ref": "#/components/schemas/Payment_Session_CurrencyPublic"
          },
          "amount": {
            "$ref": "#/components/schemas/Payment_Session_Amount"
          },
          "country": {
            "$ref": "#/components/schemas/Payment_Session_CountryPublic"
          },
          "mode": {
            "$ref": "#/components/schemas/Payment_Session_SessionModePublicEnum"
          },
          "capture_method": {
            "$ref": "#/components/schemas/Payment_Session_CaptureMethodEnum"
          },
          "channel_properties": {
            "$ref": "#/components/schemas/Payment_Session_ChannelProperties"
          },
          "allowed_payment_channels": {
            "$ref": "#/components/schemas/Payment_Session_AllowedPaymentChannels"
          },
          "expires_at": {
            "$ref": "#/components/schemas/Payment_Session_ExpiresAt"
          },
          "locale": {
            "$ref": "#/components/schemas/Payment_Session_Locale"
          },
          "metadata": {
            "$ref": "#/components/schemas/Payment_Session_MerchantMetadata"
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
          "status": {
            "$ref": "#/components/schemas/Payment_Session_SessionStatus"
          },
          "notification_channels": {
            "$ref": "#/components/schemas/Payment_Session_NotificationChannels"
          },
          "subscription": {
            "$ref": "#/components/schemas/Payment_Session_SubscriptionPublic"
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
          "payment_request_id": {
            "$ref": "#/components/schemas/Payment_Session_PaymentRequestId"
          },
          "business_id": {
            "type": "string"
          },
          "components_sdk_key": {
            "$ref": "#/components/schemas/Payment_Session_ComponentsSDKKey"
          },
          "components_configuration": {
            "$ref": "#/components/schemas/Payment_Session_ComponentsConfiguration"
          }
        }
      },
      "Payment_Session_ReferenceId": {
        "type": "string",
        "minLength": "1",
        "maxLength": "64",
        "description": "Your reference to uniquely identify the Payment Session. This is commonly used to identify your order or transaction."
      },
      "Payment_Session_CustomerId": {
        "type": "string",
        "minLength": "41",
        "maxLength": "41",
        "description": "A unique identifier automatically generated by Xendit to represent an end customer. This ID can be used as a consistent reference across multiple transactions or payment activities for the same user. You can create a customer object in advance through the Create Customer API here: https://xendit-docs.document360.io/apidocs/create-customer-request",
        "example": "cust-b98d6f63-d240-44ec-9bd5-aa42954c4f48"
      },
      "Payment_Session_CustomerDetails": {
        "type": "object",
        "required": [
          "type",
          "reference_id",
          "individual_detail"
        ],
        "properties": {
          "type": {
            "type": "string",
            "enum": [
              "INDIVIDUAL"
            ],
            "description": "Type of customer"
          },
          "reference_id": {
            "type": "string",
            "description": "Merchant provided identifier for the customer. Must be unique. Alphanumeric no special characters allowed"
          },
          "email": {
            "type": "string",
            "description": "E-mail address of customer. Maximum length 50 characters",
            "format": "email"
          },
          "mobile_number": {
            "type": "string",
            "description": "Mobile number of customer in E.164 format +(country code)(subscriber number)"
          },
          "individual_detail": {
            "$ref": "#/components/schemas/Payment_Session_XenditStandardIndividualDetail"
          }
        }
      },
      "Payment_Session_SessionTypePublicEnum": {
        "type": "string",
        "enum": [
          "SAVE",
          "PAY",
          "SUBSCRIPTION"
        ],
        "description": "The use case for Payment Session.\nSAVE: save the payment details from a customer for future payments.\nPAY: collects a one-time payment from a customer.\nSUBSCRIPTION: register a subscription payment for your customer using Xendit Subscription product, see here https://docs.xendit.co/docs/subscriptions-overview.\n"
      },
      "Payment_Session_AllowSavePaymentMethodEnum": {
        "type": "string",
        "enum": [
          "DISABLED",
          "OPTIONAL",
          "FORCED"
        ],
        "description": "The option to save the payment details from a customer for the PAY session_type.\nSaved payment details can be used for future payments.\nDISABLED: does not save the payment details.\nOPTIONAL: allows the customer to opt-in to save the payment details.\nFORCED: always save the payment details.\n"
      },
      "Payment_Session_CurrencyPublic": {
        "type": "string",
        "enum": [
          "IDR",
          "PHP",
          "VND",
          "THB",
          "SGD",
          "MYR",
          "USD"
        ],
        "description": "ISO 4217 three-letter currency code for the payment.",
        "example": "IDR"
      },
      "Payment_Session_Amount": {
        "type": "number",
        "minimum": "0",
        "description": "The payment amount to be collected from the customer.\nFor SAVE session_type, the amount must be 0.\n",
        "example": "10000"
      },
      "Payment_Session_SessionModePublicEnum": {
        "type": "string",
        "enum": [
          "PAYMENT_LINK",
          "COMPONENTS"
        ],
        "description": "The frontend integration mode for Payment Session.\nPAYMENT_LINK: redirect the customer to the Xendit Hosted Checkout page.\nCOMPONENTS: collect payment details from customer with Xendit Component SDK.\n"
      },
      "Payment_Session_CaptureMethodEnum": {
        "type": "string",
        "enum": [
          "AUTOMATIC",
          "MANUAL"
        ],
        "description": "The method to capture the payment.\nAUTOMATIC: capture the payment automatically.\nMANUAL: capture the payment manually using Payment Capture API\n"
      },
      "Payment_Session_CountryPublic": {
        "type": "string",
        "enum": [
          "ID",
          "PH",
          "VN",
          "TH",
          "SG",
          "MY"
        ],
        "description": "ISO 3166-1 alpha-2 two-letter country code for the country of transaction.",
        "example": "ID"
      },
      "Payment_Session_ChannelProperties": {
        "type": "object",
        "description": "Optional channel specific properties to be sent to specific payment channel provider.\n<iframe src=\"https://doc-widget.xendit.co/channel-table/session-optional/?iframe_id=channel-payment-iframe\" frameborder=\"0\" allowfullscreen=\"\" allow=\"accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture\" title=\"\" style=\"border:1px solid #ccc;width:100%;display:flex;margin-right:auto;max-height:800px;\" width=\"100%\" loading=\"lazy\" referrerpolicy=\"no-referrer-when-downgrade\"></iframe>\n"
      },
      "Payment_Session_AllowedPaymentChannels": {
        "type": "array",
        "description": "Specify the list of payment channels for your customer to select from the Xendit Hosted Checkout page.\nBy default all payment channels will be available if you leave this field empty.\n",
        "example": [
          "CARDS",
          "BRI_DIRECT_DEBIT",
          "DANA"
        ],
        "items": {
          "type": "string"
        }
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
      "Payment_Session_MerchantMetadata": {
        "type": "object",
        "nullable": "true",
        "description": "Key-value entries for your custom data/information.\nYou can specify up to 50 keys, with key names up to 40 characters and values up to 500 characters.\nThis is commonly used for your internal reference or reconciliation purposes. Xendit will not use this data for any processing.\n",
        "example": {
          "my_custom_id": "merchant-123",
          "my_custom_order_id": "order-123"
        }
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
      "Payment_Session_NotificationChannels": {
        "type": "array",
        "items": {
          "type": "string",
          "enum": [
            "EMAIL"
          ]
        },
        "description": "The list of notification channels to be used for the session."
      },
      "Payment_Session_SubscriptionPublic": {
        "type": "object",
        "nullable": "true",
        "description": "Subscription object for the session.",
        "required": [
          "schedule"
        ],
        "properties": {
          "schedule": {
            "$ref": "#/components/schemas/Payment_Session_SubscriptionSchedule"
          },
          "payment_link_for_failed_attempt": {
            "$ref": "#/components/schemas/Payment_Session_PaymentLinkForFailedAttempt"
          },
          "failed_cycle_action": {
            "$ref": "#/components/schemas/Payment_Session_FailedCycleAction"
          }
        }
      },
      "Payment_Session_GenericReturnUrl": {
        "type": "string",
        "description": "Specify the URL to redirect the customer after the session is completed or expired,\nor if the customer decide to stop the payment process.\nMust be HTTPS.\nFor example: \"https://yourcompany.com/example_item=my_example_item\"\n",
        "example": "https://yourcompany.com/example_item"
      },
      "Payment_Session_SessionId": {
        "type": "string",
        "minLength": "27",
        "maxLength": "27",
        "description": "A unique identifier for the Payment Session",
        "example": "ps-661f87c614802d6c402cd82d"
      },
      "Payment_Session_CreatedDateTime": {
        "type": "string",
        "format": "date-time",
        "example": "2021-12-31T23:59:59Z"
      },
      "Payment_Session_UpdatedDateTime": {
        "type": "string",
        "format": "date-time",
        "example": "2021-12-31T23:59:59Z"
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
      "Payment_Session_PaymentRequestId": {
        "type": "string",
        "nullable": "true",
        "description": "Xendit Payment Request ID used to reference the payment made during this Session.",
        "example": "pr-0800fe40-bb79-47ae-9d1e-e69394d3949c"
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
      "Payment_Session_XenditArrayOfErrors": {
        "type": "array",
        "nullable": "true",
        "items": {
          "oneOf": [
            {
              "type": "string"
            },
            {
              "type": "object"
            }
          ]
        }
      },
      "Payment_Session_XenditStandardIndividualDetail": {
        "type": "object",
        "required": [
          "given_names"
        ],
        "properties": {
          "given_names": {
            "type": "string",
            "description": "Primary or first name/s of customer. Alphanumeric. No special characters is allowed."
          },
          "surname": {
            "type": "string",
            "description": "Last or family name of customer. Alphanumeric. No special characters is allowed."
          },
          "nationality": {
            "type": "string",
            "description": "Country code for customer nationality. ISO 3166-1 alpha-2 Country Code"
          },
          "place_of_birth": {
            "type": "string",
            "description": "City or other relevant location for the customer birth place. Alphanumeric. No special characters is allowed."
          },
          "date_of_birth": {
            "type": "string",
            "description": "Date of birth of the customer. Format: YYYY-MM-DD"
          },
          "gender": {
            "enum": [
              "MALE",
              "FEMALE",
              "OTHER"
            ],
            "description": "Gender of customer"
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
      "Payment_Session_SubscriptionSchedule": {
        "type": "object",
        "description": "The schedule for the subscription.",
        "required": [
          "anchor_date",
          "interval",
          "interval_count"
        ],
        "properties": {
          "interval": {
            "$ref": "#/components/schemas/Payment_Session_ScheduleInterval"
          },
          "interval_count": {
            "$ref": "#/components/schemas/Payment_Session_ScheduleIntervalCount"
          },
          "total_recurrence": {
            "$ref": "#/components/schemas/Payment_Session_TotalRecurrence"
          },
          "anchor_date": {
            "$ref": "#/components/schemas/Payment_Session_AnchorDate"
          },
          "retry_interval": {
            "$ref": "#/components/schemas/Payment_Session_RetryInterval"
          },
          "retry_interval_count": {
            "$ref": "#/components/schemas/Payment_Session_RetryIntervalCount"
          },
          "total_retry": {
            "$ref": "#/components/schemas/Payment_Session_TotalRetries"
          },
          "failed_attempt_notifications": {
            "$ref": "#/components/schemas/Payment_Session_FailedAttemptNotifications"
          }
        }
      },
      "Payment_Session_PaymentLinkForFailedAttempt": {
        "type": "boolean",
        "description": "Whether to create a payment link for failed attempts."
      },
      "Payment_Session_FailedCycleAction": {
        "type": "string",
        "enum": [
          "RESUME",
          "STOP"
        ],
        "description": "Whether to resume or stop the subscription after a failed payment."
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
      "Payment_Session_ScheduleInterval": {
        "type": "string",
        "enum": [
          "DAY",
          "WEEK",
          "MONTH"
        ],
        "description": "The interval for the subscription."
      },
      "Payment_Session_ScheduleIntervalCount": {
        "type": "integer",
        "minimum": "1",
        "description": "The number of intervals between each subscription payment."
      },
      "Payment_Session_TotalRecurrence": {
        "type": "integer",
        "minimum": "1",
        "description": "The total number of payments to be made for the subscription."
      },
      "Payment_Session_AnchorDate": {
        "type": "string",
        "format": "date-time",
        "description": "The date to start the subscription from. Max allowed day of the month is 28. Supports time offset and UTC zero"
      },
      "Payment_Session_RetryInterval": {
        "type": "string",
        "enum": [
          "DAY",
          "WEEK",
          "MONTH"
        ],
        "description": "The interval to wait before retrying a failed payment."
      },
      "Payment_Session_RetryIntervalCount": {
        "type": "integer",
        "minimum": "1",
        "description": "The number of intervals to wait before retrying a failed payment."
      },
      "Payment_Session_TotalRetries": {
        "type": "integer",
        "minimum": "1",
        "description": "The total number of retries to be made for a failed payment."
      },
      "Payment_Session_FailedAttemptNotifications": {
        "type": "array",
        "items": {
          "type": "integer",
          "minimum": "1"
        },
        "description": "The list of failed attempt numbers to send notifications for."
      }
    },
    "responses": {
      "Payment_Session_CreateSessionError": {
        "description": "Error response for POST /sessions. Possible HTTP status codes: 400, 401, 404, 409.",
        "content": {
          "application/json": {
            "schema": {
              "type": "object",
              "required": [
                "error_code",
                "message"
              ],
              "properties": {
                "error_code": {
                  "type": "string",
                  "enum": [
                    "API_VALIDATION_ERROR",
                    "INVALID_AMOUNT",
                    "INVALID_PAYMENT_CHANNEL",
                    "INVALID_PRIMARY_PAYMENT_CHANNEL",
                    "INVALID_METADATA",
                    "INVALID_ITEM_METADATA",
                    "INVALID_CURRENCY",
                    "INVALID_COUNTRY",
                    "INVALID_CUSTOMER_ID",
                    "INVALID_URL",
                    "MISSING_CUSTOMER",
                    "DISALLOWED_CAPTURE_METHOD",
                    "INVALID_EXPIRY_DATE",
                    "ITEMS_NOT_SUPPORTED",
                    "SESSION_TYPE_NOT_SUPPORTED",
                    "MODE_NOT_SUPPORTED",
                    "INVALID_API_KEY",
                    "DATA_NOT_FOUND",
                    "DUPLICATE_ERROR"
                  ],
                  "description": "400 error codes:\n- `API_VALIDATION_ERROR` - Generic request validation failure such as missing required fields, invalid enum values, invalid field formats, or constraint violations (e.g. missing `session_type`, invalid `allow_save_payment_method` value, missing `cards_session_js` properties, invalid `components_configuration.origins`, missing `subscription.schedule` fields, `card_details` not allowed on `channel_properties.cards`, `recurring_configuration` required when `card_on_file_type` is RECURRING or MERCHANT_UNSCHEDULED, `internal_metadata` not allowed).\n- `INVALID_AMOUNT` - Amount validation failed. For PAY/SUBSCRIPTION session types, amount must be greater than zero. For SAVE session type, amount must be zero. Amount must also respect the decimal places allowed for the given currency.\n- `INVALID_PAYMENT_CHANNEL` - One or more requested payment channels are not recognized, not activated for your account, not supported for the requested session configuration, or no channels are available for the given `capture_method`, `allow_save_payment_method`, or country/currency combination.\n- `INVALID_PRIMARY_PAYMENT_CHANNEL` - A channel specified in `payment_link_configuration.primary_payment_channels` is not included in `allowed_payment_channels`.\n- `INVALID_METADATA` - Session-level metadata validation failed. Metadata supports a maximum of 20 keys, each key up to 40 characters, each value must be a string of up to 80 characters.\n- `INVALID_ITEM_METADATA` - Item-level metadata validation failed. Same constraints as session-level metadata.\n- `INVALID_COUNTRY` - The provided `country` is not supported.\n- `INVALID_CURRENCY` - The provided `currency` is not supported.`\n- `INVALID_CUSTOMER_ID` - The provided `customer_id` does not start with the required `cust-` prefix.\n- `INVALID_URL` - A URL field (e.g. `success_return_url`, `cancel_return_url`) is not a valid HTTPS URL.\n- `MISSING_CUSTOMER` - A `customer` object or `customer_id` is required but was not provided. Required when `session_type` is SAVE, when `mode` is CARDS_SESSION_JS, or when `allow_save_payment_method` is FORCED or OPTIONAL.\n- `DISALLOWED_CAPTURE_METHOD` - `capture_method` was provided for a session type that does not support it (e.g. SAVE or SUBSCRIPTION).\n- `INVALID_EXPIRY_DATE` - The provided `expires_at` value is invalid. It must be at least 10 minutes in the future and must not exceed the maximum allowed expiry duration.\n- `ITEMS_NOT_SUPPORTED` - `items` were provided for a session type other than PAY.\n- `SESSION_TYPE_NOT_SUPPORTED` - The provided `session_type` is not supported (e.g. AUTHORIZATION).\n- `MODE_NOT_SUPPORTED` - The provided `mode` is not supported.\n\n401 error codes:\n- `INVALID_API_KEY` - The API key provided is invalid or missing.\n\n404 error codes:\n- `DATA_NOT_FOUND` - The `customer_id` provided in the request does not exist.\n\n409 error codes:\n- `DUPLICATE_ERROR` - A customer with the same `reference_id` already exists for a different business.\n"
                },
                "message": {
                  "type": "string",
                  "description": "Human-readable description of the error."
                },
                "errors": {
                  "$ref": "#/components/schemas/Payment_Session_XenditArrayOfErrors"
                }
              }
            },
            "examples": {
              "apiValidationError": {
                "summary": "400 - Missing required field",
                "value": {
                  "error_code": "API_VALIDATION_ERROR",
                  "message": "request/body must have required property 'session_type'",
                  "errors": [
                    {
                      "message": "must have required property 'session_type'",
                      "path": "/body/session_type"
                    }
                  ]
                }
              },
              "invalidAmount": {
                "summary": "400 - Amount must be greater than zero",
                "value": {
                  "error_code": "INVALID_AMOUNT",
                  "message": "Amount must be greater than zero"
                }
              },
              "invalidPaymentChannel": {
                "summary": "400 - Payment channel not available",
                "value": {
                  "error_code": "INVALID_PAYMENT_CHANNEL",
                  "message": "Channel(s) INVALID_CHANNEL are not available. Please ensure that you have activated the necessary channels"
                }
              },
              "invalidPrimaryPaymentChannel": {
                "summary": "400 - Primary channel not in allowed channels",
                "value": {
                  "error_code": "INVALID_PRIMARY_PAYMENT_CHANNEL",
                  "message": "Primary channel BPI_DIRECT_DEBIT is not included in the requested channels"
                }
              },
              "invalidMetadata": {
                "summary": "400 - Metadata value exceeds limit",
                "value": {
                  "error_code": "INVALID_METADATA",
                  "message": "Metadata value must have at most 80 characters"
                }
              },
              "invalidItemMetadata": {
                "summary": "400 - Item metadata value exceeds limit",
                "value": {
                  "error_code": "INVALID_ITEM_METADATA",
                  "message": "Metadata value must have at most 80 characters"
                }
              },
              "invalidCustomerId": {
                "summary": "400 - Customer ID format invalid",
                "value": {
                  "error_code": "INVALID_CUSTOMER_ID",
                  "message": "Customer ID must start with \"cust-\""
                }
              },
              "invalidUrl": {
                "summary": "400 - Invalid URL format",
                "value": {
                  "error_code": "INVALID_URL",
                  "message": "Please provide a valid HTTPS URL"
                }
              },
              "missingCustomer": {
                "summary": "400 - Customer required but not provided",
                "value": {
                  "error_code": "MISSING_CUSTOMER",
                  "message": "Customer object or customer_id is required"
                }
              },
              "disallowedCaptureMethod": {
                "summary": "400 - Capture method not allowed for session type",
                "value": {
                  "error_code": "DISALLOWED_CAPTURE_METHOD",
                  "message": "Capture method is not supported for session type SAVE"
                }
              },
              "invalidExpiryDate": {
                "summary": "400 - Expiry date is invalid",
                "value": {
                  "error_code": "INVALID_EXPIRY_DATE",
                  "message": "expires_at must be at least 10 minutes in the future"
                }
              },
              "itemsNotSupported": {
                "summary": "400 - Items not allowed for session type",
                "value": {
                  "error_code": "ITEMS_NOT_SUPPORTED",
                  "message": "Items are allowed for session type PAY only"
                }
              },
              "sessionTypeNotSupported": {
                "summary": "400 - Session type not supported",
                "value": {
                  "error_code": "SESSION_TYPE_NOT_SUPPORTED",
                  "message": "session_type AUTHORIZATION is not supported for now"
                }
              },
              "modeNotSupported": {
                "summary": "400 - Mode not supported",
                "value": {
                  "error_code": "MODE_NOT_SUPPORTED",
                  "message": "mode INVALID_MODE is not supported for now"
                }
              },
              "invalidApiKey": {
                "summary": "401 - Invalid API key",
                "value": {
                  "error_code": "INVALID_API_KEY",
                  "message": "API key is not authorized for this API"
                }
              },
              "dataNotFound": {
                "summary": "404 - Customer ID does not exist",
                "value": {
                  "error_code": "DATA_NOT_FOUND",
                  "message": "The customer ID provided in the request does not exist"
                }
              },
              "duplicateError": {
                "summary": "409 - Duplicate customer reference_id",
                "value": {
                  "error_code": "DUPLICATE_ERROR",
                  "message": "customer: The reference_id entered has been used before. Please enter a unique reference_id"
                }
              }
            }
          }
        }
      },
      "Payment_Session_Generic5XXResponse": {
        "description": "Internal Server Error",
        "content": {
          "application/json": {
            "schema": {
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
                  ],
                  "description": "- `SERVER_ERROR` - Something unexpected happened. Please try again later.\n"
                },
                "message": {
                  "type": "string",
                  "description": "Human-readable description of the error."
                },
                "errors": {
                  "$ref": "#/components/schemas/Payment_Session_XenditArrayOfErrors"
                }
              }
            },
            "examples": {
              "serverError": {
                "summary": "500 - Internal server error",
                "value": {
                  "error_code": "SERVER_ERROR",
                  "message": "Something unexpected happened. We are investigating this issue. Please try again later."
                }
              }
            }
          }
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

