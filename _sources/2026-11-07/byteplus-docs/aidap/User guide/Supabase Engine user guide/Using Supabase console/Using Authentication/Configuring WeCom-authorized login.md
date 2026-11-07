---
title: "Configuring WeCom-authorized login"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_WeCom-authorized_login"
---

This topic introduces the workflow for configuring enterprise WeChat (hereinafter referred to as "WeCom") login for an application through the Supabase console and Admin API.

<span id="BY7KQYAm"></span>
## Prerequisites


&nbsp;

* A workspace using the Supabase engine is created, and its status is **Running**. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

* obtained `SUPABASE_BASE_URL`, `SERVICE_ROLE_KEY`, and `SUPABASE_ANON_KEY`. For more information on obtaining variables, refer to [Obtaining variables](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables).


<span id="Qqbc6dcP"></span>
## Precautions


* **Restriction and callback route of the WeCom Open Platform**

   * **Restriction:**  The WeCom Open Platform enforces verification of the owner of the **authorization callback domain**. When **configuring the authorization callback domain**, developers must place a specified file with a designated name and content in the root directory of the domain (refer to the section on "authorization callback domain" in [enabling web authorization login on WeCom](https://developer.work.weixin.qq.com/document/path/98151#%E5%BC%80%E5%90%AF%E7%BD%91%E9%A1%B5%E6%8E%88%E6%9D%83%E7%99%BB%E5%BD%95) for details). Therefore, the “authorization callback domain” can only be set to the developer’s own domain and cannot be set to a Supabase domain.

   * **Callback route**: Due to the above restriction, the OAuth callback route for WeCom Open Platform login must be: WeCom Open Platform \-\-(redirect)\-\-\> callback endpoint under the developer’s domain \-\-(redirect)\-\-\> Supabase callback endpoint. In addition, during redirection, the callback endpoint under the developer’s domain must transparently forward all parameters of the callback request (including Query Parameters, Header, and Body) to the Supabase callback endpoint.

* **Supported WeCom\-authorized login methods**: Supabase currently supports **two** WeCom\-authorized login methods. These two methods use slightly different parameters in the signInWithOAuth interface. Developers must determine the browser environment and pass different parameter values accordingly. Refer to [Determining the WeCom authorization login environment](https://docs.byteplus.com/en/docs/330/106547#MkTXbFKA).

   * WeChat embedded browser web authorization login, namely, [WeCom Open Platform - WeCom web application authorization login](https://developer.work.weixin.qq.com/document/path/91335). The signInWithOAuth interface does not require an explicit scopes parameter.

   * PC website application scan authorization login, namely, [WeCom Open Platform - WeCom scan application authorization login](https://developer.work.weixin.qq.com/document/path/98151). When calling signInWithOAuth interface, specify scopes as qr_connect in options.


<span id="J8aG36gz"></span>
## Query and modify configurations in the Supabase console


1. Configure the "authorization callback domain" in the WeCom Open Platform.


Refer to the "authorization callback domain" section in [Enabling web authorization login on WeCom](https://developer.work.weixin.qq.com/document/path/98151#%E5%BC%80%E5%90%AF%E7%BD%91%E9%A1%B5%E6%8E%88%E6%9D%83%E7%99%BB%E5%BD%95) to configure your callback domain. The callback domain in the WeCom Open Platform must be owned by the developer.


2. Redirect the callback interface of the callback domain to the Supabase callback interface.


Refer to the explanation in [WeCom Open Platform restriction and callback route](https://docs.byteplus.com/en/docs/330/106547#Qqbc6dcP), your callback domain's callback interface should implement redirection to the Supabase callback interface.

The callback URL of Supabase is` $SUPABASE_BASE_URL/auth/v1/callback`, for example, `https://br-xxxx.supabase.aidap-global.cn-beijing.volces.com/auth/v1/callback`.


3. Add the outbound IP of Volcengine Supabase to the IP allowlist in the background of the WeCom application.

   
   |**Region** |**BytePlus Supabase service outbound IP** |
   |---|---|
   |China (Beijing) |115.190.189.99 |
   

4. Query and modify configuration.

   1. Query and modify configuration in the Supabase console.

      1. Complete WeChat login settings.

         1. After entering the Supabase console, you need to configure WeCom as an OAuth 2.0 provider and enter the corresponding credentials.

         2. Go to **Authentication** \> **Sign In / Providers** \> **WeCom**. Check **Enable WeCom provider** and enter the Corp ID and secret obtained from the WeCom backend management, along with the Callback URL.

            <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            <div data-tips="true" data-tips-type="default" data-wrapper-indent="4">If your WeCom users do not have an enterprise email configured, check <strong>Allow users without an email</strong>.            </div>
            

         3. (Optional) If you need to use the scan code login function, you must additionally configure the **agentid**. For more details, refer to [Web sign-in components](https://developer.work.weixin.qq.com/document/path/98152) and [Terminology introduction](https://developer.work.weixin.qq.com/document/path/90665).

      2. Configure redirect allowlist

         Enter the page **Authentication** \> **URL Configurations**, and configure your application's URL (the redirect target after successful login, precise to path) in Redirect URLs.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9dce783aff0d380f50e6ca1c0709d170.png) </span>

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0872b883c3d96a8bf51ba84008a9a61a.png) </span>


<span id="juXzBmn6"></span>
### Main configuration item description


|**Dashboard configuration item name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|Enable WeCom provider |EXTERNAL_WECOM_ENABLED |bool |Yes |Is it required to enable WeCom registration and login? Values:<br><br><br>* `true`: enable WeCom registration and login.<br><br>* `false`: disable WeCom registration and login. |
|WeCom Corp ID<br><br> |EXTERNAL_WECOM_CLIENT_ID |string |Yes |Corp ID in the WeCom backend management. |
|WeCom Corp Secret<br><br> |EXTERNAL_WECOM_SECRET |string |Yes |The application secret in the WeCom backend management. |
|Allow users without an email |EXTERNAL_WECOM_EMAIL_OPTIONAL |bool |No |Allow the user email to be empty. Values:<br><br><br>* `true`: allow the user email to be empty.<br><br>* `false`: do not allow the user email to be empty.<br><br><br> |
|Callback URL (for OAuth) |EXTERNAL_WECOM_REDIRECT_URI |string |Yes |OAuth callback address. For the service callback address under the developer domain, refer to [WeCom Open Platform restriction and callback route](https://docs.byteplus.com/en/docs/330/106547#Qqbc6dcP). |
|Redirect URLs |URI_ALLOW_LIST |string | |List of target URLs allowed for redirection.<br><br><br>* Must exactly match the target URL, precise to the path<br><br>* When multiple, separate with commas, like: `http://www.app1.com/home,https://www.app2.com`. |


<span id="yTixg6b4"></span>
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
       "EXTERNAL_WECOM_ENABLED": true,
       "EXTERNAL_WECOM_CLIENT_ID": "mywecomcorpid",
       "EXTERNAL_WECOM_SECRET": "mywecomcorpsecret",
       "EXTERNAL_WECOM_EMAIL_OPTIONAL": "true",
       "URI_ALLOW_LIST": "http://www.app1.com/home,https://www.app2.com",
       ...
      }'
```


<span id="CCYQQlcX"></span>
## Sample \- WeChat login using the Supabase Client SDK

Supabase provides a unified signInWithOAuth method for WeChat login, but depending on the browser environment, it divides into two modes.

<span id="3ZywZllv"></span>
### Scenario 1: authorized login in the WeCom embedded browser webpage

This scenario applies when users open your web application within the WeCom client and click login, directly triggering the WeChat authorization interface.

**Implementation**: call the signInWithOAuth function and set the provider to `wecom`. There is no need to explicitly specify the scopes field in options.

```JavaScript
// initiate login in WeCom embedded browser (H5 authorization)
async function loginWithWeComEmbedded() {
  try {
    const { error } = await supabase.auth.signInWithOAuth({
      provider: 'wecom',
      options: {
        redirectTo: 'https://www.examples.com/', // redirect address after login succeeded
        // scopes: 'qr_connect' generally not required in H5 scenarios
      },
    })

    if (error) throw error
  } catch (error) {
    console.error('企业微信 H5 授权登录失败:', error)
  }
}
```


<span id="Ty4Gltmh"></span>
### Scenario 2: Scan QR code to authorize login on PC browser

This scenario applies to standalone websites accessed via PC browsers. After the user chooses WeCom login, the page generates a QR code. The user scans the QR code using the WeCom APP to complete authorization and login.

**Implementation**: when calling the signInWithOAuth function, besides setting the provider to `wecom`, you also need to specify scopes as `qr_connect` in options.

```JavaScript
// initiate WeCom scan code login on PC/normal browser page (optional example)
async function loginWithWeComQR() {
  try {
    const { error } = await supabase.auth.signInWithOAuth({
      provider: 'wecom',
      options: {
        redirectTo: 'https://www.examples.com/',
        scopes: 'qr_connect', // scan code login
      },
    })

    if (error) throw error
  } catch (error) {
    console.error('企业微信扫码登录失败:', error)
  }
}
```


<span id="MkTXbFKA"></span>
## Best practice: automatically detect browser environment to determine WeCom authorization login parameters

To support both WeCom authorization login scenarios, you can detect whether navigator.userAgent contains wxwork to determine the current browser environment (refer to the isWeComEmbeddedBrowser function below), enabling one set of code to support multiple login scenarios.

```JavaScript
// check if inside the WeCom embedded browser
function isWeComEmbeddedBrowser() {
  // WeCom built-in browser UA usually includes wxwork
  return /wxwork/i.test(navigator.userAgent || '')
}

// unified enterprise wecom login function (h5 embedded browser uses "embedded authorization"; external browsers use "scan code")
async function loginWithWeCom() {
  try {
    const options = { redirectTo: 'https://www.examples.com/' }

    // if not in WeCom embedded browser, add scopes needed for scan code login
    // supabase wecom provider: use qr_connect for scan code
    if (!isWeComEmbeddedBrowser()) {
      options.scopes = 'qr_connect'
    }

    const { error } = await supabase.auth.signInWithOAuth({
      provider: 'wecom',
      options,
    })

    if (error) throw error
  } catch (error) {
    console.error('企业微信登录失败:', error)
    // show error prompt on the interface
  }
}
```
