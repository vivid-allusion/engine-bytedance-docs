---
title: "Setting up account systems and identity authentication"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-account-settings"
---

SealSuite features a standalone account framework that allows administrators to tailor every aspect of the identity authentication process. By aligning login workflows with corporate security policies and employee habits, you can strike the perfect balance between robust security and a seamless user experience. This guide covers how to customize authentication methods, manage session validity, and configure account\-level policies.

<span id="e0c7e82e"></span>
# Getting Started


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Identity** \> **Account Setup**.

3. Navigate to the **Authentication** tab. Select the target **Organization/Unit** from the dropdown menu next to **Login Configuration**.

4. Locate the section you wish to modify, click **Edit**, and configure the parameters as described in the [Configuration Details](https://docs.byteplus.com/docs/sealsuite/docs-managing-account-settings#617937e6) section below. Click **Save** when finished.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88a12f40e1ff4e329f51617fcb546155~tplv-goo7wpa0wc-image.image) </span>


<span id="617937e6"></span>
# Configuration Details

<span id="2e5aa507"></span>
## Login Configuration

This section defines how employees authenticate and what they see on the login screen. You can mix and match traditional credentials, passwordless options, and QR scans while customizing the visual hierarchy.


* **Basic login method**

   This setting supports "Account & Password" or "Passwordless Verification" (or both). You can drag and drop these options to prioritize which one appears first in the UI.

   
   |Option |Description |
   |---|---|
   |**Username & password** |The standard login method. Once enabled, users log in using their credentials. You can specify which identifiers serve as the username: **Email, Phone Number, or User ID**.<br><br>**Note**: Ensure the selected identifiers cover your entire workforce. If some employees only have mobile numbers on file and others only have emails, both must be checked to prevent login lockout. |
   |**Email OTP** |A passwordless method that sends a One\-Time Password (OTP) to the user's registered email.<br><br>**Prerequisite**: Requires an active email gateway. Click **Configure** or see [Manage Email configuration](https://docs.byteplus.com/docs/sealsuite/docs-overview-of-notifications#598a8170). |
   |**SMS OTP** |A passwordless method that sends an OTP via text message.<br><br>**Prerequisite**: Requires an active SMS gateway. Click **Configure** or see [Manage SMS configuration](https://docs.byteplus.com/docs/sealsuite/docs-overview-of-notifications#e10840ea). |
   

* **Advanced login methods**

   Streamline the login experience by leveraging existing active sessions.

   
   |Option |Description |
   |---|---|
   |**QR Code** |Allows users to log in to the Desktop client or Web portal by scanning a QR code with their already\-authenticated SealSuite mobile app. |
   |**Desktop client assists mobile client login**<br><br>(v3.3.11+) |Authenticates a mobile device using an active Desktop session. Users simply scan the QR code found under their Desktop profile avatar to log in instantly on mobile. |
   |**Browser quick login** |Synchronizes the login state between the Desktop client and the web browser. If the Desktop client is online, the browser will automatically inherit that session.<br><br>We recommend enabling **Secondary Authorization Confirmation** to require a "Confirm" click on the Desktop client, preventing unauthorized browser access. |
   

* **Login method display order**

   Fine\-tune the visual layout of the login interface.

   * **Prioritization**: Drag the cards to reorder login tabs. The top\-ranked method becomes the default view.

   * **Extensibility**: This section automatically pulls in any active **Third\-Party Auth Sources**. To add more (e.g., SSO), manage them in the **Third\-Party Login** page.

   * **White\-labeling**: For native SealSuite logins, click the **Settings** (gear) icon on the card to customize the icon and localized display names to match your brand.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/faf11d65765d4094a5489a920baa627b~tplv-goo7wpa0wc-image.image) </span>

> **Pro Tip: Advanced Access Control**

> The settings above are global defaults. For granular, context\-aware access control (e.g., requiring MFA only for off\-site access), please refer to [Configuring advanced authentication policies](https://docs.byteplus.com/docs/sealsuite/configuring-advanced-authentication-policies).


<span id="98782d4e"></span>
## Session Settings

Control the lifecycle of an authenticated session to mitigate risks from shared or lost devices.


|Feature |Description |
|---|---|
|**Valid period** |Defines how long a user stays logged in. Default is 20 days. Options range from 1 day to 90 days, or a custom duration. Users must re\-authenticate once this expires. |
|**Client session auto extension** |A "Keep\-Alive" mechanism. When enabled, the system silently extends the session validity as long as the user is active, minimizing intrusive forced logouts. |
|**Browser session timeout** |(Web Portal only) Ties the login state to the browser session. Closing the browser window or tab immediately terminates the session. |


<span id="5dc2daae"></span>
## Unit Settings

For multi\-entity organizations, define how users identify their specific unit during login. (See [Multi-Tenant management](https://docs.byteplus.com/docs/sealsuite/managing-multi-tenant_configurations) for setup).


|Feature |Description |
|---|---|
|**Unit certification method** |Determines how users find their unit:<br><br><br>* **Select unit name**: Pick from a dropdown list.<br><br>* **Enter unit ID**: Manually type a specific Unit ID. |
|**Priority given to primary unit login** |* **Enabled**: Users skip the unit selection screen and go straight to their primary organization. Highly recommended for single\-unit companies.<br><br>* **Disabled**: Users must explicitly choose a unit. Recommended if employees frequently switch between different legal entities. |


<span id="9d4e0a4b"></span>
## More Settings

Final compliance and automation settings for the account system.


|Feature |Description |
|---|---|
|**Enterprise mailbox domain name** |Standardizes data entry. Setting a domain (e.g., @company.com) restricts both admins and users to using only official corporate email addresses. |
|**Account Expiration Alerts** |Crucial for managing contractors or temporary staff.<br><br>Set a lead time (1–15 days) to send daily reminders at 10:00 AM via SMS, Email, or IM (Lark/DingTalk).<br><br>**Critical Warning**: Upon expiration, the account is **Suspended**. All active Wi\-Fi/VPN sessions will be terminated immediately. Enabling reminders is strongly advised. |
