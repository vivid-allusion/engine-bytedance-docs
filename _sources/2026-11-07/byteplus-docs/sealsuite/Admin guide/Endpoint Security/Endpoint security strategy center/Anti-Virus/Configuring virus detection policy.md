---
title: "Configuring virus detection policy"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-policy-configuration"
---

You can configure endpoint anti\-virus policies according to your enterprise security requirements. When configuring anti\-virus policies, you can specify information such as virus types, detection methods, virus remediation methods, the detection scope, and more. This article provides instructions on how to add, edit, copy, and delete anti\-virus policies. Additionally, this article introduces general purpose configuration for the anti\-virus function, such as setting up detection allowlists and virus scanning methods.

## Prerequisites

Virus detection policy configuration is an exclusive capability of the Endpoint **Anti\-virus** module. Ensure that you have purchased the **Anti\-virus** license under **Endpoint Security**.

## Creating a policy

1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint Security** \> **Strategy Center**.

3. On the **Virus Detection** tab, click  **+ New Policy**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e2fda24252f4216a670b5fa44590627~tplv-goo7wpa0wc-image.image)

4. On the **Add New Anti\-Virus Policy** page, complete the following configurations, and click **Confirm**.

   |Area |Configuration Item |Description |
   |---|---|---|
   |**General** |**Policy name** |Create a custom name to identify the policy. |
   ||**Priority** |The priority of the current policy, ranging **from 0 to 100**. A higher value indicates a higher priority. You can have multiple policies in effect simultaneously. When SealSuite scans an endpoint, it matches policies in descending order of priority. The matching process stops once a policy is matched. If no policies are matched, the scan stops after all policies have been evaluated. If two policies have the same priority value, the one with the most recent modification time is executed first. |
   |**Antivirus Engine** |**Local Powerful Engine** |This is SealSuite's built\-in local antivirus engine, which accurately identifies various viruses even when the device is disconnected from the internet.<br><br>This feature is enabled by default and cannot be disabled. Click **Expand** on the right to view various risk types. You can adjust the severity level (**Low, Medium, High**) for each risk type based on your enterprise's security requirements. |
   |**Detection Methods** |**Scheduled Scanning** |Detection can be scheduled on a weekly, monthly, or daily basis. When enabled, the system will perform scans according to the following settings.<br><br><br>* **Default**: Scans default system paths, such as the desktop, system directory, and downloads folder.<br><br>   * **Scan frequency**: Specify **Once a day** or **Once a week**. If you select **Once a week**, you must also specify the day of the week.<br><br>   * **Scan time**: Specify the time period for the scan, accurate to the minute.<br><br>* **Custom**: Specify the paths to be scanned for different endpoints (Windows, macOS, Linux). Refer to the on\-page tips for the correct path format.<br><br>   * **Scan frequency**: Specify **Once a day**, **Once a week**, or **Once a month**. If you select **Once a week** or **Once a month**, you must also specify the day of the week or date of the month.<br><br>   * **Scan time**: Specify the time period for the scan, accurate to the minute. |
   ||**Real\-time Scanning** |Monitors operations on files and processes on the endpoint, and automatically triggers scans of files and process memory. When enabled, you must select at least one protection scenario.<br><br><br>* **Sensitive file monitoring** (Windows): Automatically scans files when they are opened. Supports Word, PE, and script files.<br><br>* **Program startup protection** (Windows): Scans the executable file and loaded modules when a program starts.<br><br>* **File download protection** (Windows, macOS): Scans files downloaded via browsers and instant messaging applications in real\-time.<br><br>* **Peripheral access protection** (Windows, macOS): Automatically scans files on peripherals upon connection. You can select the folder depth for the scan: 3 layers, 5 layers, 10 layers, or Unlimited.<br><br>* **Registry monitoring** (Windows): When the registry is modified, automatically parses the content for file paths and scans them.<br><br>* **Process memory protection** (Windows): Scans process memory when a process performs sensitive actions, such as modifying startup items or connecting to the network. This effectively protects against obfuscated malicious code and fileless attacks.<br><br>* **Sensitive directory monitoring** (Windows, macOS, Linux): Automatically scans any file, regardless of its format, when it is opened within a specified directory. Please use this feature with caution, as monitoring large directories can cause high performance overhead. |
   ||**User Triggered Scanning** |This scan occurs when users manually trigger it on their desktop agents. This feature is enabled by default and cannot be disabled. It allows client users to manually trigger a quick scan to promptly detect and eliminate potential security threats. Click **Expand** on the right to view the default scan paths for Windows, macOS, and Linux. |
   ||**Custom Path and Right Click Scan** |All macOS, Linux, and Windows client users can actively select specific paths for scanning. Additionally, Windows users can quickly initiate a scan via the right\-click context menu. This feature is enabled by default and cannot be disabled.<br><br>> **说明**<br><br><br>> All virus logs detected through Custom Path and Right Click Scan are automatically reported to the **Audit Logs** page. Related data from the scan process is also recorded and aggregated. For more information, see [View audit logs](https://docs.byteplus.com/en/docs/sealsuite/docs-zk9yxy9szc) and [Admin Console Homepage Overview](https://docs.byteplus.com/docs/sealsuite/docs-viewing-the-home-page-of-the-admin-portal).<br> |
   ||**Resource occupancy mode** |Allows you to flexibly configure the resource usage mode to balance user experience with security protection. |
   |**Action** |**Log Audit** |Records alerts in the console and on the client after a malicious file is found.<br><br>This feature is enabled by default and cannot be disabled. For malicious files that are not quarantined, you can adjust the risk level for which logs are recorded on the client. |
   ||**File Isolation** |Allows you to select whether to enable file quarantine. When enabled, the system will quarantine detected malicious files. You must configure the following:<br><br><br>* Set the risk level for files to be quarantined.<br><br>* Select additional options as needed:<br><br>   * For infected files, the system will first attempt to repair the file by removing the virus module, and then move the file to the quarantine area if it cannot be repaired.<br><br>   * After a file is quarantined, users can only delete the files and cannot restore or trust them.<br><br><br>> **说明**<br><br><br>> In the **Process memory protection** scenario, the process will be terminated and its memory dump file will be quarantined, but the original process file will not be quarantined.<br> |
   |**Notification** |\- |Allows you to select whether to enable **User Notification**. When enabled, a pop\-up window will notify the user when a malicious file is detected. You must configure the following:<br><br><br>* Set the risk level for which notifications are triggered.<br><br>* Edit the notification content for **Malicious file detected**, **Malicious process detected**, and **Peripheral scanning results pop\-up**. SealSuite provides default notification text, which you can customize and preview. Multi\-language support is available; if a specific language is not configured, the Default Language content will be displayed. |
   |**System Protection** |**Type of protection** |Enables or disables suspicious PowerShell script execution detection.<br><br>Many cryptomining and ransomware viruses use Windows PowerShell scripts to allow malicious code to persist in the system without writing to the disk. It is recommended to enable this protection.<br><br>Once enabled, you can view System Defense logs in the Audit Logs. See details in [View audit logs](https://docs.byteplus.com/en/docs/sealsuite/docs-zk9yxy9szc).<br><br>> **说明**<br><br><br><br>1. > This feature is only supported on Windows clients.<br><br><br>2. > To avoid blocking legitimate admin scripts, add trusted command\-line parameters to the [PowerShell Run Parameters Whitelist](https://docs.byteplus.com/docs/sealsuite/configuring-whitelist#07e8bf88).<br> |
   ||**Action** |Sets the action to be taken when a suspicious PowerShell script is detected.<br><br><br>* **Loose (Recommended)** : The action is transparent to the user. An alert event is reported only in the Admin Console.<br><br>* **Moderate**: Blocks the suspicious script by default. The user receives a pop\-up and can choose to **Continue to Run** to allow the action for this instance. An alert event is reported.<br><br>* **Strict**: Blocks the suspicious script by default. The user cannot allow the execution and must contact an administrator to have it whitelisted. |
   |**Scope** |\- |Limits the effective scope by **User** or **Device.** <br><br><br>* **User**: Limits the scope by **Department** or **Role**.<br><br>* **Device**: Limits the scope by **Device Name**, **Operating System (OS)** , or **Device Group**. |

## Managing policies

1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint Security** \> **Strategy Center**.

3. Switch to the **Virus Detection** tab.

4. Locate the policy you want to manage. You can then:

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bf107685cae43c7a7f5c5c9eee5c18c~tplv-goo7wpa0wc-image.image)

   * **Enable** or **disable** the policy by using the toggle button.

   * **Copy**, **Edit** or **Delete** the policy by clicking the corresponding button.

      > **说明**

      > A policy cannot be restored after being deleted. While it will no longer be used for future scans, all historical events detected by this policy will be kept in the Audit Logs.
