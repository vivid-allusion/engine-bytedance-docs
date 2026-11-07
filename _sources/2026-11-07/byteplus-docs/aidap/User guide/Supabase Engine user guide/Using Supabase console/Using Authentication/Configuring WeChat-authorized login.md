---
title: "Configuring WeChat-authorized login"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_WeChat-authorized_login"
---

This topic describes the process of configuring WeChat login for applications through the Supabase console and Admin API.

## Prerequisites

* A workspace using the Supabase engine is created, and its status is **Running**. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

* obtained `SUPABASE_BASE_URL`, `SERVICE_ROLE_KEY`, and `SUPABASE_ANON_KEY`. For more information on obtaining variables, refer to [Obtaining variables](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables).

## Precautions

* The WeChat Open Platform verifies the ownership of the authorized callback domain name. If you need to place verification files in the Root directory of the authorized callback domain name, refer to [Domain ownership verification](https://docs.byteplus.com/en/docs/aidap/Configuring_custom_routes#mXaVXsm1) best practices.

* **Supported WeChat\-authorized login methods**: Supabase currently supports ** two** WeChat\-authorized login methods. These two methods use slightly different parameters in the signInWithOAuth interface. Developers must determine the browser environment and pass different parameter values accordingly. Refer to [Determining the WeChat authorization login environment](https://docs.byteplus.com/en/docs/330/106546#jiHO8kF7).

   * WeChat embedded browser web authorization login, namely, [WeChat Open Platform - WeChat web application authorization login](https://developers.weixin.qq.com/doc/oplatform/developers/dev/auth/h5.html). The signInWithOAuth interface does not require an explicit scopes parameter.

   * PC website application scan authorization login, namely, [WeChat Open Platform - web application authorization login](https://developers.weixin.qq.com/doc/oplatform/developers/dev/auth/web.html). When calling the signInWithOAuth interface, the scopes must be specified as snsapi_login in options.

## Query and modify configurations in the Supabase console

1. Configure the "authorization callback domain" in the WeChat Open Platform.

Refer to the "authorization callback domain" section in the [WeChat Open Platform documentation](https://developers.weixin.qq.com/doc/oplatform/developers/dev/auth/h5.html) to configure your callback domain. The callback domain in the WeChat Open Platform must be owned by the developer.

2. Redirect the callback interface of the callback domain to the Supabase callback interface.

If the authorized callback domain name requires domain ownership verification first, refer to [Domain ownership verification](https://docs.byteplus.com/en/docs/aidap/Configuring_custom_routes#mXaVXsm1) best practices.

The callback URL of Supabase is` $SUPABASE_BASE_URL/auth/v1/callback`, for example, `https://br-xxxx.supabase.aidap-global.cn-beijing.volces.com/auth/v1/callback`.

3. Query and modify configuration.

   1. Query and modify configurations in the Supabase console

      1. Complete WeChat login settings.

         1. After entering the Supabase console, you need to configure WeCat as an OAuth 2.0 provider and enter the corresponding credentials.

         2. Go to **Authentication** \> **Sign In / Providers** \> **WeChat**. Check **Enable WeChat provider**, then enter the AppID and AppSecret obtained from the WeChat Open Platform or WeChat Official Account Platform, along with the Callback URL.

            > **warning**

            > Since user email cannot be obtained directly through WeChat login, make sure to check **Allow users without an email**.

      2. Configure redirect allowlist.

         Go to **Authentication** \> **URL Configurations**, and add your app's URL (the target path after successful login) to the Redirect URLs.

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9dce783aff0d380f50e6ca1c0709d170.png)

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0872b883c3d96a8bf51ba84008a9a61a.png)

### Main configuration item description

|**Dashboard configuration item name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|Enable WeChat provider |EXTERNAL_WECHAT_ENABLED |bool |Yes |Is it required to enable WeChat registration and login? Values:<br><br><br>* `true`: enable WeChat registration and login (switch on)<br><br>* `false`: disable WeChat registration and login (switch off) |
|WeChat App ID |EXTERNAL_WECHAT_CLIENT_ID |string |Yes |App ID of WeChat Open Platform or WeChat Official Account Platform. |
|WeChat App Secret |EXTERNAL_WECHAT_SECRET<br><br> |string |Yes |App Secret of WeChat Open Platform or WeChat Official Account Platform. |
|Allow users without an email |EXTERNAL_WECHAT_EMAIL_OPTIONAL<br><br> |bool |No |Allow the user email to be empty. Values:<br><br><br>* `true`: allows user email to be empty (switch on), default value<br><br>* `false`: does not allow user email to be empty (switch off)<br><br><br>> **tip**<br><br><br>> For WeChat scenarios, user emails are usually unavailable, so setting it to true is strongly recommended.<br> |
|Callback URL (for OAuth) |EXTERNAL_WECHAT_REDIRECT_URI |string |Yes |OAuth callback address. The service callback address under the developer domain name. To complete domain ownership verification for the authorized callback domain name, refer to [Domain ownership verification](https://docs.byteplus.com/en/docs/aidap/Configuring_custom_routes#mXaVXsm1) best practices. |
|Redirect URLs |URI_ALLOW_LIST |string | |List of target URLs allowed for redirection.<br><br><br>* Must exactly match the target URL, precise to the path.<br><br>* When multiple, separate with commas, like: `http://www.app1.com/home,https://www.app2.com`. |

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
       "EXTERNAL_WECHAT_ENABLED": true,
       "EXTERNAL_WECHAT_CLIENT_ID": "mywechatappid",
       "EXTERNAL_WECHAT_SECRET": "mywechatappsecret",
       "EXTERNAL_WECHAT_EMAIL_OPTIONAL": "true",
       "URI_ALLOW_LIST": "http://www.app1.com/home,https://www.app2.com",
       ...
      }'
```

## Sample \- WeChat login using the Supabase Client SDK

Supabase provides a unified signInWithOAuth method for WeChat login, but depending on the browser environment, it divides into two modes.

### Scenario 1: authorized login in the WeChat embedded browser webpage

This scenario applies when users open your web application within the WeChat client and click login, directly triggering the WeChat authorization interface.

* **Applicable platform**: WeChat built\-in browser.

* **implementation**: call the signInWithOAuth function and set the provider to WeChat. There is no need to explicitly specify the scopes field in options.

```JavaScript
// initiate login in WeChat embedded browser
async function loginWithWechatEmbedded() {
  try {
    const { error } = await supabase.auth.signInWithOAuth({
      provider: 'wechat',
      options: {
        redirectTo: 'https://www.examples.com/' // redirect address after login succeeded
      }
    });

    if (error) throw error;

  } catch (error) {
    console.error('微信网页应用授权登录失败:', error);
  }
}
```

### Scenario 2: Scan QR code to authorize login on PC browser

This scenario applies to standalone websites accessed via PC browsers. After the user chooses WeChat login, the page generates a QR code. The user scans the QR code using the WeChat APP to complete authorization and login.

* **Applicable platform**: PC browser.

* **Implementation**: when calling the signInWithOAuth function, besides setting the provider to WeChat, you also need to specify scopes as snsapi_login in options.

```JavaScript
// initiate QR code login on PC website
async function loginWithWechatWeb() {
  try {
    const { data, error } = await supabase.auth.signInWithOAuth({
      provider: 'wechat',
      options: {
        scopes: 'snsapi_login', // scope must be snsapi_login
        redirectTo: 'https://www.examples.com/' // redirect address after login succeeded
      }
    });

    if (error) throw error;

  } catch (error) {
    console.error('微信网站应用扫码登录失败:', error);
  }
}
```

## Best practice: automatically detect browser environment to determine WeChat authorization login parameters

To support both WeChat authorized login scenarios simultaneously, detect the browser's User Agent to intelligently identify the current environment (refer to the isWechatEmbeddedBrowser function below), enabling one codebase for multiple login scenarios.

```JavaScript
// check if inside the WeChat embedded browser
function isWechatEmbeddedBrowser() {
  return /MicroMessenger/i.test(navigator.userAgent || '');
}

// unified WeChat login function
async function loginWithWechat() {
  try {
    const options = { redirectTo: 'https://www.examples.com/' };

    // if not in WeChat embedded browser, add scopes needed for scan code login
    if (!isWechatEmbeddedBrowser()) {
      options.scopes = 'snsapi_login';
    }

    const { error } = await supabase.auth.signInWithOAuth({
      provider: 'wechat',
      options
    });

    if (error) throw error;

  } catch (error) {
    console.error('微信登录失败:', error);
    // show error prompt on the interface
  }
}
```
