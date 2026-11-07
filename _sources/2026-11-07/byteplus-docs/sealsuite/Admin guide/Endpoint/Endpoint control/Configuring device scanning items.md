---
title: "Configuring device scanning items"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configure-detection-items"
---

To customize risk detection on your endpoints, you can use the Scanning Item Configuration feature in SealSuite. This guide provides instructions on how to manage default baseline scanning items and add custom registry, application, and process scans. Following these procedures will help you tailor your security policies to proactively identify and remediate risks across your devices.

<span id="42416ab3"></span>
# Feature description

The item scanning configuration feature is a crucial tool for monitoring enterprise device settings, which aims to boost security and lower operational costs. You can utilize this feature to specify the content for scanning items and enable them within the device control strategy. It categorizes the scanning items into two types: configuration result\-oriented and scanning\-oriented.


* **Configuration result\-oriented type**: This primarily ensures the consistency of enterprise device configurations, such as screen lock duration and desktop screensavers.

* **Scanning\-oriented type**: This primarily checks if the enterprise device configuration meets the requirements and informs the user to help resolve issues, such as verifying the system version.


This feature can help enterprises discover more security risks by using a variety of scanning items. At the same time, it also supports flexible configuration, improving efficiency by reusing existing configurations. Additionally, this feature can automate the global standardization of built\-in baseline scanning configurations, which reduces the need for manual intervention. To meet various enterprise needs, this feature also supports custom scanning items tailored to various business requirements. For detected risks, SealSuite provides three types of remediation solutions:


* **Auto Repair**: If the baseline scan does not meet the required conditions, SealSuite will automatically perform a baseline repair.

* **Manual Repair**: When baseline scanning does not meet the conditions, the user can click the One\-click repair button on the client, and SealSuite will automatically repair the baseline.

* **Show Repair Guide**: When baseline scanning does not meet the conditions, the client will display the repair solution to guide the user in repairing the baseline.


<span id="b2c5480f"></span>
# Adding registry scanning item

Registry scanning items refer to specific projects or tasks used to check and verify registry settings in the operating system. The registry is a database that stores system configuration data and settings for applications. It is essential for the operating system to operate smoothly and for applications to install correctly.


1. Log in to the SealSuite Admin Console.

2. In the left sidebar, select **Endpoint** \> **Endpoint Control** \> **Endpoint Baseline**.

3. On the **Endpoint Baseline** page, click **Scanning Configuration** \> **Baseline Scanning Items** tab.

4. In the top right corner of the page, click **Registry Scanning Item**.

   After clicking, the **Add New Registry Scanning Item** dialog box will pop up on the right side of the page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">SealSuite supports creating new custom Windows registry scanning items.   </div>
   

5. In the **Add New Registry Scanning Item** dialog box, click **Confirm** in the bottom right corner after completing the following configurations.

   
   |**Configuration Block** |**Configuration Item** |**Description** |
   |---|---|---|
   |General |Item Name (Chinese) |Required, fill in the Chinese baseline name displayed on the client. |
   ||Item Name (English) |Optional, fill in the English baseline name displayed on the client. |
   ||Baseline Description (Chinese) |Required, fill in the Chinese baseline description displayed on the client. |
   ||Baseline Description (English) |Optional, fill in the English baseline description displayed on the client. |
   |Remediation |Remediation |Modification is not supported; this type of check item only supports the repair method of **Show Repair Guide**. |
   ||Repair plan |Click **Edit**, then in the **Edit Repair Plan** dialog, enter the Chinese and English titles and content for the repair plan, and click **Confirm** to save. |
   ||Prompt Message (Chinese) |Required, fill in the Chinese prompt text displayed on the client. |
   ||Prompt Message (English) |Required, fill in the English prompt text displayed on the client. |
   |Scanning Content |If the following conditions are met, it is considered a risk |You can add multiple conditions, and relationships between registry conditions can be **AND** or **OR**, with a maximum of 20 conditions.<br><br><br>* The detection content can be set to **meet** or **Does not match**.<br><br>   * **meet**: Defined as a risk if the specified value is matched.<br><br>   * **Does not match**: Defined as a risk if the stipulated criteria are not met.<br><br>* **Registry Main KEY**: Select a registry main KEY.<br><br>* **Path**: Enter the path where the value is located.<br><br>* **Name**: Enter the value name.<br><br>* **Value Type**: Select a value type.<br><br>* **Value Data**: Enter the value data.<br><br><br>For example if you need to determine whether value type of HKEY_LOCAL_MACHINE\ SYSTEM\ CurrentControlSet\ Services\ com.byteplus.corplink.service key Description is Service for CorpLink you can set:<br><br><br>* **Registry Main KEY**: HKEY_LOCAL_MACHINE<br><br>* **Path**: SYSTEM\CurrentControlSet\Services\com.byteplus.corplink.service<br><br>* **Name**: Description<br><br>* **Value Type**: REG_SZ<br><br>* **Value Data**: Service for CorpLink |
   


<span id="c3715606"></span>
# Managing baseline scanning items

Baseline scanning items refer to a series of key indicators, parameters, or features used for assessment, monitoring, or verification in a specific field or system. These scanning items are used as benchmarks or references to determine the performance, quality, compliance, or other important aspects of a system, product, service, or process. SealSuite provides scanning items for system configuration, network configuration, mobile configuration, login configuration, screen lock, intrusion prevention, and data security. You can configure these scanning items based on the actual business scenarios.


1. Log in to the SealSuite Admin Console.

2. In the left sidebar, select **Endpoint** \> **Endpoint Control** \> **Endpoint Baseline**.

3. On the **Endpoint Baselin**e page, click **Scanning Configuration** \> **Baseline Scanning Items** tab.

4. (Optional) At the top of the page, select **All** or specify an OS.

5. In the baseline list, find the system configuration item to be configured, and click **Configure** under the **Action** column.

   After clicking, a **Configure Baseline Scanning Item** dialog box will pop up on the right side of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7710fa0e9fc9481697b0d6fe13a76f9a~tplv-goo7wpa0wc-image.image) </span>

6. After completing the following configuration changes, click **Confirm** in the bottom right corner.

   
   |**Configuration Block** |**Configuration Item** |**Description** |
   |---|---|---|
   |General |Item Name (Chinese) |Modification is not supported. |
   ||Item Name (English) |Modification is not supported. |
   ||Baseline Description (Chinese) |Modify the Chinese baseline description displayed on the client. |
   ||Baseline Description (English) |Modify the English baseline description displayed on the client. |
   |Remediation |Remediation |* **Auto Repair**: If the baseline scan does not meet the required conditions, SealSuite will automatically perform a baseline repair.<br><br>* **Manual Repair**: If the baseline scanning does not meet the conditions, users can click the One\-click repair button in the client, and SealSuite will automatically repair the baseline.<br><br>* **Show Repair Guide**: When baseline scanning does not meet the conditions, the client will display the repair solution to guide the user in repairing the baseline. |
   ||Repair plan |Click **Edit**, in the **Edit Repair Plan** dialog box, modify the Chinese and English titles and content of the repair plan, and click **Confirm** to save.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only when you choose the repair method of <strong>Show Repair Guide</strong>, you need to configure the repair scheme.</div><br> |
   ||Prompt Message (Chinese) |Modify the Chinese prompt text displayed on the client. |
   ||Prompt Message (English) |Modify the English prompt text displayed on the client. |
   |Scanning Content |If the following conditions are met, it is considered a risk |Modification is not supported. |
   


<span id="683d046d"></span>
# Adding application scanning items

SealSuite provides some default application scanning items, and you can also set custom application scanning items. By adding new application scanning items, you can monitor risky applications on users' devices, such as checking whether non\-compliant applications are installed on users' devices. Through the configuration of application scanning items, enterprises can better manage applications on users' devices reducing security risks and improving the security and stability of devices.


1. Log in to the SealSuite Admin Console.

2. In the left sidebar, select **Endpoint** \> **Endpoint Control** \> **Endpoint Baseline**.

3. On the **Endpoint Baseline** page, click **Scanning Configuration** \> **Application Scanning Items** tab.

4. (Optional) At the top of the page, select **All** or specify an OS.

5. On the **Application Scanning Items** tab, you can view the default application scanning items provided by SealSuite.

6. In the **Application Scanning Items** tab page, click **Add New Application**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a56d77d214734f1fbce59b95cd157978~tplv-goo7wpa0wc-image.image) </span>

7. On the **Add New Application** page, complete the following configurations, and click **Confirm**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Application name |Supports Chinese and English characters, numbers, and must include at least one special character; maximum length is 64 characters. |
   |OS |Choose appropriate OS for the specified application; options include **Windows**, **macOS**, and **Linux**. Multiple selections are allowed. After selection, you need to add the application in the specified OS configuration area where you can choose **Custom** or **Install from employee** to add applications, and complete the following configurations:<br><br><br>* Select the scanning object:<br><br>   * Detect running status of **Any application**: If **Any application** is selected the application group is considered running when any of the applications in the group are running.<br><br>   * Detect the running status of **All applications**: If **All applications** is selected, it is considered that the application group is running only when all of the following applications are running. Running scanning for all applications only supports client versions v3.0.12 and above.<br><br>* Adding scanning application:<br><br>   * **Custom**: Manually add an application and set application properties.<br><br>      * You can hover over the question mark icon after the OS title to see how to obtain custom parameter information.<br><br>      * Click **Custom** to add multiple applications.<br><br>   * **From employee installation**: Select the software that has been installed on the corresponding OS devices obtained from SealSuite software statistics. Click **From employee installation** to add multiple applications. |
   |Configure Resolution |In the configuration area of each OS, you can click **Configure Resolution** in the upper right corner, and then set the corresponding repair plan for the scanning item in the **Configure Resolution** dialog box.<br><br><br>* **Non\-Compliant Applications**: You can choose to send a warning message or provide a **Resolution Guide**. Choosing **Warning Message** uses the default notification text of SealSuite, while selecting **Resolution Guide** allows you to set up custom English and Chinese repair guides.<br><br>* **Mandatory Application**:<br><br>   * You can choose to send a **Warning Message** or provide a **Resolution Guide**. Choosing **Warning Message** uses the default notification text of SealSuite, while selecting **Resolution Guide** allows you to set up custom English and Chinese repair guides.<br><br>   * You can choose **Go to Software Library**, which helps users find current software in the software library. |
   |Version scanning |In the configuration area of each OS, set the detected version. If not set, it indicates no distinction between versions. |
   

   After adding, you can view the custom application configuration information in the **Application Scanning Items** list. In the **Action** column of the custom application, you can **Configure** or **Delete** the application.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you set the application type as <strong>default</strong> for the application scanning item and later configure, the application type will change to <strong>custom</strong>.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5391a66beb3f4c31baed2fc566c282af~tplv-goo7wpa0wc-image.image) </span>


<span id="a90ee209"></span>
# Adding process scanning items

You can add process scanning items to monitor processes, such as detecting unauthorized processes on user devices. By monitoring these process scanning items, problems can be promptly identified and addressed, thereby improving the stability and security of the system.


1. Log in to the SealSuite Admin Console.

2. In the left sidebar, select **Endpoint** \> **Endpoint Control** \> **Endpoint Baseline**.

3. On the **Endpoint Baseline** page, click **Scanning Configuration** \> **Process Scanning Items** tab.

4. (Optional) At the top of the page, select **All** or specify an OS.

5. On the **Process Scanning Items** tab, you can view the default application scanning items provided by SealSuite.

6. In the **Process Scanning Items** tab page, click **Add Process Group**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c45ac71d97643d8a0101c76c2b83c20~tplv-goo7wpa0wc-image.image) </span>

7. On the **Add Process Group** page, complete the following configurations, and click **Confirm**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Process group scanning only supports client versions v3.0.12 and above.   </div>
   

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Process group name |Supports Chinese and English characters, numbers, and must include at least one special character; maximum length is 64 characters. |
   |OS |Choose appropriate OS for specified application options include **Windows**, **macOS**, and **Linux**. Multiple selections allowed. After selection, you need to add processes in specified OS configuration area and complete following configuration:<br><br><br>* Select the scanning object:<br><br>   * Check operation status of any of the following **processes**: If any of the following processes runs the process group is considered to be running.<br><br>   * Check the operation status of all the following **processes**: If all the following processes run, only then the process group is considered to be running.<br><br>* Set scanning objects: Set the file **Digital Signature** and the **Process Name** corresponding to the process.<br><br>* Add multiple processes: Click **Add** below to add multiple processes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Click the question mark icon in the upper right corner of Windows and Mac OS to learn how to obtain the corresponding OS file digital signature and process information.</div><br> |
   |Repair plan |In the configuration area of **Windows**, **macOS** or **Linux** OS, you can click **Configure Solutions** then set corresponding repair plan for scanning items in the **Configure Solutions** dialog box.<br><br><br>* Non\-Compliant Process:<br><br>   * Choose **Warning Message** to use SealSuite’s default notification text.<br><br>   * Choose **Resolution Guide** to create a custom English and Chinese repair guide.<br><br>* Mandatory process:<br><br>   * Choose **Warning Message** to use SealSuite’s default notification text.<br><br>   * Choose **Resolution Guide** to create a custom English and Chinese repair guide.<br><br>   * Select **Go to Software Library** to help users search for the current software in the software library.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Linux OS does not currently support <strong>Go to Software Library</strong>.</div><br> |
   

   After adding, you can view the process configuration information in the **Process Scanning Items** list. In the **Action** column of the process list, you can **Configure** or **Delete** a process.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f85a333945c842a4a013b5df46ca652e~tplv-goo7wpa0wc-image.image) </span>
