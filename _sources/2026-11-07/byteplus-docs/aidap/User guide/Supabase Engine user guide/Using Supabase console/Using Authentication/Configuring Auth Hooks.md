---
title: "Configuring Auth Hooks"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_Auth_Hooks"
---

**Auth Hooks** are an extension mechanism provided by Supabase Auth, allowing you to insert custom logic at key points in the user authentication process (such as before and after user creation, login, and sending email/SMS), enabling features like **email allowlist verification**, **custom token claims**, and **asynchronous event notifications**.

This topic introduces how to configure auth hooks for applications via the Supabase console or admin API. Currently, **8 types of hooks** are supported, along with the following enhancements:


* **Passing JWT Token**: HTTPS hooks can carry user JWTs for identity verification by the callback endpoint.

* **Asynchronous aggregation**: HTTPS hooks can batch trigger based on count or time thresholds to reduce pressure on the callback endpoint.


<div data-tips="true" data-tips-type="default">For detailed principles and design, refer to the official Supabase documentation <a href="https://supabase.com/docs/guides/auth/auth-hooks">Supabase Auth Hooks</a>.</div>


<span id="R8jPyBhs"></span>
## Typical applicable scenarios include:


<columns>
<columnsItem zoneid="DUoJXglbrL">

 **🛡️ Pre\-registration validation**

Verify whether the user's email and phone number comply with business rules (such as restricting company emails, filtering blacklists, etc.) through the **Before User Created** Hook and block registration if not compliant.

</columnsItem>
<columnsItem zoneid="Y0ieqRMp7E">

 **🔐 Customize JWT claims**

Inject business\-specific claims (such as tenant ID, role information) into JWT using the **Custom Access Token** Hook during issuance to extend the JWT's business semantics.

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="HJAB8AaPXi">

 **📨 Customize SMS/email templates**

take control of OTP and other notification sending logic through **Send SMS / Send Email** Hook to connect with the enterprise internal SMS gateway or email service.

</columnsItem>
<columnsItem zoneid="MvStRvDoYV">

 **📊 Asynchronous event notification**

asynchronously receive authentication events through **after user created / signed in / sms sent** hook to facilitate downstream processing such as user profiling, risk control, and data analysis.

</columnsItem>
</columns>


<span id="92MjBSQk"></span>
## Prerequisites


* A workspace using the Supabase engine is created, and its status is **Running**. For detailed steps, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* Succeeded in logging into the target workspace's Supabase console. For detailed steps, refer to [Logging in to the Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

* Obtained `SUPABASE_BASE_URL`, `SERVICE_ROLE_KEY`, and `SUPABASE_ANON_KEY`. For more information on obtaining variables, refer to [Obtaining variables](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables).


<span id="EQwv5EEr"></span>
## Query and modify configuration through the Supabase console


1. [Log in to the Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

2. Click **Authentication** in the left sidebar of the Supabase console to enter the **Authentication** page.

3. On the **Authentication** page, click the **Auth Hooks** tab.

4. Add or edit a hook:

   * Click the **Add hook** dropdown button, select the required hook type, and configure it.

   * Or click the **Configure hook** button on an existing hook to modify its configuration.

5. In the pop\-up configuration page, select the hook mode (**Postgres** or **HTTPS**) as needed, and complete the parameter configuration:

   * **Postgres mode**: select **Postgres schema** and **Postgres function**, then fill in the related statements. The Postgres function will be called when the hook is triggered.

   * **HTTPS mode**:

      1. Fill in the **URL** (callback address) and **Secret** (used to verify the request's legitimacy).

      2. (Optional) Enable **Include JWT in Header** to pass the user JWT token to the callback endpoint; if enabled, configure the **JWT Time\-to\-Live** (default 300 seconds).

      3. (Optional) Enable **Enable aggregation** to activate asynchronous aggregation; if enabled, configure the **Aggregation Count Threshold** (cumulative call count threshold) and **Aggregation Duration Threshold** (cumulative duration threshold).


<span id="ZrdrPPBO"></span>
### Supported hook list


|**Hook display name** |**HOOKNAME enum values** |**Trigger timing** |**Whether to block user interaction** |**Is PostgreSQL Function mode supported** |**Support HTTPS mode or not** |**Support passing user's JWT token** |**support async aggregation** |
|---|---|---|---|---|---|---|---|
|Before User Created |BEFORE_USER_CREATED |[trigger before creating user (auth.users table record)](https://supabase.com/docs/guides/auth/auth-hooks/before-user-created-hook) |Yes |Yes |Yes |Yes |No |
|Custom Access Token |CUSTOM_ACCESS_TOKEN |[Triggered before issuing the Access Token (JWT) to the user](https://supabase.com/docs/guides/auth/auth-hooks/custom-access-token-hook) |Yes |Yes |Yes |Yes |No |
|Send SMS |SEND_SMS |[Triggered before sending SMS to user](https://supabase.com/docs/guides/auth/auth-hooks/send-sms-hook) |Yes |Yes |Yes |Yes |No |
|Send Email |SEND_EMAIL |[Triggered before sending an Email to the user](https://supabase.com/docs/guides/auth/auth-hooks/send-email-hook) |Yes |Yes |Yes |Yes |No |
|Password Verification Attempt |PASSWORD_VERIFICATION_ATTEMPT |[Trigger before verifying password with user](https://supabase.com/docs/guides/auth/auth-hooks) |Yes |Yes |Yes |Yes |No |
|After User Created |AFTER_USER_CREATED |Triggered after user registration succeeds |No |Yes |Yes |Yes |Yes |
|After User Signed In |AFTER_USER_SIGNED |Triggered after user login succeeds |No |Yes |Yes |Yes |Yes |
|After SMS Sent |AFTER_SMS_SENT |Trigger after successfully sending an SMS to the user |No |Yes |Yes |Yes |Yes |


<span id="n3Da1GrF"></span>
### Main configuration item description

The main configuration items are as follows. Where `${HOOKNAME}` is a placeholder that should be replaced with the "HOOKNAME enum value" from the previous table.


|**Dashboard configuration name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|Enable hook |HOOK_${HOOKNAME}_ENABLED |bool |No<br><br> |Enable this hook. Values:<br><br><br>* `true`: yes (switch on).<br><br>* `false`: no (switch off). |
|URL |HOOK_${HOOKNAME}_URI |string |No |Callback URL under HTTPS mode. Required when Hook is under HTTPS mode. |
|Secret<br><br> |HOOK_${HOOKNAME}_SECRETS |string |No |Websocket secret carried in HTTPS mode:<br><br><br>* The default value is an empty string.<br><br>* The format of the customized value must meet one of the following two regular expressions:<br><br>   * `^v1,whsec_[A-Za-z0-9+/=]{32,88}`<br><br>   * `^v1a,whpk_[A-Za-z0-9+/=]{44,}:whsk_[A-Za-z0-9+/=]{44,}$` |
|Include JWT in Header |HOOK_${HOOKNAME}_ENABLE_JWT |bool |No |Under HTTPS mode, whether to send the user's JWT token, with values as follows:<br><br><br>* `true`: yes.<br><br>* `false`: no (default value). |
|JWT Time\-to\-Live (TTL) |HOOK_${HOOKNAME}_JWT_TTL |int |No |In HTTPS mode, the valid period of the user's JWT token is passed in seconds<br><br><br>* The value range is `[1,900]`<br><br>* The default value is `300` |
|Enable aggregation<br><br>&nbsp;<br><br> |HOOK_${HOOKNAME}_ENABLE_AGGREGATE |bool |No |Enable asynchronous aggregation. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no (default value). |
|Aggregation Count Threshold |HOOK_${HOOKNAME}_AGGR_COUNT_THRESHOLD |int |No |Threshold for the number of asynchronous aggregations in HTTPS mode:<br><br><br>* Value range: `[2, 10000]`.<br><br>* The default value is `100`.<br><br>* This parameter can be configured together with `HOOK_${HOOKNAME}_AGGR_DURATION_THRESHOLD`. If either of these two thresholds is met, the hook triggers, and counting and timing reset. |
|Aggregation Duration Threshold |HOOK_${HOOKNAME}_AGGR_DURATION_THRESHOLD |int |No |Duration threshold for asynchronous aggregation under HTTPS mode. Unit is second.<br><br><br>* Value range is `[60,43200]`.<br><br>* Default value is `300`.<br><br>* This parameter can be set together with `HOOK_${HOOKNAME}_AGGR_COUNT_THRESHOLD`. If either threshold is met, the hook triggers and resets the count and timer. |


<span id="KgTriHn7"></span>
## Query and modify configuration via Admin API

You can also query and modify Hook configuration via the [Auth module's Admin API](https://docs.byteplus.com/en/docs/aidap/Supabase-Using_Authentication)`/auth/v1/config/hooks` endpoint for automated deployment or integration into CI/CD workflows.


* Example for querying configuration


```Bash
curl -X GET $SUPABASE_BASE_URL/auth/v1/config/hooks \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json"
```



* Sample for modifying configuration, where body is a JSON map composed of the configuration key and configuration value from the previous section's table.


```Bash
curl -X PATCH $SUPABASE_BASE_URL/auth/v1/config/hooks \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  -d '{
    "HOOK_AFTER_USER_CREATED_ENABLED": true,
    "HOOK_AFTER_USER_CREATED_URI": "https://$SUPABASE_BASE_URL/functions/v1/after-user-created",
    "HOOK_AFTER_USER_CREATED_SECRETS": "v1,whsec_test",
    "HOOK_AFTER_USER_CREATED_ENABLE_JWT": true,
    "HOOK_AFTER_USER_CREATED_JWT_TTL": 900,
    "HOOK_AFTER_USER_CREATED_ENABLE_AGGREGATE": true,
    "HOOK_AFTER_USER_CREATED_AGGR_COUNT_THRESHOLD": 1,
    "HOOK_AFTER_USER_CREATED_AGGR_DURATION_THRESHOLD": 0,
    ...
  }'
```


<span id="oLPcQvKI"></span>
## Hook implementation example

The following example introduces the input/output contract and reference implementation of the Hook callback endpoint. The payload structure definitions for each Hook type can be further referenced in the [Supabase Auth Hooks official documentation](https://supabase.com/docs/guides/auth/auth-hooks).

<span id="4SjCT5dq"></span>
### Example of HTTPS Hook without enabled asynchronous aggregation type

Taking the **Before User Created** hook as an example, the HTTPS endpoint can be written as an Edge Function (implementing company email whitelist verification):

```TypeScript
Deno.serve(async (req) => {
  if (req.method !== "POST") {
    return new Response("Method Not Allowed", { status: 405 })
  }

  let payload: any
  try {
    payload = await req.json()
  } catch {
    return new Response(
      JSON.stringify({
        error: { http_code: 400, message: "Invalid JSON" }
      }),
      { status: 400, headers: { "Content-Type": "application/json" } }
    )
  }

  const email = payload?.user?.email ?? ""
  if (!email.endsWith("@bytedance.com")) {
    return new Response(
      JSON.stringify({
        error: { http_code: 400, message: "仅限公司邮箱注册。" }
      }),
      { status: 200, headers: { "Content-Type": "application/json" } }
    )
  }

  return new Response(JSON.stringify(payload), {
    status: 200,
    headers: { "Content-Type": "application/json" }
  })
})
```



* Input JSON example


```JSON
{
  "metadata": {
    "uuid": "1ac7639b-68fe-49be-af48-c3573168a950",
    "request_id": "20260327171750D1EAB27246339F4E5354",
    "time": "2026-03-30T09:35:07.008836097Z",
    "name": "before-user-created",
    "ip_address": "113.200.149.26",
    "workspace_id": "ws_xxx",
    "branch_id": "br_xxx"
  },
  "user": {
    "id": "5d3a681c-a031-41fb-8b57-55ea5d2337ab",
    "aud": "authenticated",
    "role": "",
    "email": "alex@bytedance.com",
    "phone": "",
    "app_metadata": {
      "provider": "email",
      "providers": [
        "email"
      ]
    },
    "user_metadata": {},
    "identities": [],
    "created_at": "0001-01-01T00:00:00Z",
    "updated_at": "0001-01-01T00:00:00Z",
    "is_anonymous": false
  },

  "user_id": "5d3a681c-a031-41fb-8b57-55ea5d2337ab",

  "aggr_count": 1,
  "aggr_start_time": "2026-03-30T09:35:07.008836097Z",
  "aggr_end_time": "2026-03-30T09:35:07.008836097Z"
}
```



* Output requirements



|**Hook result** |**HTTP Response Code** |**HTTP Response Body** |**Sample** |
|---|---|---|---|
|Succeeded<br><br> |200 |1. For the "Custom Access Token" hook, return a JSON string containing the `claims` structure; refer to [customizing user Access Tokens (JWT)](https://supabase.com/docs/guides/auth/auth-hooks/custom-access-token-hook) for details<br><br>2. For other hooks, returning an empty JSON string is allowed |1. Response example of “Custom Access Token” hook<br><br><br>```JavaScript```<br>```return new Response(```<br>```  JSON.stringify({```<br>```    claims,```<br>```  }),```<br>```  { status: 200, headers: { 'Content-Type': 'application/json'} }```<br>```)```<br><br><br><br>2. Response example of other hooks<br><br><br>```JavaScript```<br>```return new Response(```<br>```  JSON.stringify({}),```<br>```  { status: 200, headers: { "Content-Type": "application/json" } }```<br>```)```<br> |
|Failed |non 200 |JSON string containing error information |```JavaScript```<br>```return new Response(```<br>```  JSON.stringify({```<br>```    error: { ```<br>```      http_code: 400, ```<br>```      message: "Please sign up with a company email address.'" ```<br>```    },```<br>```  }),```<br>```  { status: 400, headers: { "Content-Type": "application/json" } }```<br>```)```<br> |


<span id="riLeCpXH"></span>
### Example of HTTPS Hook with enabled asynchronous aggregation type


* Input JSON example


```JSON
{
  "metadata": {
    "uuid": "1ac7639b-68fe-49be-af48-c3573168a950",
    "request_id": "20260327171750D1EAB27246339F4E5354",
    "time": "2026-03-30T09:35:07.008836097Z",
    "name": "before-user-created",
    "ip_address": "113.200.149.26",
    "workspace_id": "ws_xxx",
    "branch_id": "br_xxx"
  },
  "user": {},
  "user_id": "",

  "aggr_count": 3,
  "aggr_start_time": "2026-03-30T09:34:07.008836097Z",
  "aggr_end_time": "2026-03-30T09:36:27.008836097Z"
}
```



* Output requirement: consistent with the output requirement of non\-asynchronous aggregation


<span id="y3DIBcNR"></span>
### Example of PostgreSQL function

Still taking BEFORE_USER_CREATED as an example, the PostgreSQL hook function is written as follows:

```TypeScript
Deno.serve(async (req) => {
  if (req.method !== "POST") {
    return new Response("Method Not Allowed", { status: 405 })
  }

  let payload: any
  try {
    payload = await req.json()
  } catch {
    return new Response(
      JSON.stringify({
        error: { 
          http_code: 400, 
          message: "Invalid JSON" 
        },
      }),
      { status: 400, headers: { "Content-Type": "application/json" } }
    )
  }

  const email = payload?.user?.email ?? ""
  if (!email.endsWith("@example.com")) {
    return new Response(
      JSON.stringify({
        error: { 
          http_code: 400, 
          message: "Please sign up with a company email address.'" 
        },
      }),
      { status: 200, headers: { "Content-Type": "application/json" } }
    )
  }

  return new Response(JSON.stringify(payload), {
    status: 200,
    headers: { "Content-Type": "application/json" }
  })
})
```


<span id="y1kjHx7Z"></span>
## Timeout and retry mechanism

&nbsp;

The timeout and retry rules for different hook modes are as follows:


|**Hook mode** |**Single execution timeout** |**Failed Retry strategy** |**Overall timeout** |
|---|---|---|---|
|PostgreSQL Function |3 seconds |Failed/timeout, retry after 2 seconds, up to 3 times (including the first) |— |
|HTTPS (async aggregation not Enabled) |8 seconds |Retry every 2 seconds after failure/timeout, up to 3 times (including the first time). |Blocking hook: 30 seconds; non\-blocking hook: 1 minute |
|HTTPS (asynchronous aggregation enabled) |15 seconds |Failed/timeout, retry after 2 seconds, up to 3 times (including the first) |Blocking hook: 30 seconds; non\-blocking hook: 1 minute |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After exceeding the retry limit, the system will no longer retry and only record error logs. Whether the hook blocks user interaction can be referenced in the "Does it block user interaction" field in the "Supported hook list" above.</div>
