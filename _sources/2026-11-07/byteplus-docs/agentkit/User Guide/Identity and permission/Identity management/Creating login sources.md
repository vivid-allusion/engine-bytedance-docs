---
title: "Creating login sources"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/add-an-external-identity-provider"
---

A login source is a wizard defined by AgentKit for quickly creating an identity source (IdP) or a client. After configuring a login source, users can log in to your application using their existing enterprise accounts (e.g., WeCom, Feishu), social accounts (e.g., Google), or a fixed username and password.

## Feature overview

The login source is the core entry point in the "Identity and Permission" module of the AgentKit console for quickly creating login user groups. It consists of two core underlying objects: identity providers (i.e., IdPs, such as Feishu, DingTalk, and other third\-party identity providers) and login clients. It serves as the unified configuration carrier for enabling single sign\-on with enterprise accounts. Relevant definitions and descriptions are as follows:

* If you choose to use Feishu, DingTalk, WeCom, OIDC, SAML, or other **identity providers** as the user login source, the wizard will create both a client and the corresponding identity provider for you. After configuration is complete, users can sign in to your application with their existing enterprise accounts, so you do not need to create and manage individual passwords for them in the user pool. An identity provider is typically a cloud\-hosted service, often used in conjunction with a single sign\-on (SSO) provider to authenticate users.

* If you choose to use **password login** (local username and password) as the user login source, the wizard will only create a client for you, and the user pool will centrally store and verify usernames and passwords.

## Document guide

This topic divides the configuration process into two parts: **General operation steps** and **Detailed operation steps for each type**. Both parts need to be read in conjunction:

* **General operation steps**: Describes the complete main process from logging into the console to completing verification. All login source types share this section. Steps 4–6 in the process (configuring parameters, authorization, or filling in parameters, filling in the callback URL) vary by type.

* **Detailed operation steps for each type**: Provides prerequisites, parameter lists, callback URL entry locations, and verification details according to the login source type. This is the specific expansion of Steps 4\-6 in the general steps.

Recommended reading method: First, follow the **General operation steps** to complete the main process. At Steps 4~6 of this process, jump to the corresponding subsection in the **Detailed operation steps for each type** based on the selected type to complete the parameters and callback URL.

## Prerequisites

* A user pool has been created. For related operations, see [Creating user pools](https://docs.byteplus.com/en/docs/agentkit/create-user-pool).

* The identity source currently in use by the enterprise has been selected, such as Feishu, DingTalk, WeCom, OIDC IdPs like Okta / Azure AD / Keycloak, SAML IdPs like ADFS, or local password accounts used only for testing. If enterprise SSO (Feishu / DingTalk / WeCom / OIDC / SAML) is selected, please arrange in advance to collaborate with the relevant IdP / office platform administrator. Proceeding alone on the business side is not recommended.

## General operation steps

All login source types follow the main process below. Steps 4–6 involve differences by type. Please refer to the actual display on the console. When proceeding, operate according to the selected type by referring to the [Detailed operation steps for each login source type](https://docs.byteplus.com/en/docs/agentkit/add-an-external-identity-provider?lang=en#mxH6Pw89).

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Identity & Permission \> User management".

3. In the "Actions" column to the right of the target user pool, click "Create login source".

4. Configure login source parameters.

   1. **Select type**: Select the login source type, set the login source name, and then click "Next".

      * **Type**: The external identity types supported by AgentKit are listed in the table below.

         |**Type** |**Method** |**What you need to do** |**Prerequisite permissions/restrictions** |Recommendation |
         |---|---|---|---|---|
         |Feishu |Feishu OAuth 2.0 federated login<br><br> |The Feishu administrator performs authorization by scanning a QR code with their mobile phone. The platform automatically creates the application and automatically obtains the App ID/Secret. The administrator only needs to enter a redirect URL. |Requires permission to allow the Feishu administrator to scan the QR code. By default, the application requests read\-only permissions for user basic information, email, user ID, and other address book data. |**The first choice**. Many enterprises in China use Feishu. |
         |DingTalk |DingTalk OAuth 2.0 federated login |Create a custom application on the DingTalk Open Platform, and enter the Client ID and Secret into the wizard. |The user needs to have permission to create and publish custom applications on the DingTalk Open Platform. |Enterprises already using DingTalk |
         |WeCom |WeCom OAuth federated login |Enter the credentials for the WeCom custom app. Add the AgentKit egress IP to the trusted IP allowlist in the WeCom admin console. |**A fixed egress IP must be used**. Otherwise, the WeCom server will reject the callback request and report an abnormal status. |Enterprises that already use WeCom |
         |Enterprise OIDC |* OpenID Connect 1.0 (OIDC 1.0, based on OAuth 2.0)<br><br>* Integrate with any compatible IdP |Create the OIDC application on the IdP side, and enter the Issuer, Client ID, Client Secret, Authorization / Token / UserInfo addresses, and Scope into the wizard. |The IdP must support OIDC (Okta, Azure AD / Entra ID, Keycloak, Auth0, or internal enterprise IdPs). |Foreign enterprises, multinational teams, self\-developed IdPs, and customers using Okta or Entra ID |
         |SAML 2.0 |SAML 2.0 Web SSO |Exchange SAML Metadata with the user's IdP (or manually enter the IdP metadata/signing certificate), and configure the ACS callback URL and Entity ID provided by AgentKit into the IdP. |Requires collaboration with the user's IdP administrator. |For finance, government, and large state\-owned enterprises, the IdP is a traditional system such as ADFS / Ping Identity |
         |Password user |AgentKit logs in using a local account and password. It does not need an external IdP. |Manually or batch create accounts in "User management". Users log in using their usernames and passwords. |* There is no external identity source. You need to manage the account lifecycle manually.<br><br>* Using this as a long\-term production SSO solution is not recommended. |POC demos, internal testing, and temporary small teams |

      * **Name**: Customize a name that users can easily understand when logging in, for example, `Company Employee`, `Partner Portal`, or `Test Account`. This name will appear on the sign\-in button and in agent forms.

   2. **Authorize or enter parameters**: Perform authorization operations based on the selected external identity type. For example, scan the QR code for Feishu, or fill in the corresponding credentials and endpoints for DingTalk / WeCom / OIDC / SAML.

   3. **Enter callback URL**: Copy the callback URL provided by the wizard, paste it into the "Redirect URL / Redirect URI / ACS" option of the external IdP, and then return to the wizard to check "I have pasted and saved it".

      > **tip**

      > Only some login source types require the callback URL. Proceed according to the actual configuration displayed on the console.

   4. **Complete and verify login**: Use a real account, click the "Open login page to verify" button, and complete a real SSO login. Only after obtaining the authorization code will the login source status change from **Pending verification** to **Available**.

      > **tip**

      > The entry in the login source list will display the status as **Available**, and under "Associated agents" you will see the agents associated afterwards.

## Detailed operation steps for each login source type

This section corresponds to Steps 4~6 of the [General operation steps](https://docs.byteplus.com/en/docs/agentkit/add-an-external-identity-provider?lang=en#1K2hzlKS), covering the prerequisites, parameter lists, callback URL entry locations, and verification details according to the identity source type.

**Feishu (recommended)**

### Preparations

Have permission to create custom apps on the Feishu Open Platform. For more information, see [Documentation for Feishu Open Platform](https://open.larkoffice.com/document/develop-process/self-built-application-development-process).

### Procedure

1. In the [AgentKit console](https://console.byteplus.com/agentkit), follow the general operation steps to select "Feishu", enter a name, and then click "Next".

2. A QR code will appear on the page. Scan it using the Feishu app. Confirm on your mobile device to create an internal app for the enterprise. The wizard will automatically request read\-only permission for contacts (basic user information, email, user ID).

3. After a successful scan, the wizard will automatically populate the App ID and App Secret fields.

4. When the AgentKit console prompts "Administrator has confirmed, app credentials have been automatically populated", click "Create".

5. Copy the callback address provided by the system and paste it into the Feishu Open Platform as instructed in the console.

6. On the Feishu Open Platform, find the enterprise custom app created in the prerequisites. According to the schematic diagram in the AgentKit console, paste the callback address into the corresponding field and save it.

7. Return to the [AgentKit console](https://console.byteplus.com/agentkit), check "I have pasted and saved it," and then click "Create".

8. Click "Open login page to verify" and complete a login authorization using a real Feishu account.

9. After a successful authorized login, if the Identity test page correctly retrieves your user information, it means the Feishu OAuth flow has been established.

   The wizard creates a **Web\-type client** by default, which is suitable for employee browser SSO. Client types such as CLI, M2M, SPA, and mobile apps are not included in this wizard. You need to create them manually in the "Client List" afterwards.

**DingTalk**

### Prerequisites

* Create an internal enterprise application on the DingTalk open platform and obtain the Client ID and Client Secret. For more information, see [Documentation for DingTalk Open Platform](https://open.dingtalk.com/document/development/basic-concepts-beta).

* The following permissions are enabled for the DingTalk internal enterprise application. For how to enable them, see [Documentation for DingTalk Open Platform](https://open.dingtalk.com/document/personalapp/add-interface-call-permissions):

   * `openid` (basic login, this permission is enabled by default)

   * `Contact.User.Read` (permission to read personal information in contacts)

   * If a phone number or email is required, you also need to enable permissions such as `Contact.User.mobile`.

### Procedure

1. In the [AgentKit console](https://console.byteplus.com/agentkit), follow the general operation steps to select "DingTalk", enter a name, and then click "Next".

2. Paste the Client ID and Client Secret obtained in the prerequisites into the corresponding input boxes, and then click "Create".

3. Copy the callback address provided by the system and paste it into the "Callback domain" on the "Development configuration \> Share settings" page of the target application on the DingTalk Open Platform, then save it.

4. Return to the [AgentKit console](https://console.byteplus.com/agentkit), check "I have pasted and saved it", then click "Create".

5. Click "Open login page to verify" and complete a real authorization using DingTalk.

6. After a successful authorized login, if the Identity test page correctly retrieves your user information, it means the DingTalk flow has been established.

   On the DingTalk side, you need to enable OAuth permissions related to "Login account information" in the application permissions and change the application version status to **Online**. Otherwise, the login will report a missing Scope error.

   If the SSO connectivity test result shows failure, you can fix the issue according to the system prompts. In common scenarios, due to the DingTalk OAuth 2.0 version, an error `failed to get user id from userinfo with id attribute: userid` will occur. You can find the target DingTalk identity source in the AgentKit console, edit the identity source information, and change the value of "User unique identifier attribute" to `openId`.

**WeCom**

### Prerequisites

* Create a custom application in the WeCom admin console and obtain the Corp ID (CorpID), AgentId, and Secret. For more instructions, see [Documentation for WeCom developer center](https://developer.work.weixin.qq.com/document/path/90664).

* Because the WeCom backend requires callbacks to come from a fixed IP allowlist, you need to ensure that you have applied for a fixed egress IP for this user pool in AgentKit Credential management \> "OAuth connection \-\> Egress IP configuration" module. Otherwise, WeCom will directly block the request, and AgentKit will not display any error. For detailed instructions, see [Creating OAuth connection credentials](https://docs.byteplus.com/en/docs/agentkit/creating-oauth-connection-credentials).

### Procedure

1. In the [AgentKit console](https://console.byteplus.com/agentkit), follow the general operation steps to select "WeCom", enter a name, and then click "Next".

2. Paste the Corp ID, AgentId, and Secret obtained from the prerequisites into the corresponding input fields, then click "Create".

3. Copy the callback URL provided by the system, open the WeCom admin console, go to the target application, and on the application details page, click "Set trusted domain" in the "Web authorization and JS\-SDK" module. Paste the callback URL and save.

4. Copy the IP provided by AgentKit, paste it into the "Enterprise trusted IP" module of the WeCom application, and save.

5. Return to the [AgentKit console](https://console.byteplus.com/agentkit), check "I have pasted and saved it", then click "Create".

6. Click "Open login page to verify" and complete a real authorization using WeCom.

7. Perform authorization in the WeCom client and follow its configuration guidelines to establish the WeCom OAuth channel.

**Enterprise OIDC**

### Prerequisites

Create an OIDC application in the customer's IdP (Okta / Azure AD / Entra ID / Keycloak / Auth0 / internal IdP) and obtain:

* Issuer (issuer address, for example `https://<your-idp>.example.com`)

* Client ID and Client Secret

* Authorization address, Token address, and UserInfo address (some IdPs automatically discover these through the Issuer)

* Required scope (including at least `openid`, `profile`, and `email`)

### Procedure

1. In the [AgentKit console](https://console.byteplus.com/agentkit), follow the general operation steps to select "Enterprise OIDC", enter a name, then click "Next".

2. Paste the Issuer URL, Client ID, and Client Secret obtained in the prerequisites into the corresponding input boxes, then click "Create".

3. Copy the callback address provided by the system, paste it into the corresponding position of the IdP application configuration \-\> Redirect URIs in the enterprise OIDC application, and save it.

4. Return to the [AgentKit console](https://console.byteplus.com/agentkit), check "I have pasted and saved it", then click "Create".

5. Click "Open login page to verify" and complete a login using a real IdP account.

**SAML 2.0**

### Prerequisites

* Agree on the SAML metadata exchange method with the IdP administrator: Prioritize using the Metadata URL, followed by manually uploading the IdP metadata/signing certificate.

* Export the SAML metadata XML from the IdP side (including entity ID, endpoints, and certificates).

### Procedure

1. In the [AgentKit console](https://console.byteplus.com/agentkit), follow the general operation steps to select "SAML 2.0", enter a name, then click "Next".

2. Paste the SAML metadata XML obtained in the prerequisites into the corresponding input box, and then click "Create".

3. Copy the callback address provided by the system, paste it into the corresponding position of the IdP's SP configuration \-\> Assertion Consumer Service URL in SAML 2.0, and save it.

4. Return to the [AgentKit console](https://console.byteplus.com/agentkit), check "I have pasted and saved it", then click "Create".

5. Click "Open login page to verify" and complete a login using a real IdP account.

6. In the AgentKit console, find the target SAML 2.0 identity source, edit the identity source information, and configure the following mapping relationships in "User attribute mapping".

   Email ← email, Name ← displayName, Department ← department

**Password user**

### Prerequisites

Agree on the SAML metadata exchange method with the customer's IdP administrator: Prioritize using the Metadata URL, followed by manually uploading the IdP metadata/signing certificate.

### Procedure

1. In the [AgentKit console](https://console.byteplus.com/agentkit), follow the general operation steps to select "Password user", enter the name, then click "Next".

2. Create accounts and configure related parameters.

   * **First batch of accounts**: Enter the login account in the format `username, mobile number with international dialing code`, for example, `Zhang San,+86151********`. Enter one account per line. After creation, a temporary password will be automatically generated, and an SMS notification will be sent. After adding the first batch of accounts, you can then create or batch import more accounts via CSV in the "User" module. For detailed instructions, see [Creating users](https://docs.byteplus.com/en/docs/agentkit/create-user).

   * **Automatic registration**: When enabled, users can register themselves on the login page.

3. Click "Finish" to complete the configuration of the password user login source. After successful creation, the password user is displayed on the "Client" tab of the target user pool.

4. On the application's login page, users select "Test account" and log in using the username and password.

   > **warning**

   * > Password users do not have external identity sources. Account onboarding, offboarding, and password changes must all be handled manually by the administrator.

   * > Do not keep user accounts intended for the production environment in the password user category permanently. This login source is only intended for POCs or temporary collaboration accounts.

## Identity source management

**View and enable/disable**

* The "User management \> Login sources" list displays all sources, including name, type, status (**Available**/**Pending verification**/**Abnormal**), member count, which Agents use it, and the last login time.

* Each source can be enabled or disabled independently. If disabled, the entry will no longer appear on the login page. However, tokens that have already been issued remain valid until they expire.

**Edit identity source**

On the "Identity source" tab of the target identity pool, click "Edit" in the "Actions" column to update the configuration for the corresponding identity source. Detailed parameter descriptions are as follows.

> **tip**

> Some parameters are only displayed on the edit page for certain provider types. The actual configurable parameters are subject to what is shown in the console.

|**Parameter​**  |**Description** |
|---|---|
|**Basic information** ||
|Provider name |The name of the identity source will be displayed on the user login page for selection. |
|**Egress configuration** ||
|Egress method |Select the network egress used when this identity source calls the upstream IdP. For scenarios like WeCom that require verifying the server's source IP, you need to bind a fixed egress IP and add this egress IP range to the trusted IP allowlist in the IdP backend. Otherwise, callbacks will be rejected, and status errors will be reported.<br><br><br>* **Platform default egress (unstable)** : Uses the platform's unified egress IP. Stability is not guaranteed, and it may be blocked by the external risk control system.<br><br>* **Custom egress IP (recommended)** : Binds a fixed egress IP for the current resource to ensure successful verification by the IdP allowlist. |
|Status |Controls whether this identity source is available. Multiple login sources can be enabled or disabled independently of each other.<br><br><br>* **Enable**: Users can see and select this entry on the login page.<br><br>* **Disable**: This entry will no longer appear on the login page. However, already\-issued tokens remain valid until they expire. |
|**WeCom login configuration** ||
|Enterprise ID |The unique tenant identifier (CorpId) for WeCom. Obtain it in the WeCom admin console. It is used to identify the integrated WeCom entity. |
|Agent ID |The application identifier (AgentId) of the WeCom custom app is obtained from the WeCom application details and is used to identify the specific custom app being called. |
|Agent Secret |The application secret (Secret) of the WeCom custom application is used in conjunction with CorpId and AgentId to exchange for access credentials. This is sensitive information and must be stored securely to avoid leakage. |
|**Core configuration (DingTalk & Feishu)**  ||
|Client ID |The unique client identifier obtained after registering the application on the IdP side: App ID for Feishu and AppKey/Client ID for DingTalk. It is used to identify the trust relationship between the current user pool and the IdP. |
|Client secret |The application secret that is paired with the Client ID: App Secret for Feishu, AppSecret / Client Secret for DingTalk. It is used to verify the legitimacy of the user pool as an OAuth client. This is sensitive information and must be stored securely to avoid leakage. |
|Authorization scope |The scope of user information permissions expected from the IdP. Request based on the principle of least privilege.<br><br><br>* Feishu defaults to `contact:user.base:readonly` and `contact:contact.base:readonly`.<br><br>* DingTalk requires enabling permissions for "login account information", reading personal information in contacts (`Contact.User.Read`), email (fieldEmail), and then publishing the version. |
|**SAML core configuration** ||
|SAML metadata |The metadata XML exported from the SAML IdP (including entity ID, SSO endpoint, and signing certificates). It supports directly pasting XML content or uploading a file for parsing and is used to establish metadata federation trust with the IdP. |
|Enable signature verification |If enabled, Agent Identity will use the signature certificate provided by the IdP to sign SAML requests, preventing SAML requests from being tampered with. |
|Enable encryption |If enabled, Agent Identity will use the encryption certificate provided by the IdP to encrypt the SAML response (assertion). |
|**OIDC core configuration** ||
|Issuer URL |The unique identifier URL of the external OIDC identity provider (e.g., `https://<tenant>.okta.com`), which must be exactly consistent with the IdP configuration, is used for OIDC discovery and to verify the legitimacy of the identity token's issuing source. |
|Client secret |The Client Secret obtained after registering the OIDC application in the IdP is used in conjunction with the Client ID to verify the legitimacy of the user pool as an OIDC client. This is sensitive information and must be stored securely to avoid leakage. |
|Authorization scope |The scope of user information to be obtained from the IdP. It needs to include at least `openid`, and typically also `profile` and `email`. Otherwise, basic user information cannot be retrieved after login (resulting in empty or incorrect user fields). |
|**Security configuration** ||
|Enable PKCE to enhance security |We recommend enabling it. Add PKCE (Proof Key for Code Exchange) validation to the OAuth authorization code flow to prevent interception and replacement of authorization codes, enhancing browser login security. You can keep the default when the IdP has no explicit requirements. |
|**User identity federation configuration** | |
|User attribute mapping |Configure how the user fields returned by the IdP are written to the user pool. You can map upstream attributes (such as `emails`, `displayName`, and `departmentIds`) to standard user attributes (such as `user.email` and `user.name`), custom attributes (`custom.<name>`), or authoritative department affiliations (`system.department_assignment`).<br><br>> **warning**<br><br><br>> The field name must exactly match the claim name returned by the IdP. If the source path does not exist, this mapping will be automatically skipped.<br> |
|User unique identifier attribute |Specify the unique attribute field used to identify and associate local users (such as sub, email, NameID, or email address). It must be consistent with the IdP metadata / returned attributes. Configuration errors will cause the same user to be created repeatedly in the user pool or fail to associate with an existing account. |
|Allow new user registration |Whether to allow new users to register accounts via this identity source on the registration page.<br><br><br>* **Enable**: Allow registration<br><br>* **Disable**: Disallow registration |
|Auto create accounts |Whether to automatically create an account when the user is not found in the platform upon logging in through the identity source.<br><br><br>* **Enable**: Automatically create<br><br>* **Disable**: Manual association/registration required |
|Auto\-update user information |Whether to automatically update user information (platform user attributes are synchronized in real time from the third\-party IdP).<br><br><br>* **Enable**: Automatic update<br><br>* **Disable**: Synchronize only on the first login |
|Auto link configuration |When a user already exists, the provider identity is automatically associated through the specified attribute to avoid duplicate creation. |
|**User information transmission** ||
|Information propagation method |Controls how IdP upstream user claims are propagated and carried when issuing tokens to downstream businesses/agents (corresponds to `ClaimsPropagationConfig`). Available modes:<br><br><br>* Do not carry (default)<br><br>* Minimal required<br><br>* Full claim passthrough<br><br>* Custom claim set |

**Delete identity source**

> **warning**

* > Before deletion, detach this login source from any agent or access rule that references it. Otherwise, deletion will be blocked.

* > After deletion, users can no longer log in via this source, but account records in the user directory are retained.

1. In the "Actions" column of the login source list, click "Delete".

   If this source is still referenced by an agent or access rule, the system will prompt you to detach it first. After detaching all references and deleting again, the system will clean up related objects such as the identity provider, login application, and user pool in a cascading order.

2. After deletion, users can no longer log in via this source, but account records in the user directory are retained.
