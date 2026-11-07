---
title: "Managing threat response tasks"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-threat-response-tasks"
---

**Threat Response** serves as the centralized command and task management hub for the SealSuite Endpoint Security system. It integrates remediation requirements from multiple modules—including Endpoint Management, Antivirus, and Endpoint Detection and Response (EDR)—providing administrators with a unified workbench to distribute response tasks, track progress, and audit results.

<span id="0352885c"></span>
## Prerequisites

You must have an active license for either **Endpoint Antivirus** or **Endpoint Detection and Response (EDR)** .

This document provides operational guidance for both modules. Please refer to the specific features available based on your enterprise's purchased licenses. Unless otherwise specified as module\-exclusive, all operations and interface descriptions apply to both modules by default.

<span id="1e924273"></span>
## Understanding feature associations and task sources

As the underlying execution engine, Threat Response processes instructions from various security modules to enable a "centralized analysis, unified execution" closed\-loop workflow.


|Task Source Module |Trigger Scenario |Associated Response Action |
|---|---|---|
|**Endpoint Detection and Response (EDR)**  |Remediate detected attack items from the **Threat Alerts** \> **Threat Behavior** details page. |Terminate process, isolate file, delete scheduled task, delete registry entry, disable service. |
|* **Endpoint Antivirus**<br><br>* **Endpoint Detection and Response (EDR)** <br><br>* **Agent Security** |Remediate physical malicious files from the **Threat Alerts** \> **Malicious Files** page or the **AI Security** \> **Security Protection** \> **Skill Security Detection** \> **Malicious Skill** page. |Isolate file, restore file, extract file. |
|**Endpoint Management**<br><br>(Supported in future versions) |Perform O&M operations on specific devices from the **Endpoint Details** page. |Extract file, isolate/restore endpoint network access. |
|**Threat Response** |Create and issue tasks manually from the **Threat Response** page. |Supports all task types listed above. |


<span id="6f906e7b"></span>
## Notes


* **High\-risk operation warning**: Actions such as **Delete scheduled task** and **Delete registry startup entry** are irreversible. Always verify the malicious nature of a target entity before issuing these commands to prevent disrupting critical system functions.

* **Audit compliance**: To meet cybersecurity standards such as MLPS Level 3, Threat Response retains all task execution records for **180 days**.


<span id="46dd11f9"></span>
## Manually issue response tasks

In addition to automated triggers from security modules, administrators can manually create and distribute tasks.


1. Log in to the SealSuite Admin Console.

2. Navigate to **Endpoint Security** \> **Threat Response**.

3. Click **Issue Task** in the upper\-right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e45257fb91d4ddcab466f018347da07~tplv-goo7wpa0wc-image.image) </span>

4. Configure the following task parameters:

   * **Task Configuration**: Select a **Task Type** and provide the required parameters.

      
      |Task Type |Applicable OS |Required Parameters |Issuance Timeout (Cloud Window) |Execution Timeout (Endpoint Window) |Remarks |
      |---|---|---|---|---|---|
      |**File Extraction** |Windows, macOS |* **File path**: Up to 10 paths; cumulative size limit: 180 MB. Supports absolute paths, environment variables, and wildcards. See [Appendix](https://docs.byteplus.com/docs/sealsuite/managing-threat-response-tasks#c06d1443).<br><br>* **Encryption password**: Custom password for the compressed package. |3 days |60 minutes |Extracted files are retained on the server for **3 days** before automatic deletion. |
      |**Quarantine / Uquarantine File** |Windows, macOS |**File path**: Supports absolute paths, environment variables, and wildcards. See [Appendix](https://docs.byteplus.com/docs/sealsuite/managing-threat-response-tasks#c06d1443). |15 days |30 minutes |Supports multiple paths. Max isolation depth: 30 levels; max file count: 300. |
      |**End Process** |Windows, macOS |* **Process path** (Required): Executable full path.<br><br>* **Process PID** (Optional): Recommended for targeting specific process instances. |15 days |30 minutes |/ |
      |**Disable / Enable Service** |Windows |**Service name**: Internal system name (e.g., `WSearch`). |15 days |30 minutes |/ |
      |**Delete Scheduled Task** |Windows |**Full task path**: Includes directory and task name. |15 days |30 minutes |**Irreversible**: Permanently removes the task configuration. |
      |**Delete Registry Startup Item** |Windows |**Value Name**: The specific registry value name. |15 days |30 minutes |**Irreversible**: Cleans up auto\-start entries. |
      

   * **Scope**: Select the scope by **User** (department, role, or individual) or **Device** (group or specific ID). Use **Exclude Object** to refine the scope if necessary.

5. Click **Confirm**. The endpoint client will pull and execute the task within 1 minute. If a task remains "Pending," check the endpoint's network connectivity and client status.


<span id="53eabe85"></span>
## Monitor and manage task status

Administrators can track task delivery and results in real\-time from the Threat Response list.

<span id="0fd2106e"></span>
### Understand task statuses

Track progress through overall task status and individual endpoint subtask status.


* **Task Status**

   View general progress on the Threat Response list page.

   
   |Task Status |Meaning |Description |
   |---|---|---|
   |**Pending** |Awaiting retrieval |Task generated; waiting for the endpoint to pull it during the next heartbeat cycle. |
   |**Executing** |In progress |At least one endpoint has received and started processing the command. |
   |**Completed** |Finished |All endpoint subtasks have concluded. Check **Details** for specific success/failure results. |
   |**Cancelled** |Withdrawn |Administrator manually cancelled the task while it was still pending. |
   

* **Subtask Status**

   Click **Details** to view the status for each target endpoint.

   
   |Remediation Status |Meaning |Description |
   |---|---|---|
   |**Pending** |Awaiting retrieval |Task generated; waiting for the endpoint to connect and pull the instruction. |
   |**Executing** |In progress |Endpoint received the command; results have not yet been reported. |
   |**Completed** |Success |Endpoint successfully performed the action (e.g., isolated file, terminated process). |
   |**Failed** |Error |Execution failed due to missing files, insufficient permissions, etc. |
   |**Issuance Timeout** |Cloud timeout |Endpoint failed to connect and pull the task within 15 days (3 days for file extraction). |
   |**Timed Out** |Feedback timeout |Endpoint received the task but failed to report results within the time limit (30/60 minutes). |
   |**Cancelled** |Withdrawn |Administrator manually cancelled the subtask while it was still pending. |
   


<span id="5c6fe236"></span>
### Manage task operations

Perform follow\-up actions from the details page based on task feedback.


* **Retry failed tasks**: Available for subtasks marked "Failed" or "Timed Out."

   * **Single retry**: Click **Retry** in the **Action** column.

   * **Batch retry**: Click **Retry All** at the top of the list.

* **Cancel issuance**: Available for tasks marked "Pending" to intercept commands before they reach endpoints.

   * **Single cancel**: Click **Cancel Issuance** in the **Action** column.

   * **Batch cancel**: Click **More Actions** \> **Cancel All**.

* **Download files**: For "File Extraction" tasks marked "Completed."

   * **Isolated files**: Extracted from the `infected` folder. Extraction password is `infected`.

   * **Standard files**: Uses the custom password set during task issuance.

   * **Note**: Files are only available for **3 days**. Please download them promptly.


<span id="c06d1443"></span>
## Appendix

<span id="1b8a1920"></span>
### Path expression support

When configuring **File Extraction** or **Isolate File** tasks, use environment variables and wildcards to match dynamic directories or naming patterns.

**1. Supported environment variables**

Variables must be combined with a path or wildcard (e.g., `%TEMP%\*.log`). Entering a standalone variable (e.g., `%TEMP%`) is not supported.


* **Windows**:

   * `%USERPROFILE%`: User home directory (e.g., `C:\Users\Alice`).

   * `%USERNAME%`: Logged\-in username.

   * `%PROGRAMDATA%`: Shared application data directory.

   * `%TEMP%` or `%TMP%`: Temporary file directory.

   * `%HOMEDRIVE%`: Home directory drive letter (usually `C:`).

   * `%system32%`: System core directory.

   * `%syswow64%`: 64\-bit system's 32\-bit compatibility directory.

* **macOS**:

   * `$HOME`: User home directory.


**2. Supported wildcards**

Wildcards cannot be used as the first character of a path.


* `*` (Asterisk): Matches any string of any length. Example: `C:\Downloads\*` matches all files in the directory.

* `?` (Question mark): Matches any single character. Example: `app?.exe` matches `app1.exe` but not `app12.exe`.


**3. Configuration examples**


* ✅ **Valid (Windows)** : `%TEMP%\sys_update_*.exe` (Matches all matching executables in the Temp folder).

* ✅ **Valid (macOS)** : `$HOME/Downloads/malware_?.dmg` (Matches single\-character variants like `malware_1.dmg`).

* ❌ **Invalid**: `%TEMP%` (Missing specific path).

* ❌ **Invalid**: `*\sys_update.exe` (Wildcard at the beginning).
