---
title: "Configuring EDR behavior collection policy"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-edr-behavior-collection-policy"
---

The effectiveness of Endpoint Detection and Response (EDR) depends on continuous monitoring of endpoint behavior data. **The log collection policy** is used to define the types of behavior events that the SealSuite client collects and reports, such as process startup, network connections, and file operations. By configuring this policy, administrators can define the scope and depth of data collection, providing the necessary data support for risk identification, security auditing, and event tracing.

## Prerequisites

1. The log collection policy is an exclusive capability of the **EDR** module. Ensure that you have purchased the license for **Endpoint Security** \> **EDR**.

2. The SealSuite client of version **3.3.16** or later has been installed on user desktop endpoints.

## Feature Purpose

* **Define the data collection scope**: Specify the types of behavior events that endpoints need to report based on security operations requirements, ensuring that the system can obtain key security telemetry data.

* **Adjust monitoring intensity on demand**: Provides daily and forensic collection modes, allowing quick switching between routine monitoring and emergency response scenarios to meet analysis requirements at different stages.

* **Support threat detection and antivirus capabilities**: The collected low\-level behavior logs support upper\-level security services. On the one hand, they are used to generate dynamic threat behavior alerts. On the other hand, file hashes extracted during collection are compared with the cloud intelligence database. Once malicious signatures are matched, static file alerts are directly generated in the virus detection and removal list of the "Endpoint Antivirus" module.

## Execution logic

SealSuite EDR behavior collection policies follow a  **"single policy, priority\-based"**  model. The system uses the following mechanism to ensure that each endpoint runs exactly one set of detection rules:

1. **Single active policy**

   Policies do not stack or merge. Based on priority evaluation, the system pushes only one final active policy to the target endpoint.

2. **Priority evaluation**

   * **Numeric priority**: Administrators assign a priority value to each policy. **A higher value indicates a higher priority**. When an endpoint matches multiple policies, the system enforces the one with the highest numeric priority.

   * **Time\-based tiebreaker**: If multiple matching policies have the same priority value, the system enforces the one that was **most recently modified or added** (sorted by policy update time in descending order).

## Create an EDR Behavior Collection Policy

1. Log in to the Admin Console.

2. In the left navigation pane, go to **Endpoint Security** \> **Strategy Center**.

3. On the **Strategy Center** page, switch to the **EDR Behavior Collection Config** tab.

4. Click  **+ Create Policy** in the upper\-right corner of the page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60cc22a4370743e7b9060d18aefaca93~tplv-goo7wpa0wc-topic.webp)

5. Configure the following parameters based on business requirements.

   * **General**

      |Configuration Item |Description |
      |---|---|
      |**Policy name** |Custom name used to identify the policy. It supports 1 to 100 characters. |
      |**Priority** |Sets the execution order of policies. **A larger value indicates a higher priority.**  For details, see [Execution logic](https://docs.byteplus.com/docs/sealsuite/configuring-edr-behavior-collection-policy#75372a91). |

   * **EDR endpoint behavior collection**

      Administrators can independently define collection items for different operating systems. **At least one collection item must be enabled for Windows or macOS**. After the item is enabled, you can customize the event collection scope. By default, all events are selected. You can deselect events as needed. **Process creation** is the system\-level monitoring basis and cannot be deselected. By recording the process startup path and command\-line parameters, the system can restore attack chains and identify malicious script execution.

      Details of the events supported on Windows and macOS are as follows:

      * **Windows**

         Windows collection capabilities are supported on Windows 7 and later.

         |Event Type |Specific Event |Security Monitoring Purpose |
         |---|---|---|
         |**Process behavior** |Process creation (required), Process exit, Process access, Module loading, Process injection, Remote thread creation |Monitors the complete lifecycle of programs and cross\-process operations. **Process injection** and **Remote thread creation** are key indicators for identifying "fileless attacks" and in\-memory Trojans. |
         |**File behavior** |File creation, File write, File read, File rename, File deletion, File creation time modified, Shortcut creation |Monitors read and write operations on disk data. This can be used to detect large\-scale file encryption and abnormal export of sensitive files by **ransomware**. |
         |**Network behavior** |Network access, DNS query, IP scan, Port scan |Monitors internal and external network communication of endpoints. This is used to identify **Trojan callbacks to command\-and\-control** **servers (C2)** , lateral movement scanning, port probing, and abnormal data exfiltration. |
         |**Service action** |Service creation, Service modification, Service started |Monitors changes to system services. Attackers often **maintain privileged access** by creating malicious services that automatically start at boot. |
         |**Scheduled task behavior** |Scheduled task registration, Scheduled task start, Scheduled task update, Scheduled task deletion, Scheduled task trigger |Monitors Windows Task Scheduler. This is an important dimension for detecting hidden assets, automated malicious script execution, and **persistent stealth**. |
         |**Registry behavior** |Registry key creation, Registry key deletion, Registry value modification, Registry value deletion, Registry value query |Monitors changes to the system configuration database. This is used to block attacks that modify registry startup items or hijack system components. |
         |**Account event** |Account login success/failed, Remote account login success/failed, Add/remotely add account to account group, Create/remotely create new account, Remotely modify account password/information |Monitors authentication and login behaviors to identify brute force attacks, credential leaks, unauthorized remote control, and local privilege escalation, persistent stealth, and other risk signals. |
         |**System behavior** |Driver loading |Records the loading of kernel drivers. This helps prevent attackers from obtaining high system privileges by loading malicious drivers. |
         |**Script event** |Script execution |Performs dedicated auditing for script execution behaviors such as PowerShell and VBScript. |
         |**Named pipe** |Named pipe creation, Named pipe connection |Monitors inter\-process communication channels, which are often used to detect command delivery by post\-exploitation tools such as Cobalt Strike. |
         |**Persistent event** |Registry startup item collection, Executable file startup item collection, Scheduled task startup item collection, Service startup item collection |Periodically scans auto\-start locations on endpoints to ensure continuous monitoring of existing potential persistence points. |

      * **macOS**

         |Event Type |Specific Event |Security Monitoring Purpose |Supported Operating System |
         |---|---|---|---|
         |**Process behavior** |Process creation (required), Process exit |Monitors the startup and lifecycle of macOS applications and terminal commands. |macOS 11+ |
         |**File behavior** |File creation, File read, File modification, File deletion, File rename, File extended attribute deletion, File extended attribute settings, File permission change, pkg file creation |Monitors file I/O operations. **File permission change** and **File extended attribute modification** are often used to detect privilege escalation attacks or hidden malware attributes. |macOS 11+ |
         |**Network behavior** |Network access, DNS query, IP scan, Port scan |Monitors internal and external network communication of endpoints. This is used to identify **Trojan callbacks to command\-and\-control servers (C2)** , lateral movement scanning, port probing, and abnormal data exfiltration. |macOS 11+ |
         |**Account event** |Account created, Account password changed, Account remote login, Account login |Monitors changes to system identities. **Remote login**, such as SSH, and abnormal account creation are important signals for identifying controlled endpoints. |* Account login/account remote login: macOS 13+<br><br>* Account created/account password changed: macOS 14+ |
         |**Persistence** |Background task added |Monitors background task registration under the modern macOS service management framework. This helps prevent attackers from achieving **startup persistence and long\-term stealth** by implanting hidden background tasks. |macOS 13+ |
         |**Security** |XProtect malware detected, XProtect malware remediation, User overrides Gatekeeper |Integrates data from the native macOS security framework. Records malware blocked by the system and user actions that manually bypass security protection. |* XProtect malware detected/remediation: macOS 13+<br><br>* User overrides Gatekeeper: macOS 15+ |
         |**Scheduled collection** |Login startup items, Startup items, Background task items |Periodically inventories the system startup environment. |* Login startup items/startup items: earlier than macOS 13<br><br>* Background task items: macOS 13+ |

   * **Scope**

      |Configuration Item |Description |
      |---|---|
      |Effective objects |Defines the scope to which the policy applies. You can select **All objects** or **Partial objects** by **User** or **Device**. |
      |Exclude objects |Further excludes specific employees or devices from the selected effective objects, so that they are not affected by this policy. |

6. Click **Confirm** to complete the configuration. After an administrator saves the policy configuration, the SealSuite client pulls the latest configuration from the server every 1 minute. There is usually a synchronization delay of less than 1 minute before the configuration is applied to endpoints and takes effect.

## Manage EDR behavior collection policies

On the **Strategy Center \> EDR Behavior Collection Config** list page, administrators can centrally manage all rules and adjust the monitoring scope in real time based on business changes.

* **Status monitoring**: View the number of **Devices in effect** and configuration synchronization progress through the dashboard at the top of the page. The **Server configuration version** is the global version identifier of the current EDR policy library. After an administrator edits, adds, or deletes any policy, the server configuration version is automatically updated. This version number is the only benchmark for determining policy synchronization status. If an endpoint successfully pulls the latest server version, all policy configurations matched by the endpoint have been synchronized to the latest status.

* **Search**: Supports combined filtering by effective status, user/department, device name, and policy ID.

* **Manage policies**: In the policy list, administrators can intuitively preview the core parameters of each policy and perform the following operations:

   * **Parameter preview**: Quickly view the policy **Priority** value, enabled **Detection item** categories, such as "Account Events" and "Process Behavior", and target **Scope**.

   * **Status switching**: Enable or disable a specific policy with one click through the switch in the **Status** column. After a policy is disabled, affected endpoints automatically rematch the next policy with the highest priority.

   * **View policy change information**: In the policy list, you can directly view the **Last modified by** and **Last modified time** of each policy to quickly trace its change history.

   * **View effective endpoints**: Click the number in the **Actual/Expected** column in the policy list to enter the **Policy in Effect** details page. You can view the **Policy version update time** of the endpoints. Click the **Refresh** button next to the number to proactively fetch the latest effective status data.

   * **Other operations**:

      * **Copy**: Quickly create a new rule based on an existing policy as a template.

      * **Edit**: Modify policy parameters, handling methods, or effective scope.

      * **Delete**: Permanently remove policies that are no longer needed. Deletion cannot be undone. Perform this operation only after confirming the business impact.

## Log Audit

After the policy configuration is completed, the SealSuite client collects endpoint behavior based on the scope defined in the policy. Administrators can go to the **Endpoint Security** \> **Log Investigation** page to search, trace, and analyze raw logs. For detailed instructions, see [EDR Log Investigation and Analysis](https://docs.byteplus.com/docs/sealsuite/edr-log-investigation-and-analysis).
