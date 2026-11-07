---
title: "Outbound file control policy management"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule"
---

SealSuite DLP provides outbound file control to protect an enterprise's core digital assets. It prevents sensitive data from being unintentionally or maliciously leaked through various channels. By configuring granular audit and blocking policies, you can comprehensively monitor, collect evidence for, and intercept data outbound activities on employee endpoints. This helps protect enterprise intellectual property and meet compliance audit requirements.

Outbound file control detects local files on the endpoint. It checks files sent by employees through desktop applications, browsers, or computer peripherals. It then records or blocks outbound activities based on policies.

# Preparations

The core of an outbound file control policy is matching sensitive data. Check whether the built\-in sensitive data meets your requirements in advance, and add enterprise\-specific custom sensitive data. For more information, see [Overview of data identification](https://docs.byteplus.com/en/docs/sealsuite/data-identification-overview?lang=en).

# Add an outbound file control policy

## Procedure

1. Log in to the Admin Console.

2. In the left navigation pane, choose **DLP** ＞ **Strategy Center** ＞ **Control Strategy** ＞ **Document Outgoing Control**.

3. On the **Policy List** tab, create an outbound file control policy.

   * Method 1: Click **New Rule** in the upper\-right corner of the list.

      ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/swg-ndlp-en-20260923/swg-file-policy-list-redacted-v2.png)

   * Method 2: Click **More** ＞ **Policy template** in the upper\-right corner of the list, and use a built\-in SealSuite template to create a policy.

4. On the policy configuration page, complete the following settings:

   * **General**

      * **Policy name**: Customize a name to identify the policy.

      * **Policy description**: Add supplementary information. This field is not used for logical evaluation.

      * **Priority**: Define the policy execution order (0\-100). **A higher value indicates earlier matching**. If policies with the same priority are matched, the most recently created or updated policy is executed.

      * **Manage labels**: Select a tag to associate with the current policy (optional). The drop\-down list displays only tags granted to the current administrator. Associated tags isolate policy permissions between administrators in different regions or business lines. To add or adjust visible tag options in the drop\-down list, a super administrator must modify the "Management tag scope" for your administrator role in **Enterprise Settings** \> **Administrator Permissions**. For instructions, see [Edit administrator permissions](https://docs.byteplus.com/en/docs/sealsuite/docs-editing-or-deleting-administrator?lang=en).

   * **Control action**

      Set different **control actions** to address different security requirements:

      * **Allow**: Detects and records sensitive outbound file transfer activities without interception, enabling activity tracking without interrupting employees.

      * **Deny**: Intercepts and records high\-risk sensitive outbound file transfer activities, enforcing security policies.

      > **Note**

      > **Configuration reference**

      * > Highly sensitive groups: Configure the "Allow" action for common office software to record and archive all outbound file transfers. Configure the "Deny" action for uncommon or high\-risk software.

      * > Regular employees: Configure more relaxed "Allow" policies to focus on recording and maintain the office experience.

   * **Control channel**

      Define the activity channels to control. Multiple selections are supported. The configuration details are as follows:

      |**Configuration item** |**Description** |
      |---|---|
      |**Desktop application** |Audits or blocks employee outbound activities through client software, such as chat applications, cloud drives, and email clients.<br><br>If the built\-in application list does not contain the required control channel, go to **Strategy Center** \> **Channel List** \> **Desktop Application** to add a custom channel. For more information, see [Add a custom desktop application](https://docs.byteplus.com/en/docs/sealsuite/channel-lookup-and-custom-configuration?lang=en#f6f9639d).<br><br>> **Warning**<br><br><br>> Some applications differ in how controls take effect or configuration restrictions. **Make sure to read** [Appendix: Special application control instructions](https://docs.byteplus.com/en/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule?lang=en#c8ef7d1b) before configuration.<br> |
      |**Website** |Audits or blocks file uploads to websites through browsers. After selecting a browser, you can also configure control for all websites or specified websites. This policy detects uploaded local files on the endpoint and identifies sensitive content before files leave the device.<br><br>If the built\-in website list does not contain the required control channel, go to **Strategy Center** \> **Channel List** \> **Web Website** to add a custom channel. For more information, see [Add a custom Web website](https://docs.byteplus.com/en/docs/sealsuite/channel-lookup-and-custom-configuration?lang=en#3774821c).<br><br>> **Note**<br><br><br>> To check manual webpage input or form submissions, or to detect file uploads and downloads on the gateway side, go to **DLP** \> **Strategy Center** \> **Control Strategy** \> **Network DLP** to configure the corresponding policy. For instructions, see [Configure a Web data protection policy](https://docs.byteplus.com/en/docs/sealsuite/configuration-web-data-protection-policy?lang=en).<br> |
      |**Computer peripherals** |The supported types vary based on the selected **control action**:<br><br><br>* **Allow**: Supports auditing file outbound activities through **storage peripherals** (USB drives and removable hard disks) and **printers**.<br><br>* **Deny**: Supports only blocking file transfers to **storage peripherals**.<br><br><br>> **Note**<br><br><br>> **Supported scope**<br><br><br><br>* > **Platform restriction**: Blocking for storage peripherals is currently supported only on Windows.<br><br><br>* > **Control scope**: Storage peripheral blocking on Windows currently controls only file copy and access activities performed through **system folders (File Explorer)**.<br><br><br>* > **Printer**: Only "Allow" auditing is supported, and Windows 7 or macOS 10.15 or later is required.<br> |
      |**Exclude internal address** |To balance Data Security and office efficiency, SealSuite supports granular internal address allowlist rules for different types of business channels. Operations that match internal addresses are not logged or blocked.<br><br>**Procedure**<br><br><br>1. Click  **＋ Import** in the upper\-right corner, and select the internal addresses to exclude from the configured internal address list.<br><br>2. Click **OK** to complete the internal address configuration.<br><br><br>> **Note**<br><br><br><br>* > For **Web websites** and **AI tools**, if the pop\-up list does not contain a matching internal address, click the quick add button in the upper\-right corner of the page to go to **Strategy Center** \> **Internal Addresses**. Then manually add or batch import the corresponding internal addresses. For more information, see [Internal address configuration instructions](https://docs.byteplus.com/en/docs/sealsuite/internal-address-configuration?lang=en). After adding the addresses, return to the original page and click the refresh icon. You can then select the newly added internal addresses for exclusion.<br><br><br>* > To add other types of internal addresses, first go to **Strategy Center** \> **Internal Addresses** and add the resources to exclude to internal addresses. Then enable the corresponding channel type here and import the added resources. For more information, see [Internal address configuration instructions](https://docs.byteplus.com/en/docs/sealsuite/internal-address-configuration?lang=en).<br> |

   * **Sensitive Content**

      Apply the sensitive data configured during preparation to this policy as the core basis for policy matching. Click **Add Data** on the right, and select the specific sensitive data content that this policy needs to detect.

   * **Action**

      Define the response action after a policy is matched.

      |Disposition method |Description |
      |---|---|
      |**Log reporting** |Reports violation events to the Admin Console. This item is enabled by default and cannot be disabled. View events on the **Investigation Audit** \> **Audit Log** \> **File Sharing Log** page. For more information, see [View outbound file logs](https://docs.byteplus.com/en/docs/sealsuite/docs-viewing-audit-alerts?lang=en). |
      |**Screenshot** |After this option is enabled, the system captures the employee desktop as evidence when the employee triggers an outbound file transfer activity. Click **Configure** on the right to select effective systems (Windows, macOS, Linux).<br><br><br>* **Windows/Linux**: No employee awareness.<br><br>* **macOS**: The "Screen Recording" permission must be enabled. On macOS 14+, frequent system privacy prompts are displayed. We recommend going to [Forensic screenshot configuration](https://docs.byteplus.com/en/docs/sealsuite/configuring-system-settings-for-file-egress-control-policies?lang=en#5dfef9f3) and switching to **Outbound screenshot** mode to reduce disruption to normal employee work. |
      |**File archiving** |Retains the original outbound files as evidence. Download and view them on the **Investigation Audit** \> **Audit Log** \> **File Sharing Log** page. |
      |**Terminal notification** |Sends risk notification messages to employees on the endpoint side. After enabling this option, click **Configure** on the right to go to the **Notification Pop\-up Template** configuration page. Then create or reuse an outbound file control notification template. For more information, see [Configure a notification pop-up template](https://docs.byteplus.com/en/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule?lang=en#0ef1e66d). |

   * **Scope**

      Define the scope of this policy. Granular settings are supported by **employee** (department/role) or **device** (operating system/group), and exclusion objects are supported.

      > **Note**

      > To handle temporary outbound file transfer needs for controlled employees, such as handover during resignation or urgent business transfers, we recommend that you do not frequently modify exclusion objects in global policies. Configure time\-limited inspection\-free allow rules by referring to [Manage the outbound file blocking allowlist](https://docs.byteplus.com/en/docs/sealsuite/managing-file-outbound-block-allowlists?lang=en). This provides more flexible exception management.

## Configure a notification pop\-up template

After **Terminal notification** is enabled, the SealSuite client displays a pop\-up notification on the endpoint when an endpoint user triggers the current policy. Based on whether the selected control action is **Allow** or **Deny**, the system displays the corresponding **audit** or **block** notification pop\-up template. On this page, you can configure pop\-up display rules and choose to create a notification template or quickly reuse an existing template.

> **Note**

> **Template binding rules**: The same notification template can be bound to multiple control policies. The same control policy can be bound to only one notification template.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d81cd5f504754902b6ae8edb4038041d~tplv-goo7wpa0wc-topic.webp)

### Configure pop\-ups

1. In the **Pop\-up Configuration** area, click **Configure** and complete the following parameter settings.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e57e33283db3403b84287334a0494f25~tplv-goo7wpa0wc-topic.webp)

   * **Popup quiet time**: The minimum interval between two adjacent pop\-up displays after an endpoint user triggers a policy. The unit can be seconds, minutes, or hours. During the silent period, the client continues to execute the policy control action but does not display the pop\-up. We recommend setting an appropriate pop\-up silent period based on the policy trigger frequency to avoid frequent pop\-ups that affect user experience.

      > **Note**

      > If the user selects "Do not remind me again today" on the pop\-up page, the pop\-up is no longer displayed according to the configured silent period rule after it is closed.

   * **Pop\-up Display Time**: The time that the pop\-up stays on the endpoint (1\-60 seconds). After the timeout, the pop\-up automatically closes and the corresponding control action is executed.

2. Click **OK** to complete the configuration. All notification pop\-ups under this control action synchronize this configuration.

### Configure templates

Based on the endpoint notification requirements of the current policy, you can select **Create Notification Template** or **Reuse Existing Template**.

> **Note**

> **Template configuration selection instructions**:

* > If the current policy requires independent notification text, or existing templates do not meet requirements, we recommend selecting **Create Notification Template**.

* > If multiple policies need to display the same or similar notification content, we recommend selecting **Reuse Existing Template** to avoid duplicate configuration. Before reuse, view the policies bound to the template to confirm the template usage scope.

#### Create a notification template

1. In the **Notification Pop\-up Template** window, click **Create Notification Template** and complete the following configurations in the drawer that appears.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee96e09a9a5345749523b03edde3b519~tplv-goo7wpa0wc-topic.webp)

   * **General**

      * **Template name**: Customize a name to identify the current notification template. Template names cannot be duplicate and cannot exceed 50 characters.

      * **Multilingual configuration**: Follows the system language configuration by default. You can add, delete, or switch language labels to configure multilingual notifications.

         > **Caution**

         * > Multilingual configuration currently supports **Chinese, English, Japanese, and Korean**. We recommend keeping only the language labels actually required. To restore a deleted language label, click **Add Language** to add it again.

         * > After setting language labels, configure the notification title, notification content, and button text for each language. This avoids inconsistent notification content. If no configuration is provided, the system displays the prefilled copy for that language.

      * **Notification title**: Customize the notification title, which is displayed at the top of the pop\-up and cannot exceed 100 characters.

      * **Notification content**: Customize the notification content, which is displayed in the body area of the pop\-up and cannot exceed 500 characters. We recommend describing the trigger reason, control result, and subsequent processing method.

      * **Button Label**: Customize the pop\-up button text. It cannot exceed 20 characters. After an employee clicks this button, the pop\-up closes.

2. **View the pop\-up preview:**  In the **Preview** area on the right, you can view the pop\-up effect on the endpoint side in real time. Switch language labels to check whether the title, body, and button text are correct in different languages.

3. After confirming that the configuration is correct, select a save mode as needed.

   * **Save as template**: Saves the configuration only to the public template library. The current policy does not reference it yet.

   * **Save as Template And Use**: Saves the configuration to the public template library and associates the template with the current policy.

   > **Note**

   > Templates saved to the public template library can be reused later. You can further **edit/copy/delete** public templates. For more information, see [Manage public templates](https://docs.byteplus.com/en/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule?lang=en#2aa1b07c).

#### Manage public templates

In the **Template Configuration** area of the **Notification Pop\-up Template** window, the system displays the list of notification templates that match the current control action. The list includes created templates and system built\-in templates. You can directly select the target template from the list. You can also enter a template name in the search box to search.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/231e2d0f15fd45f784aafd826d5bc185~tplv-goo7wpa0wc-topic.webp)

Hover over the **More Actions** icon on the right side of a template card to **edit**, **copy**, or **delete** the template.

* **Edit**: To modify the template text or other configurations, select **Edit**. After modification, select a save mode as needed.

   > **Caution**

   > If this template is bound to other policies, all bound policies use the updated template configuration after you edit and save it. We recommend clicking **Number of bound policies** to view related policy details, and then performing the operation after confirming the impact scope.

* **Copy**: To adjust content based on an existing template without affecting the original template and its bound policies, select **Copy**. The system generates a **copy** template based on the current template. You can modify the related configurations of the copy template.

* **Delete**: If you confirm that a template is no longer needed, select **Delete**.

   > **Caution**

   > Templates bound to policies cannot be deleted. To delete one, first disable **Terminal notification** in all bound policies and save the policies. Then delete the template after unbinding it. When related policies enable Endpoint notification again later, the notification template must be reconfigured.

# Manage the policy lifecycle

On the **Document Outgoing Control** list page, you can perform routine management for created policies.

* **View policy statistics**: At the top of the policy list, the system provides a visual data dashboard. After an administrator issues a new policy or modifies an existing policy, the dashboard tracks policy delivery progress and deployment status across all network endpoints in real time. This ensures that control requirements are actually implemented. The **server configuration version** number is the key basis for determining whether the client policy is up to date. Each time you edit or update any policy, this version number changes. If the version number reported by a client is the same as the number displayed here, the client policy has been synchronized to the latest version.

* **View policy change information**: In the policy list, you can directly view the **Last modified by** and **Last modified time** of each policy to quickly trace its change history.

* **View effective endpoints**: Click the number in the **Actual/Expected** column in the policy list to enter the **Policy in Effect** details page. You can view the **Policy version update time** of the endpoints. Click the **Refresh** button next to the number to proactively fetch the latest effective status data.

* **Enable/disable**: Use the switch in the **Status** column of a policy to quickly control the effective status of the policy.

* **Edit/copy/delete**: In the **Action** column of a policy, modify the policy, quickly create a similar policy, or remove a policy that is no longer needed. After a policy is deleted, it cannot be restored. However, historical detected events are still recorded in the alert event list.

* **Import/export**: Use the import/export buttons in the **More** drop\-down list in the upper\-right corner of the list to back up and restore policies in JSON format.

# Appendix: Special desktop application control instructions

When configuring desktop application control channels, some applications have independent effective logic or configuration restrictions.

## Code hosting applications

1. **Configuration restrictions for code version management tools**

   If only "code version management tools" (Git or SVN) are selected in desktop applications and the control action is **Deny**, the policy performs channel\-level overall interception. In other words, if the target address is not in the internal address allowlist, the transfer is directly intercepted regardless of the Outbound content. In this case:

   * **Sensitive Content** cannot be configured. The **Add Data** button is grayed out and unavailable.

   * Actions that depend on file content in **Action**, such as file archiving, are forcibly disabled.

## AI applications

1. **Outbound attribution rules for specific AI applications**

   For the six AI Agents that support plugins and tool calls, **OpenClaw**, **QClaw**, **EasyClaw**, **StepClaw**, **TRAE IDE, and TRAE CN IDE**, SealSuite uses the following attribution rules for outbound file transfers:

   * If the preceding AI Agents call other known file transfer tools (or applications) in the background to transfer files, SealSuite monitors the process that actually executes the transfer. Therefore, the Outbound channel is recorded as the file transfer tool, and the allowlisting policies and control rules of that tool are applied.

   * The Outbound channel is recorded as the Agent only when the preceding AI Agents use unknown tools, such as Python or other non\-standard transfer tools, or directly read local document data to interact with large models.

2. **Control plugins for specific AI applications**

   To control outbound file transfer activities in the four AI applications **OpenClaw**, **QClaw**, **EasyClaw**, and **StepClaw**, first go to **Strategy Center** \> **System Configuration** \> **Agent Plugin Control** and enable plugin control for the corresponding AI application. Make sure that the effective objects of the plugin control cover the effective objects of the current outbound file transfer policy. Otherwise, the control does not take effect. For more information, see [Agent plugin control](https://docs.byteplus.com/en/docs/sealsuite/configuring-system-settings-for-file-egress-control-policies?lang=en#cc404e17).
