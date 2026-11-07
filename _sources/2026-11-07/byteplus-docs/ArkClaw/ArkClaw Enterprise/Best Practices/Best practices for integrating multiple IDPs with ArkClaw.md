---
title: "Best practices for integrating multiple IDPs with ArkClaw"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Best_practices_for_integrating_multiple_IDPs_with_ArkClaw"
---

This topic describes how to integrate multiple IDPs, such as Feishu, DingTalk, and Lark, with ArkClaw in scenarios where multiple identity systems coexist within a single enterprise.

<span id="3NYSqB2L"></span>
## Scenario overview

In organizations with complex architectures such as group enterprises, merged entities, or multinational corporations, multiple identity systems often coexist. For example, entities in the Chinese mainland use Feishu, entities outside the Chinese mainland use Lark (international version of Feishu), acquired companies use DingTalk, offices outside the Chinese mainland use Microsoft Teams or Entra ID, and some internal systems are attached to on\-premises Active Directory  (a Microsoft hybrid domain architecture, hereinafter referred to as AD). In such cases, setting up separate ArkClaw workspaces for each system will lead to fragmented accounts, inconsistent permissions, and high operational costs.

ArkClaw can integrate with multiple identity sources through the **multi‑IDP co‑existence mode** to consolidate all users into a unified identity pool.


* Employees log in to ArkClaw by using their familiar accounts. This preserves existing identity systems.

* Administrators can manage all group users from a unified view and synchronize permissions and organizational structures.

* When providing services externally, end users are presented with a unified login entry for a consistent experience.


Typical applicable combinations: Feishu + Lark (branches in and outside the Chinese mainland), Feishu + DingTalk (merged companies and parallel business units), and Teams (Entra) + on‑premises AD.

<span id="snIOJ4T6"></span>
## Solution selection

The following table describes two typical deployment modes in multi‑IDP scenarios.


|**Solution** |**Applicable scenario** |**Core features** |
|---|---|---|
|**Solution A:**  One space + multiple IDPs in Identity |Manage all users within the same ArkClaw space, with unified permissions and organizational structures. |Create one user pool in Identity configured with multiple external IDPs, and ArkClaw connects to the user pool by using the OIDC protocol. All users reside in a single identity pool. |
|**Solution B:**  Multi\-space isolation |Complete isolation across business entities is required, such as separate data, independent billing, and strict compliance boundaries. |Create a separate ArkClaw space for each identity source. Each space is configured with a single authentication protocol, and users log in to their respective spaces. |


If no strong isolation is required, **Solution A** is recommended because it achieves unified identity management with minimal operational overhead and can be smoothly extended to include more identity sources. The following content describes the complete configuration steps for **Solution A** (Feishu + DingTalk). The configuration steps are the same for other combinations (such as Feishu + DingTalk and Microsoft Teams + AD). You only need to select the corresponding external IDP type in **Step 2**.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you select <strong>Solution B (multi‑workspace isolation), you only need to activate a separate ArkClaw space under each project</strong>:</div>



* <div data-tips="true" data-tips-type="warning">Configure an authentication protocol for each workspace (such as Feishu for Workspace 1, Lark for Workspace 2, and Teams for Workspace 3). Do not use multiple single‑IDP login methods within one workspace.</div>


* <div data-tips="true" data-tips-type="warning">ArkClaw spaces are independent from each other. You need to purchase seats and ModelArk Plans, and add enterprise public knowledge bases and public agent templates for each workspace separately.</div>


* <div data-tips="true" data-tips-type="warning">Configure security policies (password policy, MFA, and login IP allowlist) for each workspace to ensure compliance in strong isolation scenarios.</div>



<span id="sPriUZtx"></span>
## Considerations


* **Account unique identifier and merging policy**

   * **Preferentially use email addresses as the unique identifier**: Make sure that all IDPs return users with enterprise email addresses. In this way, Agent Identity can automatically merge accounts of the same person from different IDPs based on email addresses. This prevents duplicate accounts.

   * **Use employee IDs as authoritative identifiers**: If your organization includes regular employees, contractors, and vendors, you can write employee IDs into the extended attributes of each IDP. In this way, Agent Identity can merge accounts by employee ID, with email address as an auxiliary field.

   * **Avoid using mobile numbers as the unique identifier**: Employees across different countries may have multiple country\-specific mobile numbers, which can easily lead to account merging failures.

* **Permission and organizational structure synchronization**

   * After IDPs are integrated with Agent Identity, you can enable **automatic organizational structure synchronization** to synchronize department and position data from IDPs such as Feishu and Lark to Agent Identity. Then, use ArkClaw to grant permissions on workspaces, projects, and knowledge bases based on the unified organizational structure.

   * In multi‑IDP scenarios, we recommend **defining permissions in ArkClaw by entity, region, or department** to prevent permission misassignment for users across IDPs due to structural differences.

* **Security and compliance**

   * **Enforce HTTPS:**  The discovery URL of Agent Identity, callback URL, and the ArkClaw access entry must use HTTPS to prevent tokens from being intercepted during transmission.

   * **Regularly rotate secrets:**  Rotate Identity client secrets and IDP App secrets every **90** days, and update ArkClaw configurations accordingly.

   * **Multi‑factor authentication (MFA):**  Uniformly enable MFA in Agent Identity for administrator and high‑privileged accounts. Do not implement a separate MFA within ArkClaw to prevent policy fragmentation.

   * **Login audit:**  Enable login audit logs in both Agent Identity and ArkClaw, and regularly check for abnormal logins, such as cross\-country logins within a short period or an excessive number of login failures.

   * **Disabling/offboarding synchronization:**  Make sure that account disabling/offboarding events are synchronized between Agent Identity and each IDP. In this way, upon employee departure, the account is immediately disabled in Identity, preventing the former employee from logging in to ArkClaw.


<span id="s0EwnCnP"></span>
## Prerequisites

Before starting configuration, make sure that the following conditions are met:


* ArkClaw Enterprise of BytePlus has been activated, and you have **tenant administrator** or **identity management permissions.**  The current ArkClaw Enterprise service is only available to users who have completed enterprise real\-name authentication.

   * **If you have not completed enterprise authentication**, refer to [Enterprise real‑name authentication](https://docs.byteplus.com/en/docs/6261/64937).

   * **If you have only completed personal authentication and need to upgrade to enterprise authentication**, refer to [Upgrading personal authentication to enterprise authentication](https://docs.byteplus.com/en/docs/6261/65159).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you are using a BytePlus IAM user, the root user needs to grant the necessary permissions to the IAM user. For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Authorizing_an_IAM_user_to_use_ArkClaw_Enterprise">Authorizing IAM users to access ArkClaw Enterprise edition</a>.   </div>
   

* The Agent Identity service has been activated, and you have permissions to **create user pools, create clients, and configure external identity providers** in Agent Identity. For related operations, see [Activate the agent identity and permission management platform and complete authorization](https://docs.byteplus.com/docs/identity/Enable_Agent_Identity_and_complete_authorization).

* In each external identity source, such as Feishu Open Platform, Lark Open Platform, DingTalk Open Platform, and Azure Portal, you have created a self‑managed application and obtained the **App ID/Client ID** and **App Secret/Client Secret** of the application.

   * [Configure the Feishu application and obtain information](https://docs.byteplus.com/en/docs/ArkClaw/Feishu_authentication?lang=zh#tXfPdJrI)

   * [Configure the DingTalk application and obtain information](https://docs.byteplus.com/en/docs/87732/2356402?lang=zh#3mdm2LMH)

   * For other external identity sources, refer to the corresponding authentication documentation in [Getting Started](https://docs.byteplus.com/en/docs/ArkClaw/Quick_start_guide?lang=zh).

* Make sure that the email addresses or mobile numbers of all users are maintained in each self‑managed application, for account merging/deduplication in Agent Identity if needed.


<span id="eWczptiU"></span>
## Procedure

The overall process consists of three phases: Create a user pool and client in Identity → Configure multiple external IDPs in the user pool → Complete OIDC login configuration in ArkClaw.

<span id="b8whSWhn"></span>
### Step 1: Create a user pool and client in Agent Identity


1. Log in to the [Agent Identity console](https://console.byteplus.com/identity/region:identity+cn-beijing/user-pools?projectName=default).

2. In the left navigation pane, click "User identity management". Then, click "Create user pool".

3. Configure the user pool parameters based on the following table.

   
   |Parameter​ |Description |
   |---|---|
   |**User pool name** |Specify a unique name for the user pool. In this example, set the value to `my-app-docs`. |
   |**Attributes for user pool login** |Select the identity identifier that a user can use during login. In this example, select **Username**, **Mobile number**, and **Email address.** <br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration cannot be modified after creation.</div><br> |
   |**Attributes for user pool registration** |Select the identity identifier that a user needs to provide during registration. In this example, select **Username and Mobile number**. |
   |**Associated project** |Select the project to which the user pool belongs for resource isolation and management. The current project is selected by default. |
   

4. After the configuration is complete, click "Confirm". Then, click the icon in the upper\-right corner to exit the user pool creation panel.

5. In the user pool list, click the name of the newly created user pool. In the left navigation pane, click Clients. Then, click Create client **.** 

6. Configure the client parameters based on the following table.

   
   |Parameter​ |Description |
   |---|---|
   |**Client name** |Specify the name of the application client. In this example, set the value to `my-company-portal`. |
   |**Client type** |Select the client type based on the application type. In this example, Feishu and DingTalk applications are used. Therefore, select **Web application**. |
   |**Authorization callback URL** |After a user logs in and completes authorization, the system redirects the user to this URL. **Do not specify this parameter for now**. After you have activated an ArkClaw space subsequently, you will paste the "SSO authorization code redirect URL" provided by ArkClaw into this field. |
   

7. After the configuration is complete, click "Confirm". In the client list, click the name of the newly created client. On the details page, obtain the **Client ID** and **Client secret**. You need to specify these two parameters in the ArkClaw Enterprise console.


<span id="BZW5s5Jh"></span>
### Step 2: Configure external IDPs (such as Feishu and DingTalk) for the user pool


1. In the left navigation pane, click "External IdP" under the user pool `my-app-docs`. Then, click "Create provider".

2. Add the first external IDP (Feishu) based on the following table. Keep the default values for parameters that are not mentioned in the table.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This topic only provides an example of how to configure Feishu and DingTalk. For details on adding other types of external IDPs, see <a href="https://docs.byteplus.com/en/docs/identity/Add_external_identity_providers?lang=zh">Adding external IDPs</a>.   </div>
   

   
   |Parameter​ |Description |
   |---|---|
   |Provider name |Enter the name of the external IDP. This will be displayed on the user login page for selection. In this example, set the value to **Feishu**. |
   |Provider type |The authentication protocol used by the external IDP. Supported protocols include OAuth 2.0, SAML 2.0, and OIDC. In this example, Feishu and DingTalk are used, both of which use OAuth 2.0. Therefore, select **OAuth 2.0 provider**. |
   |Provider |Select the actual external IDP. Agent Identity presets Feishu and DingTalk as external IDPs, which can be directly used. In this example, select **Feishu**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the external IDP is neither Feishu nor DingTalk, select "Custom".</div><br> |
   |Egress method |Select the resource egress method. In this example, select the **platform default egress**. |
   |Client ID |The App ID of the Feishu application. In the [Feishu Open Platform](https://open.larkoffice.com/app?lang=zh-CN), click the name of the target Feishu application, click "Basic Info \> Credentials & Basic Info" in the left\-side navigation pane, and obtain the App ID. |
   |Client secret |The App Secret of the Feishu application. In the [Feishu Open Platform](https://open.larkoffice.com/app?lang=zh-CN), click the name of the target Feishu application and click "Basic Info \> Credentials & Basic Info" in the left navigation pane to obtain the App Secret. |
   

3. Repeat the preceding two steps to add the second external IDP (DingTalk). After the configuration is complete, click "Confirm".

   
   |Parameter​ |Description |
   |---|---|
   |Provider name |Enter the name of the external IDP. This will be displayed on the user login page for selection. In this example, set the value to **DingTalk**. |
   |Provider type |The authentication protocol used by the external IDP. Select **OAuth 2.0 provider**. |
   |Provider |Select **DingTalk** as the actual external IDP. |
   |Egress method |Select the resource egress method. In this example, select the **platform default egress**. |
   |Client ID |The Client ID (formerly AppKey and SuiteKey) of the DingTalk application. In the [DingTalk Open Platform](https://open-dev.dingtalk.com/fe/app?hash=%23%2Fcorp%2Fapp#/corp/app), click the target application name, click "Basic Info \> Credentials & Basic Info" in the left\-side navigation pane, and obtain the Client ID. |
   |Client secret |The Client Secret (formerly AppSecret and SuiteSecret) of the DingTalk application. In the [DingTalk Open Platform](https://open-dev.dingtalk.com/fe/app?hash=%23%2Fcorp%2Fapp#/corp/app), click the target application name, click "Basic Info \> Credentials & Basic Info" in the left\-side navigation pane, and obtain the Client Secret. |
   |User unique identifier attribute |The unique identifier attribute of the user extracted from the OAuth response, such as user_id and email. In this example, set the value to **unionId**. |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you also need to integrate Microsoft Entra ID (Teams) or on‑premises AD (via SAML/OIDC proxy), continue adding them one by one in the same manner. All external IDPs will then be displayed as multiple login buttons on the Agent Identity unified login page.   </div>
   

<span id="t7j1TZPy"></span>
### Step 3: Configure the OIDC login protocol in ArkClaw


1. Activate an ArkClaw space.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you are using an activated ArkClaw space, skip this step.   </div>
   

   1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), and use the **Other standard protocols** authentication method to quickly activate a space.

   2. Click “Buy now” based on the on\-screen instructions to purchase seats.

2. In the left navigation pane, click “User management” and configure the authentication method.

   1. For a newly created space, click "Instant configuration". For a space that already has user data, click “Edit” on the “Login configuration” tab.

   2. Specify the parameters based on the following table. After the configuration is complete, click “Save”.

      
      |Configuration item |Description |
      |---|---|
      |Select protocol |Select the identity authentication protocol to be used. For ArkClaw, the external IDP being integrated is Agent Identity. Therefore, you need to select **OIDC**, which is the protocol type of Agent Identity. |
      |Client ID |The client ID created in Agent Identity. |
      |Client secret |The client secret created in Agent Identity. |
      |Issuer URL |The unique identifier address of the OIDC IDP. The system will automatically discover the authorization endpoint, token endpoint, and user information endpoint by using the address.<br><br>This is the `https://domain` part of the "OIDC Discovery URL" of the user pool created in Agent Identity.<br><br>Example:<br><br><br>* The OIDC discovery URL is `https://userpool-a4894bb0-8665-xxxx-979a-ec87c2999b2c.userpool.auth.id.cn-beijing.volces.com/.well-known/openid-configuration`.<br><br>* The issuer URL is `https://userpool-a4894bb0-8665-xxxx-979a-ec87c2999b2c.userpool.auth.id.cn-beijing.volces.com`. |
      |Unique identifier policy |The unique identifier policy is used to **determine whether the same employee has been imported multiple times**: When the employee list is imported again, the system will merge records for the same employee into a single entry based on the unique identifier you select. This field **only determines the basis for merging and does not determine the login method**.<br><br>* **Mobile number:**  Applicable to scenarios involving external contractors or temporary accounts.<br><br>         * **Email address:**  Applicable to scenarios where employee email addresses are standardized and uniformly managed across the enterprise.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>After the unique identifier policy is selected, we recommend not switching it midway</strong>: After switching, existing employee records may not match newly imported employee records, resulting in duplicate accounts.</div><br> |
      


<span id="A1kSUEb4"></span>
### Step 4: Configure the callback information of the Agent Identity client


1. On the “Login configuration” tab of the user management page, copy the "redirect URI of standard OIDC SSO authorization code".

   2. Return to the [BytePlus Agent Identity console](https://console.byteplus.com/identity). In the left navigation pane, click "User identity management". In the user pool list, click the name of the user pool `my-app-docs` created in **Step 1**.

   3. In the left navigation pane, click “Client” under the user pool `my-app-docs`. Find the `my-company-portal` client created in **Step 1**, and click “Edit” in the “Actions” column.

   4. Paste the copied ArkClaw SSO authorization code redirect URL into "Allowed callback URIs". Then, click "Confirm".


<span id="nQpeQbrU"></span>
### Step 5: Configure the callback information of the Feishu/DingTalk application


1. In the left navigation pane of the [BytePlus Agent Identity console](https://console.byteplus.com/identity), click "User identity management". In the user pool list, click the name of the user pool `my-app-docs` created in **Step 1**.

   2. On the user pool details page, copy “OAuth callback URL”.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The Feishu and DingTalk applications use OAuth. Therefore, copy the OAuth registered callback URL. If you are configuring an external application of a different type, such as OIDC or SAML, copy the corresponding registered callback URL.   </div>
   

   3. Configure the callback information of the Feishu application.

      1. Go to the [Feishu Open Platform](https://open.larkoffice.com/app?lang=zh-CN). Click the Feishu application name configured in the external IDP of Agent Identity.

      2. On the “Security configuration” page, paste the copied OAuth callback URL into the **Redirect URL** field and click “Add”. The URL will take effect immediately.

   4. Configure the callback information of the DingTalk application.

      1. Go to the [DingTalk Open Platform](https://open-dev.dingtalk.com/fe/app?hash=%23%2Fcorp%2Fapp#/corp/app). Click the DingTalk application name configured in the external IDP of Agent Identity.

      2. On the “Security configuration” page, paste the copied OAuth callback URL into the **Redirect URL** field and click “Save”.

      3. In the left navigation pane​, click "Application Publication \> Version Management and Release". Then, click "New version".

      4. Specify the version number and version description. For the **Application availability scope** parameter, keep the same scope as the previous release. No additional configuration is needed. The configuration is complete.


<span id="eA9xowis"></span>
### Step 6: Verify the configuration


1. On the "Space Overview" page of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), copy the employee login link.

2. Open the link in a browser to go to the login page. Log in to ArkClaw by using either Feishu or DingTalk. You will be redirected to the corresponding platform for authorization. On first login, an account will be automatically created in ArkClaw. You can view the new user by navigating to **User Management \> Users**.
