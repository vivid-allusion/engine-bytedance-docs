---
title: "Create Temporary Token"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/create-temporary-token"
---

Temporary tokens are used in scenarios where different end users call OpenAPI in different identities under the same application token. When creating a temporary Token, it only verifies whether the application Token exists, and does not verify whether the bound user has project or resource permissions; the actual permissions are checked by the subsequent business OpenAPI according to the bound user during the use phase.

# Interface definition

|**Field** |**Description** |
|---|---|
|Method |POST |
|Path |`/marketing_agent/api/v2/open_application/user_application/temporary_token/create` |
|Content\-Type |`application/json` |
|authentication method |`Authorization: Bearer < Application Token >` |

# Request Header

|**Header** |**Required** |**Description** |
|---|---|---|
|Authorization |Yes |Fixed application token in the format `Bearer < app_token >`. The `app_token` here is the AK returned by the application. |

> **说明**

> Creating a temporary token does not require `X-Org`/ `X-Tenant`or `api_paths`/ `tenant_id`. These capability boundaries come from the application token itself.

# Request body

|**Field** |**Type** |**Required** |**Description** |
|---|---|---|---|
|user |string |Yes |End user account for temporary Token binding. When calling OpenAPI with a temporary token later, the system will pass the account as an `X-User`to the downstream interface. |
|expire_minutes |integer |No |Token valid period in minutes. Do not pass the default 7 days, that is, `10080`minutes; the maximum 1 year, that is, `525600`minutes; must be greater than 0. |

## cURL example

```Bash
curl --location 'https://your-domain/marketing_agent/api/v2/open_application/user_application/temporary_token/create' \\
  --header 'Authorization: Bearer <APP_TOKEN_AK>' \\
  --header 'Content-Type: application/json' \\
  --data '{
    \"user\": \"user@example.com\",
    \"expire_minutes\": 10080
  }'
```

## Successful response

The interface returns the open API unified response structure: `code/msg/message/data`. Success `code = 0`.

|**Field** |**Type** |**Description** |
|---|---|---|
|data.token |string |Generated Temporary Token plaintext. This value is displayed only once in this response, and the server level database only saves the hash. |
|data.notice |string |Fixed Tip: `The token is only displayed once in clear text, please save it properly`. |
|data.expires_at |integer |Temporary Token expiration time, Unix second timestamp. |
|data.account |string |The end user account bound to the temporary token, corresponding to the `user`in the request body. |
|data.user_application_id |integer |The application record ID corresponding to the application Token is only used to locate the application. |
|data.org_id |integer |The organization ID to which the application Token belongs. |

```JSON
{
  \"code\": 0,
  \"msg\": \"success\",
  \"message\": \"success\",
  \"data\": {
    \"token\": \"tmp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx\",
    \"notice\": \"This token is only displayed in plain text once, please save it properly\",
    \"expires_at\": 1780157073,
    \"account\": \"user@example.com\",
    \"user_application_id\": 123,
    \"org_id\": 1
  }
}
```

# API Invoke Using Temporary Tokens

After the temporary token is successfully created, the way to call the business OpenAPI can be seen [Step 2: Use Token to invoke the API](https://docs.byteplus.com/docs/dataagent/Enterprise_Knowledge_Engine_OpenAPI#c58aa895), that is, use `Authorization: Bearer < token >`, and continue to pass `X-Org`and `X-Tenant`. The system will first identify the temporary Token, check its associated application Token, reuse the application Token project and interface authority verification, and pass the user account bound to the temporary Token to the downstream interface as `X-User`.

# Common mistakes

|**Error message** |**Reason** |**Solution** |
|---|---|---|
|`Authorization missing` |Authorization Header not provided |Add the application token header when creating a temporary token. |
|`Need bearer auth` |Authorization format error |Use the `Bearer < app_token >`format. |
|`invalid app token` |Application Token does not exist |Check if the application token is correct. |
|`user account is missing` |User is empty |Pass in the user account to be bound in the request body. |
|`expire_minutes must be positive` |Valid period less than or equal to 0 |Enter the number of minutes greater than 0. |
|`expire_minutes must be <= 525600` |Valid period more than 1 year |The valid period is controlled within 525600 minutes. |

# Key constraint

* When creating a temporary token, it is not checked whether the bound user has project or resource permissions; the actual permissions are checked by the downstream interface according to the bound user during use.

* No `token_type` is returned in the response. The returned `token` is the original certificate, and the caller can put `Authorization: Bearer < token >` according to the open API convention.

* The temporary token plaintext is only displayed once, and the server level only saves the hash; the caller needs to save it properly.

* Temporary Token status currently includes: `1 = ACTIVE`available, `2 = REVOKED`revoked; expired by `expires_at`.
