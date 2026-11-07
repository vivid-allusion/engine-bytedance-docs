---
title: "Credential management"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Credential_management"
---

With credential management, administrators can centrally record and manage the keys or tokens that ArkClaw uses to call external services. Compared with hardcoding keys in assistant configurations, credential management supports centralized rotation, auditing, and permission control.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This feature is in beta. It is visible and available only after being enabled. To request a trial, contact your account manager.</div>


<span id="Ebadxgdi"></span>
## Credential types


* Credentials are classified by authentication method into API key credentials and OAuth client credentials:

   
   |**Authentication method** |**Description** |
   |---|---|
   |API Key |A key string used for authentication. When you request resources, the system includes the key in the request based on the delivery method you set. |
   |OAuth client |Authorization credentials based on the OAuth protocol. After you enter the client information registered with the identity provider (IDP), the system exchanges it for an access token following the standard authorization process. |
   

* OAuth client credentials are classified by usage into exclusive credentials and shared credentials:

   
   |**Credential type** |**Applicable scenario** |**Authorization methods** |
   |---|---|---|
   |Exclusive credentials (for single\-user account scenarios) |Each employee uses their own account in the downstream business system to complete authorization. For example, each authorizes with their own Feishu account. |After creation, the system automatically completes authorization. No manual operation is required. |
   |Shared credentials (for account sharing scenarios) |Multiple employees share the same downstream business system account. For example, several operations team members share a Shopee merchant account. |After creation, an administrator must manually complete client authorization once before all employees with permissions can use the credentials. |
   

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">An IDP refers to a service that issues and verifies identity credentials for you, such as Feishu. After you register a client on the platform, you obtain the corresponding client ID and secret.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">After a shared credential is authorized, the <strong>Authorization status</strong> column in the credential list displays <strong>Authorized</strong>. If authorization is not completed, <strong>Unauthorized</strong> is displayed and the credential is unavailable. Exclusive credentials do not have an authorization status.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">You cannot separately specify authorized users for credentials. The accessible scope of credentials is the same as the authorization scope of the associated MCP.</div>



<span id="Ik2v6opz"></span>
## Enter credentials

<span id="sq3pyTje"></span>
### Enter an API key

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To ensure security, enter the API key only in controlled and secure environments. Avoid entering API keys on public devices.</div>



1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "O&M and Security \> Credentials".

3. On the "Credentials" page, click the "API Key" tab.

4. On the "API Key" tab, click "Enter credential".

5. Refer to the table below to configure API key information.

   
   |Parameter​ |Description |
   |---|---|
   |API Key name |Enter a custom name for the API key credential to facilitate identification and management in subsequent operations. |
   |API Key value |The key value used for authentication. |
   |Set API key delivery method |The method used to include the key during a resource request.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If you do not specify a method, the system uses the default method, in which the parameter location is Header, the parameter name is Authorization, and the prefix is Bearer.</div><br><br><br>* <div data-tips="true" data-tips-type="default">To specify a custom method, you can select Header or Query as the delivery method and specify the corresponding parameter name and prefix.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Parameter location</strong>:</div><br><br><br>      * <div data-tips="true" data-tips-type="default"><strong>Header (recommended)</strong>: The API key is passed in the HTTP request header, which is more secure than Query.</div><br><br><br>      * <div data-tips="true" data-tips-type="default"><strong>Query</strong>: The API key is passed as a URL query parameter. <strong>This method exposes the key in the URL, which may be captured by logging systems, proxy servers, or browser history. This poses a risk of key leakage</strong>. Use this method only when the target service does not support header\-based transmission.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Parameter name</strong>: Specify a parameter name for the API key in the request, such as <code>Authorization</code> in the header or <code>api_key</code> in the query.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Prefix</strong> (Optional): Specify the prefix for the API key (such as Bearer) to define the format for API key transmission.</div><br> |
   

6. Click the "Confirm" button to complete the configuration.


<span id="8OraJAk1"></span>
### Enter an OAuth client

<span id="1t1sD0Zp"></span>
#### Exclusive credentials (for single\-user account scenarios)

This applies to scenarios where each employee uses their own account in downstream business systems for authorization. After filling in the information, click **Confirm**. The system automatically completes the authorization without requiring your manual effort.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "O&M and Security \> Credentials".

3. On the "Credentials \> Client" tab, click "Enter credential".

4. Select the "Single user account scenario" tab.

5. Refer to the table below to configure OAuth client information.

   
   |Parameter​ |Description |
   |---|---|
   |OAuth client name |The custom name of the credential for the OAuth client type. It helps you identify and manage the credential. |
   |OAuth client source |The type of IDP where you register this client.<br><br>You can select Feishu, Coze, GitHub, Shopee, TikTok Shop, or Custom. The required parameters vary based on the selected source.<br><br><br>* **Feishu, Coze, and GitHub:**  Enter only the client ID and secret.<br><br>* **Shopee and TikTok Shop**: Enter the client ID, secret, and additional client parameters.<br><br>* **Custom**: Enter the client ID and secret, as well as the authorization server metadata. |
   |OAuth client ID |The ID assigned by the IdP when you register the client with the IdP. |
   |Client secret |The key assigned by the IdP when you register the client with the IdP. |
   |Configuration method |**This parameter is required only when the OAuth client source is "Custom"** .<br><br><br>* **Automatic discovery (recommended)** : Enter the automatic discovery URL provided by the IdP to automatically obtain authentication service configuration information.<br><br>* **Manual configuration**: If the IdP does not support synchronizing authentication service parameters via an automatic discovery URL, you need to manually configure each parameter. |
   |Automatic discovery URL |**This parameter is required only if "OAuth client source" is set to "Custom" and "Configuration type" is set to "Automatic discovery"** .<br><br><br>* Enter the automatic discovery URL provided by the IDP. The system automatically obtains the configuration information for the authentication service.<br><br>* The URL must start with http or https and cannot exceed 500 characters in length. |
   |Issuer URL |**This parameter is required only if "OAuth client source" is set to "Custom" and "Configuration type" is set to "Manual configuration"** .<br><br><br>* The unique identifier URL of the IdP, which is the issuer. The URL is provided by the IDP and is used to verify the legitimacy of the source for the identity token.<br><br>* The URL must start with `http` or `https` and cannot exceed 500 characters in length. |
   |Authorization endpoint |**This parameter is required only if "OAuth client source" is set to "Custom" and "Configuration type" is set to "Manual configuration".** <br><br>The URL of the page to which users are redirected after they log in and agree to authorize. |
   |Token endpoint |**This parameter is required only if "OAuth client source" is set to "Custom" and "Configuration type" is set to "Manual configuration"** .<br><br>The endpoint address where the application exchanges the authorization result for an access token. |
   |Response type |**This parameter is required only if "OAuth client source" is set to "Custom" and "Configuration type" is set to "Manual configuration"** .<br><br>The result expected to be returned in the first step of the authorization process. You can select multiple options. By default, code is selected. |
   |**Advanced configuration** ||
   |Permission scope |The scope of the OAuth authorization request. Default value: “open_id”. You can enter multiple values separated by commas (,). |
   |Custom parameter |Other parameters that need to be sent along with the authorization request. The parameters are entered as key‑value pairs. |
   |Additional client parameters |Configure the following key\-value pairs **only when the OAuth client source is "Shopee" or "TikTok Shop"** :<br><br><br>* **When the OAuth client source is "Shopee":** <br><br>   * **Environment**: The value can be Production (production environment, used for processing real shop data) or Sandbox (sandbox environment, used for development and testing).<br><br>   * **Region**: Specify the geographic region of the application service, which determines the domain name used for authorization and API calls.<br><br>   * **AuthType**: Specify the entity type for OAuth authorization.<br><br>* **When the OAuth client source is "TikTok Shop":** <br><br>   * **AuthorizationType**: Specify the entity type for OAuth authorization. Supported types are Seller, Creator, and Partner. Select the type based on the business entity your application integrates with.<br><br>   * **Market**: Specify the TikTok Shop marketplace where the shop is located (such as US, GB, ID, and TH), which determines the region's domain name used for authorization and API calls. Fill in this field according to the shop's marketplace.<br><br>   * **ServiceID**: The unique service identifier obtained after the application is registered in TikTok Shop Partner Center. This identifier is used to construct the authorization URL and informs TikTok which application is requesting authorization. |
   |OAuth authentication scenario |The authorization verification method.<br><br><br>* **User delegation**: The user needs to access the login page and confirm authorization.<br><br>* **Machine‑to‑machine**: Services directly communicate with each other without user involvement. The client directly obtains the token by using its secret. |
   |Re\-authorize on every request |This feature is disabled by default. After this feature is enabled, users need to confirm authorization again for each request (each login). |
   |Maximum token validity period |The maximum validity period of the token. Default value: 3600. Valid values: 10 to 9999. Unit: seconds. The value must be less than the IDP limit. After expiration, the token must be obtained again. |
   

6. Click the "Confirm" button to complete the configuration.


<span id="yQAVjlvT"></span>
#### Shared credentials (for account sharing scenarios)

This scenario applies when multiple employees share the same account for a downstream business system. The procedure for this scenario consists of two steps: creating OAuth client credentials first and then authorizing the credentials for the client.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "O&M and Security \> Credentials".

3. On the "Credentials \> Client" tab, click "Enter credential".

4. Select the "Shared account scenario" tab.

5. Create OAuth client credentials.

   1. Refer to the table below to configure OAuth client information.

      
      |Parameter​ |Description |
      |---|---|
      |OAuth client name |The custom name of the credential for the OAuth client type. It helps you identify and manage the credential. |
      |OAuth client source |The IdP where you registered this client. In shared account scenarios, only Shopee and TikTok Shop are supported. |
      |OAuth client ID |The ID assigned by the IdP when you register the client with the IdP. |
      |Client secret |The key assigned by the IdP when you register the client with the IdP. |
      |Configuration method |**This parameter is required only when the OAuth client source is "Custom"** .<br><br><br>* **Automatic discovery (recommended)** : Enter the automatic discovery URL provided by the IdP to automatically obtain authentication service configuration information.<br><br>* **Manual configuration**: If the IdP does not support synchronizing authentication service parameters via an automatic discovery URL, you need to manually configure each parameter. |
      |**Advanced configuration** ||
      |Permission scope |The scope of the OAuth authorization request. Default value: “open_id”. You can enter multiple values separated by commas (,). |
      |Custom parameter |Other parameters that need to be sent along with the authorization request. The parameters are entered as key‑value pairs. |
      |Additional client parameters |* When the OAuth client source is "Shopee" **,**  configure the following key\-value pairs:<br><br>   * **Environment**: The value can be Production (production environment, used for processing real shop data) or Sandbox (sandbox environment, used for development and testing).<br><br>   * **Region**: Specify the geographic region of the application service, which determines the domain name used for authorization and API calls.<br><br>   * **AuthType**: Specify the entity type for OAuth authorization.<br><br>* When the OAuth client source is "TikTok Shop", configure the following key\-value pairs:<br><br>   * **AuthorizationType**: Specify the entity type for OAuth authorization. Supported types are Seller, Creator, and Partner. Select the type based on the business entity your application integrates with.<br><br>   * **Market**: Specify the TikTok Shop marketplace where the shop is located (such as US, GB, ID, and TH), which determines the region's domain name used for authorization and API calls. Fill in this field according to the shop's marketplace.<br><br>   * **ServiceID**: The unique service identifier obtained after the application is registered in TikTok Shop Partner Center. This identifier is used to construct the authorization URL and informs TikTok which application is requesting authorization. |
      |OAuth authentication scenario |Specify the verification method for authorization. Currently, only "User delegation" is supported. |
      |Re\-authorize on every request |This feature is disabled by default. After this feature is enabled, users need to confirm authorization again for each request (each login). |
      |Maximum token validity period |The maximum validity period of the token. Default value: 3600. Valid values: 10 to 9999. Unit: seconds. The value must be less than the IDP limit. After expiration, the token must be obtained again. |
      

   2. Click the "Next" button.

6. Complete the authorization of the credentials for the client. This example uses "Shopee" for demonstration.

   1. Enter the credential name and click "Confirm and authorize".

   2. On the "OAuth2 authorization flow" page, click "Open authorization page" or click "Copy authorization URL" and open it in your browser.

   3. After being redirected to the Shopee login page, enter your Shopee account information to complete the login.

   4. The Shopee authorization confirmation page opens. Select the permissions that you want the application to obtain (such as public profile, store information, and more), and click "Confirm authorization" **.** 

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_752d004c8163d2857a819cde15637778.png) </span>

   5. In the "Confirm the authorization period" pop\-up window, select the expiration time from the drop\-down list (for example, 7 Days), and click "Confirm Authorization".

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_53c5290da9e0107feda187ca97100229.png) </span>

   6. The page displays that the application has been granted access. Click "Close".

   7. Return to the [ArkClaw Enterprise](https://console.byteplus.com/arkclaw/enterprise) console. The system automatically obtains the token and displays **Authorization successful**. Click "Completed" to complete the operation.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For credentials that have been successfully authorized, the "Authorization status" column displays "Authorized."      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the "Authorization status" column for the credential displays "Unauthorized", click "Edit" in the Actions column of the target credential to perform authorization on the edit page.      </div>
      


<span id="TnDSwzwp"></span>
## Manage credentials


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, choose "O&M and Security" \> "Credential management" to view and manage existing credentials that are not associated with resources.

   
   |Operation name |Procedure |
   |---|---|
   |**View credential details** |In the credentials list, click the target credential name to view the basic information, advanced configuration, and associated resources. |
   |**Edit credentials** |<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Credentials associated with MCP cannot be edited. The <strong>Edit</strong> button is grayed out and unavailable.</div><br><br><br>Click "Edit" in the Actions column that corresponds to the target credential in the "Unassociated" state. Then, you are redirected to the edit page. Modify the information to complete the operation. |
   |**Delete credentials** |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><strong>Deleted credentials cannot be recovered. Proceed with caution</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Credentials associated with resources can be deleted only after they are disassociated. After disassociation, assistants that depend on the credentials cannot access the corresponding external services. Confirm the scope of impact before you proceed.</div><br><br><br><br>Click "Delete" in the Actions column that corresponds to the target credential in the "Unassociated" state. In the pop\-up message, confirm again and click "Delete" to complete the operation. |
   |**Delete user\-associated credentials** |After an employee completes personal account authorization using an OAuth 2.0 dedicated credential, the system generates a dedicated credential associated with the account of the employee. Administrators can view credentials associated with specific users on the Credentials page and delete any credentials they no longer need.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Deleted credentials cannot be recovered. Employees cannot use the deleted credentials to access applications and need to reauthorize their personal accounts to restore access.</div><br><br><br><br>1. On the dedicated credential details page, click the "Associated credentials" tab.<br><br>2. Click "Delete" in the "Actions" column that corresponds to the credential associated with the target user. In the pop\-up message, confirm again and click "Delete" to complete the operation. |
