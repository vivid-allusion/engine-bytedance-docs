---
title: "Configuring dynamic policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-dynamic-policies"
---

<span id="overview"></span>
## Overview

Dynamic Control lets administrators define rules that automatically apply controls based on employee account information, device status, or actions. For example, a rule can require additional verification when employees connect to the VPN outside working hours, or restrict network access when a device has a security risk. Use a predefined template or configure your own trigger conditions and remediation actions.

Templates cover the following scenarios:


* **Network access and security:**  Check baseline, software, and process risks or virus\-count thresholds, then restrict or block access. Notify employees through a third\-party bot and require additional verification for logins from unusual locations or outside China, or for application access from unusual locations.

* **Access control and employee activity:**  Require VPN authentication for unfamiliar devices or connections outside working hours. Adjust visible VPN nodes by department or location, and notify administrators when a Wi\-Fi account is used on more devices than allowed.

* **Scheduled maintenance:**  Require employees to reset network access passwords during specified periods.


<span id="592ae546"></span>
## Creating a rule group

For configuration examples, see [Best practices for dynamic control](https://docs.byteplus.com/docs/sealsuite/docs-best-practices-for-dynamic-control).


1. Log in to the Admin Console.

2. In the left navigation bar, click **Dynamic Control** \> **Control Policies**.

3. On the **Control Policies** page, click **Create New Policy**. You can also click **Create with Template** to use a predefined rule template.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/mfa-en-20260928/en-control-final.png) </span>

4. On the **Add a Policy Group** page, configure the following settings and click **Confirm**.

   To enable the policy later, clear **Enable immediately after creation** before saving, then enable it in the policy list when needed.

   
   |**Configuration Area** |**Description** |
   |---|---|
   |**General** |**Policy name**: A custom name used to identify the current rule group. |
   |**Trigger Type** |**Real\-time Protection**: Evaluate changes to endpoint accounts and devices immediately, without a scheduled interval. Add one or more account, device, or behavior parameters. |
   | |**Event Trigger**: Indicates that when the security status of an endpoint changes because of the specified device risk events, virus\-related events, or data leakage prevention events, SealSuite will trigger the current rule group in real time. In addition, you can set a triggering interval for the rule group.<br><br><br>* After selecting **Event Trigger**, you need to configure triggering events for the current rule group by selecting one or more of the following options:<br><br>   * **Device Security Risk Detection**: Trigger the rule when the client reports security check results. Select endpoint baseline, application, or process risks to evaluate.<br><br>   * **Device risk changes**: Trigger the rule when baseline, application, or process risks change, such as when the number of detected risks increases.<br><br>   * **Virus Event**: Indicates that in the event that a virus is detected on the client, SealSuite will trigger the current rule group.<br><br>   * **DLP Event**: Indicates that in the event that a data leakage prevention event is detected on the client, SealSuite will trigger the current rule group.<br><br>   * **Peripheral\-control events**: Trigger the rule when a peripheral\-control event is detected.<br><br>   * **Period (5 min)** : Indicates that the current rule group will be triggered every five minutes.<br><br>* **Trigger parameters:**  In this option, you can select one or more properties and logical conditions from the drop\-down list to construct a logical expression which functions as a trigger parameter. The available trigger properties include **Account Info**, **Operation Info**, **Device Info**, **Behavior Info**, **Device security status** and **Builtin function**. |
   | |**Action Trigger**: Indicates when user actions including VPN connections, network access, login/logout and application access occur on devices, SealSuite will trigger the current rule group.<br><br><br>* **Trigger Event:**  After selecting **Action Trigger**, you need to configure triggering actions for the current rule group by selecting one or more of the following options.<br><br>   * **Application Access**: Indicates that the current rule group will be triggered when users access applications through APIs or devices.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The <strong>API resources</strong> field is available only if your enterprise has purchased the application gateway feature and enabled it for the selected applications.      </div><br>      <br><br>      For API access, select a specific application or use tags to control multiple applications. Assign tags in the application details before using tag\-based matching. See [Managing Web App](https://docs.byteplus.com/en/docs/SealSuite/managing-web-app).<br><br>   * **VPN**: Indicates that the current rule group will be triggered when a user connects to a VPN or obtains a VPN node within the endpoint.<br><br>   * **Network Access**: Indicates that the current rule group will be triggered when users connect to wireless or wired networks, obtain network credentials, or get billed for network access.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After selecting <strong>Network Access</strong> \> <strong>Network Connection Status Reporting (Network Accounting)</strong> in the <strong>Trigger Event</strong>, the Device online check option appears under <strong>Operation info in Trigger parameters.</strong> By specifying the Device online check option as a triggering parameter, you can enable SealSuite to trigger the current rule group in the event that a client heartbeat is detected.      </div><br>      <br><br>   * **Portal Operation**: This rule will be triggered when a user logs in or out of the SealSuite portal.<br><br>   * **Client Operation**: This rule will be triggered when a user logs in or out of the SealSuite client.<br><br>* **Trigger parameters**: In this option, you can select one or more properties and logical conditions from the drop\-down list to construct a logical expression which functions as a trigger parameter. The available trigger properties include **Account Info**, **Operation Info**, **Device Info**, **Behavior Info**, **Device security status** and **Builtin function**. |
   |**Rules** |By default, the configuration area for a single remediation rule is displayed under the **Rules** section. To set up multiple remediation rules, click **Add rules** right next to the rule you just configured. Remediation rules are displayed by their priorities under the Rules section, with rules placed to the left having higher priority. For each remediation rule, you need to configure the following information:<br><br>**Logical expression**: Specify the logical relations for the trigger parameters that you just added by choosing your desired operators listed below.<br><br><br>* `!`: negation<br><br>* `in`: within a set<br><br>* `not in`: outside a set<br><br>* `>`: greater than<br><br>* `>=`: greater than or equal to<br><br>* `==`: equal to<br><br>* `!=`: not equal to<br><br>* `<`: less than<br><br>* `<=`: less than or equal to<br><br>* `+`: addition<br><br>* `-`: subtraction<br><br>* `*`: multiplication<br><br>* `/`: division<br><br>* `&&`: AND<br><br><br>**Remediation**: When detecting risk events that satisfy the current rule group on users’ devices, SealSuite can handle the events using the remediation actions listed below. Select one or more of the following actions for a single rule group:<br><br><br>* **Network Restriction**: Use this option to restrict or prohibit access to the corporate network. When selecting actions related to access restriction, you need to specify a restriction rule, which is used to add an allowlist or a blocklist for your enterprise's network resource.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following actions are unavailable when employees use Portal authentication for network access.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Limit device Wi\-Fi usage</strong>   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Restrict account from Wi\-Fi usage</strong>   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Limit device to wired</strong>   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Restrict account from wired usage</strong>   </div><br>   <br><br>   The disconnect\-network action is unavailable with 802.1X authentication.<br><br>* **Force Action**: When a risk event is detected, SealSuite can take actions such as **Kick out session by did**, **Kick out session by uid**, **Deactivate account**, and **Reset Wi\-Fi password**. Select one or more actions as needed.<br><br>   You can also change device groups or user roles. For a device, add a group, remove a group, replace the current group, or change extension attributes. For a user, add, remove, or replace roles. Either change can be reverted automatically after the risk is remediated.<br><br>* **Notification**: Select either **Send notification via third party app** or **Send notification via SealSuite Client**.<br><br>   * **Send notification via third party app**: A third\-party robot must be enabled and linked to the current rule group. After adding a third\-party robot, you can select the robot in the drop\-down list under the **Select Third\-Party IM** option. Multiple selection is supported. For more information on how to manage third\-party robots, please refer to [Manage third-party IM](https://docs.byteplus.com/en/docs/SealSuite/docs-overview-of-notifications#7e2d6168).<br><br>   * **Send notification via SealSuite Client**: Supports setting system notifications or strong reminders, and manual configuration of notification or reminder content is required.<br><br>* **Application**: Select **Allow Access**, **Deny Access**, or **Deny Download**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Application</strong> is only applicable to <strong>Action Trigger</strong>.   </div><br>    |
   | |**Notify employees after automatic recovery:**  After turning on this switch, you can select **Third Party Notification** **to Employees** or **Notify SealSuite Clients**. SealSuite notifies employees when risks are remediated or VPN, Wi\-Fi, and other controls recover automatically.<br><br><br>* **Third Party Notification to Employees**: A third\-party robot must be enabled and linked to the current rule group. After adding a third\-party robot, you can select the robot in the drop\-down list under the **Select Third\-Party IM** option. Multiple selection is supported.<br><br>* **Notify SealSuite Clients**: Send **System notification.**  You need to configure the notification content. |
   


The logical OR operator is `||`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Account information supports custom attributes for real\-time, event, and action triggers. Values depend on the attribute type. If a referenced custom attribute is deleted, the corresponding parameter becomes invalid. See <a href="https://docs.byteplus.com/en/docs/SealSuite/docs-configuring-custom-attributes">Configuring custom attributes</a>.</div>


<span id="vpn-secondary-authentication"></span>
### VPN secondary authentication

For VPN connection triggers, select **Require MFA** to require employees who match the rule to verify their identity before connecting.

Mobile VPN supports SMS and email verification codes. Before configuring the rule, go to **Identity** \> **Account Setup** \> **MFA Setup** and configure the mobile primary and alternative authentication methods for **Connect to VPN**. See [Configuring multi-factor authentication (MFA)](https://docs.byteplus.com/en/docs/SealSuite/docs-configuring-multi-factor-authentication-mfa-).


* When a mobile client matches the rule, it uses the saved mobile primary and alternative methods.

* The rule can require authentication even when the mobile switch in **Connect to VPN** is off.

* Dynamic Control can require authentication again within the configured authentication validity period. Check the relevant rules if employees receive frequent authentication requests.

* If no authentication method is available, employees cannot connect to the VPN. Check the configured methods, SMS or email service, and the employee's phone number or email address.


<span id="a360fdd9"></span>
## Managing a rule group


1. Log in to the Admin Console.

2. In the left navigation bar, click **Dynamic Control** \> **Control Policies**.

3. On the **Control Policies** page, locate the specific rule group and perform the following operations.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/mfa-en-20260928/en-control-final.png) </span>

   * Enable or disable a rule group.

      * When the switch is turned on, the current rule group takes effect, and SealSuite will apply the configured actions to the device according to the rule group configuration.

      * When the switch is turned off, the current rule group is not effective, and the device behavior does not trigger the rule group.

   * **Copy**, **Edit**, or **Delete** the rule group.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Deleting a rule group is permanent. SealSuite stops applying that rule group, but its historical remediation records remain available.      </div>
      

<span id="related-documents"></span>
## Related documents

[Viewing remediation logs](https://docs.byteplus.com/en/docs/SealSuite/docs-processing-records)

[Managing trigger logs](https://docs.byteplus.com/en/docs/SealSuite/docs-trigger-event-logs)

[Best practices for security compliance scenarios](https://docs.byteplus.com/en/docs/SealSuite/docs-best-practices-for-dynamic-control)
