---
title: "Inbound authorization: Integrate enterprise SSO for federated login"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Integrate_enterprise_SSO_for_federated_login"
---

To allow your enterprise employees to log in to your application using their existing enterprise accounts, you can configure the Agent Identity and Access Management Platform to integrate with your identity system like Okta, Azure AD, or Google Workspace. This guide provides step\-by\-step instructions for this integration, enabling a seamless single sign\-on experience without requiring users to register again.

<span id="8535406f"></span>
## Prerequisites


* You have activated the Agent Identity and Access Management Platform service and completed authorization. For details, see [Enable Agent Identity and complete authorization](https://docs.byteplus.com/docs/identity/89601).

* You have obtained information from the external identity provider, including `Issuer/Discovery URL`, `Client ID`, and `Client Secret`.


<span id="eec9a3f2"></span>
## Step 1: Create a user pool

A user pool is a container for storing user accounts. All your user data, such as usernames, passwords, and phone numbers, will be stored here.


1. Log in to BytePlus Agent Identity Console.

2. In the left navigation bar, select **User Pools**.

3. Click **Create User Pool** in the upper right corner.

4. Configure the user pool parameters.

   * **User pool name**: Enter an easily identifiable name, such as `my-web-app-pool`.

   * Other parameters can remain at their default values.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/463f1825a7044e3685096e7c464920b4) </span>

5. Click **OK**.


<span id="ba5a7c4f"></span>
## Step 2: Create a client

To enable your application to connect to the user pool you just created, you need to register a client.


1. On the resulting page, click **Create Client**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d601dd4c37894e12bf70490cb0a1a848) </span>

2. Configure the basic client information.

   * **Client name**: `my-webapp-client`.

   * **Client type**: Select **Web app**.

   * **Authorization callback URL**: This is a critical configuration. This is the address to which Agent Identity will redirect users after a successful login.

      * Local debugging example: `http://localhost:8000/callback`

      * Production environment example: `https://agent.com/auth/callback`

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The URL configured here must be exactly the same as the Redirect URI configured in your code (including the trailing slash), otherwise a <code>redirect_uri_mismatch</code> error will occur.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/31a37ab5e346495082e72c9685aa21f3) </span>

3. Click **OK**.


<span id="9524f908"></span>
## Step 3: Add an external identity provider


1. In the user pool list, click the user pool name.

2. Switch to the **External Identity Providers** tab and click **Create Provider**.

3. Configure the relevant information.

   * **Provider name**: Enter a name for your provider. This name will be displayed on the user login page for users to select when logging in. For example, `my-corporate-idp`.

   * **Provider type**: Select **OIDC**.

   * **Issuer URL**: Enter the issuer URL of the external identity provider.

   * **Client ID / Client Secret**: Enter the client identification information and secret obtained from the external identity provider. These are used to establish the trust relationship between this user pool and the external identity provider and to authorize access.

   * **Authorization scope**: The scopes of information to request. Enter at least `openid`.

   * **User identity linkage configuration**: Keep the default.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d322e1ea2309489395e9de46d0fe0a1c) </span>

4. Click **OK**.


<span id="1c48b384"></span>
## Step 4: Fill in the callback address


1. In the user pool list, locate the user pool you created.

2. Click the user pool name to view the user pool details.

3. Find the system\-generated OIDC login callback address.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3baec109172c4b8ca56ac4a321c077d0) </span>

4. Copy this address.

5. Return to your external identity provider's console and enter this address in the **Redirect URI** field of its OAuth application configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After authentication by the external identity provider is successful, the user's credentials must be securely sent back to Agent Identity through this address.   </div>
   

<span id="723dcd7b"></span>
## Verify the configuration


1. Open the Agent login page.

2. In addition to the username and password input fields, a new button will appear on the page.

3. The button name is the name of the external identity provider you configured in Step 3.

4. Click this button:

   1. The browser should redirect to your enterprise login page.

   2. Enter your enterprise account to complete the login.

   3. The browser is redirected back to the Agent Identity platform, which then redirects the user to your application.

5. Your Agent successfully obtains the token information of the current employee.
