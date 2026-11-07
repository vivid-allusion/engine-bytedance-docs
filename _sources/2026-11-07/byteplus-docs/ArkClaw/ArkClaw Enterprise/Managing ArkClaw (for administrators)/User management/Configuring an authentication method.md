---
title: "Configuring an authentication method"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_users"
---

The user management feature allows you to flexibly configure employee access methods.

<span id="0x8CWpkE"></span>
## Operation instructions


* You can select an employee authentication method for access control, such as **Lark,**  **Slack**, **Microsoft Teams, or Platform\-hosted**. To modify an authentication method or switch to another method, follow the steps in the [Switch authentication methods](https://docs.byteplus.com/en/docs/ArkClaw/Managing_users#tGbEb66U) section below.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>After you switch to another authentication method, the original login method becomes immediately unavailable. Employees need to log in via the new method to create ArkClaw instances. Instances created using the original authentication method are unavailable and need to be manually deleted and released by the administrator.</strong>   </div>
   

* If you select **Other standard protocols** as the employee access control method when creating a space, configure the standard protocol authentication parameters to establish an encrypted trust channel between ArkClaw and your identity provider (IdP). This implements SSO and on\-demand authorization. For detailed steps, see the [Configure authentication information](https://docs.byteplus.com/en/docs/ArkClaw/Managing_users#SgeyDnIM) section in this topic.


<span id="JOEdn2Wc"></span>
## Prerequisites

Whether you are switching authentication methods or configuring authentication information, ensure you have obtained relevant application information. For detailed steps, see [Getting started](https://docs.byteplus.com/en/docs/ArkClaw/Quick_start_guide), and read the topic corresponding to your authentication method (such as , Lark authentication, or Feishu authentication).

<span id="1BSI5a7L"></span>
## View authentication method


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. In the upper\-right corner of the Users page, you can view the current authentication method.


<span id="tGbEb66U"></span>
## Switch authentication methods


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. On the "Users" page, go to the "Login configuration" tab and click "Edit".

4. Select the target authentication method and follow the on\-screen prompts to provide the corresponding configuration information.

   
   |Authentication method |Configuration information |
   |---|---|
   |Feishu |* App ID: Enter the App ID of the enterprise Feishu.<br><br>* App Secret: Enter the App Secret of the enterprise Feishu.<br><br>* UID policy:<br><br>   * Select this option based on the primary identity information used within your enterprise. When you switch authentication methods, the system automatically merges accounts that share the same mobile number or email address. **This identifier cannot be used to log in to Claw instances**.<br><br>   * During full or incremental user information synchronization from Feishu with a few clicks, the system will match and deduplicate users based on the selected unique identifier.<br><br>* Custom attribute mapping:<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If an administrator has configured a user attribute with the update type set to "Automatic update", when switching authentication methods, you also need to configure the mapping field corresponding to this attribute. For operations related to user attributes, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?TagIDs=2,522,512,502&lang=en#ReGX3H0s">Managing user attributes</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After configuring custom attribute mapping, the system can automatically update attribute information via the mapping when users log in to the employee portal via SSO.   </div><br>   <br><br>   * Custom attribute: The name of the current user attribute, automatically specified by the system, cannot be modified.<br><br>   * Mapping field: Enter the field name in the new authentication method that corresponds to the old user attribute, so that attribute information can be automatically inherited after switching authentication methods. For example, if the old attribute is "Job title" and the corresponding field in the new authentication method is "Position", enter "Position". |
   |Lark |* App ID: Enter the App ID of the Lark.<br><br>* App Secret: Enter the App Secret of the Lark.<br><br>* UID policy:<br><br>   * Select this option based on the primary identity information used within your enterprise. When you switch authentication methods, the system automatically merges accounts that share the same mobile number or email address. **This identifier cannot be used to log in to Claw instances**.<br><br>   * During full or incremental user information synchronization from Lark with a few clicks, the system will match and deduplicate users based on the selected unique identifier.<br><br>* Custom attribute mapping:<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If an administrator has configured a user attribute with the update type set to "Automatic update", when switching authentication methods, you also need to configure the mapping field corresponding to this attribute. For operations related to user attributes, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?TagIDs=2,522,512,502&lang=en#ReGX3H0s">Managing user attributes</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After configuring custom attribute mapping, the system can automatically update attribute information via the mapping when users log in to the employee portal via SSO.   </div><br>   <br><br>   * Custom attribute: The name of the current user attribute, automatically specified by the system, cannot be modified.<br><br>   * Mapping field: Enter the field name in the new authentication method that corresponds to the old user attribute, so that attribute information can be automatically inherited after switching authentication methods. For example, if the old attribute is "Job title" and the corresponding field in the new authentication method is "Position", enter "Position". |
   |Slack |* **Client ID**: Enter the ID of the Slack application.<br><br>* **Client Secret**: Enter the Secret of the Slack application.<br><br>* Unique identifier policy: Set this item based on the primary identity information used within your enterprise. When you switch authentication methods, the system will automatically merge accounts that share the same mobile number or email address. **This identifier cannot be used to log in to Claw instances**.<br><br>* Custom attribute mapping:<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If an administrator has configured a user attribute with the update type set to "Automatic update", when switching authentication methods, you also need to configure the mapping field corresponding to this attribute. For operations related to user attributes, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?TagIDs=2,522,512,502&lang=en#ReGX3H0s">Managing user attributes</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After configuring custom attribute mapping, the system can automatically update attribute information via the mapping when users log in to the employee portal via SSO.   </div><br>   <br><br>   * Custom attribute: The name of the current user attribute, automatically specified by the system, cannot be modified.<br><br>   * Mapping field: Enter the field name in the new authentication method that corresponds to the old user attribute, so that attribute information can be automatically inherited after switching authentication methods. For example, if the old attribute is "Job title" and the corresponding field in the new authentication method is "Position", enter "Position". |
   |Microsoft Teams |* **Client ID**: Enter the Application (client) ID assigned by Teams.<br><br>* **Client Secret**: Enter the Value information assigned by Teams as the Client Secret.<br><br>* **Tenant ID**: Enter the Directory (tenant) ID assigned by Teams.<br><br>* **Client ID**: Enter the (client) ID assigned by Teams.<br><br>* **Client Secret**: Enter the value information assigned by Teams as the Client Secret.<br><br>* **Tenant ID**: Enter the directory (tenant) ID assigned by Teams.<br><br>* Unique identifier policy: Set this item based on the primary identity information used within your enterprise. When you switch authentication methods, the system will automatically merge accounts that share the same mobile number or email address. **This identifier cannot be used to log in to Claw instances**.<br><br>* Custom attribute mapping:<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If an administrator has configured a user attribute with the update type set to "Automatic update", when switching authentication methods, you also need to configure the mapping field corresponding to this attribute. For operations related to user attributes, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?TagIDs=2,522,512,502&lang=en#ReGX3H0s">Managing user attributes</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After configuring custom attribute mapping, the system can automatically update attribute information via the mapping when users log in to the employee portal via SSO.   </div><br>   <br><br>   * Custom attribute: The name of the current user attribute, automatically specified by the system, cannot be modified.<br><br>   * Mapping field: Enter the field name in the new authentication method that corresponds to the old user attribute, so that attribute information can be automatically inherited after switching authentication methods. For example, if the old attribute is "Job title" and the corresponding field in the new authentication method is "Position", enter "Position". |
   |OIDC |* Create an application at your IdP, obtain application information (such as the client ID, client secret, authorization endpoint, token endpoint, and user information endpoint), and fill in the form with these details to complete identity integration.<br><br>* Unique identifier policy: Set this item based on the primary identity information used within your enterprise. When you switch authentication methods, the system will automatically merge accounts that share the same mobile number or email address. **This identifier cannot be used to log in to Claw instances**.<br><br>* Custom attribute mapping:<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If an administrator has configured a user attribute with the update type set to "Automatic update", when switching authentication methods, you also need to configure the mapping field corresponding to this attribute. For operations related to user attributes, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?TagIDs=2,522,512,502&lang=en#ReGX3H0s">Managing user attributes</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After configuring custom attribute mapping, the system can automatically update attribute information via the mapping when users log in to the employee portal via SSO.   </div><br>   <br><br>   * Custom attribute: The name of the current user attribute, automatically specified by the system, cannot be modified.<br><br>   * Mapping field: Enter the field name in the new authentication method that corresponds to the old user attribute, so that attribute information can be automatically inherited after switching authentication methods. For example, if the old attribute is "Job title" and the corresponding field in the new authentication method is "Position", enter "Position". |
   |OAuth 2.0 |* Create an application at your IdP, obtain information such as the client ID, client secret, and Issuer, and fill in the form with these details to complete identity integration.<br><br>* Unique identifier policy: Set this item based on the primary identity information used within your enterprise. When you switch authentication methods, the system will automatically merge accounts that share the same mobile number or email address. **This identifier cannot be used to log in to Claw instances**.<br><br>* Custom attribute mapping:<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If an administrator has configured a user attribute with the update type set to "Automatic update", when switching authentication methods, you also need to configure the mapping field corresponding to this attribute. For operations related to user attributes, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?TagIDs=2,522,512,502&lang=en#ReGX3H0s">Managing user attributes</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After configuring custom attribute mapping, the system can automatically update attribute information via the mapping when users log in to the employee portal via SSO.   </div><br>   <br><br>   * Custom attribute: The name of the current user attribute, automatically specified by the system, cannot be modified.<br><br>   * Mapping field: Enter the field name in the new authentication method that corresponds to the old user attribute, so that attribute information can be automatically inherited after switching authentication methods. For example, if the old attribute is "Job title" and the corresponding field in the new authentication method is "Position", enter "Position". |
   |SAML |* SAML metadata: Obtain it from the IdP and configure it in the form to complete identity integration.<br><br>* User attribute mapping: Enter the user attribute mapping information.<br><br>   * System fields:<br><br>      * id_attribute: The unique identifier of the user. ArkClaw uses this field to distinguish between different users. **Required**. Typically mapped to the email address or employee ID in the enterprise identity system.<br><br>      * name: The user's full name, which is displayed on the page after login.<br><br>      * email: The user's email address, which is used for receiving notifications.<br><br>      * phone_number: The user's phone number.<br><br>   * IDP attribute name: The name of the user information field that the enterprise identity system (such as AD FS) sends to ArkClaw after user login. ArkClaw uses this name to locate the corresponding value (such as email address or name) and match it with the system fields on the left.<br><br>* Security configuration: **Response signature verification** and **assertion encryption** are both enabled by default, which can effectively ensure the security of the login process and do not require manual adjustment.<br><br>* Unique identifier policy: Set this item based on the primary identity information used within your enterprise. When you switch authentication methods, the system will automatically merge accounts that share the same mobile number or email address. **This identifier cannot be used to log in to Claw instances**.<br><br>* Custom attribute mapping:<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If an administrator has configured a user attribute with the update type set to "Automatic update", when switching authentication methods, you also need to configure the mapping field corresponding to this attribute. For operations related to user attributes, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?TagIDs=2,522,512,502&lang=en#ReGX3H0s">Managing user attributes</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After configuring custom attribute mapping, the system can automatically update attribute information via the mapping when users log in to the employee portal via SSO.   </div><br>   <br><br>   * Custom attribute: The name of the current user attribute, automatically specified by the system, cannot be modified.<br><br>   * Mapping field: Enter the field name in the new authentication method that corresponds to the old user attribute, so that attribute information can be automatically inherited after switching authentication methods. For example, if the old attribute is "Job title" and the corresponding field in the new authentication method is "Position", enter "Position". |
   

5. After configuration is complete, click "Save" in the lower\-right corner.

6. After you switch authentication methods, configure the callback information based on the current authentication method. For detailed steps, see , and refer to the "Configure callback information" section in the topic corresponding to the authentication method (such as , Lark authentication, or Feishu authentication).


<span id="SgeyDnIM"></span>
## Configure authentication information

<span id="mWGM7W0A"></span>
### OAuth 2.0


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. On the "Users" page, go to the "Login configuration" tab and click "Edit".

4. Select the standard protocol to use and fill in the relevant information.

   For a list of relevant parameters, see [OAuth 2.0](https://docs.byteplus.com/en/docs/ArkClaw/OAuth).

   
   |Item |Description |
   |---|---|
   |Client ID |The unique client identifier that identifies the current application. This unique client identifier is automatically generated when the application is registered with the IDP. |
   |Client secret |The key that ensures secure communication with the IDP. It is generated after the application is created at the IDP.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">It needs to be kept securely to prevent leakage.</div><br> |
   |Authorization endpoint |The authorization endpoint (login redirect URI) provided by the IDP for initiating the OAuth authorization flow. |
   |Token endpoint |The endpoint used to exchange an authorization code for an access token. It must be obtained from the application configurations at the IDP. |
   |UserInfo endpoint |The endpoint that requests detailed information (such as username and email address) about the logged\-in user with the access token included. It must be obtained from the application configurations at the IDP. |
   |Authorization scope |* The scope of user information requested during login authorization. For example, whether to obtain only basic identity information or also obtain personal information (such as avatar and nickname), email address, and phone number. **You can directly select or manually enter the scope**.<br><br>* The following values are typically included:<br><br>   * openid: The unique user identifier that identifies the user.<br><br>   * profile: The personal information of the user, such as the avatar, nickname, and name.<br><br>   * email: The email address of the user.<br><br>   * phone: The phone number of the user.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The authorization scope must be consistent with that supported by the IDP. For details, see the official documentation of the corresponding IDP.</div><br><br><br><br>* The following content provides an example of the configuration result:<br><br>   * Administrators set the authorization scope to `openid`, `profile`, `email`, or `phone`.<br><br>   * When you log in for the first time, the page will display the following requested permission information: |
   |Unique user identifier |* It is used to identify a user and match a logged\-in user with existing users in the system. This field is generated by the IDP.<br><br>* Enter the fields in the user information returned by the IdP. The fields must be **globally unique and not easily changed**, and their values must be in **English**.<br><br>   * **We recommend** choosing user ID\-type fields, such as `sub` or `user_id`. If no user ID\-type fields are available, you may choose `email`, which is relatively stable but may also change, and needs to be updated when necessary.<br><br>   * Using fields such as `name` or `nickname` that may be modified or duplicated is **not recommended**.<br><br>* Method of viewing user attributes: Access the **OIDC discovery URL of the IdP** (`https://****/.well-known/openid-configuration`), and view the list of supported attributes by using the `claims_supported` node. For example: |
   |Enable PKCE |Adds an additional layer of security protection to the authorization code flow. If you select this option, the client (e.g., mobile app) uses PKCE to prevent authorization code interception, enhancing security. |
   |Unique identifier policy |Select this option based on the primary identity information used within your enterprise. When you import employee information, the system will automatically merge accounts that share the same mobile number or email address. **Email addresses or mobile numbers cannot be used to log in to Claw instances**. |
   

5. Click "Confirm".

6. Configure the callback information according to the current authentication method. For detailed steps, see the "Configure callback information" section in the [OAuth 2.0](https://docs.byteplus.com/en/docs/ArkClaw/OAuth) topic.


<span id="7pEdUTnk"></span>
### OIDC


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. On the "Users" page, go to the "Login configuration" tab and click "Edit".

4. Select the standard protocol to use and fill in the relevant information.

   For a list of relevant parameters, see [OIDC](https://docs.byteplus.com/en/docs/ArkClaw/OIDC_protocol).

   
   |Item |Description |
   |---|---|
   |Client ID |The unique client identifier that identifies the current application. This unique client identifier is automatically generated when the application is registered with the IDP. |
   |Client secret |The key that ensures secure communication with the IDP. It is generated after the application is created at the IDP.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">It needs to be kept securely to prevent leakage.</div><br> |
   |Issuer address |The unique identifier address of the OIDC IDP. The system will automatically discover the authorization endpoint, token endpoint, and user information endpoint by using the address.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After you create an application at the IdP, copy the "OIDC Discovery URL" and paste it into the address bar of the browser to open it. Pretty\-print the output and obtain the issuer URL.</div><br> |
   |Authorization scope |* The scope of user information requested during login authorization. For example, whether to obtain only basic identity information or also obtain personal information (such as avatar and nickname), email address, and phone number. **You can directly select or manually enter the scope**.<br><br>* The following values are typically included:<br><br>   * openid: The unique user identifier that identifies the user.<br><br>   * profile: The personal information of the user, such as the avatar, nickname, and name.<br><br>   * email: The email address of the user.<br><br>   * phone: The phone number of the user.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The authorization scope must be consistent with that supported by the IDP. For details, see the official documentation of the corresponding IDP.</div><br><br><br><br>* The following content provides an example of the configuration result:<br><br>   * Administrators set the authorization scope to `openid`, `profile`, `email`, or `phone`.<br><br>   * When you log in for the first time, the page will display the following requested permission information:<br><br><br> |
   |Enable PKCE |Adds an additional layer of security protection to the authorization code flow. If you select this option, the client (e.g., mobile app) uses PKCE to prevent authorization code interception, enhancing security. |
   |Unique identifier policy |Select this option based on the primary identity information used within your enterprise. When you import employee information, the system will automatically merge accounts that share the same mobile number or email address. **Email addresses or mobile numbers cannot be used to log in to Claw instances**. |
   

5. Click "Confirm".

6. Configure the callback information according to the current authentication method. For detailed steps, see the "Configure callback information" section in the [OIDC](https://docs.byteplus.com/en/docs/ArkClaw/OIDC_protocol) topic.


<span id="23KVCTeJ"></span>
#### 

<span id="Vt61dYeO"></span>
### SAML protocol


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. On the "Users" page, go to the "Login configuration" tab and click "Edit".

4. Select the standard protocol to use and fill in the relevant information.

   For related parameters, see [SAML protocol](https://docs.byteplus.com/en/docs/ArkClaw/SAML_protocol).

   
   |Item |Description |
   |---|---|
   |SAML metadata |Paste the content of the FederationMetadata.xml file downloaded from your IdP (such as Microsoft AD FS). |
   |User attribute mapping |Enter the user attribute mapping information.<br><br><br>* System fields:<br><br>   * id_attribute: The unique identifier of the user. ArkClaw uses this field to distinguish between different users. **Required**. Typically mapped to the email address or employee ID in the enterprise identity system.<br><br>   * name: The user's full name, which is displayed on the page after login.<br><br>   * email: The user's email address, which is used for receiving notifications.<br><br>   * phone_number: The user's phone number.<br><br>* IDP attribute name: The name of the user information field that the enterprise identity system (such as AD FS) sends to ArkClaw after user login. ArkClaw uses this name to locate the corresponding value (such as email address or name) and match it with the system fields on the left.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The IDP attribute names need to be obtained from the enterprise IT administrator.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For example, if the enterprise uses "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress" to pass the email address, enter this name in the IDP attribute name field corresponding to the "email" row. ArkClaw will then recognize it as the user's email address.</div><br> |
   |Security configuration |Both **Response signature verification** and **Assertion encryption** are enabled by default. They effectively ensure the security of the login process and do not require manual adjustment. |
   |Unique identifier policy |Select this option based on the primary identity information used within your enterprise. When you import employee information, the system will automatically merge accounts that share the same mobile number or email address. **Email addresses or mobile numbers cannot be used to log in to Claw instances**. |
   

5. Click "Confirm".

6. Configure the callback information according to the current authentication method. For detailed steps, see the "Configure callback information" section in the [SAML protocol](https://docs.byteplus.com/en/docs/ArkClaw/SAML_protocol).
