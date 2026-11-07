---
title: "Configuring data collection policy"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/Configuring_data_collection_policy"
---

SealSuite will regularly scan the devices to check if they contain sensitive files based on the collection policy. You can create a data collection policy, which includes the range of data types, the path of data collection, and the collection period. The sensitive file information collected will be displayed on the pages for leak investigation, sensitive data landscape, and insider risk.

<span id="da1420de"></span>
# Creating data collection policy


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, select **DLP** \> **eDiscovery**.

3. Click the **Data Collection Policy** tab, and in the upper right corner, click **Create New Policy**.

4. On the **Add New Policy** page, configure the relevant parameters and click **Confirm**. The parameter description is shown in the table below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/802e5f7458ad4964b7da6f2c913a7cfa~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Policy Name** |Customize the name to identify the policy. Please ensure the permission policy name is globally unique.<br><br>The policy name can include Chinese and English characters, and numbers, and must contain at least one special character, and can be up to 128 characters long. |
   |**Collection Scope** |Collection scope refers to which types of sensitive data are scanned.<br><br>Click **Add New Sensitive File**, and select sensitive files from sensitive data. For methods of configuring sensitive files refer to [Managing sensitive data](https://docs.byteplus.com/docs/sealsuite/docs-managing-sensitive-data). |
   |**Collection Path** |Click **Collection Path** or **Exclusion Path**, then click **Add Custom Path** to add the corresponding path. Up to 20 paths can be set.<br><br><br>* **Collection Path**: SealSuite will scan the enabled collection path to see if it contains sensitive files.<br><br>* **Exclusion Path**: SealSuite will scan folders outside the exclusion path to see if they contain sensitive files.<br><br><br>Click the delete button on the right side of a path to delete that path. |
   |**Collection time** |* **Collect Now**: SealSuite will immediately start scanning the device to see if it contains sensitive files.<br><br>* **Custom**: Set the repeat frequency and collection period for the collection task. |
   |**Scope** |Configure data collection scopes, supporting limiting workflow scope by **User** or **Device** dimensions.<br><br><br>* When choosing **User**, you need to restrict the user scope by **Department** or **Role**.<br><br>* When selecting a **Device**, you need to restrict the device's scope through the **Device**, **OS**, **Group**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Before configuring the data collection policy, please define the user scope <a href="https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule">Configuring policy for file\-sharing behavior</a> or <a href="https://docs.byteplus.com/docs/sealsuite/Configuring_block_policy_for_application">Configuring block policy for application</a> to define sensitive file sharing policy.</div><br> |
   


<span id="54b6c439"></span>
# Managing data collection policy


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, select **DLP** \> **eDiscovery**.

3. Click on the **Data Collection Policy** tab. In the **Policy list**, you can perform the following operations.

   
   |**Task** |**Description** |
   |---|---|
   |View task details |View the number of ongoing, completed, and terminated jobs within the policy list. |
   |Enable or disable the policy |In the **Status** area, click the switch to enable or disable the policy.<br><br><br>* Enable the policy: SealSuite will scan the devices for sensitive files according to the policy.<br><br>* Disable the policy: The policy is disabled. |
   |View Job |In the **Action** column, click **View**, on the **Task Details** page, you can perform the following operations:<br><br><br>* View task details, including execution time, status, collection progress (number of devices Completed/total number of collections), etc.<br><br>* Click **Device Details** to view the list of devices for the job, including devices that have completed collection and devices that have not finished collection.<br><br>* On the **Device Details** page, click **View Local Sensitive Files** to view the details of local sensitive files on that device.<br><br>* Click **End Task** to terminate the ongoing **Running** collection job. After termination, this task cannot continue, and you must wait for the next collection period to automatically initiate a collection job. |
   |Edit routing policy |In the **Actions** column, click **Edit** to modify the data collection policy.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After editing the policy, it will not take effect until the next time the task is executed. This does not affect the tasks that are currently running.</div><br> |
   |Collect again |For tasks that are not **Running** and have a collection frequency set as **Collect Now**, you can click **Collect Now** in the **Action** column to collect the data again. |
   |Copy policy |Select a task, click\*\*...\*\* in the **Action** column, select **Copy**, and edit the policy parameters, and click **Confirm**. |
   |Delete Policy |Select a task, click\*\*...\*\* in the **Action** column, select **Delete**, and click **OK** in the confirm dialog box.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Once the policy is deleted, it cannot be recovered, and SealSuite will no longer continue to check the devices through this policy for files, but the detail of already detected sensitive files will still be recorded in the employee's sensitive files detail.</div><br> |
