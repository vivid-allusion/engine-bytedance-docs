---
title: "Viewing clipboard logs"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/viewing-clipboard-logs"
---

Clipboard logs provide a detailed record of sensitive data copy and paste events, enabling administrators to investigate and audit potential data leaks. This guide explains how to access these logs, interpret the data fields, analyze detailed evidence like screenshots, and manage the event lifecycle from alert to resolution.

<span id="bbbe3b75"></span>
## Prerequisites

To view clipboard logs, make sure a clipboard control policy has been configured and is in effect, and that an employee has triggered a cross\-application sensitive data copy or paste action on an endpoint that was detected and reported by the SealSuite client. For policy configuration instructions, see [Configuring clipboard control policies](https://docs.byteplus.com/docs/sealsuite/configuring-clipboard-control-policies).

<span id="f76f647f"></span>
## Procedure


1. Log in to the Admin Console.

2. In the left navigation pane, choose **DLP** \> **Investigation audit** \> **Audit log**.

3. Switch to the **Clipboard log** tab to view alert event details.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42e294111e354d7c951e41c3c4c6c367~tplv-goo7wpa0wc-image.image) </span>


<span id="046f4ca8"></span>
## Log list fields

The log list displays the following core fields by default, helping administrators quickly understand event overviews and locate high\-risk behaviors. You can use the filter options at the top of the page for queries with multiple conditions.


|**Field** |**Description** |
|---|---|
|**Send time** |The specific time when the clipboard control policy was triggered. |
|**Control action** |The final action the system took for this behavior (**Allow** / **Block**). Administrators can filter for "Block" logs first to verify the accuracy of blocking rules and assess the employee's intent. |
|**Data Governance Type** |The specific operation type of the event (**Copy** / **Paste**). |
|**External files** |If **File archiving** is enabled in the policy configuration, the system materializes the content actually copied or pasted by the endpoint user and automatically generates a `.txt` file. The file content consists of either the text from the user’s clipboard or the text extracted from images through OCR. Hover over this area to **preview**, **download**, or **copy** the filename. |
|**Sensitive data hit** |The specific sensitive data rules and their classification levels that were matched by this clipboard action. |
|**Source channel** |The source application or target channel that triggered the behavior. |
|**User** |The name of the employee who performed the action. Hover over the name to quickly view additional background information such as department, title, and contact details. |
|**Triggered policy** |The specific **clipboard control policy** name that caused this behavior to be recorded or blocked. Click the policy name to go directly to the policy, allowing administrators to quickly fine\-tune it when false negatives or false positives are identified. |
|**Disposal status** |The processing status of this log entry in the Admin Console (**Pending**, **In progress**, or **Resolved**). |
|**Action** |Click **Details** in the Action column to view more event details and perform follow\-up audit actions. |


Click **Export List** in the upper\-right corner of the list to export the alert information in the current list to your local device.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Administrator operation audit note</strong>: To meet compliance audit requirements, the system automatically records the administrator’s action of exporting clipboard logs in the <strong>Admin Log</strong>.</div>


<span id="4e8ea8b4"></span>
## View log details

Click **Details** in the Action column to open the event details dialog for in\-depth analysis. The details page consolidates all data related to the event, from the triggering behavior to the endpoint's status, including:


* **Outbound information**

   Records the core elements of the violation, including event ID, outbound time, reporting time, outbound channel (source/target), and control action (Allow/Block).

   If the policy has **Screenshot evidence** enabled, administrators can click the eye icon here to view a full\-screen screenshot captured at the moment of the violation, helping assess the employee's intent.

* **File information**

   If the policy has File archiving enabled, this section displays the file's basic attributes (filename, size, hash value, and so on).

   Click **View details** next to **Matched classification rules** to open a details dialog showing the specific matches of the predefined rules. If [File content snippet reporting configuration](https://docs.byteplus.com/docs/sealsuite/configuring-system-settings-for-file-egress-control-policies#ecf2276c) is enabled in System Configuration, you can view the matched sensitive words and their context snippets directly in the **Snippet preview** tab.

* **File activity timeline**

   This section traces the lifecycle of the content on the endpoint through a chronological timeline.

* **User information** and **Device information**

   This section provides background profiles of the violating subject. User information includes the employee's name, department, and email. Device information shows the risk endpoint's operating system, IP address, SealSuite version, and so on.

   Use the **All alerts for this user** and **All alerts for this device** shortcut buttons in the upper\-right corner of each section to quickly review the user's or device's historical compliance record, helping determine whether the current violation is an isolated incident or persistent malicious behavior.


<span id="a8c6c68e"></span>
### Event handling and closure

If, after analysis, you determine that the alert's current risk status does not match expectations, you can manually update the risk status.


1. In the upper\-right corner of the details page, click **Mark**.

2. In the Mark log dialog, update the status based on your analysis.

3. Click **Confirm** to close the audit loop.


<span id="69c1d734"></span>
## Log export

SealSuite supports exporting logs to a Syslog or Elasticsearch service for storage. For detailed log export instructions and format specifications, see [Log Export and Auditing](https://docs.byteplus.com/docs/sealsuite/docs-zk9yxy9szc).
