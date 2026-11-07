---
title: "Malicious File Monitoring and Handling"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/malicious-file-monitoring-and-handling"
---

In the SealSuite endpoint security system, local antivirus engines, cloud scanning, and EDR threat intelligence correlation are used to comprehensively monitor malicious file risks on endpoints. Administrators can use the unified malicious file workbench to monitor, handle, and perform full\-lifecycle trace analysis on virus files across the enterprise in real time.

<span id="7cc5b387"></span>
## Prerequisites

A [virus detection policy ](https://docs.byteplus.com/en/docs/sealsuite/docs-policy-configuration)or EDR behavior collection policy has been configured and has taken effect, and virus files have been detected on employee endpoint devices within the effective scope of the policy.

This document covers operation guides for both the "Antivirus" and "Endpoint Detection and Response (EDR)" modules. When reading this document, refer to the feature modules actually purchased by your enterprise. Unless a feature is explicitly marked as exclusive to a specific module, the remaining operations and UI descriptions apply to both modules by default.

<span id="8c1c8dfd"></span>
## View Enterprise\-Wide Virus Status

Log in to the SealSuite Admin Console and go to **Endpoint Security** \> **Threat Alerts** \> **Malicious Files**. The system aggregates discrete detection events into **file entities**. Multiple detection records for the same file under the same path are automatically merged, so administrators can view the current final handling status of the file through a single list item.

<span id="146e06bc"></span>
### Multidimensional Filtering and Risk Location

Administrators can use a wide range of filtering tools to assess the security health status of enterprise endpoints from different dimensions:


* **Granular attribute filtering**: Supports combined filtering by **Virus type**, **Status**, **File Path**, **Threat level** (High risk, Medium risk, Low risk), and other dimensions, helping administrators prioritize high\-threat detections.

* **Locate by user and device**: Use **User** and **Device** search to quickly locate specific users with concentrated risks or high\-risk endpoints.

* **View global device status**: Click **Check device virus status** in the upper\-right corner of the page to go to Endpoint **Assets \> Security Posture** and enter a device\-based management view. From there, administrators can centrally view the virus detection overview and the status of enabled protection capabilities of endpoints across the enterprise.


<span id="f554f9c7"></span>
### Virus Scan List Field Description

Administrators can click the **Columns** icon on the right side of the list, and select and arrange the following fields based on audit requirements:


|List Item |Description |
|---|---|
|**Latest alert time** |The time when the file entity was most recently detected or when its status last changed. |
|**Earliest alert time** |The time when the file entity was first discovered on the endpoint by the system. By comparing \*\*Earliest alert time \*\*with **Latest alert time**, administrators can identify how long the virus has remained on the endpoint and whether it has repeatedly reappeared. |
|**Virus file information** |The malicious file entity uniquely defined by the system based on **device + file path + file hash**. Hover over the field to view detailed information about the virus file. |
|**File path** |The absolute storage path of the malicious file in the endpoint system. |
|**Status** |Displays the current handling result of the virus file.<br><br><br>* **Not isolated (red)** : The risk has not been eliminated. This includes scenarios such as an initial detection that has not been handled, manual restoration from isolation without adding the file to the whitelist, or trust being canceled.<br><br>* **Isolated / Disinfected / Deleted / Trusted (green)** : The file has been safely handled or confirmed as a trusted object. |
|**User information** |The employee name and department information associated with the endpoint that triggered the alert. Hover over the field to view more detailed onboarding information and account status. |
|**Device information** |The hostname, real\-time online status, and unique device ID (DID) of the endpoint that triggered the alert. |
|**OS** |The operating system type and specific version of the endpoint that triggered the alert, such as Windows 11 or macOS 14. |
|**Data source** |Identifies the technical source that discovered the threat. The visibility of different data sources depends on the enabled feature modules.<br><br>If the **Antivirus** module is enabled, the visible data sources include:<br><br><br>* **Local Advanced Engine / Cloud Scan Engine**: Detected by the virus scan engine.<br><br>* **Custom Blacklist**: Matches a blacklist file manually configured by the administrator in the antivirus policy, such as a specific process name or SHA1 value.<br><br>* **File Intelligence Library**: Detected by comparing the file against the cloud file intelligence database through the virus scan engine. This depends on the related intelligence subscriptions enabled in the File Intelligence Library, such as phishing software, ransomware, and other advanced threat intelligence.<br><br><br>If the **Endpoint Detection and Response (EDR)**  module is enabled, the visible data source is:<br><br><br>* **Threat Intelligence**: Detected when the EDR module collects endpoint behavior logs, such as file creation and execution logs, extracts file hashes at the same time, and compares them with the cloud threat intelligence database in real time. Static malicious file alerts generated based on EDR data are aggregated into the current list, allowing administrators to centrally perform file handling operations such as file isolation and deletion. |
|**Triggered policy** |Whether the current virus event triggers an endpoint antivirus policy. If a policy is hit, the policy name is displayed. |


<span id="717f5313"></span>
## Handle Malicious Files

Administrators can issue handling instructions for one or more malicious files based on the threat nature, to block risks or fix false positives.


1. Log in to the SealSuite Admin Console and go to **Endpoint Security** \> **Threat Alerts** \> **Malicious Files** \> **Virus Killing**

2. Select the handling objects:

   * **Single handling**: In the **Action** column of the target file row, click **Actions**.

   * **Batch handling**: Select one or more checkboxes on the left side of the list, and then click **Batch disposition** in the lower\-left corner of the list.

3. In the pop\-up window, select the required response action based on the assessment result.

   
   |**Handling Action** |**Applicable Scenario** |**Logic Description** |
   |---|---|---|
   |**Quarantine file** |Confirmed or high\-risk malicious files. |Forcefully stops the file from running and moves it to the system isolation area to prevent risk spread. |
   |**Restore Quarantine file** |Quarantined files that need to be restored due to false positive remediation or confirmed safety. |Restores the file from the isolation area to its original storage path. |
   |**Trusted file** |Clearly safe business files or known whitelist files. |Adds the file to the trust list. The system will no longer generate alerts or automatically handle the file. |
   |**Untrust file** |Trusted files whose risks need to be reassessed. |Removes the file from the trust list and restores normal system detection and prevention capabilities for the file. |
   |**Delete file** |Malicious samples that have been confirmed as unnecessary to retain and need to be completely removed. |Physically deletes the file entity from the endpoint disk. This operation cannot be undone. |
   

4. Confirm the execution logic for batch handling:

   * **Intelligent validation**: The system automatically compares the current status of files. If the selected objects include files for which the same action has already been performed, the system automatically skips them and only issues instructions to valid objects.

   * **Verify the quantity**: Before clicking **Confirm**, carefully verify the actual number of files to be processed as prompted in the pop\-up window.

5. Click **Confirm**. The system immediately issues the corresponding security task to the target endpoints. You can then go to the "Malicious File Actions Timeline" on the **Details** page to view the execution result.


<span id="5c7d426d"></span>
## Trace the File Lifecycle

Click **Details** in the list to enter the in\-depth analysis page for the virus file. This page integrates file attributes, risk background, and handling traces into a unified view, helping administrators accurately assess the file.


* **Risk Feature Overview**

   The top of the page displays the identity information and current threat level of the malicious file:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75c1cde59e0b4000ac7c224706907413~tplv-goo7wpa0wc-image.image) </span>

   * **Basic Information**: View the file name, threat level, handling status, file path, size, hash information, digital signature, and other core attributes.

   * **Quick Actions**:

      * **Actions**: Click to directly issue instructions such as quarantine, trust, or delete.

      * **Extract file**: Obtain a virus sample. If the target device is currently online, the system executes the extraction task in real time. If the device is offline, the instruction is automatically converted into a background response task and executed after the device comes online again. You can go to the **Threat Response** page to view the task execution status and download the extracted file. For details, see [Managing threat response tasks](https://docs.byteplus.com/docs/sealsuite/managing-threat-response-tasks).

* **Associated Environment Audit**

   The system automatically associates the affected user and device context to help administrators assess the impact scope and targeting of the threat.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3094b97689e403bac0ab28eee4b8a8e~tplv-goo7wpa0wc-image.image) </span>

   * **User Details**: View the associated employee's department, name, hire date, and account status. Click **Check all alerts for the employee** to trace all historical virus infection records across devices under this employee.

   * **Device Details**: View the target endpoint's IP address, operating system version, and DID. Click **Check all alerts for the device** to go to the scan list filtered by this device.

* **Malicious File Actions Timeline**

   The **Malicious File Actions Timeline** at the bottom of the page fully records the execution history of the virus file from its first detection to each handling action. Each timeline record includes the operation time, file status change result, and the corresponding trigger source. Administrators can use this timeline to trace the threat discovery path and track the delivery progress and feedback results of manual instructions in real time, ensuring that risk handling is fully closed\-loop.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1cb62b70f53a413096838883d5c9b389~tplv-goo7wpa0wc-image.image) </span>


<span id="b7c7683d"></span>
## View System Defense Logs

If **Suspicious powershell script execution detection** has been configured and enabled in the virus detection policy, and suspicious PowerShell events have been detected on employee endpoint devices within the effective scope of the policy, system defense logs will be generated. Currently, many cryptomining viruses and ransomware use Windows PowerShell scripts to achieve long\-term persistence in the system without writing malicious code to disk, and continuously launch attacks. You are advised to closely monitor system defense logs.


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Endpoint Security** \> **Threat Alerts** \> **Malicious Files**.

3. Click the **System Defense** tab. You can view system defense events detected by SealSuite on endpoint devices. Click **Columns** in the upper\-right corner of the list to customize the displayed columns and their display order. The key event information is described in the following table.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31545c97d92c458d858d513449d54a93~tplv-goo7wpa0wc-image.image) </span>

   
   |**Information Item** |**Description** |
   |---|---|
   |**Triggered time** |The time when the endpoint device generated the virus event alert, accurate to the second. |
   |**Employee** |The name and department of the endpoint device user. Hover over the employee name to view detailed user information. |
   |**Device information** |The name and DID of the endpoint device. Hover over the device information to view detailed device information. |
   |**Threat description** |The threat description, including **suspicious powershell command execution** or **suspicious powershell script execution**. |
   |**Command line arguments** |The arguments of the suspicious PowerShell command line. Hover over the command line to view detailed command line arguments. |
   |**Target information** |Information about the suspicious PowerShell script, including file size, file path, file MD5, and file SHA1. |
   |**Action** |Displays the system defense action configured in the antivirus policy, including **Loose**, **Moderate**, and **Strict**. |
   |**Client side results** |The handling result of the PowerShell command or script on the client based on the system defense action.<br><br><br>* **Intercept**: When the action is **Strict** or **Moderate**, the default result is "Intercept".<br><br>* **User active release**: When the action is **Moderate**, if the user chooses to **continue execution**, the result is "User active release".<br><br>* **Default release**: When the action is \*\*\*\* **Loose**, the default result is "Default release". |
   |**Triggered policy** |Indicates whether the current virus event triggered an endpoint antivirus policy. If a policy is triggered, the policy name is displayed. |
   |**OS** |The operating system and version number running on the endpoint device. The supported operating system is Windows. |
   |**Action** |Click **Parameter whitening** in the **Action** column to add the PowerShell command to the whitelist.<br><br>You can go to **Strategy Center** \> **Whitelist** \> **PowerShell Run Parameters Whitelist** to view, edit, or delete command line arguments that have been added to the whitelist. |
   

4. (Optional) In the upper\-right corner of the list, click **Export List** to export a .csv file containing the current list data.
