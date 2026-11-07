---
title: "Outbound authorization: The agent accesses third-party resources on behalf of the user"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Agent_accesses_third-party_resources_on_behalf_of_the_user"
---

To enable your agent to securely access third\-party services like Google Weather or Feishu on behalf of a user, you can configure identity credential hosting. This guide provides step\-by\-step instructions on setting up the necessary user pool and client, and then configuring an OAuth client for a third\-party service, using the Feishu Open Platform as a detailed example.

<span id="4b6fc863"></span>
## Prerequisites


* You have enabled the Agent Identity and Permission Management Platform service and completed authorization. For details, see [Enable Agent Identity and complete authorization](https://docs.byteplus.com/docs/identity/89601).

* You have registered an application on the third\-party developer platform and obtained the `App ID` (Client ID) and `App Secret` (Client Secret).


<span id="a523f4dc"></span>
## Step 1: Create a user pool

A user pool is a container for storing user accounts. All your user data (such as username, password, phone number, and other information) will be stored here.


1. Log in to BytePlus Agent Identity Console.

2. In the left navigation bar, select **User Pool**.

3. Click **Create User Pool** in the upper right corner.

4. Configure user pool parameters.

   * **User pool name**: Enter an easily identifiable name, such as `my-web-app-pool`.

   * Other parameters can be left as default.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/463f1825a7044e3685096e7c464920b4) </span>

5. Click **OK**.


<span id="43d9c9df"></span>
## Step 2: **Create a client**

To allow your application to "connect" to the user pool you just created, you need to register a client.


1. On the returned page, click **Create Client**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d601dd4c37894e12bf70490cb0a1a848) </span>

2. Configure basic client information.

   * **Client name**: `my-webapp-client`.

   * **Client type**: Select **Web app**.

   * **Authorization callback URL**: **Key configuration**. This is the address where Agent Identity redirects the user back to your application after a successful login.

      * Local debugging example: `http://localhost:8000/callback`

      * Production environment example: `https://agent.com/auth/callback`

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The URL configured here must exactly match the Redirect URI configured in your code (including the trailing slash), otherwise a <code>redirect_uri_mismatch</code> error will occur.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/31a37ab5e346495082e72c9685aa21f3) </span>


<span id="4bb18ed7"></span>
## **Step 3: Create a user**

Create a test account to log in to the application and verify the process.


1. On the returned page, click **Create User**.

2. Configure user information.

   * **Username**: `testuser`.

   * **Phone number**: `+86173********`.

   * **Temporary password**: Set a password that meets the following requirements.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The password must contain numbers, special characters, and both uppercase and lowercase letters.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The length must be at least 8 characters.      </div>
      

   * **Additional attributes**: Set an additional attribute (such as last name and first name).

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f0578cb8475f44b4ae1b42cf8b016266) </span>

3. Click **OK**.


<span id="1d9a1001"></span>
## Step 4: Configure the OAuth client


1. Log in to BytePlus Agent Identity Console.

2. In the left navigation bar, select **Credential hosting**.

3. Click **Create a credential** and select **Create an OAuth Client**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/fd80b439178448c2a3fc5869224ef139) </span>

4. Configure the relevant parameters.

   * **Provider name**: Customize an easily identifiable ID, such as `downstream-feishu-service`.

   * **Provider type**: Select **Lark**.

   * **Client ID / Client Secret**: Enter the application credentials obtained from the Feishu open platform.

   * **Scope**: Enter the list of permissions you need to request (for example, `contact:user.base:readonly`), separating multiple permissions with line breaks.

   * **Callback URL**: **Key configuration**. This is the address where Agent Identity will redirect the user back to your application after the provider authorization is completed.

      * Local debugging example: `http://localhost:8000/callback`

      * Production environment example: `https://agent.com/auth/callback`

5. Click **OK**.


<span id="af63069d"></span>
## Step 5: Fill in the callback address

You need to configure the third\-party service (Feishu) so that it can send the token to Agent Identity.


1. In the user pool list, find the user pool you created.

2. Click the user pool name to view the user pool details.

3. Find the system\-generated OIDC login callback address.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3baec109172c4b8ca56ac4a321c077d0) </span>

4. Copy this address.

5. Log in to the Feishu open platform and select the application details page where you need to configure the redirect URL.

6. Find **Development configuration \> Security settings** and paste the copied address into the redirect URL field.


<span id="36ddda0f"></span>
## Verify the configuration

When the Agent needs to call the Feishu open platform API, it requests an access credential from the Agent Identity and Permission Management Platform.


* **First call**: The Agent Identity and Permission Management Platform detects that there is no valid authorization for the user and returns a redirect URL. The Agent's frontend needs to redirect the user to this URL, where the user will log in and authorize on the page. After successful authorization, the Agent Identity and Permission Management Platform securely saves the refresh token.

* **Subsequent calls**: When the Agent requests access credentials again, the Agent Identity and Permission Management Platform uses the saved refresh token to silently obtain a new access token for the user in the background and returns it to the Agent. The Agent can then use this token to call Feishu, and the entire process is transparent to the user.


<span id="744ccd3e"></span>
## **View and revoke authorization**


* You can view the managed credentials, but you cannot directly see the user's Refresh Token.

* To revoke a user's authorization for this agent, you can delete the corresponding outbound credential management configuration or revoke the authorization in the downstream service.
