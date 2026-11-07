---
title: "Managing endpoint devices"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-viewing-device-information"
---

To centrally manage and secure all endpoint devices in your organization, you can use the Asset List in the SealSuite Admin Console. This guide provides detailed instructions on how to view comprehensive device information, collect client logs, perform remote actions like locking or erasing a device, and respond to security incidents by quarantining endpoints or fetching files for forensic analysis.

<span id="0801da51"></span>
# Viewing device information

The **Asset List** page displays information about devices that users have used to log in to the SealSuite client. From this page, you can view a summary of information about the devices, including a device list, basic device information, installed software, system status, and more.


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Assets** \> **Asset List**.

3. On the list page, select a device group on the left and filter for target devices on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cafebf937bb047439202b7e84fac5601~tplv-goo7wpa0wc-image.image) </span>

4. In the results, click the device name to open the details page. You can view the following information:

   
   |**Tab** |**Description** |
   |---|---|
   |**General** |View basic information. |
   |**Software List** |If you have enabled software statistics, you can view the software asset information collected by the SealSuite desktop client on this device.<br><br>For more information about software statistics, see [Viewing software statistics](https://docs.byteplus.com/docs/sealsuite/docs-viewing-software-statistics). |
   |**Login/Logout** |View login or logout information such as the time, IP address, geographic location, and login account. |
   |**Utilization Details** |View system information, including hard disk status, CPU usage, memory usage, network adapter traffic, and running processes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">System status is only available for devices where the SealSuite desktop client is active.</div><br> |
   |**Client Management** |Collect logs or uninstall the SealSuite client from a user's device.<br><br><br>* **Collect User Log**: View the history of client log collection tasks and download the logs. For more information, see [Collecting Client Logs](https://docs.byteplus.com/docs/sealsuite/docs-viewing-device-information#d1828411).<br><br>* **Uninstall SealSuite Client**: View the history of client uninstallation tasks. For more information, see [Uninstalling the SealSuite Client](https://docs.byteplus.com/docs/sealsuite/docs-viewing-device-information#30af4379). |
   |**MDM** |On the **MDM** page, you can click each tab to view MDM\-related information for the device.<br><br><br>* **Profile**: View information about the configuration profiles installed on the device. Supported on macOS and iOS only.<br><br>* **Policies**: View the MDM policies associated with the device and their execution status. Click **View** in the **Actions** column to see policy details. For more information, see [Configuring MDM Policies](https://www.google.com/url?sa=E&q=%2F4q5lwbix%2F5pda6tst).<br><br>* **Remote Commands**: View the history of remote commands sent to the device. In the **Actions** column, you can:<br><br>   * **View Key**: View the key for the current record. This is available only for **Lock** or **Erase** commands on macOS, and **Lock** commands on Windows.<br><br>   * **View Log**: View the detailed log for the corresponding command.<br><br>* **Scripts**: View the history of script execution tasks for the device, including task name, execution status, and update time. Click **View** to see the task's execution status and script configuration. Supported on macOS, Windows, and Linux.<br><br>* **EPM**: View the privilege policies associated with the device and their execution status. Click **View** to see the deployment status and configuration details. Supported on macOS and Windows only. For more information, see [Configuring Privilege Management](https://www.google.com/url?sa=E&q=%2F4q5lwbix%2Flfsrpi5n). |
   |**Diagnostic Report** |* Select a diagnostic record and click **View** in the **Actions** column to see the report, which includes:<br><br>   * Basic device and hardware information.<br><br>   * Disk, memory, and CPU load.<br><br>   * Details of running processes, including memory and CPU usage.<br><br>   * System startup items and critical services.<br><br>* Select a record and click **Copy Link** to share the report link with IT for assistance. |
   |**Policy in Effect** |View the status of effective policies on the current device.<br><br><br>* Check the status of policies like Device Control, DLP, and Client Settings. The **Actions** column provides details on the specific policies in effect.<br><br>* For macOS devices, you can view the status of permissions such as **Full Disk Access**, **Screen Recording**, **Network Extension**, and **Accessibility**. |
   


<span id="d1828411"></span>
# **Collecting Client Logs**


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Assets** \> **Asset List**.

3. In the appropriate device group, locate the target device.

4. In the **Actions** column for the device, click **More** \> **Capture client side logs**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature requires the SealSuite client to be version v2.1.0 or higher.   </div>
   

5. In the **Collect User Log** page that appears, wait for the collection to finish, then click **Download log**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2375155e3ada44baa9a4da519d9e1ec1~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the device is active and connected to the network, collection starts immediately. If the device is inactive, the system will wait up to 24 hours. The task will run as soon as the device becomes active within this period. If the timeout is exceeded, the task will fail.   </div>
   

<span id="30af4379"></span>
# **Uninstalling the SealSuite Client**


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Assets** \> **Asset List**.

3. In the appropriate device group, locate the target device.

4. In the **Actions** column for the device, click **More** \> **Uninstall SealSuite Client**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For client versions v2.1.16 and higher, you can choose to clear the device's network access credentials during uninstallation.   </div>
   

5. In the confirmation dialog, click **Continue uninstall**. You can check the uninstallation status in the device details page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The uninstallation typically completes within 30 seconds if the device is active and connected. The task will fail if the device remains inactive for 24 hours, has poor network connectivity, or fails to return a result within 5 minutes of the command being sent.   </div>
   

<span id="b7be08f1"></span>
# **Device Remediation**

The Admin Console provides extensive device remediation capabilities, including **Remote Commands** for daily management and **Response** actions for security incident response.

<span id="91c4694a"></span>
## **Executing Remote Commands**

You can send commands like **Restart**, **Shut Down**, **Lock**, and **Erase** to devices managed by MDM. For MDM configuration, see [Configuring MDM Policies](https://www.google.com/url?sa=E&q=%2F4q5lwbix%2F5pda6tst). If **Security Check** is enabled for the device, you must enter a private key or command signature when sending **Lock** or **Erase** commands.


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Assets** \> **Asset List**.

3. Locate the target device and click its name to view its details.

4. In the upper\-right corner of the device details window, click the **Actions** button and hover over the **Remote Commands** category.

5. Select the desired remote command.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/366b5f75f233420ba42ace1910a8f0bf~tplv-goo7wpa0wc-image.image) </span>

   
   |**Remote Command** |**Description** |**Additional Information** |
   |---|---|---|
   |**Sync MDM Policies** |Immediately syncs the latest MDM policy configuration and reports device information. |/ |
   |**Restart** |Sends a restart command to the device. |/ |
   |**Shut Down** |Sends a Shut Down command to the device. |/ |
   |**Lock** |Locks the device, preventing user login and use until it is unlocked. |* Not supported on Linux devices.<br><br>* If **Security Check** is enabled, you must enter the private key to generate a command signature. The client will only execute verified commands. See [Enabling Endpoint Device Security Check](https://docs.byteplus.com/docs/sealsuite/docs-viewing-device-information#4686d722). |
   |**Erase** |Erases all data and settings from the device. This action is irreversible. |If **Security Check** is enabled, you must enter the private key to generate a command signature. See [Enabling Endpoint Device Security Check](https://docs.byteplus.com/docs/sealsuite/docs-viewing-device-information#4686d722). |
   |**Enable/Disable Lost Mode** |Send the **Enable Lost Mode** command to lock the device's screen. Once locked, the device can only be unlocked by sending the **Disable Lost Mode** command. When enabling lost mode, you can add notes and customize the on\-screen notification message. Once configured, click **Enable** to apply the settings. |* Supported on iOS/iPadOS devices only.<br><br>* While in Lost Mode, you can view the device's location or play a sound from the **MDM** \> **Remote Commands** tab to help find it. |
   


<span id="37f1a0d1"></span>
## **Security Incident Response**

The Admin Console provides **Quarantine endpoint network** and **Fetch files** actions to contain damage, prevent threat proliferation, and conduct forensic investigations when an endpoint is compromised.


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Assets** \> **Asset List**.

3. Locate the target device and click its name to open its details page.

4. In the upper\-right corner of the device details window, click the **Actions** button and hover over the **Response** category.

5. Select the desired response action.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8258b4f2a90b4f94bd1d09ba5e99a478~tplv-goo7wpa0wc-image.image) </span>

   
   |**Response** |**Description** |**Additional Information** |
   |---|---|---|
   |**Fetch files** |Extract a specific file or all files from a directory on the device.<br><br>In the **Extract File** drawer:<br><br><br>1. Click **Add Path** to add file/directory paths (up to 10 per task).<br><br>2. Enter an **Encryption password** as prompted. This password is required to decrypt the downloaded file archive.<br><br>3. Click **Confirm** to begin. |1. **File Size**: The total size of files per extraction task cannot exceed 180MB.<br><br>2. **File Validity**: Extracted files are stored on the server for 3 days and are automatically deleted afterward. Download them promptly.<br><br>3. **File Download**: All extraction operations are logged. To download:<br><br>   1. Return to the Asset List, click **Terminal Remediation** \> **Remediation Logs** in the upper\-right corner.<br><br>   2. Use the filters to find the relevant record for the device.<br><br>   3. Click **Download** in the **Actions** column. |
   |**Quarantine/Restore endpoint network** |The **Quarantine endpoint network** action restricts a device's network access, preventing all communication except with the management platform.<br><br>Once the threat has been removed from the endpoint, you can execute the **Restore endpoint network** action to reconnect it to the network and resume normal operation. |1. **View Network Status**: Check the device's current network status in its **General** Information:<br><br>   * **Normal**: Default state.<br><br>   * **Quarantining**: Quarantine command sent, pending execution.<br><br>   * **Quarantined**: Device is successfully **quarantined**.<br><br>   * **Restoring**: Restore command sent, pending execution.<br><br>2. **Query Operation Records**: All quarantine and restore actions are logged. To view them:<br><br>   1. Return to the Asset List, click **Terminal Remediation** \> **Remediation Logs**.<br><br>   2. View the detailed information on the logs page.<br><br>3. **Endpoint pop\-up notification**: Endpoint devices quarantined from the network receive a pop\-up notification. You can customize the pop\-up notification.<br><br>   1. On the endpoint list page, click **Terminal Remediation** \> **Remediation Configuration** in the upper\-right corner.<br><br>   2. On the **Terminal Isolation Pop\-up Configuration** page, customize the notification title and content. Multilingual configuration is supported.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>The pop\-up cannot be closed</strong>. We recommend describing the reason for the network quarantine and the follow\-up solution in the notification content.   </div><br>    |
   


<span id="4686d722"></span>
# **Enabling Endpoint Device Security Check**

This feature is disabled by default. When enabled, you must enter a private key or command signature to authorize sensitive remote commands like Lock or Erase, which ensures operational security.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The security check feature for endpoint devices and software distribution can be controlled independently. For software distribution, see <a href="https://docs.byteplus.com/docs/sealsuite/docs-distributing-software-to-user-devices">Distributing software to user devices</a>.</div>



1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Assets** \> **Asset List**.

3. Locate the target device and open its details page.

4. At the top of the device details page, click **Security Check Disabled**.

5. In the **Enable Security Check** window, enter the private key or command signature, then click **Enable Security Check**.

   To disable this feature, you will need to re\-enter the key or signature.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Please contact the SealSuite service provider to obtain the private key and signature.</div>


* <div data-tips="true" data-tips-type="tip">When entering the private key, you must include the <code>BEGIN</code> and <code>END</code> lines.</div>
