---
title: "Best practices for anti-virus control on devices"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/Best-practices-for-anti-virus-control"
---

This article aims to assist IT administrators in configuring SealSuite anti\-virus features to meet their company's specific security requirements effectively. Through a flexible scan\-and\-discover mechanism, including system regular inspection and real\-time scanning, it ensures the data security of employees' devices.

<span id="c675dd14"></span>
# Feature overview

SealSuite's anti\-virus control provides a robust and adaptable solution for virus removal. By integrating the SealSuite anti\-virus policy with your enterprise's security framework, the SealSuite client will equip corporate devices with robust virus detection and eradication functions, safeguarding device data security within its operational scope. The anti\-virus policy includes settings for detection methods like system regular inspection and real\-time scanning.


* **System regular inspection**: Conducts thorough checks on devices during specified periods to identify any viruses that may be present.

* **Real\-time scanning**: Ensures viruses are promptly removed during critical scenarios, such as executing computer programs or file downloads.


<span id="537d4efa"></span>
# Scenario One: Real\-time scanning for downloaded files

<span id="f91b42f0"></span>
## Scenario introduction

In this scenario, the enterprise administrator sets up the anti\-virus policy in the SealSuite Admin Console to ensure that the SealSuite client delivers real\-time scanning during program execution and file downloads. When employees download files via browsers or instant messaging tools on their devices, the SealSuite client promptly detects, identifies, and eliminates any viruses.

<span id="3c7a4459"></span>
## Procedure


1. Log in to the SealSuite Admin Console.

   You need to log in to the SealSuite Admin Console with an administrator account.

2. In the left navigation bar, select **Anti\-Virus** \> **Policy Management**.

3. On the **Policy Management** page, click on **New Policy** in the **Policy Configuration** tab.

4. On the **Add Detection Policy** page, complete the following configuration and click **Add**.

   
   |**Configuration Item** |**Description** |**Recommended Value** |
   |---|---|---|
   |Policy Name |Custom name used to identify the policy. |Scanning for and eliminating malicious files that have been downloaded |
   |Priority |Current policy priority. The value range is 0 to 100, with higher numbers indicating higher priority. You can enable multiple policies at the same time. SealSuite, when detecting devices, matches policies in order of priority value, stopping once a policy is hit. If there is no hit, it will stop after executing all policies. If there are two policies with the same priority value, the one with the most recent modification time will be executed first. |Set **100** to the most critical policy. |
   |Detection Item |It is recommended that you select all detection Items. You can specify the scope of detection for this policy, supporting the detection of viruses, trojans, hacker tools, malicious advertising, etc. |Select the **select all** checkbox. |
   |Detection Methods |Supports **System regular inspection** or **Real\-time scanning**.<br><br><br>* **System regular inspection** refers to the process of conducting one or more virus scans on a device during a specified time period.<br><br>* **Real\-time scanning** refers to the detection and timely eradication of viruses in specified scenarios within the devices. |* Check the **Real\-time scanning** checkbox.<br><br>* In the **Scenarios** area, select the **Computer programs** and **File download** checkboxes. |
   |Action |The **Action** area will only appear after selecting at least one detection item. You can set the action after a virus is detected:<br><br><br>* **Loose**: \*\*\*\* Remind users only.<br><br>* **Moderate**: \*\*\*\* Remind users and automatically quarantine virus files, users can restore, trust, delete files.<br><br>* **Strict**: \*\*\*\* Alert users and automatically quarantine virus files, users can only delete files |Choose **Moderate** option for the optimal user experience. |
   |Scope |Supports restricting effective Scope based on either **User** or **Device** dimensions.<br><br><br>* When selecting **User**, you need to restrict user scope through **Department** or **Role**.<br><br>* When selecting **Device**, you need to restrict device scope through **device name**, **OS**, and **Group**. |* Select **User** to include all devices under the user for comprehensive checks.<br><br>* On the **Department** tab, select the **Select All** check box. |
   

5. Return to the **Policy Configuration** tab, check the created policies, and make sure the switch for **Status** is turned on.

   After finalizing the strategy or activating the policy status, the policy will take effect within 1 to 2 minutes.


<span id="4a6abe30"></span>
## Results

When employees download files, if the file is detected to contain a virus, the SealSuite client will immediately isolate the file and alert the employee, while providing a recovery option.

<span id="2e26e387"></span>
# Scenario two: Regular virus scanning of corporate devices

<span id="00b28edf"></span>
## Scenario introduction

In this scenario, the administrator configures the anti\-virus policy in the SealSuite Admin Console, choosing both a specific time frame and a scan frequency to conduct scheduled scanning of the devices to ensure security configuration is successfully deployed in the corporate environment and discover any outliner for remediation. The SealSuite client will perform multiple virus scans on the devices within the designated period to guarantee system security.

<span id="6f1d87d4"></span>
## Procedure


1. Log in to the SealSuite Admin Console.

   You need to log in to the SealSuite Admin Console with an administrator account.

2. In the left navigation bar, select **Anti\-Virus** \> **Policy Management**.

3. On the **Policy Management** page, click on **New Policy** in the **Policy Configuration** tab.

4. On the **Add Detection Policy** page, complete the following configuration, and click **Add**.

   
   |**Configuration Item** |**Description** |**Recommended Value** |
   |---|---|---|
   |Policy Name |Custom name used to identify the policy. |Scanning for and eliminating malicious files that have been downloaded. |
   |Priority |Current policy priority. The value range is 0 to 100, with higher numbers indicating higher priority. You can enable multiple policies at the same time. SealSuite, when detecting devices, matches policies in order of priority value, stopping once a policy is hit. If there is no hit, it will stop after executing all policies. If there are two policies with the same priority value, the one with the most recent modification time will be executed first. |Set **100** to the most critical policy. |
   |Detection Item |You can specify the scope of detection for this policy, supporting the detection of viruses, trojans, hacker tools, malicious advertising, etc. It is recommended that you select all Detection Items. |Select the **select all** checkbox. |
   |Detection Methods |Supports **System regular inspection** or **Real\-time scanning**.<br><br><br>* **System regular inspection** refers to the process of conducting one or more virus scans on a device during a specified time period.<br><br>* **Real\-time scanning** refers to the detection and timely eradication of viruses in specified scenarios within the devices. |* Select the **System regular inspection** checkbox.<br><br>* **Scan mode** includes selecting the **Document scanning** and **Process scanning** checkboxes to ensure all processes are monitored.<br><br>* **Scan path** set to **Default**.<br><br>* **Scanning frequency** is set to \*\*Once a day \*\*to ensure optimal system performance.<br><br>* **Scan time** is set to either 7:00 \- 8:00 or 20:00 \- 21:00 to avoid scanning during office hour and impacting the client performance. |
   |Action |The **Action** area will only appear after selecting at least one detection item. You can set the action after a virus is detected:<br><br><br>* **Loose**: \*\*\*\* Remind users only.<br><br>* **Moderate**: \*\*\*\* Remind users and automatically quarantine virus files, users can restore, trust, delete files.<br><br>* **Strict**: \*\*\*\* Alert users and automatically quarantine virus files, users can only delete files |Choose **Moderate** option for the optimal user experience. |
   |Scope |Supports restricting effective Scope based on either **User** or **Device** dimensions.<br><br><br>* When selecting **User**, you need to restrict user scope through **Department** or **Role**.<br><br>* When selecting **Device**, you need to restrict device scope through **device name**, **OS**, and **Group**. |* Select **User** to include all devices under the user for comprehensive checks.<br><br>* On the **Department** tab, select the **Select All** check box. |
   

5. Return to the **Policy Configuration** tab, check the created policies, and make sure the switch for **Status** is turned on.

   After finalizing the strategy or activating the policy status, the policy will take effect within 1 to 2 minutes.


<span id="003a6ed8"></span>
## Results

The administrator has successfully set up a system regular inspection task, which will automatically run every day 7:00 \- 8:00 or 20:00 \- 21:00. After each system regular inspection is completed, the system will generate an inspection report, and the administrator can view the inspection results and statistics in the Admin Console.

<span id="426bdff0"></span>
# Scenario Three: The end user activates the anti\-virus scan on their devices

<span id="7b6698a6"></span>
## Scenario introduction

After enterprise administrators configure and activate the anti\-virus policy in the SealSuite Admin Console, all users within the effective scope of the policy can proactively perform a virus scan through the SealSuite client.

<span id="73876985"></span>
## Procedure


1. Log in to SealSuite client.

   The anti\-virus control feature enables virus scanning on desktop clients, necessitating a login to the SealSuite desktop client.

2. In the left navigation bar, click **Security**, and click **One\-click detection** to initiate an active virus scan.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8523ac7f6be43fdbfca8808c43472ec~tplv-goo7wpa0wc-image.image) </span>


<span id="f2b5ec3a"></span>
## Results

Employees initiate a virus scan proactively through the SealSuite client, which then begins scanning for potential threats in the system. Once the scan is complete, the client will display the results, which will include the number of detected viruses and the status.

<span id="3bd10d0a"></span>
# Scenario Four: An employee restores a file that was incorrectly quarantined

<span id="007f8954"></span>
## Scenario introduction

After the enterprise administrator configures and activates the anti\-virus policy on the SealSuite Admin Console, SealSuite will carry out virus removal on all devices within the effective scope of the policy. If an administrator has configured the SealSuite to allow manual recovery of quarantined files, employees can easily retrieve files that were incorrectly quarantined by accessing the file recovery section within the SealSuite client.

<span id="31534bf5"></span>
## Procedure


1. Reach out to the administrator to ensure that the SealSuite client supports manual recovery of quarantined files.

2. Log in to SealSuite client.

3. In the left\-side navigation bar, click **Security**, and in the upper right corner of the page, click **Quarantine Area**.

4. On the **Quarantine Area** page, locate the mistakenly quarantined file, in the **Action** column click **Recover**.

   After the file is restored, you can find it in the original location within the device.


<span id="c24bf990"></span>
## Results

After communicating with the administrator, the employee confirmed the restoration of permissions and found the file quarantine area in the SealSuite client. The employee identified the mistakenly quarantined files in the file quarantine area and successfully performed the recovery. Restored files will reappear in their original location on the device, enabling employees to resume their work seamlessly while maintaining system security.
