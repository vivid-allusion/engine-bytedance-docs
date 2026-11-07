---
title: "Monitoring and remediating malicious Skills"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/monitoring-and-remediating-malicious-skills"
---

Malicious code or sensitive content in a Skill used on an Endpoint can expose the enterprise to security risk.

Once the **Skill Security Detection** policy is enabled, SealSuite generates an alert whenever it detects a malicious Skill file on an Endpoint. Administrators can monitor enterprise\-wide exposure on the **Malicious Skill** page, review matched evidence on the alert details page, and respond quickly through actions such as file extraction and whitelist configuration.

This document explains how to view malicious Skill alerts in the Admin Console and how to respond by extracting files or adding whitelist.

 &nbsp;

<span id="view-skill-alerts"></span>
## View Skill alerts

 &nbsp;

<span id="procedure"></span>
### Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, go to **AI Security** \> **Security Protection** \> **Skill Security Detection**.

3. At the top of the page, switch to the **Malicious Skill** tab.

   On this page, each row of data represents an independent malicious Skill file entity detected on an endpoint. Multiple detection or deletion actions for the same file under the same path are automatically merged to update its status. This allows administrators to see the final status of the file in a single list item.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/298227e2bc814e458446ffe8b976af5c~tplv-goo7wpa0wc-topic.webp) </span>


 &nbsp;

<span id="alert-list-fields-reference"></span>
### Alert list fields reference

In the alert list, you can use various filter conditions in combination to quickly locate target threat events. You can also click **Custom Columns** in the upper right corner of the list to select and adjust the displayed information based on your audit needs. The core fields are described below:

&nbsp;


|Field |Description |
|---|---|
|**Updated at** |The time when the file entity was most recently detected by the system or its status changed. |
|**First Alert Time** |The time when the file was first discovered by the system on the endpoint. Compare it with the last alarm time to determine the threat's dwell time. |
|**Skill name** |The name of the detected extension component. |
|**Skill path** |The absolute storage path of the malicious file on the endpoint. |
|**Hit Risk Type** |Displays the specific risk types detected through Skill cloud scan (e.g., Prompt injection detected in skill.md). If a Skill hits multiple risks, hover over it to view all. |
|**Skill Hash** |The unique Hash identifier of the malicious Skill file. |
|**Scan Mode** |The trigger mechanism when the event was detected (real\-time scan, scheduled scanning, or manual scan). |
|**User information** |The employee name and department associated with the endpoint that triggered the alert. |
|**Device information** |The hostname, online status, and other details of the endpoint that triggered the alert. |
|**OS** |The operating system type and version of the alert endpoint. |
|**Status** |Displays the current remediation status of the malicious file:<br><br><br>* **Pending**: The risk has not been eliminated and the employee has not disposed of it.<br><br>* **Allowed**: Administrators or the cloud scan engine have determined it as an allowlist item.<br><br>* **Deleted**: The user has deleted it locally. |
|**Triggered policy** |The name of the Skill detection policy that detected the risk. |


 &nbsp;

<span id="查看告警详情"></span>
## View Alert Details

Click **Details** in the **Operation** column of the alert list to enter the malicious Skill details page, where you can obtain deeper risk evidence and traceback information.

<span id="事件详情"></span>
### Event Details

The **Event Details** tab centrally displays the basic information, risk information of the Skill, as well as the details of the end user and device triggering the alert.


* **General**

   Displays the Skill Hash, cloud scan mode, triggered policy, and text description of the Skill.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1667d78b3f54fbe8236f5079c4e3fe1~tplv-goo7wpa0wc-topic.webp) </span>

* **Risk Information**

   Details all risk types and descriptions hit by the Skill. After expanding the details, the **Matching** **Evidence** will be visually displayed. The system will highlight the specific code snippets and line numbers hitting the risk with a red left border to assist security personnel in quick qualitative analysis.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66862712a129494fac701da76f86b58a~tplv-goo7wpa0wc-topic.webp) </span>

* **User and Device Details**

   Provides detailed network and device information (e.g., Device IP, SealSuite version) of the terminal triggering the alert. Supports clicking the upper right corner to view all alerts associated with the employee or device with one click.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03beded9bd3e4ff68cf19da46380a011~tplv-goo7wpa0wc-topic.webp) </span>

* **Quick Disposal**

   After researching the risk information, you can directly click the **Extract File** or **Add Allowlist** button in the upper right corner of the details page to quickly dispose of the malicious Skill. For specific operations, please refer to [Alert remediation and analysis](https://docs.byteplus.com/en/docs/31/101264#alert-remediation-and-analysis).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a32c63160bd4178b4096f4942bb4a41~tplv-goo7wpa0wc-topic.webp) </span>


<span id="处置记录"></span>
### Remediation Logs

Under the **Remediation Logs** tab, the full lifecycle flow trajectory of the malicious Skill from the first alert to final disposal is recorded. Timeline nodes include occurrence time, status change, and specific change instructions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae100fbd16d744589b478e3c8840b115~tplv-goo7wpa0wc-topic.webp) </span>

 &nbsp;

<span id="alert-remediation-and-analysis"></span>
## Alert remediation and analysis

For malicious files in the list, administrators can issue the following response commands to complete event research and evidence collection or policy correction.

 &nbsp;

<span id="extract-files"></span>
### Extract files

If you discover a suspicious unknown threat or need to conduct an in\-depth security analysis, you can use the **Extract file** feature to retrieve the malicious file from the endpoint to the Admin Console.


1. Locate the **Malicious Skill** file to be extracted and perform any of the following operations to issue the extraction command:

   * **Extract in the alert list**: In the **Operation** column of the target alert event, click **Extract File**.

   * **Extract on the alert details page**: Click the target alert to enter the details page, and click **Extract File** in the upper right corner.

2. When you confirm the extraction, the system automatically generates a file extraction task in **Endpoint Security** \> **Threat Response**.

   * If the target device is currently online, the system executes the extraction task in real time.

   * If the device is offline, the task is suspended in the background and will execute automatically the next time the device connects to the network.

3. Go to the **Threat Response** page to monitor the task progress. Once the extraction is successful, you can download the file for further analysis.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The Admin Console retains extracted files for only <strong>3 days</strong>. After this period, they are automatically deleted and can no longer be downloaded. Please analyze them promptly.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the endpoint user has already deleted the Skill file locally on the client, the system cannot extract the file from the endpoint.   </div>
   


 &nbsp;

<span id="configure-skill-allowlist"></span>
### Configure Skill allowlist

Administrators can configure an allowlist to exempt trusted extension components, preventing them from being falsely reported as malicious Skills and affecting normal use. Based on actual scenarios, the following two allowlist methods are supported:

 &nbsp;

<span id="method-1:-quick-allowlist-from-alert-events"></span>
#### Method 1: Quick allowlist from alert events

Use this method when processing a known alert and confirming that the flagged file is a false positive that requires immediate exemption.


1. Locate the malicious Skill alert to be allowlisted, and perform any of the following operations to open the allowlist configuration pop\-up:

   * **Operate in the alert list**: In the **Operation** column of the target alert event, click **Add Allowlist**.

   * **Operate on the alert details page**: Click the target alert to enter the details page, and click **Add Allowlist** in the upper right corner.

2. In the **Add allowlist** panel, configure the following parameters:

   * **OS**: Select the system environment (Windows / macOS / Linux) where the allowlist applies.

   * **Allowlist settings (File path)** : The system automatically fills in the file path of the current alert. You can also modify it as needed. The path field supports the wildcard `*`. For example, `C:\Users\*\Documents\*` matches all files under all user document directories.

   * **Remarks**: Optional. We recommend entering the reason for adding the allowlist (such as "Exemption for self\-developed tools") to facilitate future auditing.

   * **Scope**: Select whether the allowlist applies to **All objects** or **Partial objects** (specific users or devices).

3. Click **Confirm**.


Once added, the system stops triggering alerts for files that match this rule. You can manage this rule centrally in **AI Security** \> **Security Protection** \> **Skill Security Detection**\> **Skill Whitelist**.

 &nbsp;

<span id="method-2:-manually-define-an-allowlist-rule"></span>
#### Method 2: Manually define an allowlist rule

Use this method when the characteristics of known compliant components (such as SHA256 or file path) are already known and you want to configure an exemption before any alert is triggered.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported on SealSuite client version <strong>3.3.17 and later</strong>.</div>



1. In the left navigation pane, go to **AI Security** \> **Security Protection** \> **Skill Security Detection**.

2. Switch to the **Skill Whitelist** tab.

3. Click  **+ Add Allowlist** on the right side of the page.

4. In the dialog box that appears, complete the following configuration and click **Confirm**:

   * **OS**: Select the operating system where this allowlist rule takes effect (Windows, macOS, or Linux).

   * **Allowlist settings**: Click  **+ Add rule**. You can combine the following conditions ("AND" logic):

      * **File SHA256**: Identifies files based on their unique content hash. This method is recommended as the preferred option to prevent path spoofing.

      * **File path**: Exempts files based on their absolute path on the endpoint.

   * **Remarks** (optional): We recommend entering the reason for adding the allowlist (for example, "In\-house tool exemption") for future audit purposes.

   * **Scope**: Select whether this allowlist applies to **All objects** or **Partial objects** (specific users or devices).
