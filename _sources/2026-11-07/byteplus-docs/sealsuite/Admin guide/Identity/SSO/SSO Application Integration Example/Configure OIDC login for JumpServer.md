---
title: "Configure OIDC login for JumpServer"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-oidc-login-for-jumpserver"
---

After you complete the OIDC configuration in both SealSuite and JumpServer, users can log in to JumpServer using SealSuite for centralized authentication. This document describes how to create an application, map user attributes, configure authentication parameters, and verify login.

## Prerequisites

Use a JumpServer Enterprise Edition that supports OIDC. Feature availability depends on the version and license you use.

Before configuration, make sure you have administrator accounts for the SealSuite Admin Console and the JumpServer Portal.

In the following examples, `{JumpServer-Host}` indicates the domain name or IP address of the JumpServer service. Replace this placeholder with the value for your environment.

## Step 1: Create an OIDC application

Create an OIDC application in the SealSuite Admin Console, and configure the access URL, callback URL, and application authorization scope for JumpServer.

1. Log in to the SealSuite Admin Console, go to **Identity \> SSO**, click **Custom Application**, and select **OIDC**.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/b1ab7cb14603a22b.png)

2. On the application information page, fill in **Application address**, **Callback address**, and **ID_TOKEN signature algorithm** as described in the following table.

The following table describes the requirements for each application information field. Replace `{JumpServer-Host}` in the examples with the actual domain name or IP address of the JumpServer service.

|Configuration item |Description |
|---|---|
|**Application address** |Enter the JumpServer service address, for example, `http://{JumpServer-Host}`. |
|**Callback address** |Enter the following two URLs, and keep the trailing `/`.<br><br><br>* `http://{JumpServer-Host}/core/auth/openid/callback/`<br><br>* `http://{JumpServer-Host}/` |
|**ID_TOKEN signature algorithm** |Select **RS256**. |

3. After completing the application information configuration, click **Confirm**.

4. On the **Authorization** tab, configure the applicable scope.

   Select **Enable for all members** or **Enable for selected members**. If you select Enable for selected members, set the scope by department, individual, or role. For detailed operations, see [Add a single sign-on application](https://docs.byteplus.com/en/docs/sealsuite/docs-add-application).

## Step 2: Configure attribute mapping

Configure the mapping between SealSuite user attributes and JumpServer application user attributes, so JumpServer can read the corresponding user identity information.

1. Open the OIDC application created in SealSuite.

2. Go to the application's **Single Sign\-on** tab. In **Mapping Relation**, click **Edit**, then click **Add mapping**.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/5c8fc52c5eb5d4f4.png)

3. Add the following two mappings. Fill in the configuration items as described in the following table, and click **Confirm**.

|SealSuite field |Mapping rule |Application field |
|---|---|---|
|Email Prefix |Data Field Mapping |`PrefixEmail` |
|Email Prefix |Data Field Mapping |`sub` |

## Step 3: Obtain access parameters

Obtain the client ID, client secret, and OIDC endpoint URLs of the SealSuite application. Use them to configure JumpServer in the next step.

1. Open the OIDC application created in SealSuite.

2. On the application's **Single Sign\-on** tab, obtain **CLIENT ID** and **CLIENT SECRET** under **SealSuite Configurations**. Use them as the **Client ID** and **Client secret** of JumpServer.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/ab03acfefe836a30.png)

3. In the application's **Single Sign\-on** configuration, view API endpoints and obtain the following URLs from the OIDC configuration.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/a1b7ca9ebf1d29f6.png)

   The following table shows the mapping between each field and the JumpServer configuration item.

   |OIDC configuration field |JumpServer configuration item |
   |---|---|
   |`authorization_endpoint` |Authorization endpoint URL |
   |`token_endpoint` |Token endpoint URL |
   |`userinfo_endpoint` |User information endpoint URL |
   |`end_session_endpoint` |Logout session endpoint URL |
   |`jwks_uri` |JWKS endpoint URL |

## Step 4: Configure JumpServer

Enable OIDC in JumpServer, and enter the client information, endpoint URLs, and authentication options of the SealSuite application. This allows JumpServer to authenticate users through SealSuite.

1. Log in to the JumpServer Portal with an administrator account, and go to **System Settings \> Authentication Settings \> OIDC**.

2. Enable **OIDC authentication**, and enter the JumpServer service address, client ID, and client secret obtained in Step 3 as described in the following table.

   |Configuration item |Description |
   |---|---|
   |Enable OIDC authentication |Enable |
   |JumpServer address |Enter the JumpServer service address, for example: `http://{JumpServer-Host}` |
   |Client ID |Enter the corresponding value obtained from the SealSuite application in Step 3. |
   |Client secret |Enter the corresponding value obtained from the SealSuite application in Step 3. |

3. Configure the authentication method, endpoints, and signing parameters as described in the following table.

   Verify each endpoint URL against the OIDC configuration obtained in Step 3.

   |Configuration item |Description |
   |---|---|
   |Client authentication method |Select Client Secret Post. |
   |Use Keycloak |Disable |
   |Endpoint URL |Use the OIDC endpoint provided for your SealSuite application. Use the addresses obtained in Step 3 for your deployment. |
   |Authorization endpoint URL |Filled in automatically. Verify it against the OIDC configuration obtained in Step 3. |
   |Token endpoint URL |Filled in automatically. Verify it against the OIDC configuration obtained in Step 3. |
   |JWKS endpoint URL |Correct it to the value in the OIDC configuration obtained in Step 3. |
   |User information endpoint URL |Correct it to the value in the OIDC configuration obtained in Step 3. |
   |Logout session endpoint URL |Filled in automatically. Verify it against the OIDC configuration obtained in Step 3. |
   |Signing algorithm |Select RS256 |
   |Signing key |Access the JWKS public key URL in a browser, and enter the content returned in the browser into this field. Find **JWKS public key address** under **API Endpoint** on the **Single Sign\-on** tab (shown in Step 3). |

4. Set the remaining authentication options as described in the following table, and enter the JSON configuration after the table in **User attribute mapping**.

   |Configuration item |Description |
   |---|---|
   |Enable PKCE |Do not enable |
   |Scope |Keep the default value. No change is required. |
   |Token validity period |Keep the default value. No change is required. |
   |Claims |**Disable** this configuration |
   |Use state |**Enable** this configuration |
   |Nonce validation |**Disable** this configuration |
   |Always update user information |**Disable** this configuration |
   |Ignore SSL certificate verification |**Enable** this configuration |
   |Shared session |**Enable** this configuration |
   |User attribute mapping |Enter the following content |

   ```json
   {
     "name": "fullname",
     "username": "PrefixEmail",
     "email": "email"
   }
   ```

5. After checking the configuration, click **Save**.

## Step 5: Verify login

After saving the configuration, verify that users can log in through OIDC.

1. Open the JumpServer login page, and initiate authentication using the configured OIDC login method.

2. After the OpenID authentication redirect, complete identity authentication through SealSuite and check whether you can log in to JumpServer.
