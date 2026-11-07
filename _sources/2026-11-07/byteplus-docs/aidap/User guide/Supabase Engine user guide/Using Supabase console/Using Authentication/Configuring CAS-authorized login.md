---
title: "Configuring CAS-authorized login"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_CAS-authorized_login"
---

CAS (Central Authentication Service) is an open\-source single sign\-on (SSO) protocol for web applications. Its core is to enable a single login to access multiple trusted systems through a central authentication server, using a ticket mechanism to ensure security and stateless interaction.

Supabase supports CAS\-authorized login through simple configuration.

<span id="tgeSucn9"></span>
## Prerequisites


* A workspace using the Supabase engine is created, and its status is **Running**. For detailed steps, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* Succeeded in logging into the target workspace's Supabase console. For detailed steps, refer to [Logging in to the Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

* Obtained `SUPABASE_BASE_URL`, `SERVICE_ROLE_KEY`, and `SUPABASE_ANON_KEY`. For more information on obtaining variables, refer to [Obtaining variables](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables).


<span id="nVYsnru2"></span>
## Procedure


1. Query and modify configuration

   1. Query and modify configuration in the Supabase console

      1. Configure CAS\-related parameters

         Enter Authentication \-\> Sign In / Providers \-\> CAS page, check "Enable CAS provider," and fill in CAS\-related parameters.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f4706cb4dcb3cd55adbcf4e4e895c441.png) </span>

      2. Configure redirect allowlist

         Enter Authentication \-\> URL Configurations page, add your app's URL (the redirect target after successful login, including the path) into Redirect URLs.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_665f6529bad9cc0cc1d18d86e6f25eb6.png) </span>

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_27e6b0f119f714a8facd25a8d72f9034.png) </span>


<span id="hA2n6DLy"></span>
### Main configuration item description


|**Dashboard configuration item name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|Enable CAS provider |EXTERNAL_CAS_ENABLED |bool |Yes |Enable CAS authorization login. Values:<br><br><br>* true: yes (switch ON)<br><br>* false: no (switch OFF) |
|CAS Server URL |EXTERNAL_CAS_URL |string |Yes |CAS Server address. Values: |
|CAS Protocol Version |EXTERNAL_CAS_VERSION |string |Yes |CAS server version. Values:<br><br><br>* `2.0`: CAS 2.0<br><br>* `3.0`: CAS 3.0 |
|Allow users without an email |EXTERNAL_CAS_EMAIL_OPTIONAL |bool |Yes |Allow the Email field in CAS Response to be empty. Values:<br><br><br>* `false`: login will fail if the Email field is empty. Default value.<br><br>* `true`: whether the Email field is empty does not affect user login.<br><br><br> |
|Email attribute key |EXTERNAL_CAS_EMAIL_KEY |string |Yes |Key representing the Email field in CAS Response (case\-sensitive).<br><br><br>* The default value is `email`.<br><br>* If not empty, the value of this key extracted from CAS Response will be used as the user's unique identifier. |
|Phone attribute key |EXTERNAL_CAS_PHONE_KEY |string |No |Key representing the Phone field in CAS Response (case\-sensitive).<br><br><br>* The default value is "" (an empty string).<br><br>* If not empty, attempts to extract the value of this key from CAS Response and save it as the user’s phone number.<br><br><br> |
|Callback URL (for OAuth)<br><br> |EXTERNAL_CAS_REDIRECT_URI |string |No<br><br> |CAS callback address, which can be one of the following two:<br><br><br>1. Supabase Callback interface address `/auth/v1/callback` (default).<br><br>2. Service callback interface address under the developer domain. It must redirect to the Supabase Callback interface address, passing through all parameters of the callback request (including query parameters, headers, and body). |
|Display name attribute key |EXTERNAL_CAS_DISPLAY_NAME_KEY |string |No |The key representing the user's display name in CAS Response (case\-sensitive).<br><br><br>* The default value is "" (an empty string).<br><br>* If not empty, extracts the value of this key from CAS Response and saves it as user metadata. |
|Redirect URLs |URI_ALLOW_LIST |string | |List of target URLs allowed for redirection.<br><br><br>* Must exactly match the target URL, precise to the path<br><br>* If multiple, separate with commas, in the form of: `http://www.app1.com/home,https://www.app2.com` |



   2. Query and modify configuration via Admin API

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
       "EXTERNAL_CAS_ENABLED": true,
       "EXTERNAL_CAS_URL": "https://cas.example.com/cas",
       "EXTERNAL_CAS_VERSION": "3.0",
       "EXTERNAL_CAS_EMAIL_OPTIONAL": false,
       "EXTERNAL_CAS_EMAIL_KEY": "email",
       "URI_ALLOW_LIST": "http://www.app1.com/home,https://www.app2.com",
       ...
      }'
```



2. Configure CAS Client Service URL on the CAS Server

   1. Copy the Supabase Callback URL: on the Supabase CAS configuration page, click the "Copy" button in the "Callback URL (for OAuth)" textbox to copy, obtaining a URL similar to `https://br-xxx.supabase.aidap-global.cn-beijing.volces.com/auth/v1/callback`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe4caf3e5ecc76c934d3062216e7efb9.png) </span>

   2. Configure the CAS Client Service URL on the CAS Server to the Supabase domain

      Modify the above URL to a regular expression, paying attention to escaping the dots (.) and the wildcard at the end (.\*$), for example: `^https://br-xxx\\.supabase\\.aidap-global\\.cn-beijing\\.volces\\.com/auth/v1/callback.*$`.

      Set the modified string as the CAS Client Service URL on the CAS Server, as shown in the example below.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e58a59b2901f5b630e42eb4bab2cc3bd.png) </span>


<span id="Zb7URLhS"></span>
## Sample

Authenticate login via CAS using Supabase Client SDK

Call the signInWithOAuth function for authorized login, specifying `provider` as `cas`.

```JavaScript
import { createClient } from '@supabase/supabase-js'
const supabase = createClient(
  "<SUPABASE_BASE_URL>",
  "<SUPABASE_ANON_KEY>")

// phone number + SMS verification code (OTP) login
async function signInWithCAS() {
  try {
    const { error } = await supabase.auth.signInWithOAuth({
      provider: 'cas', // specify provider as cas
      options: {
        redirectTo: 'https://www.examples.com/' // redirect address after successful login
      }
    });

    if (error) throw error;

  } catch (error) {
    console.error('CAS授权登录失败:', error);
  }
}
```
