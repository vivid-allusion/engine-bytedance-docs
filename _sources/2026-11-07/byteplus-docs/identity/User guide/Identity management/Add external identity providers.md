---
title: "Add external identity providers"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Add_external_identity_providers"
---

You can manage user identities outside the Agent Identity and Access Management Platform by configuring external identity providers. External identity providers can provide identity information to Agent Identity via OAuth, OIDC, or SAML, establishing trust between your Agent Identity account and the external identity provider.

After adding the configuration, users will be able to log in to your application using their existing enterprise accounts (such as WeCom, Azure AD) or social accounts (such as Google), and you will not need to create or manage passwords for these users in the user pool.

<span id="3629064c"></span>
## Prerequisites

You have created a user pool. For related operations, refer to [Create a user pool](https://docs.byteplus.com/docs/identity/89611).

<span id="1953eda3"></span>
## Steps


1. Log in to the BytePlus Agent Identity Console.

2. In the left navigation bar, select **Identity Management \> User Pool**.

3. Click the target user pool name to enter the details page for the specified user pool.

4. Switch to the **External Identity Provider** tab and click **Create Provider**.

5. Customize the provider name. This name will be displayed on the user login page for users to select when logging in.

6. Configure the corresponding parameters according to the provider type.

   
   <Tabs>
   <Tab zoneid="LOcojC40MW" title="OAuth 2.0">
   <TabTitle>OAuth 2.0</TabTitle>
   
   * **OAuth 2.0 core configuration**
   
      **Create an application with the identity provider, obtain the client ID and client secret, and configure them in the form to complete identity federation integration.** 
   
      * **Client ID**: Required. The unique client identifier obtained when registering the application with the IdP (for example, 1234567890\-abcd1234.apps.googleusercontent.com), used to identify the trust relationship between the current user pool and the IdP.
   
      * **Client secret**: Required. The client secret obtained when registering the application with the IdP is used with the Client ID to verify the legitimacy of the user pool (as an OIDC client), for example, to verify identity when exchanging tokens in the authorization code flow. It must be properly safeguarded to prevent disclosure.
   
      * **Authorization scope**: Required. The range of user information you wish to obtain from the IdP. Must include at least openid. It may also typically include profile and email.
   
      * **Authorization endpoint**: Required. The URL used to initiate the user login and authorization process.
   
      * **Token endpoint**: Required. The URL used to exchange the authorization code for a token.
   
      * **User info endpoint**: Required. After obtaining the access token, call this URL to retrieve the user's basic information, such as username and email.
   
   * **Security configuration**
   
      * **Enable PKCE to enhance security**: Recommended to enable. Adds an extra layer of security protection to the authorization code flow. Once enabled, the client (such as a mobile application) uses PKCE to prevent interception of the authorization code.
   
   * **User identity linkage configuration**
   
      **Ensures the legitimacy of the authorization process and that users have reasonable control over resources.** 
   
      * **User unique identifier attribute**: Required. The field name of the user's unique identifier returned by the external identity provider (such as email or sub), used to associate with the local user.
   
      * **Allow new user registration**: If enabled, this setting determines whether to allow manual or automatic creation of a new user when a user from the external identity provider logs in for the first time and does not exist in the user pool.
   
      * **Automatically create account**: When enabled, no manual confirmation is required; when a user logs in via this IdP for the first time, a user account is automatically created in the user pool, the user's information from the external identity provider (such as name and email) is populated in the user pool, and the external identity is associated with the user.
   
      * **Automatically update user information**: When enabled, each time the user logs in, the local account automatically synchronizes the latest attributes from the external identity provider, such as avatar and department.
   
   
   </Tab>
   <Tab zoneid="mApTlGLi4P" title="OIDC">
   <TabTitle>OIDC</TabTitle>
   
   * **OIDC core configuration**
   
      **Create an application with the identity provider, obtain the client ID and client secret, and configure them in the form to complete identity federation integration.** 
   
      * **Issuer URL**: Required. The unique identifier URL of the external identity provider (IDP), which must match the configuration of the external identity provider and is used to verify the legitimacy of the identity token source.
   
      * **Client ID**: Required. The unique client identifier obtained when registering the application with the IDP (such as 1234567890\-abcd1234.apps.googleusercontent.com), used to identify the trust relationship between the current user pool and the IDP.
   
      * **Client secret**: Required. The client secret obtained when registering the application with the IDP, used together with the Client ID to verify the legitimacy of the user pool (as an OIDC client), for example, to verify identity when exchanging tokens during the authorization code flow. It must be properly safeguarded to prevent disclosure.
   
      * **Authorization scope**: Required. The scope of user information to obtain from the IdP. Must include at least openid. It may also include profile and email.
   
   * **Security configuration**
   
      * **Enable PKCE to enhance security**: Recommended to enable. Adds an extra layer of security protection to the authorization code flow. After enabling, the client (such as a mobile application) uses PKCE to prevent interception of the authorization code.
   
   * **User identity linkage configuration**
   
      **Ensures the legitimacy of the authorization process and that users have appropriate control over resources.** 
   
      * **Map user attributes from ID token**: OIDC relies on the ID token to transmit user information. If this setting is enabled, user attributes are mapped from claims such as sub/name in the ID token; if disabled, user information is obtained from the UserInfo endpoint.
   
      * **Allow new user registration**: After enabling, when a user from the external identity provider logs in for the first time and does not exist in the user pool, you can choose whether to allow creation of a new user manually or automatically.
   
      * **Automatically create account**: After enabling, no manual confirmation is required. When a user logs in through this IdP for the first time, a user account is automatically created in the user pool, and information from the external identity provider (such as name and email) is populated. The external identity is then linked to this user.
   
      * **Automatically update user information**: After enabling, each time the user logs in, the local account will automatically synchronize the latest attributes from the external identity provider (such as avatar and department).
   
   
   </Tab>
   <Tab zoneid="cWHiVPTYgL" title=" SAML 2.0">
   <TabTitle> SAML 2.0</TabTitle>
   
   * **SAML core configuration**
   
      **Register your application with the SAML 2.0 identity provider, obtain the metadata file, and upload it to the user pool to establish a trust relationship with the SAML identity provider.** 
   
      *  ** SAML metadata**: The metadata XML exported from the SAML IdP (including entity ID, endpoints, certificates, and more). Supports direct input of XML content or file upload for parsing.
   
      * **Enable signature authentication**: When enabled, Agent Identity uses the signature certificate provided by the IdP to sign SAML requests. This prevents the requests from being tampered with.
   
      * **Enable encryption**: When enabled, Agent Identity uses the encryption certificate provided by the IdP to encrypt SAML responses. This prevents the responses from being tampered with.
   
   * **User identity linkage configuration**
   
      **Ensures the legitimacy of the authorization process and that users have reasonable control over resources.** 
   
      * **User attribute mapping**: Maps attributes returned by the IdP to attributes in the Agent Identity user pool, such as mapping the email attribute from the IdP to the email attribute in the user pool.
   
      * **User unique identifier attribute**: Specifies the unique attribute used to identify users (such as email or NameID), which must match the attribute in the IdP metadata.
   
      * **Allow new user registration**: When enabled, determines whether to allow manual or automatic creation of new users when a user from an external identity provider logs in for the first time and does not exist in the user pool.
   
      * **Automatic account creation**: When enabled, users are automatically created in the user pool when logging in via this IdP for the first time, without manual confirmation. The external identity provider information (such as name and email) is populated, and the external identity is linked to the user.
   
      * **Automatic user information update**: When enabled, the local account automatically synchronizes the latest attributes from the external identity provider (such as avatar and department) each time the user logs in.
   
      * **Automatic linkage configuration**: For existing users, automatically links the SAML identity using specified attributes (NameID or Email) to avoid duplicate creation.
   
   
   </Tab>
   <Tab zoneid="Z4yJgXSfex" title="Feishu (OAuth 2.0)">
   <TabTitle>Feishu (OAuth 2.0)</TabTitle>
   
   Agent Identity currently provides a preconfigured external IdP for Feishu (**OAuth 2.0**), which you can use directly.
   
   
   * **Feishu core configuration**
   
      **Create an application in the Feishu developer console, obtain the client ID and client secret, and configure them in the form to complete identity federation integration.** 
   
      * **Client ID**: Required. The unique identifier of the Feishu application (App ID), which can be obtained in the Feishu developer console under **`Credentials & Basic Information > Application Credentials`** (for example, `cli_9d13f****`).
   
      * **Client Secret**: Required. The application secret for Feishu (App Secret) is the key assigned by the OIDC provider to prove the application's identity. It can be obtained in the Feishu developer console under **`Credentials & Basic Information > Application Credentials`** (for example, `UQj2QK****`).
   
      * **Authorization scope**: The default scopes are `contact:user.base:readonly` and `contact:contact.base:readonly`.
   
   * **Security configuration**
   
      * **Enable PKCE to enhance security**: It is recommended to enable this option. Adds an extra layer of security protection to the authorization code flow. After enabling, the client (such as a mobile application) uses PKCE to prevent interception of the authorization code.
   
   * **User identity linkage configuration**
   
      **Ensures the legitimacy of the authorization process and that users have appropriate control over resources.** 
   
      * **User unique identifier attribute**: Required. The field name for the unique user identifier returned by the external identity provider (such as email or sub), used to associate with local users.
   
      * **Allow new user registration**: If enabled, this setting determines whether to allow the creation of a new user when a user from the external identity provider logs in for the first time and does not exist in the user pool.
   
      * **Automatically create account**: After enabling, no manual confirmation is required. When a user logs in through this IdP for the first time, a user account is automatically created in the user pool and the user's information from the external identity provider (such as name and email) is filled in, and the external identity is linked to the user.
   
      * **Automatically update user information**: After enabling, each time the user logs in, the local account will automatically synchronize the latest attributes from the external identity provider (such as avatar and department).
   
   
   </Tab>
   </Tabs>
   


<span id="94ecc903"></span>
## Other operations


* **Enable/Disable**: On the identity provider details page, you can enable or disable any IdP at any time. After disabling, users will not be able to log in through this provider.

* **Edit restrictions**: After creation, some core configurations (such as the provider type) cannot be modified. If major changes are required, it is recommended to delete and recreate the provider.
