---
title: "Viewing file outbound alerts"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-viewing-audit-alerts"
---

When an employee endpoint performs an outbound file transfer that triggers a file transfer control policy, the SealSuite client sends an alert event to the Admin Console. You can view these alert events in file control alerts.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the DLP agent is enabled, see <a href="https://docs.byteplus.com/docs/sealsuite/viewing-and-analyzing-ai-audit-logs">Viewing and analyzing AI audit logs</a> for information about alert events identified by AI Sensitive Data Identification policies.</div>


<span id="8c0ac63f"></span>
# Prerequisite

If you need to view audit alerts, ensure that DLP policies are configured and activated. Moreover, ensure that the SealSuite client has detected outbound file transfers and uploaded the corresponding alerts. For instructions on how to configure DLP policies, please refer to [Configuring file outbound control policies](https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule).

<span id="8060f4c0"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Investigation Audit** \> **Audit Log** \> **File Sharing Log**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e51c8d825834fb7afccd45a18f995b2~tplv-goo7wpa0wc-image.image) </span>


<span id="74246413"></span>
## Filter Settings

At the top of the **Log** page, you can set filters such as **Trigger period**, **Processing status**, and **Data type** to find specific alerts. Click **Custom Filter** to select additional filters, including **Department**, **Event ID**, and **Data sensitive level**. Click **Columns** in the upper\-right corner of the list to configure which columns are displayed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d7f88ea7f834a87a056bca1728c4544~tplv-goo7wpa0wc-image.image) </span>

<span id="427ed95f"></span>
## View the Alert Event Overview

Click the icon in the upper\-right corner of the list to view an overview of the current event data, including the total number of events, risk status and processing status.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7dd556856a64b4c99d48c88af883136~tplv-goo7wpa0wc-image.image) </span>

<span id="ba77ec3a"></span>
## Export List

Click **Export List** in the upper\-right corner of the list to export the alert information in the current list to your local device.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Administrator operation audit note</strong>: To meet compliance audit requirements, the system automatically records the administrator’s action of exporting file sharing logs in the <strong>Admin Log</strong>.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0239de0bb6db4dffb3c1b7086e2fe174~tplv-goo7wpa0wc-image.image) </span>

For offline, centralized auditing that requires specific file content or screenshots of the transfer, select **Source file download link** or **Screenshot download link** in the export dialog box. This adds columns with clickable hyperlinks to the exported table, allowing you to download forensic attachments directly.


* **Permission and authentication requirements**: Only administrators with the "**View alert event details/outbound information/screenshot evidence**" or "**View alert event details/outbound information/download file**" permissions can view and select these options.

* **Link validity period setting**: When you select **Source file download link** or **Screenshot download link**, you must set a time limit for the links. The default is 6 hours, and you can customize it up to a maximum of 24 hours. This prevents sensitive source files from long\-term exposure if the offline table is leaked. Once the limit expires, the hyperlink automatically invalidates on the server, ensuring data security. We recommend setting a duration that aligns with your audit schedule.


<span id="6aed334d"></span>
## Operate on the Alert List

Administrators can quickly verify, investigate, and handle risk for one or more alert events in the list.

<span id="39c7c0e0"></span>
### Quick Actions in the Log List

Administrators can verify basic information directly in the list view:


* **Source file verification:**  If the matched policy has **File archiving** enabled, hover over the **Source file** column to preview, download, or copy the file.

* **Employee identity verification:**  Hover over the **User** column to quickly view background information such as the employee’s department, job title, and contact details.

* **Triggered policy review:**  Click the name in the **Triggered Policy** column to go to the policy configuration page and review whether the interception rules are appropriate.

* **Batch risk status:**  Select multiple alerts of the same type with obvious characteristics, such as known false positives, and click **Batch Mark** at the bottom of the list to update their risk status in bulk to **Risky**, **Risk\-free**, or **False positive**.

* **Download forensic files in batches:**  Select multiple log records that contain forensic files, then click **Download forensic files in batches** at the bottom of the list. The system packages and downloads all files associated with those logs to your local device in ZIP format, making it easier for security personnel to share and archive them.

   * **Directory structure:**  After extracting the downloaded ZIP package, the system uses the **Event ID** as the folder name, and the original forensic files are stored under their original names in the corresponding event folders, so that each file can be mapped one to one with the alert event in the management console.

   * **Skip empty files:**  If the selected logs include records without retained forensic files, the system automatically skips those records during package download.


<span id="05af3336"></span>
## View Alert Event Details

Click **Details** in the **Actions** column to view alert event details for a comprehensive investigation. The details page provides multi\-dimensional data to help administrators understand the details of the violation.

<span id="27927448"></span>
### Event Details

The event details page centrally displays complete data from alert triggering to endpoint status.


* **Alert Basic Information**

   This section records the core elements including the **Event ID**, the exact **Trigger Period**, the **Report time**, as well as the **Outgoing channel** and **Control action**.

   * Through the **Outgoing channel** field, you can identify the specific application involved in the data leak.

   * If **Screenshot** is enabled in the policy, the administrator can click the **View** to check the full\-screen screenshot captured at the moment the violation occured, helping determine the employee’s intent.

* **File Information**

   This section centrally displays the basic attributes of the outbound file, such as the file name, size, extension, and creation and modification time.

   * If \*\*File archiving \*\*is enabled in the policy, the administrator can preview or download the outbound file by clicking its name.

   * **File path** records the exact location of the file on the endpoint disk.

   * **File md5** provides a unique digital fingerprint for the file, making cross\-device tracking easier.

   * Click **View details** to the right of the matched classification and grading rule to open the details dialog and view the specific conditions that were matched by the predefined rule. If [File content snippet reporting configuration](https://docs.byteplus.com/docs/sealsuite/configuring-system-settings-for-file-egress-control-policies#ecf2276c) is enabled in the system configuration, you can directly view the matched sensitive terms and their surrounding context on the **Snippet preview** tab.

* **User Information and Device Information**

   This section provides a background profile of the user who triggered the alert. **User Information** includes the involved employee’s name, department, job title, and account status. **Device Information** displays the IP address of the risky endpoint, the operating system version, and the SealSuite client version.

   Click **Check all alerts for the user** and **Check all alerts for the device** in the upper\-right corner of the section, administrators can quickly switch views and trace the historical compliance records of the user or device, helping determine whether the current violation is an isolated incident or part of continuous malicious behavior.


<span id="06c070d4"></span>
### **File Transfer Records**

This section visually traces the file lifecycle on the endpoint from detection, creation, and download to transfer, with support for up to the 10 most recent transfer nodes. The system provides **Flow chart** and **Timing diagram**. The **Flow chart** is suitable for tracing asset relationships, while the **Timing diagram** is suitable for quickly reviewing the action timeline. Administrators can switch between them based on audit preferences.


* **Node details pop\-up:**  In the **Flow chart**, hover over any action node on the timeline to view detailed context for that node, including:

   * **Channel Address:**  The channel URL where the action occurred.

   * **File Name:**  The file name at the time of the action.

   * **File MIME:**  The standard MIME type identified at the time of the action. By comparing MIME values across nodes, administrators can determine whether the file was converted to another format, such as PDF, or disguised by renaming, where only the extension changed while the content remained the same. This helps identify attempts to evade security auditing.

   * **File Path:**  The location of the file on disk at the time of the action.

* **Supported actions:**  Supported actions include file download, creation, editing, copying, moving, renaming, and extension changes. Administrators can identify complex file transfer activities that may indicate attempts to evade detection. For detailed transfer actions and supported software, go to **DLP\> Data Identification \> File Transfer Action Library**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Not all file formats support transfer traceability.</strong> If the current file type is not supported, this tab displays “This alert cannot currently display file transfer records,” and historical transfer actions cannot be traced. To check support for specific formats, go to <strong>DLP \> Data Identification \> File Type Library</strong>.</div>


<span id="82dd2ce8"></span>
### AI Analysis Details

If the **AI Sensitive Data Identification** feature of the data security agent is enabled, an AI analysis report is generated. For details, see [Viewing and analyzing AI audit logs](https://docs.byteplus.com/docs/sealsuite/viewing-and-analyzing-ai-audit-logs).

<span id="710d8787"></span>
### Event Handling and Closure

If the current risk status of the alert event does not match the findings of the investigation, you can manually update the risk status.


1. Click **Mark** in the upper\-right corner of the page.

2. In the **Mark Log** dialog box, update the status based on the investigation result.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7527200d9397422fbbda377d78aa4bf4~tplv-goo7wpa0wc-image.image) </span>

3. Click **Confirm** to complete the audit workflow closure.


<span id="32be50b0"></span>
# Log Export

SealSuite supports forwarding logs to **Syslog** or **Elasticsearch** for storage. For detailed instructions on log forwarding and log format descriptions, see [Log Export and Auditing](https://docs.byteplus.com/docs/sealsuite/docs-zk9yxy9szc).
