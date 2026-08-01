---
title: "List accounts"
slug: "list-accounts"
updated: 2026-07-09T07:00:03Z
published: 2026-07-09T07:00:03Z
canonical: "docs.xendit.co/list-accounts"
---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.xendit.co/llms.txt
> Use this file to discover all available pages before exploring further.

# List accounts

Get/v2/accounts

Use this endpoint to retrieve information about your sub accounts. You can filter by email, creation date, type, name, or status. The results are paginated and ordered by creation date

> Use API key permission Accounts Read to perform this request

> This endpoint is backward compatible with Accounts created using the /accounts endpoint

SecurityHTTPType basic

Query parametersemailarray of string

The email addresses of the accounts that will be filtered. If not specified, all account emails will be returned.

Item Max length255Item Exampletest@example.co
statusarray of string

The statuses of the accounts that will be filtered. If not specified, all account status will be returned.

Valid Item values[
  "INVITED",
  "REGISTERED",
  "AWAITING_DOCS",
  "PENDING_VERIFICATION",
  "LIVE",
  "SUSPENDED"
]
public_profile.business_namestring

The public profile or business name of the accounts that will be filtered. If not specified, all account business name will be returned. This is the business name specified during account creation

typestring

The type of accounts that will be filtered. If not specified, all account types will be returned.

Valid values[
  "MANAGED",
  "OWNED"
]
created[gte]string

Start time of accounts by created date. If not specified will list all dates.

created[lte]string (date-time) 

End time of accounts by created date. If not specified will list all dates.

updated[gte]string (date-time) 

Start time of accounts by updated date. If not specified will list all dates.

updated[lte]string (date-time) 

End time of accounts by updated date. If not specified will list all dates.

limitnumber

A limit on the number of transactions to be returned for each request.

Minimum1.0Maximum50.0Default10.0
before_idstring

ID of the immediately following item.

after_idstring

ID of the immediately previous item. Use this with links on the response for pagination.

Responses200<select class='api-response-data' aria-label='Media type'><option value='cc3b69a4-53ba-4f55-9668-71e65c6f854e'>application/json</option>
</select><select class='select-example' aria-label='Media type'><option value='27736d1a-b6a6-4eb2-a588-55c73b49e2f1'>Get Owned Account Response</option>
</select>Get Owned Account Response

```json
{
  "data": [
    {
      "id": "5cafeb170a2b18519b1b8761",
      "created": "2021-01-01T10:00:00Z",
      "updated": "2021-01-01T10:00:00Z",
      "type": "OWNED",
      "email": "angie@pinkpanther.com",
      "public_profile": {
        "business_name": "Angie's lemonade stand"
      },
      "status": "LIVE"
    },
    {
      "id": "3cafeb170a2b18519b1b8762",
      "created": "2023-03-22T09:15:00Z",
      "updated": "2023-03-22T09:30:00Z",
      "type": "MANAGED",
      "email": "carol@cooldrinks.com",
      "public_profile": {
        "business_name": "Carol's Cool Drinks"
      },
      "status": "LIVE"
    }
  ],
  "has_more": true,
  "links": [
    {
      "href": "/v2/accounts?after_id=623ace8270bbddf93816b3g1",
      "rel": "next",
      "method": "GET"
    }
  ]
}
```

Expand Allobject  data Array of object (ListAccountResponseSchema)   object  idstring    

ID of your Account, use this in the for-user-id header to create transactions on behalf of your Account

createdstring  (date-time)    

Timestamp of when the object was created

updatedstring  (date-time)    

Timestamp of when the object was updated

typestring    

The type of account created

Valid values[
  "MANAGED",
  "OWNED"
]
emailstring  (email)    

A valid email address associated with the object

Max length255Exampletest@example.co
public_profileobject (public_profile)  business_namestring    

Public name of the account.

descriptionstring    

Additional description visible publicly.

countrystring    

The country (based on ISO 3166-1 Alpha-2) of incorporation for a business, or the country of residence for an individual.

Valid values[
  "ID",
  "PH",
  "VN",
  "MY",
  "TH"
]
statusstring    

Status of the Account you are creating.

Valid values[
  "INVITED",
  "REGISTERED",
  "AWAITING_DOCS",
  "PENDING_VERIFICATION",
  "LIVE",
  "SUSPENDED"
]

has_moreboolean    

Indicates whether there are more items to be queried with `after_id` of the last item from the current result. Use the `links` to follow to the next result.

links Array of object   

The links to the next page based on HATEOAS if there is next result. The HATEOAS format are: `href`: URI of target, this will be to the next link. `rel`: The relationship between source and target. The value will be `next`. `method`: The HTTP method, the value will be `GET`.

object  hrefstring    
relstring    
methodstring    

400

Bad Request

<select class='api-response-data' aria-label='Media type'><option value='029e78c9-b296-4a9a-af20-ad117823a0cb'>application/json</option>
</select>object  

Inputs are failing validation. The errors field contains details about which fields are violating validation.

error_codestring    Valid values[
  "API_VALIDATION_ERROR",
  "INVALID_CONFIGURATION",
  "INVALID_JSON_FORMAT",
  "TYPE_AND_CONFIGURATION_CONFLICT",
  "INVALID_SOURCE_OR_DESTINATION_ERROR",
  "INSUFFICIENT_BALANCE",
  "INVALID_FEE_AMOUNT",
  "DUPLICATE_ERROR",
  "INVALID_AMOUNT",
  "INSUFFICIENT_ACCOUNT_HOLDER_DATA",
  "MISMATCH_PAYLOAD_FOR_REFERENCE",
  "INVALID_URL_FORMAT"
]
messagestring    
errors Array  OneOfstringstring
objectobject

404

Not Found

<select class='api-response-data' aria-label='Media type'><option value='137dc97d-0333-4c69-a585-50d60c67c798'>application/json</option>
</select>object  

The object being referenced does not exist

error_codestring    Valid values[
  "DESTINATION_ACCOUNT_NOT_FOUND",
  "DATA_NOT_FOUND",
  "CALLBACK_AUTHENTICATION_TOKEN_NOT_FOUND_ERROR"
]
messagestring    
errors Array  OneOfstringstring
objectobject
