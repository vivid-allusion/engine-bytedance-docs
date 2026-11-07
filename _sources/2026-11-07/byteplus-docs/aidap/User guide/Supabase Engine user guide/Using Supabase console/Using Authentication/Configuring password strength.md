---
title: "Configuring password strength"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_password_strength"
---

This topic describes configuring password strength for your application through the Supabase console and Admin API.

<span id="euGzcnTR"></span>
## Precautions

You can configure password strength via the Supabase console or API. Note that although the configuration item is located under **Authentication** \> **Providers** \> **Email** in the console, this password policy is a global setting and applies to all providers****.

<span id="Ceht9Jd9"></span>
## Query and modify configurations in the Supabase console

<span id="GaiEzk0O"></span>
### Prerequisites


* A workspace using the Supabase engine is created, and its status is **Running**. For detailed steps, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* Succeeded in logging into the target workspace's Supabase console. For detailed steps, refer to [Logging in to the Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).


<span id="m0jNLwDx"></span>
### Procedure

The Supabase console provides four preset password strength levels.

This configuration item is located on the **Authentication** \> **Providers** \> **Email** workspace settings page and applies to the entire project after adjustment.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_80a9c6232c9d6266b189207cc6aa825b.png) </span>

&nbsp;

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f601ebb7d518fbb497b2164ec8fc63a6.png) </span>

<span id="ZEWSRgsX"></span>
### Configuration item description


|**Dashboard configuration item name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|Minimum Password Length |PASSWORD_MIN_LENGTH |int<br><br> |No |Minimum length of the password.<br><br><br>* The default value is 6.<br><br>* The minimum value is 6. |
|Password Requirements |PASSWORD_REQUIRED_CHARACTERS |string |No |Password character set list. Character range used to validate the password.<br><br><br>* Value is a multi\-segment string separated by English colons. Each segment represents a character set. The password must contain at least one character from each character set.<br><br>* Dashboard provides four built\-in options as shown in the table below.<br><br>* Users can also customize the character set list. |


The character set list for passwords (`PASSWORD_REQUIRED_CHARACTERS`) in the Supabase console includes the following built\-in options.


|**Built\-in options on the dashboard** |**Value** |
|---|---|
|No strength requirement (default) |"" (empty string) |
|Letters + numbers |abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ:0123456789 |
|Uppercase letter + lowercase letter + number |abcdefghijklmnopqrstuvwxyz:ABCDEFGHIJKLMNOPQRSTUVWXYZ:0123456789 |
|Uppercase letter + lowercase letter + number + symbol |abcdefghijklmnopqrstuvwxyz:ABCDEFGHIJKLMNOPQRSTUVWXYZ:0123456789:!@#$%^&\*()_+\-=[]{};\'\\:"\|<\>?,./`~ |


<span id="XxMtOva9"></span>
## Query and modify configuration via Admin API

The above parameters can be queried and modified using the [Auth module Admin API](https://docs.byteplus.com/en/docs/aidap/Supabase-Using_Authentication) /auth/v1/config.


* Example of querying configuration


```Bash
curl -X GET $SUPABASE_BASE_URL/auth/v1/config \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json"
```



* Sample for modifying configuration. Where body is a JSON map composed of configuration item keys and configuration item values from the previous table


```Bash
curl -X PATCH $SUPABASE_BASE_URL/auth/v1/config \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  -d '{
       "PASSWORD_MIN_LENGTH": true,
       "PASSWORD_REQUIRED_CHARACTERS": "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ:0123456789"
      }'
```
