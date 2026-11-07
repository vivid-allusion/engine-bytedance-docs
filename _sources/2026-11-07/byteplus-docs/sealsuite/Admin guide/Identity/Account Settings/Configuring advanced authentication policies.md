---
title: "Configuring advanced authentication policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-advanced-authentication-policies"
---

SealSuite's **Advanced Authentication** provides dynamic identity verification and application access control through a conditional access mechanism. Instead of a one\-size\-fits\-all approach, you can customize security entry requirements based on user login context, device environment, and account scope.

<span id="8d67b44d"></span>
## Policy Scenarios

Policies are categorized based on when the security check is triggered:


|**Category** |**Scenarios** |**Interception Point** |**Core Value** |
|---|---|---|---|
|**Login Scenario** |Portal login, Desktop client login, Mobile client login, Staff Wi\-Fi Portal, Admin Console login |When a user launches the SealSuite client or attempts to enter the workspace. |**Entry Protection**: Defines allowed authentication methods for different environments to prevent unauthorized access. |
|**Application Access** |Specific SSO Applications |When a user clicks to open a specific **SSO App** within the office portal. |**Continuous Verification**: Ensures that sensitive apps require baseline checks or MFA even after the initial login. |


<span id="242eac5a"></span>
## Navigation Path


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Identity** \> **Account Setup** \> **Advanced Authentication**.

3. For first\-time setup, click the center toggle to enable the feature.

4. Confirm the activation in the pop\-up.

   * **Note**: Once enabled, the Admin Console session will be separated from the User Portal session for enhanced security, requiring a re\-login.


<span id="f6709ee2"></span>
## Configuring Login Scenario Policies

Use this scenario to define the authentication strength, environmental requirements, and session validity for users logging into SealSuite.

<span id="6818c37a"></span>
### Procedure


1. On the **Advanced Authentication** page, click  **+**  **Add Policy**.

2. Select the specific **Login Scenario** and **Organization Unit**, then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23e635c4828f4bec851f645517abc193~tplv-goo7wpa0wc-image.image) </span>

3. Configure the policy details as follows:

   * **General**

      
      |**Configuration** |**Required** |**Description** |
      |---|---|---|
      |**Policy Name** |Yes |A unique identifier for the policy. |
      |**Policy Description** |No |Optional details or administrative notes. |
      |**Priority** |Yes |Higher values indicate higher priority. Custom policies must be \> 0 to override the system default (Priority 0).<br><br>**Logic**: High\-risk **block** rules should be set to 100. Standard rules range from 1–99. If priorities match, the system follows the  **"Restrictive First"**  rule: **Block \> MFA \> Allow**. |
      |**Unit** |Yes |Read\-only. |
      

   * **Policy Management**

      
      |**Parameter** |**Required** |**Description** |
      |---|---|---|
      |**Detect login environment** |No |Sets the entry threshold. If enabled, only users/devices passing these posture checks can log in. Conditions can be linked via **AND/OR** logic. |
      |**Configure optional primary authentication methods** |Yes |Determines which login options (e.g., Password, SMS, Lark) appear on the user's login page. Drag and drop to reorder the icons to set their display priority.<br><br>**Note**: Methods must be pre\-configured in the **Identity Authentication** or **Third\-Party Login** modules. "Browser quick login" is automatically hidden for Desktop/Mobile scenarios. |
      |**Configure the effective account range** |Yes |Defines the target audience. Can be set to "All Users" or specific Departments, Roles, or Individuals using AND/OR logic. |
      |**The authentication method used by the user** |No |Authentication routing: Used to apply different security strengths based on the user's chosen login method. This allows for a "Silent pass for strong auth, additional verification for weak auth" balance. If a user’s method falls within this selected scope, the subsequent action (MFA/Block) is triggered. Otherwise, the system proceeds to the next lower\-priority policy. |
      |**Configure how to proceed after primary authentication** |Yes |The logic executed after the first authentication step is completed:<br><br><br>* **Pass**: Grants immediate access.<br><br>* **Required MFA**: Prompts for a second factor. Drag to reorder available MFA methods.<br><br>* **Block**: Terminates the session. Allows for custom multi\-language **Warning Text** (e.g., "Access denied due to security non\-compliance"). |
      |**The two\-factor authentication method used by the user** |No |Only visible if **Required MFA** is selected. Choose "All" or specify a subset of MFA methods. If the user uses a specified method, the policy continues to execute subsequent validity settings. |
      |**Configure login validity period** |Yes |* **Valid period**: Duration of the login state (default 20 days).<br><br>* **Client session auto extension**: Extends the session if the user remains active.<br><br>* **Browser session timeout**: Clears the login state when the browser is closed. |
      


<span id="b58ab556"></span>
### Scenario Examples

<span id="4ec0ec96"></span>
#### Example 1: Mandatory MFA for Internal Logins


* **Goal**: Ensure employees in Department A always use SMS MFA when logging in from the office.

* **Configuration**:

   * **Detect login environment**: Enabled (Check if IP is in the Internal Range).

   * **Target Scope**: Department A.

   * **Action**: Require MFA (SMS Code).


<span id="90349962"></span>
#### Example 2: Geofencing for High\-Risk Groups


* **Goal**: Allow general staff to work from home, but restrict Department A to office\-only access.

* **Logic**:

   1. **Policy X (Priority 100)** : If User is in **Dept A** AND IP is **NOT** Internal \-\> **Action: Block**.

   2. **Policy Y (Priority 10)** : If User is **Anyone** \-\> **Action: Allow**.

* **Outcome**: Dept A members attempting to log in from home will trigger the high\-priority Block rule. Others will bypass Policy X and match Policy Y.


<span id="d21dd8c9"></span>
## Configuring Application Access Policies

This scenario adds a security layer to specific sensitive SSO apps (e.g., Finance systems, Code Repositories).


1. Click **Add Policy** and select **App Access**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd73e3a59aef45ccb49817ea88b40817~tplv-goo7wpa0wc-image.image) </span>

2. Configure the policy details as follows:

   * **General**

      
      |**Configuration** |**Required** |**Description** |
      |---|---|---|
      |**Policy Name** |Yes |A unique identifier for the policy. |
      |**Policy Description** |No |Optional details or administrative notes. |
      |**Priority** |Yes |Higher values indicate higher priority.<br><br>**Logic**: High\-risk **block** rules should be set to 100. Standard rules range from 1–99. If priorities match, the system follows the  **"Restrictive First"**  rule: **Block \> MFA \> Allow**. |
      |**Unit** |Yes |Read\-only. |
      

   * **Policy Management**

      
      |**Configuration** |**Required** |**Description** |
      |---|---|---|
      |**Configure application scope** |Yes |* **Selection Mode**: Choose by **App Name** or **App Tag** (for bulk management).<br><br>* **Scope**: Apply to "All" SSO apps or a "Partial" list of specific apps. |
      |**Environment detection** |No |* **Time Range**: Access only during specific hours.<br><br>* **Login IP**: Restrict to office/VPN IPs.<br><br>* **User\-Agent**: Limit access to specific browsers or OS versions.<br><br>* **MFA Age**: Force a re\-authentication if the last MFA was more than X hours ago.<br><br>* **Primary Auth Used**: Trigger actions based on how the user first logged into SealSuite (e.g., force MFA if they only used a password). |
      |**Configure the effective account range** |Yes |Define which users/departments are subject to this app\-level check. |
      |**Configure disposal method** |Yes |* **Pass**: Immediate access to the app.<br><br>* **Require MFA**: Triggers a challenge before opening the app.<br><br>* **Block**: Denies access with a custom explanation (e.g., "Disk encryption required for this app"). |
      


<span id="751b0942"></span>
## Policy Management

<span id="a4d47813"></span>
### Global Control

The **Master Toggle** in the top right allows you to enable or disable the entire Advanced Authentication module.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a843c460b9748fc8dfa13b0a2a3a16b~tplv-goo7wpa0wc-image.image) </span>


* **Disabling**: Suspends all login and app access rules, reverting all accounts to the system default state.

* **Security Note**: Disabling this feature terminates current admin sessions and removes the login isolation between the User Portal and Admin Console.


<span id="45ac7061"></span>
### Priority Management

SealSuite uses a  **"Top\-to\-Bottom, First Match"**  logic.


* **Adjustment**: Drag the priority bubble next to a policy or enter a value manually.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfce1c7aec26400a8ba5da114d5a1b5d~tplv-goo7wpa0wc-image.image) </span>

* **Best Practice**: Place specific, high\-risk, or restrictive policies at the top and broad, general "catch\-all" policies at the bottom.


<span id="279fa813"></span>
### Policy Lifecycle


* **Enable/Disable**: Toggle policies on or off without deleting them—perfect for troubleshooting or phased rollouts.

* **Edit**: Update scopes, posture checks, or actions in real\-time.

* **Copy**: Copy existing configurations to quickly deploy similar rules for different departments or apps.

* **Delete**: Permanently remove a policy. *Warning: Ensure a lower\-priority policy exists to prevent a security vacuum.* 


<span id="af89f227"></span>
### Searching and Filtering

Use the toolbar to quickly locate policies by:


* **Name**: Keyword search.

* **Status**: Filter by Enabled/Disabled.

* **Scenario**: Filter by Login or App Access types.

* **App Scope**: Search for policies affecting a specific SSO application.
