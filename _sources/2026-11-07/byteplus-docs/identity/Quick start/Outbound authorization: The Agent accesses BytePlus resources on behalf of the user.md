---
title: "Outbound authorization: The Agent accesses BytePlus resources on behalf of the user"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Agent_accesses_BytePlus_resources_on_behalf_of_the_user"
---

To enable the Agent to access BytePlus cloud resources, configure a dedicated IAM role for the Agent through the Agent Identity and Permission Management Platform to securely authorize calls to relevant services.

<span id="21d6ab40"></span>
## Prerequisites

You have enabled the Agent Identity and Permission Management Platform service and completed authorization. For details, see [Enable Agent Identity and complete authorization](https://docs.byteplus.com/docs/identity/89601).

<span id="80b68f64"></span>
## Agent Identity configuration

You need to create a user pool, client, and user in the Agent Identity and Permission Management Platform console.

<span id="fae1c564"></span>
### Step 1: Create a user pool

A user pool is a container for storing user accounts. All your user data (usernames, passwords, phone numbers, and more) will be stored here.


1. Log in to BytePlus Agent Identity Console.

2. In the left navigation pane, select **User Pools**.

3. Click **Create User Pool** in the upper right corner.

4. Configure user pool parameters.

   * **User pool name**: Enter an easily identifiable name, such as `my-web-app-pool`.

   * Other parameters can remain at their default values.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/463f1825a7044e3685096e7c464920b4) </span>

5. Click **OK**.


<span id="9dd2999d"></span>
### Step 2: **Create a client**

To allow your application to "connect" to the user pool you just created, you need to register a client.


1. On the page that appears, click **Create Client**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d601dd4c37894e12bf70490cb0a1a848) </span>

2. Configure basic client information.

   * **Client name**: `my-webapp-client`.

   * **Client type**: Select **Web Application**.

   * **Authorization callback URL**: This is a key configuration. This is the address to which Agent Identity will redirect the user after a successful login.

      * Local debugging example: `http://localhost:8000/callback`

      * Production environment example: `https://agent.com/auth/callback`

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The URL configured here must be exactly the same as the Redirect URI configured in your code (including the trailing slash), otherwise a <code>redirect_uri_mismatch</code> error will occur.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/31a37ab5e346495082e72c9685aa21f3) </span>


<span id="636b24e0"></span>
### **Step 3: Create a user**

Create a test account to log in to the application and verify the process.


1. On the page that appears, click **Create User**.

2. Configure user information.

   * **Username**: `testuser`.

   * **Phone number**: `+86173********`.

   * **Temporary password**: Set a password that meets the following requirements.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The password must contain numbers, special characters, and both uppercase and lowercase letters.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The length must be at least 8 characters.      </div>
      

   * **Additional attributes**: Set an additional attribute (such as last name or first name).

   * Click **OK**.

      <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f0578cb8475f44b4ae1b42cf8b016266) </span>


<span id="050905f6"></span>
## Access control configuration

Access control mainly involves creating sub\-accounts and roles.

<span id="6255f04d"></span>
### Step 1: Create a BytePlus sub\-account and complete authorization


1. Log in to the BytePlus IAM Console.

2. On the left side of the page, select **User Management \> User**.

3. Click **Create New User**, and configure the user's basic information.

   * In the **User Information** section, enter the **User name**; other information is optional.

   * In the **Access method** section, check **Programmatic Access**, and set **Allow users to manage their own API keys**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/db1f069b68a34672aca9ad66399efd67) </span>

5. Click **Next**, select **Add permissions directly**, and check `AdministratorAccess`.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/85d9091c80e74276a4b606a32d8859ae) </span>

6. Click **Next**, confirm and save the configuration.

7. In the User information list, copy **Access key ID** and **Secret Access Key**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/bf79376e4a8248148b2bb75f0467347e) </span>


<span id="3c1e5a31"></span>
### Step 2: Configure an IAM role

To allow the Agent to securely access other cloud resources, you need to create an IAM role and grant it appropriate permissions.


1. Log in to the BytePlus IAM Console.

2. On the left side of the page, select **Role Management**.

3. Click **Create New Role**, and refer to the following configuration.

   * Select trusted identity: Account.

   * Select identity: Current account.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/273ac55099934d43a1b6e0370adb8a1d) </span>

4. Click **Next**. Set the role name.

5. Click **Next**, search for the policy `IDReadOnlyAccess` and check it, set the scope to **Global**.

6. Click **Submit**.

7. In the role list, click the created role name to view details.

8. Copy the role TRN information.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/52cb7efbd68c42a081eee4b101ad7c8f) </span>


<span id="1d28d196"></span>
## Integration configuration


1. In the Agent Identity Console or Access Control Console, obtain the following information and map it to your environment configuration file:

   
   |Environment variables |Note |Acquisition method |
   |---|---|---|
   |`OAUTH2_AUTHORIZATION_URL` |OAuth 2.0 authorization address, in the format `https://auth.id.cn-beijing.byteplus.com/userpool/<user-pool-id>/authorize` |Agent Identity Console \> User Pool Details page<br><br> |
   |`OAUTH2_TOKEN_URL` |OAuth 2.0 token address, in the format `https://auth.id.cn-beijing.volces.com/userpool/<user-pool-id>/ oauth/token` ||
   |`OAUTH2_USERINFO_URL` |OAuth 2.0 user information address, in the format `https://auth.id.cn-beijing.volces.com/userpool/<user-pool-id>/ userinfo` ||
   |`OAUTH2_CLIENT_ID` |Client ID |Agent Identity Console \> User Pool \> Client Details page |
   |`OAUTH2_CLIENT_SECRET` |Client secret |Agent Identity Console \> User Pool \> Client Details page |
   |`AGENT_ROLE_TRN` |IAM role TRN used by the Agent |IAM Console \> Role Details page |
   |`VOLCENGINE_ACCESS_KEY` |BytePlus Access Key |IAM Console \> User Details page |
   |`VOLCENGINE_SECRET_KEY` |BytePlus Secret Key ||
   

2. Apply the relevant configuration and start your Agent.


<span id="471e8322"></span>
## Verify the configuration

When the Agent needs to call BytePlus's API, it requests an access credential from the Agent Identity and Permission Management Platform.


* **First call**: The Agent Identity and Permission Management Platform detects that there is no valid authorization for this user and returns a redirect URL. The Agent's frontend needs to redirect the user to this URL, where the user will log in and authorize on the page. After successful authorization, the Agent Identity and Permission Management Platform securely saves the Refresh Token.

* **Subsequent invocation**: When the Agent requests access credentials again, the Agent Identity and Permission Management Platform uses the saved Refresh Token to silently obtain a new Access Token for the user in the background and returns it to the Agent. The Agent can then use this token to access BytePlus resources.
