---
title: "Skill Security Detection"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-skill-detection-policy"
---

Skill Security Detection checks Skill files on endpoints. It helps administrators discover malicious code, view detection results, handle false positives, and extract files for analysis.

## Feature introduction

A Skill is a set of instructions and related resources for an AI Agent to perform specific tasks. It may include operating instructions, scripts, templates, and other files. When employees download or use third\-party Skills, the instructions or scripts may guide the Agent to perform high\-risk operations. Therefore, the content and source must be checked. administrators can configure real\-time scans and scheduled scans to check risks when files are written to disk, changed, or reach a specified time.

SealSuite compares file hashes with the Threat Intelligence database to identify known malicious Skills. After content cloud lookup is enabled, SealSuite also uploads Skill file content to the cloud to check for malicious content and high\-risk code. After a risk is detected, the client reports alerts to the Admin Console. If **Endpoint notification** is enabled in the policy, the client also sends an alert notification to employees and guides them to handle risk files. administrators can centrally view risk code and affected devices, extract files for further analysis, or add a allowlist after confirming a false positive.

Only one Skill Security Detection policy is executed on the same endpoint. Multiple policies are not overlaid or merged. If multiple policies match, the policy with the highest priority value is executed first. If the values are the same, the most recently added or modified policy is executed.

## Prerequisites

The enterprise has activated **AI Security license**, and the administrator has menu and operation permissions for the corresponding feature. For detailed billing information, see [Billing items](https://docs.byteplus.com/en/docs/sealsuite/pricing).

## Add a Skill Security Detection policy

A detection policy specifies the scan method, detection scope, and notification method for Skills. When you use this feature for the first time, create and enable a policy first. Enable at least one of **Real\-time scan** and **Periodic scan**. You can also enable both. After the policy takes effect, risks detected on endpoints are displayed in **Audit Log**.

1. Log in to the Admin Console.

2. In the left navigation pane, choose **AI Security** \> **Supply Chain Security** \> **Skill Security Detection**.

3. Switch to the **Policy Management** tab, and click  **＋ Create policy** on the right.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-13.png)

4. On the **Create policy** page, complete the following configurations, and click **OK**.

   > **说明**

   > **Skill** cloud lookup supports Windows, macOS, and Linux. The client version requirements are as follows.

   * > **Skill Hash Cloud Lookup**: Requires SealSuite client **3.3.12 or later**.

   * > **Skill Content Cloud Search**: Requires SealSuite client **3.3.21 or later**.

   **Basic information**

   |Configuration item |Description |
   |---|---|
   |Policy name |Custom name used to identify the current policy. The name can contain up to 100 characters. |
   |Priority |Set the priority of the current policy. Valid values: 0 to 100. A larger value indicates a higher priority. Multiple policies can be enabled at the same time. If multiple policies match the same endpoint, only the policy with the highest priority is executed. If the values are the same, the most recently added or modified policy is executed. |

   **Cloud Scan Mode**

   |Configuration item |Description |
   |---|---|
   |Skill Hash cloud lookup |Enabled by default and cannot be disabled. This feature quickly identifies known malicious Skills by comparing Skill file hash values against the threat intelligence library. |
   |Skill content cloud lookup |After this feature is enabled, Skill source code content is uploaded to the cloud for semantic\-level detection to identify potential unknown malicious behaviors. Only Skill file content is uploaded. |

   **Scan method**

   |Configuration item |Description |
   |---|---|
   |Real\-time scan |After this is enabled, Skill files on endpoints are scanned in real time. Detection is triggered when a new Skill file is written to disk or changed, to identify potential malicious content and report alerts. |
   |Scheduled scan |After this is enabled, scheduled checks are performed on the status of existing local Skill files on endpoints, to discover dormant or tampered malicious Skills. |
   |Scan frequency |You can specify **Once per hour** or **Once per day**. If you select **Once per day**, you must set **Detection time**. The time is based on the server time zone displayed on the page. SealSuite starts one scan within the allowed time period. After the task starts, the end time is not limited by this time period. If an endpoint remains offline or cannot be scanned during the entire time period, such as when it is powered off, the system automatically skips the scan task for that day. |

   **Remediation method**

   |Configuration item |Description |
   |---|---|
   |Log audit |Reports audit logs for malicious Skills. Enabled by default and cannot be disabled. Detected risk events are centrally summarized and displayed on the **Audit Log** page in the Admin Console, helping security administrators monitor and trace risks globally. |

   **Notification**

   |Configuration item |Description |
   |---|---|
   |Endpoint notification |After this is enabled, when a malicious Skill is found on an endpoint, the client proactively displays a pop\-up notification to the user, indicating a security risk. You can click **Configure** on the right to customize multilingual pop\-up notification content. |

   **Effective scope**

   |Configuration item |Description |
   |---|---|
   |Effective scope |Defines the objects to which the current policy applies. You can select **All** or select some objects by **Employee/Device**. You can also further exclude specific employees or devices from the selected effective objects, so that they are not affected by this policy. |

## Manage detection policies

After creating a detection policy, administrators can view the policy delivery and effective status, and adjust the priority, effective scope, or enabled status as needed. To maintain existing policies, perform the following steps.

1. Log in to the Admin Console.

2. In the left navigation pane, choose **AI Security** \> **Supply Chain Security** \> **Skill Security Detection**.

3. On the **Policy Management** page, administrators can perform the following management operations:

   * **Running status monitoring**: Use the dashboard at the top of the page to view the **Number of configured policies**, **Number of effective devices**, and configuration synchronization progress. **Server configuration version** is the version identifier of the current policy configuration. It is updated after policies are added, modified, or deleted. Use **Pulled the latest configuration**, **Pulled configuration, but devices are not on the latest version**, and **Devices that did not pull the latest configuration** to check which endpoints still need synchronization. When an endpoint pulls the latest version, the detection configuration has been synchronized.

   * **Policy search**: Filter by effective status, employee or department, device, policy name, or ID, and sort by edit time.

   * **Daily O&M**: In the policy list, administrators can preview the core parameters of each policy and perform the following operations:

      * **Status switching**: Use the switch in the **Effective status** column to enable or disable a specific policy with one click. After a policy is disabled, affected endpoints automatically match the next policy with the highest priority.

      * **View policy change information**: In the policy list, you can directly view the **Last modified by** and **Last modified at** values for each policy, and quickly trace the policy change history.

      * **View effective endpoint devices**: Click the number in the **Actually effective devices/Expected effective devices** column in the policy list to open the **Policy effective status** details page. On the details page, you can view the **Policy version update time** of endpoints. Click the **Refresh** button next to the number to proactively obtain the latest effective status data.

      * **Other operations**:

         * **Copy**: Quickly create a new rule from an existing policy as a template.

         * **Edit**: Modify policy parameters, remediation methods, or effective scope.

         * **Delete**: Permanently remove policies that are no longer needed. Deletion cannot be undone. Perform this operation only after confirming the business impact.

## View audit logs

After an endpoint detects a malicious Skill, administrators can view the risk file, matched policy, affected employee and device, and current remediation status in **Audit Log**. To troubleshoot detection results or follow up on file processing, perform the following steps.

### View path

1. Log in to the Admin Console.

2. In the left navigation pane, choose **AI Security** \> **Supply Chain Security** \> **Skill Security Detection**.

3. At the top of the page, switch to the **Audit Log** tab.

   Each row in the list displays a malicious Skill file on an endpoint. If the file on the same endpoint and in the same path is detected again or deleted, the same record is updated. You can directly view the latest status of the file.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-14.png)

### Alert list fields reference

In the alert list, you can combine filter conditions to quickly locate target threat events. You can also click **Columns** in the upper\-right corner of the list to select and adjust the information displayed in the list based on audit requirements. The core fields are described below:

|List item |Description |
|---|---|
|**Status update time** |The time when the file entity was last detected by the system or its status changed. |
|**First alert time** |The time when the file was first detected on the endpoint and an alert was reported. Compare it with the status update time to understand the time span from the first occurrence of the alert to the latest update. |
|**Skill name** |The name of the detected extension component. |
|**Skill path** |The absolute storage path of the malicious file in the endpoint system. |
|**Matched risk type** |Displays the specific risk types detected by Skill cloud lookup, such as executing high\-risk commands at runtime. If a Skill matches multiple risks, hover over the field to view all risks. |
|**Skill Hash** |The unique Hash identifier of the malicious Skill file. |
|**Scan method** |The trigger mechanism when the event was detected. The value can be **Real\-time scan** or **Periodic scan**. To check the scan frequency, view the matched detection policy. |
|**User information** |The employee name and department associated with the endpoint that triggered the alert. |
|**Device information** |The hostname, online status, and other information of the endpoint that triggered the alert. |
|**Operating system** |The operating system type and version of the alerting endpoint. |
|**Remediation status** |Displays the current remediation status of the Skill file:<br><br><br>* Pending: The risk has not been removed and the employee has not handled it.<br><br>* Deleted: The employee has deleted it locally.<br><br>* Allowlisted: The administrator or cloud lookup engine determined that it is allowlisted. |
|**Matched policy** |The name of the Skill detection policy matched when the risk was detected. |

## View alert details

Click **Details** in the **Operation** column of the alert list to open the malicious Skill details page. You can view file risks, affected devices, and remediation records.

### Event details

The **Event details** tab centrally displays the basic information, risk information, and details about the endpoint user and device that triggered the alert.

|Information category |Description |
|---|---|
|Basic information |Displays the Skill Hash, cloud lookup method (Skill Hash cloud lookup / Skill content cloud lookup), matched policy, and Skill text description. |
|Risk information |Lists all risk types and descriptions matched by the Skill. After you expand the details, **Matched code evidence** is displayed. The system highlights the specific code snippets and line numbers that match the risk with a red left border, helping administrators understand which code triggered detection. |
|User and device details |Provides detailed network and device information about the endpoint that triggered the alert, such as device IP address and SealSuite version. Click the upper\-right corner to view all alerts associated with the employee or device with one click. |
|Quick remediation |After viewing the risk information, you can directly click **Extract file** or **Add Allowlist** in the upper\-right corner of the details page to quickly remediate the malicious Skill. For details, see Process risk files and configure a allowlist. |

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-15.png)

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-16.png)

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-17.png)

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-18.png)

### Remediation records

On the **Remediation records** tab, you can view detection and remediation records for the malicious Skill by time, including the occurrence time, remediation status, and detailed description. This helps you track the handling process for risk files.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-19.png)

## Process risk files and configure a allowlist

For malicious files in the list, administrators can issue the following response commands, extract risk files, or configure allowlists for files confirmed as trusted.

### Extract files

When a suspicious unknown threat is found, or in\-depth security analysis is required for an alert, administrators can use **Extract file** to send the malicious file on the endpoint back to the Admin Console.

To extract multiple files at once, select target records in the alert list, and click **Batch extract files** below the list. After extraction, view the execution results of each task in **Endpoint Security \> Threat Response**.

> **说明**

> **administrator operation audit notice**: To meet compliance audit requirements, the system automatically records administrator actions for extracting Skill files in **administrator operation logs**.

1. Locate the **malicious Skill** file to extract, and perform one of the following operations to issue the extraction command:

   * **Extract in the alert list**: In the **Operation** column of the target alert event, click **Extract file**.

   * **Extract on the alert details page**: Click the target alert to open the details page, and click **Extract file** in the upper\-right corner.

2. After extraction is confirmed, the system automatically creates a file extraction task in **Endpoint Security** \> **Threat Response**.

   * If the target device is online, the system executes the extraction task in real time.

   * If the device is offline, the command automatically switches to a background pending state and is executed the next time the device connects to the network.

3. Go to the **Threat Response** page to view task progress. After extraction succeeds, download the file for further analysis.

> **说明**

* > Extracted files are retained in the Admin Console for only **3 days**. After expiration, they are automatically deleted and cannot be viewed or downloaded. Process them in time.

* > If the endpoint user has deleted the Skill file locally in the client, the system can no longer extract the file from the endpoint.

### Configure a Skill allowlist

Administrators can configure a allowlist to exempt trusted extension components. This prevents false positives that identify them as malicious Skills and affect normal use. Based on actual scenarios, the following two allowlisting methods are supported:

> **说明**

> Basic matching capabilities (file path and file SHA256) are supported by SealSuite client **3.3.17** and later. For endpoints earlier than this version, add exemptions through **Antivirus allowlist \> Path allowlist**. After the allowlist is delivered, endpoints must pull the configuration and complete local verification. When endpoints are online and the network is normal, the effective latency does not exceed **3 minutes**.

#### Method 1: Quickly allowlist from alert logs

This applies when you confirm that a file is a false positive while handling a known alert and need to exempt it immediately.

1. Locate the malicious Skill alert to allowlist, and perform one of the following operations to open the allowlist configuration pop\-up window:

   * **Operate in the alert list**: In the **Operation** column of the target alert event, click **Add Allowlist**.

   * **Operate on the alert details page**: Click the target alert to open the details page, and click **Add Allowlist** in the upper\-right corner.

2. On the **Add Allowlist** side panel, configure the following parameters:

   * **Operating system**: Select the system environment where the allowlist takes effect. Multiple selections are supported: **Windows**, **macOS**, and **Linux**.

   * **Allowlist configuration (file SHA256)** : The system automatically fills in the file SHA256 of the current alert. Files to exempt are matched by this value. This entry does not provide file path rules. To exempt by path, follow the steps in **Proactively define allowlist rules** below.

   * **Remarks**: Optional. We recommend entering the reason for adding the allowlist, such as "self\-developed tool exemption", for future audits.

   * **Effective scope**: Select whether the allowlist applies to **All objects** or only **Some objects** (specific employees/devices).

3. After the configuration is complete, click **OK**.

After the allowlist is added, the system no longer triggers alerts for files that match the allowlist rule. The rule is centrally maintained in **AI Security** \> **Supply Chain Security** \> **Skill Security Detection** \> **Allowlist**.

#### Method 2: Proactively define allowlist rules

This applies when you know the characteristics of compliant components, such as SHA256 or paths, and want to configure exemptions before alerts occur.

1. In the left navigation pane, choose **AI Security** \> **Supply Chain Security** \> **Skill Security Detection**.

2. Switch to the **Allowlist** tab.

3. Click  **+ Add allowlist** on the right side of the page.

4. In the dialog box that appears, complete the following configurations, and click **OK**.

   * **Operating system**: Select the system environment where the allowlist takes effect. Multiple selections are supported: **Windows**, **macOS**, and **Linux**.

   * **Allowlist configuration**: Click  **+ Add rule**. You can combine the following conditions with an AND relationship:

      * **File SHA256**: Identifies files based on the unique hash of file content. We recommend prioritizing this method to prevent path spoofing. When adding multiple SHA256 values, separate them with line breaks.

      * **File path**: Exempts files based on their absolute paths on endpoints. The path field supports the wildcard `*`, which matches any character or path segment. For example, `C:\Users\*\Documents\*` matches all files in the document directories of all users. When adding multiple paths, separate them with line breaks.

   * **Remarks**: Optional. We recommend entering the reason for adding the allowlist, such as "self\-developed tool exemption", for future audits.

   * **Effective scope**: Select whether the allowlist applies to **All objects** or only **Some objects** (specific employees/devices).

After adding a rule, you can filter rules on the **Allowlist** tab by operating system, allowlist configuration, remarks, and the most recent creator or modifier. You can also **Edit** or **Delete** rules in the Operation column. Before modification, check **Effective objects** and **Excluded objects** to confirm the employees or devices to which the rule applies.

## Handle malicious Skills in the client

When the policy takes effect and the SealSuite client detects malicious Skill files on endpoints, the client interface changes and the user remediation process are as follows:

1. **Real\-time pop\-up warning**: If **Notification** is enabled in the detection policy, the client displays a bubble notification on the user's desktop once a malicious Skill is found. The notification content is displayed based on the custom text you configured in the policy.

2. **Security status change**: On the **Security overview** page of the SealSuite client, a risk prompt for **malicious Skills** appears and displays the current number of detected malicious Skills.

3. **User self\-remediation**: Guide endpoint users to click the pop\-up notification or the malicious Skill risk prompt on the interface, enter the remediation page, and delete the malicious Skill to remove the local risk file.
