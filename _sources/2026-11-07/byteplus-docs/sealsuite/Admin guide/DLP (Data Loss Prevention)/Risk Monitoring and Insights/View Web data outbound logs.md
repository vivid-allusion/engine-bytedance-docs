---
title: "View Web data outbound logs"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/view-web-data-outbound-logs"
---

Web data outbound logs record employee actions that match Web data protection policies on websites and cloud apps. View outbound users, target applications, matched policies, and disposition results to trace sensitive text, file upload, and file download actions.

<span id="doxcnbHA4c3n393zueIVjnxO7Ad"></span>
## Log recording scope

Logs are triggered by actual actions. Creating or enabling a policy does not directly generate data outbound logs. Logs appear here only after employee actions are detected by a policy and reported.


|Trigger type |Log focus |
|---|---|
|Text outbound transfer |Which sensitive data rules were matched when an employee submitted text to a website or cloud app, and whether the action was blocked. |
|File upload |Which files an employee uploaded, and which sensitive data rules the files matched. File upload supports audit only. Logs do not indicate that the upload was intercepted. |
|File download |Which files an employee downloaded from which application. Detection is based on file size and type. Sensitive content in downloaded files is not scanned. |


When viewing records, check the action to understand the result. **Audit** means the action is recorded but not intercepted. **Block** means the matched action is intercepted.

<span id="HmWadF94BorFe6xQPP2c84fXn3F"></span>
## Log usage notes


* To view records of policy creation, modification, or deletion, go to **Admin Log** in **Audit Logs**. These operations are not employee data outbound logs.

* If expected records are not found, first check the query time, user, and device conditions. Then check the policy status, effective scope, excluded objects, and target applications. For content detection, also check traffic steering, HTTPS decryption, and classification and sensitivity level rules. File upload uses asynchronous detection. Detection results and logs may appear later. If logs are not found immediately after upload, the file may still have matched rules.

* An empty sensitive data field in a file download record does not mean the downloaded file has passed sensitive content detection.


<span id="doxcnBIukHUXnPxYaBtHD5hoMTh"></span>
## Prerequisites

A Web data protection policy has been configured and enabled, and employee actions have matched the policy and reported logs. For policy configuration, see [Configure a Web data protection policy](https://docs.byteplus.com/en/docs/sealsuite/configuration-web-data-protection-policy?lang=en).

<span id="doxcnlR0hDTrUzUHNlf4Ukvrfjv"></span>
## Query logs


1. Log in to the SealSuite Admin Console.

2. Choose **DLP** \> **Investigation Audit** \> **Audit Log**.

3. Switch to the **Network DLP** tab.

4. Select **All**, **Audit**, or **Block**, and set filter conditions as needed, including **Operation time**, **User**, **Device**, and **Policy name**. Some conditions are available after you click **Expand**.


The main fields in the list are as follows. Click **Columns** to adjust the displayed fields.


|Field |Description |
|---|---|
|Trigger period |The time when the outbound action occurred. |
|User |The employee who triggered the action and the department information. |
|Action |Whether this action uses audit or block. |
|Sensitive data |The sensitive data matched in this detection. File downloads do not undergo sensitive content detection, so this field may show "\-". |
|Trigger type |Text outbound transfer, file upload, or file download. |
|Triggered policy |The name of the policy that triggered this log. |
|Application |The website or cloud app involved in this action. |


<span id="doxcnlR8TeOcE7vZATFsSUDMAnf"></span>
## View log details

In the **Actions** column of the target record, click **Details** to view information about this action.

<span id="doxcnF7B2kHjp47jO6X7IFF3aMg"></span>
### Event details

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/swg-ndlp-en-20260923/web-details-en.png) </span>


* **Alert Basic Information**: View the event ID, outbound time, report time, disposition method, matched policy, application category, accessed cloud app, trigger URL, and outbound action. Use the outbound time to locate the employee operation. Use the report time to verify when the log reached the backend.

* **Sensitive Information**: View text or file detection information by action type. Text outbound transfer focuses on matched rules. File upload focuses on file information and matched rules. File download focuses on the file name, type, and extension, and does not include sensitive content detection results.

* **User information**: Confirm information such as the employee name, department, and account status.

* **Device information**: Confirm the operating system, device IP address, device ID, and SealSuite version to locate the endpoint that triggered the action.


<span id="doxcn9fL6ZO6iGkulzHTnkzjPRd"></span>
### Original log

For further troubleshooting, switch to the **Original Log** tab to view reported records. Use the event ID, time, and trigger URL to verify the same action with relevant personnel.

In **Request Details**, switch between **Basic Info** and **More Info** to view the request time, target address, HTTP information, and network connection information. A field value of "\-" indicates that the record has no corresponding value to display.


|Field |Description |
|---|---|
|timestamp_ms (request time) |The time when the request occurred. The page displays the time with millisecond precision. |
|user (user) |The employee who initiated the request. |
|status (status code) |The HTTP response status code. Do not determine whether a policy blocked the action based only on the status code. Use the disposition method in the event details. |
|host (application host) |The target host name of the request. |
|uri (HTTP URL) |The request address and path, used to locate the specific resource. |
|method (request method) |The HTTP method, such as GET or POST. |
|level (log status) |The log status of the reported record. It is not equivalent to the policy audit or block action. |
|duration (request round\-trip time) |The request round\-trip time, in milliseconds. |
|user_agent (User Agent) |The identifier of the software, browser, or runtime environment that initiated the request. |
|sip (source IP) |The source IP address of this request record. |
|sport (source port) |The port used by the source connection. |
|size (request size) |The size of this request record, in bytes (Byte). |
|protocol (HTTP version) |The HTTP version, such as HTTP/1.1 or HTTP/2.0. |
|scheme (protocol) |The protocol, such as http or https. |
|intranet_ip (gateway intranet IP address) |Gateway\-related address field, used to troubleshoot the gateway that processed the request. |


<span id="doxcn9BOUsbT3We8B66VMWS5nOd"></span>
## Export logs

After setting filter conditions in the list, click **Export List** and follow the on\-screen instructions to export a CSV file. You can customize the selected list items during download. The complete log file contains the following fields.


|Field |Description |
|---|---|
|Alert time |The time when the alert occurred. |
|Alert ID |The identifier used to locate the same alert. |
|Outbound website link |The target website address of this action. |
|Sensitive data |The sensitive data matched in this detection. |
|Triggered policy |The policy that triggered the alert. |
|Device ID |The device identifier that triggered the action. |
|Employee ID |The employee identifier that triggered the action. |
|Triggered application |The application associated with this action. |
|Application category |The category of the triggered application. |
|Configuration type |Whether the configuration is file download, file upload, or sensitive text. |
|Sensitive level |The sensitivity level of the sensitive data matched in this detection, such as L1, L2, L3, or L4. |
|Version |The SealSuite client version. |
|Employee name |The name of the employee who triggered this action. |
|Employee email |The email address associated with the employee account that triggered this action. |
|Employee phone number |The phone number associated with the employee account that triggered this action. |
