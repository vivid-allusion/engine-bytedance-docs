---
title: "Configuring email-based registration and login"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_email-based_registration_and_login"
---

This topic describes the process of configuring email login for applications through the Supabase console and Admin API.

<span id="qYxRmKKI"></span>
## Prerequisites


* A workspace using the Supabase engine is created, and its status is **Running**. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

* obtained `SUPABASE_BASE_URL`, `SERVICE_ROLE_KEY`, and `SUPABASE_ANON_KEY`. For more information on obtaining variables, refer to [Obtaining variables](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables).


<span id="YUykh7VN"></span>
## Query and modify configurations in the Supabase console


1. Complete email login configuration

   1. In the Supabase console, click **Authentication** on the left to enter the **Authentication ** page.

   2. On the **authentication** page, click **Configure** \> **Emails** to enter the **Emails** page

   3. On the **Emails** page, configure email login and email templates separately.

      * Click the **SMTP Settings** tab, turn on the **Enable Custom SMTP** switch, then configure email logins.

      * (Optional) Click **Templates** to view and modify various email templates. Supabase provides default templates that can be customized. Templates can reference variables using the `{{ }}` format, such as `{{ .ConfirmationURL }}`.

2. Set whether email verification is required.

   1. In the Supabase console, click **Authentication** on the left to enter the **Authentication ** page.

   2. On the **Authentication** page, click **Configure** \> **Sign In / Providers** to enter the **Sign In / Providers** page.

   3. On the **Sign In / Providers** page, locate the **User Signups** area, enable the **Confirm email** toggle, then click **Save changes**.


<span id="X0cW8uXr"></span>
### **Main configuration item description**


|**Dashboard configuration item name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|Sender email |SMTP_ADMIN_EMAIL<br><br> |string |Yes |Sender email. |
|Sender name |SMTP_SENDER_NAME |string |Yes |Sender name |
|Host |SMTP_HOST |string |Yes |SMTP server address |
|Port number |SMTP_PORT |string |Yes |SMTP server port. Must be a valid port number string, such as "465" or "587" |
|Minimum interval between emails being sent |SMTP_MAX_FREQUENCY |int |No<br><br> |Minimum email sending interval. The default value is 60 seconds. The unit is second. |
|Username |SMTP_USER |string |Yes |SMTP server user name |
|Password |SMTP_PASS |string |Yes |SMTP server password |
|Confirm email |MAILER_AUTOCONFIRM |bool |No<br><br> |Whether user verification of the email is required. Values:<br><br><br>* `true`: skip verification (switch off), default value.<br><br>* `false`: verification required (switch on). |


<span id="VZDIVmfF"></span>
## Query and modify configuration via Admin API

The above parameters can be queried and modified using the [Auth module Admin API](https://docs.byteplus.com/en/docs/aidap/Supabase-Using_Authentication) /auth/v1/config.


* Sample for querying configuration


```Bash
curl -X GET $SUPABASE_BASE_URL/auth/v1/config \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json"
```



* Sample for modifying configuration, where body is a JSON map composed of the configuration key and configuration value from the previous section's table.


```Bash
curl -X PATCH $SUPABASE_BASE_URL/auth/v1/config \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  -d '{
       "SMTP_ADMIN_EMAIL": true,
       "SMTP_SENDER_NAME": "test-sender",
       "SMTP_HOST": "smtp.qq.com",
       "SMTP_PORT": "465",
       "SMTP_USER": "test-user",
       "SMTP_PASS": "test-pwd",
       "MAILER_AUTOCONFIRM": false,
       ...
      }'
```


<span id="VMc9NT6q"></span>
## Sample \- email registration and login using the Supabase Client SDK


* Sample for email registration


```JavaScript
import { createClient } from '@supabase/supabase-js'
const supabase = createClient(
  "<SUPABASE_BASE_URL>",
  "<SUPABASE_ANON_KEY>")

// email registration
async function signUp() {
  const { data, error } = await supabase.auth.signUp({
    email: 'user@example.com',
    password: 'password123'
  })

  if (error) {
    console.log('注册失败:', error.message)
    return
  }
  console.log('注册成功，请查收邮箱验证', data)
}
```



* Sample for Email login


```JavaScript
import { createClient } from '@supabase/supabase-js'
const supabase = createClient(
  "<SUPABASE_BASE_URL>",
  "<SUPABASE_ANON_KEY>")

// account and password login
async function signIn() {
  const { data, error } = await supabase.auth.signInWithPassword({
    email: 'user@example.com',
    password: 'password123'
  })

  if (error) {
    console.log('登录失败:', error.message)
    return
  }
  console.log('登录成功', data.user)
}
```
