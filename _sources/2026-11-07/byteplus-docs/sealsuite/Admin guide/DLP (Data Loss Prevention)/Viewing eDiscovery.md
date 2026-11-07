---
title: "Viewing eDiscovery"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-viewing-data-trends"
---

SealSuite’s eDiscovery module provides various data capabilities such as tracing data leaks and understanding the sensitive data landscape within the corporate devices. Utilizing these functions, you can trace sensitive files by using filter criteria such as specific file contents or sensitive data names, and view the location and file transfer records of sensitive data.

 &nbsp;

<span id="function-overview"></span>
# Function Overview

The eDiscovery function provides a visual display of information about data distribution, amount of data, data changes, and more, helping you understand and utilize data better. This function consists of the following features:


* **Data Leaks**: With this feature, you can trace the source of data leaks by uploading the leaked data files or filtering leaked data files by specific file names, file contents, or sensitive data labels.

* **Sensitive Data Landscape**: In the mind map of the **Sensitive Data Landscape**, you can view the location and transfer records of sensitive data, achieving dynamic monitoring of sensitive data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Location refers to the behavior of users who obtain sensitive files through applications or download them from websites, and store them on the local hard disk or other storage devices.   </div>
   

* **Security Posture Report**: On the **Security** tab, you can view security posture reports on data leakage prevention, including coverage of DLP policies, data discovery, and risk of data leak, and export the corresponding PDF files.


 &nbsp;

<span id="viewing-data-leaks"></span>
# Viewing Data Leaks

Sensitive data leaks refer to the process of tracking and investigating the unauthorized leakage of sensitive data, with the main purpose of determining the source, time, and method of data leakage, and personnel involved in this process. You can trace the source of data leaks by uploading files, entering file names, content, or sensitive data labels, and taking corresponding measures to enhance data security.


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **eDiscovery**.

3. On the **Leakage Investigation** tab, you can search for sensitive data in any of the following ways:

   * **Method 1**: Enter keywords in the search box and click the search icon on the right side.

      You can also select a search type below the search box to improve the accuracy of search results.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a54d0a31bf34e6fafa08a09825e4d0a~tplv-goo7wpa0wc-topic.webp) </span>

   * **Method 2**: Click the file icon on the right side of the search box, then upload a local file for sensitive data detection.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/affb01e36af742dabcefa0e8fb2ebfee~tplv-goo7wpa0wc-topic.webp) </span>

4. On the search results page, click **Details** on the right of the file name to learn more about the data details.

   In the selection criteria area above the results list, you can search for sensitive data again by keyword, file type, and period.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95cfd335093f4814b2d4171c2bbbb9d3~tplv-goo7wpa0wc-topic.webp) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Shared sensitive files</strong> refer to data outbound alerts collected and reported based on configured <a href="https://docs.byteplus.com/en/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule">document outgoing control policies</a> and <a href="https://docs.byteplus.com/en/docs/sealsuite/Configuring_block_policy_for_application">channel control policies</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Local sensitive files</strong> refer to sensitive file information collected and reported based on configured <a href="https://docs.byteplus.com/en/docs/sealsuite/docs-viewing-data-trends#creating-data-collection-policy">data collection policies</a>.   </div>
   

5. On the **File Transfer Details** page, click the card to view details of the device that has created, received, downloaded, or sent the current file, as well as the details of the user that has transferred out the current file.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1434ce7150bb4bb3b13891d279205283~tplv-goo7wpa0wc-topic.webp) </span>

6. On the device information card, click **File Transfer** to view the file transfer records.

7. Click the **File Transfer Analysis** tab to view the employees, operations, and distribution channels related to the sensitive file.

   * On the **Users** page, view all employees associated with the sensitive file by employee. Click an employee, and the right side displays a timeline of the employee’s operations on the sensitive file. Click **File Transfer Records** to view the file transfer records.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3e6bf7c08624940b7bd7f01bd1f93c5~tplv-goo7wpa0wc-topic.webp) </span>

   * On the **Operations** page, view how many operations were performed on the sensitive file on each date. Click a date, and the right side displays a timeline showing when related employees performed which operations on the sensitive file. You can also filter transfer records by operation behavior, such as outbound events.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/caeadfe266514c47821b29f5086b087f~tplv-goo7wpa0wc-topic.webp) </span>

   * On the **Sharing Channel** page, you can filter the transfer records of the sensitive file by channel.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba52885ea69e479290c16d819dacc4cb~tplv-goo7wpa0wc-topic.webp) </span>


 &nbsp;

<span id="viewing-sensitive-data-landscape"></span>
# Viewing Sensitive Data Landscape

The Sensitive Data Landscape refers to the overall situation and trend of enterprises in protecting their sensitive data. Sensitive Data Landscape assessment can help you understand the risks and threats of data security, and develop corresponding policies and measures to protect data security, thereby reducing the risk of data leakage.


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **eDiscovery**.

3. On the **Sensitive Data Landscape** tab, set the time interval for data auditing.

   You can select a time interval in the drop\-down list or set a custom time interval.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa5a1cdf63b248899a4ed72b07f65179~tplv-goo7wpa0wc-topic.webp) </span>

4. Click a data classification card to view files that belong to a specific data classification level.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ec538a8cae343c6b5582f911540a8b9~tplv-goo7wpa0wc-topic.webp) </span>


 &nbsp;

<span id="hqQwTpzlR"></span>
# Configure Data Collection Policy

You can create data collection policies, including the sensitive data scope, data collection paths, and collection task cycle. SealSuite periodically scans endpoints for sensitive files based on the collection policy. The collected sensitive file information is displayed on the **Discovered files** page in task details.

<span id="hGYdkStgN"></span>
## Creating Data Collection Policy


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, select **DLP** \> **eDiscovery**.

3. Click the **Data Collection Policy** tab, and in the upper right corner, click **Create New Policy**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/802e5f7458ad4964b7da6f2c913a7cfa~tplv-goo7wpa0wc-topic.webp) </span>

4. On the **Add New Policy** page, configure the relevant parameters and click **Confirm**. The parameter description is shown in the table below.

&nbsp;

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Policy Name** |Customize the name to identify the policy. Please ensure the policy name is globally unique.<br><br>The policy name can include Chinese and English characters, numbers, and must contain at least one special character, and can be up to 128 characters long. |
   |**Manage labels (Optional)**  |Select the tags to associate with the current collection policy. The drop\-down list displays only the tags granted to the current administrator.<br><br>To add or adjust the tag options, the super administrator needs to modify the **Manageable Tag Scope** for your administrator role in **Enterprise Settings** \> **Admin Access**. For details, see [Editing Administrator Access](https://docs.byteplus.com/en/docs/sealsuite/docs-editing-or-deleting-administrator). |
   |**Collection Scope** |Collection scope refers to which types of sensitive data are scanned.<br><br>Click  **+**  **Add Data**, and select sensitive files from sensitive data. For methods of configuring sensitive files, refer to [Managing sensitive data](https://docs.byteplus.com/docs/sealsuite/docs-managing-sensitive-data). |
   |**Collection Path** |Click **Collection Path** or **Exclusion Path**, then click **Add Custom Path** to add the corresponding path. Up to 20 paths can be set.<br><br><br>* **Collection Path**: SealSuite will scan the enabled collection path to see if it contains sensitive files.<br><br>* **Exclusion Path**: SealSuite will scan folders outside the exclusion path to see if they contain sensitive files.<br><br><br>Click the delete button on the right side of a path to delete that path. |
   |**Collection Scope** |Supports configuring the file type and file size.<br><br><br>* **File type**: Select the file types to scan. The available options are the same as the file type library in **Data Identification**.<br><br>* **File size**: Set the maximum file size to scan. SealSuite scans only files that are less than or equal to the specified size. |
   |**Collection configuration** |Supports customizing the depth and scope of file parsing to meet deep scanning and forensics requirements. The system provides default global configurations, which can be modified or reset as needed.<br><br><br>* **File content segment reporting configuration**<br><br>   After this feature is enabled, SealSuite extracts and reports relevant content snippets from sensitive files to provide identification evidence and contextual information. You can set the maximum length of a single content snippet and the maximum number of snippets reported for a single file.<br><br>* **File parsing configuration**<br><br>   This feature improves deep parsing capabilities for complex files, such as large files or multi\-layer nested compressed files, to prevent sensitive data from being hidden in packages to evade scanning. It includes the following configuration items.<br><br>   * **Single file content parsing configuration**: Set the maximum file size for deep content parsing by file type. This configuration is designed to prevent client resources from being exhausted when parsing oversized files. For files that exceed the configured size limit, the system may skip deep content scanning.<br><br>   * **Nested file parsing configuration**: Define the maximum depth for parsing multi\-layer compressed files or multi\-layer nested files. After you enable directory structure reporting, alert details include the full path of the sensitive file within the compressed package.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If your custom parsing configuration is higher than the system default configuration, endpoints will perform deep scanning on files again after the policy is delivered. To reduce the impact on endpoint performance, we recommend validating the configuration on a small scale before gradually rolling it out.</div><br> |
   |**Collection period** |* **Collect Now**: SealSuite will immediately start scanning the device to see if it contains sensitive files.<br><br>* **Custom**: Set the repeat frequency and collection period for the collection task. |
   |**Scan performance** |Supports configuring limits on endpoint resources used by the scanning process to reduce the impact on daily endpoint use.<br><br><br>* **Scan process CPU resource limit**: Configure the maximum CPU usage of the scanning process (10% \- 80%).<br><br>* **Scan only when the endpoint device is idle**: After this option is selected, scanning starts if no keyboard or mouse activity is detected on the endpoint within 30 seconds. If keyboard or mouse activity occurs, scanning pauses after the current file is scanned.<br><br>* **Scan only when the terminal device is connected to power**: After this option is selected, scanning does not start when the device is not connected to power. If power is disconnected during scanning, the scan pauses after the current file is completed and the progress is saved. After the device is connected to power again, scanning resumes from the saved progress. |
   |**Scope** |Configure data collection scopes, supporting limiting collection scope by **User** or **Device** dimensions.<br><br><br>* When choosing **User**, you need to restrict the user scope by **Department** or **Role**.<br><br>* When selecting a **Device**, you need to restrict the device's scope through the **Device**, **OS**, and **Group**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Before configuring the data collection policy, please define the user scope by referring to <a href="https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule">Configuring policy for file\-sharing behavior</a> or <a href="https://docs.byteplus.com/docs/sealsuite/Configuring_block_policy_for_application">Configuring block policy for application</a> to define sensitive file sharing policy.</div><br> |
   


 &nbsp;

<span id="hcRbthPe0"></span>
## Managing Data Collection Policy


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, select **DLP** \> **eDiscovery**.

3. Click on the **Data Collection Policy** tab. In the **Policy list**, you can perform the following operations.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93e0a453c9594d509b594b5e54b37728~tplv-goo7wpa0wc-topic.webp) </span>


* **View task status**: View the number of ongoing, completed, and terminated jobs within the policy list.

* **Enable or disable the policy**：In the **Status** area, click the switch to enable or disable the policy.

   * Enable the policy: SealSuite will scan the devices for sensitive files according to the policy.

   * Disable the policy: The policy is disabled.

* **Edit policy**: In the **Actions** column, click **Edit policy** to modify the data collection policy.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After editing the policy, it will not take effect until the next time the task is executed. This does not affect the tasks that are currently running.   </div>
   

* **Copy policy**: Select a task, click **More** \> **Copy** in the **Action** column, then edit the policy parameters, and click **Confirm**.

* **Delete Policy**: Select a task, click **More** \> **Delete** in the **Action** column, and click **Confirm** in the dialog box.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Once the policy is deleted, it cannot be recovered, and SealSuite will no longer continue to check the devices through this policy for files, but the details of already detected sensitive files will still be recorded in the employee's sensitive files detail.   </div>
   

* **Collect now**: For tasks that are not in progress and whose collection frequency is **Collect now**, click **More** \> **Collect Now** in the **Action** column to collect data again.


<span id="hQtqq7kPV"></span>
## View Data Collection Task Details


1. Log in to the Admin Console.

2. In the left navigation pane, choose **DLP** \> **eDiscovery**.

3. Click the **Data Collection Policy** tab. In the data collection policy list, click **View** in the Action column to view the list of all historical execution tasks under the policy.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad95671869104e358eb2fe164bc4a46d~tplv-goo7wpa0wc-topic.webp) </span>

   * **End task**: Click **End Task** in the task **Action** column to terminate an ongoing collection task. After termination, the current task cannot continue. You must wait for the next collection cycle to automatically start a new collection task.

   * **View details**: Click **View details** in the task **Action** column to go to the task execution details dashboard, where you can view the following information.

      * **Basic information**: The upper part of the page displays the user scope, scan path, sensitive data collection scope, excluded object, excluded path, and creation time.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f21f96df2dff4e32b71ae5b57f7528c3~tplv-goo7wpa0wc-topic.webp) </span>

      * **Terminal collection status**: View execution statistics for the endpoints covered by the current task as well as the specific device list. Click **Details** for a device to view its detailed execution status.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb8ee8f3decd42e8901b4fc445bbac93~tplv-goo7wpa0wc-topic.webp) </span>

      * **Discovered files**: View all sensitive files discovered by the current task. Multi\-dimensional filtering by department, employee, device, and file information is supported. Click **Export List** in the upper\-right corner of the list to export sensitive files locally for offline audit.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/648c6c1d582a4a3faf133a8c4b57beb8~tplv-goo7wpa0wc-topic.webp) </span>

         Click **Details** in the file list to further view the details of the matched classification and sensitivity level rules.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f5b99c72df8425fb95f1cd591af7910~tplv-goo7wpa0wc-topic.webp) </span>

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">Note         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3"><strong>Discovered files</strong> are displayed only for clients of version <strong>3.3.11 or later</strong>. Earlier client versions cannot display the file list.         </div>
         

<span id="exporting-security-posture-report"></span>
# Exporting Security Posture Report

Security posture report refers to the report used by enterprises to track and monitor their data leakage prevention measures and policies, including information on coverage of DLP policies, data discovery, and risk of data leak. This security posture report can help you understand the current situation and trends of enterprise data security, and identify data protection measures and strategies that need improvement.


1. Log in to the Admin Console.

2. In the left navigation bar, click **Dashboard**. On the **Dashboard**, click **Security** \> **DLP**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f31dbdc1c69944cf8ed0d7b29a419a20~tplv-goo7wpa0wc-topic.webp) </span>

3. (Optional) Above the security posture report, enter the department name and select the audit time to filter the report results.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Time filtering does not affect the data in the <strong>Coverage of DLP policies</strong> section.   </div>
   

4. On the right of the **DLP** tab, click **Export Report** to export a PDF file.
