---
title: "Configuring DingTalk authorized login"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Configuring_DingTalk_authorized_login"
---

This topic describes the process of configuring DingTalk login for applications through the Supabase console and Admin API.

<span id="C2IelmrP"></span>
## Prerequisites


* A workspace using the Supabase engine is created, and its status is **Running**. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

* obtained `SUPABASE_BASE_URL`, `SERVICE_ROLE_KEY`, and `SUPABASE_ANON_KEY`. For more information on obtaining variables, refer to [Obtaining variables](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables).


<span id="u1p1aITB"></span>
## Precautions

Currently only OAuth login via web (browser) is supported, including PC\-side QR code login and mobile browser account/password or redirect authorization. DingTalk client H5 micro\-app silent login is not supported yet.


|Scenario |Supported or not |Decscription |
|---|---|---|
|Scan QR code to login on PC browser |Support |Standard OAuth2 redirect to DingTalk login page |
|mobile browser OAuth login |Support |At the same authorized address, the mobile client will display account and password or launch the DingTalk app for authorization |
|H5 micro application login\-free in DingTalk |Not support |Requires using JSAPI to obtain corpAccessToken + login\-free code, using a different set of interfaces |
|DingTalk mobile SDK login (iOS/Android) |Not support |Native SDK is required to initiate DingTalk authorization |


<span id="rCPLcUKi"></span>
## Query and modify configurations in the Supabase console


1. Log in to [DingTalk developer console](https://open-dev.dingtalk.com/#/loginMan), on the target app details page, click **Development configuration** \> **Security settings**, and fill in the **Redirect URL (callback domain)** .

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a7b65f185df51336de891c4b0feb2393.png) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The Supabase callback URL is <code>$SUPABASE_BASE_URL/auth/v1/callback</code>, for example <code>https://br-xxxx.supabase.aidap-global.cn-beijing.volces.com/auth/v1/callback</code>.   </div>
   

2. Query and modify configuration

   1. Query and modify configuration in the Supabase console

      1. Configure DingTalk related parameters

         1. On the DingTalk developer platform, find your app \> credentials and basic info, and get your **Client ID** and **Client Secret**.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_67354924ff62ae79a88b2617e1e10cef.png) </span>

         2. After entering the Supabase console, you need to configure DingTalk as an OAuth 2.0 provider and enter the corresponding credentials. Enter the page **Authentication** \> **Sign In / Providers** \> **DingTalk**.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fb6d74af994a32be8aa59ac56389cf92.png) </span>

         3. Check **Enable DingTalk provider**, then enter the AppID and AppSecret obtained from DingTalk Open Platform, along with the Callback URL.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_108fe8de63f60c910d66170690d193eb.png) </span>

            <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="4">warning            </div>
            

            <div data-tips="true" data-tips-type="warning" data-wrapper-indent="4">If your DingTalk users do not have an email configured, check <strong>Allow users without an email</strong>.            </div>
            

      2. Configure redirect allowlist

         Enter the page **Authentication** \> **URL Configurations**, add your app's URL (the redirect target after successful login, including the path) into Redirect URLs.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5ba1377afd9fe5372eef4f91874d347b.png) </span>

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_710486fd1b00c8376b741ea11149d9ff.png) </span>


<span id="dcn3ikZs"></span>
## Account after login

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_78bfbb346f905f4d30f1e3673a9112d0.png) </span>

<span id="hfsDLsHa"></span>
## Main configuration item description


|**Dashboard configuration item name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|Enable DingTalk provider |EXTERNAL_DINGTALK_ENABLED |bool |Yes |Enable DingTalk registration and login Values:<br><br><br>* `true`: enable (switch on)<br><br>* `false`: disable (switch off) |
|DingTalk App Key |EXTERNAL_DINGTALK_CLIENT_ID |string |Yes |DingTalk app key |
|DingTalk App Secret |EXTERNAL_DINGTALK_SECRET<br><br> |string |Yes |App Secret for DingTalk application. |
|Allow users without an email |EXTERNAL_DINGTALK_EMAIL_OPTIONAL<br><br> |bool |No |Allow the user email to be empty. Values:<br><br><br>* `true`: allows user email to be empty (switch on), default value<br><br>* `false`: does not allow user email to be empty (switch off)<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For the DingTalk scenario, the user email may not be available, so setting to <code>true</code> is recommended.</div><br> |
|Callback URL (for OAuth) |EXTERNAL_DINGTALK_REDIRECT_URI |string |Yes |OAuth callback address. It can be one of the following two types of addresses:<br><br><br>1. The default callback address of Supabase: `$SUPABASE_BASE_URL/auth/v1/callback`.<br><br>2. Service callback address under the developer domain. For more details, refer to [Restriction and callback route of the WeChat Open Platform](https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_WeChat-authorized_login#KOiKadDI). |
|Redirect URLs |URI_ALLOW_LIST |string | |List of target URLs allowed for redirection.<br><br><br>* Must exactly match the target URL, precise to the path.<br><br>* When multiple, separate with commas, like: http://www.app1.com/home,https://www.app2.com. |


<span id="71dar37s"></span>
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
    "EXTERNAL_DINGTALK_ENABLED": true,
    "EXTERNAL_DINGTALK_CLIENT_ID": "dingxxxxxxxxxxxxxxxx",
    "EXTERNAL_DINGTALK_SECRET": "xxxxxxxxxxxxxxxx",
    "EXTERNAL_DINGTALK_REDIRECT_URI": "https://your-domain.example.com/auth/v1/callback",
    "EXTERNAL_DINGTALK_EMAIL_OPTIONAL": true,
    "URI_ALLOW_LIST": "http://www.app1.com/home,https://www.app2.com",
       ...
      }'
```


<span id="aZMs4Qeq"></span>
## Sample

This scenario applies to standalone websites accessed via PC browsers. After the user chooses DingTalk login, the page generates a QR code. The user scans the QR code using the DingTalk APP to complete authorization and login.

**Applicable platform**: PC browser.

```JavaScript
// initiate QR code login on PC website
async function loginWithDingTalkWeb() {
  try {
    const { data, error } = await supabase.auth.signInWithOAuth({
      provider: 'dingtalk'
    });

    if (error) throw error;

  } catch (error) {
    console.error('钉钉网站应用扫码登录失败:', error);
  }
}
```
