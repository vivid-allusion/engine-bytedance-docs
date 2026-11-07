---
title: "Managing DataFlow policies"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Managing_DataFlow_policies"
---

This topic explains how to create, edit, and delete DataFlow policies.

<span id="a5e5b655"></span>
## Background information

DataFlow policies enable automatic metadata and data import, data export, and data eviction.


|**Feature** |**Description** |
|---|---|
|Import |* Description: This feature synchronizes Torch Object Storage (TOS) write, modify, and delete operations with FileNAS. It allows you to import data with high\-performance semantic file access requirements into the file system beforehand.<br><br>* Trigger condition: Once the **Import rule** is set in the DataFlow policy, FileNAS continuously monitors data and triggers import tasks for any TOS actions — writes, modifications, or deletions — automatically synchronizing these changes to FileNAS. |
|Export |* Description: This feature automatically synchronizes write, modify, and delete operations in the file system with the TOS bucket, enabling data protection, aggregation, and transmission.<br><br>* Trigger condition: When the **Settlement rule** is set in the DataFlow policy, FileNAS continuously monitors data and triggers export tasks for any FileNAS actions — writes, modifications, or deletions — automatically synchronizing these changes to TOS. |
|Eviction |* Description: This feature removes rarely used data in the file system, freeing up space and lowering storage costs. The file's data blocks will be cleared, but metadata will be retained. By default, the eviction process preserves data that has been modified in the file system.<br><br>* Trigger condition: Once the **Eviction rule** is set in the DataFlow policy, FileNAS continuously monitors data and triggers eviction tasks for any data meeting the specified conditions. |


<span id="6ef447b5"></span>
## Prerequisites


* You have created a Cache FileNAS file system. For instructions, see [Creating file systems](https://docs.byteplus.com/docs/nas/Creating_file_systems).

* You have created a TOS bucket in the same region as the file system. For instructions, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).


<span id="87eff02b"></span>
## Notes


|**Category** |**Description** |
|---|---|
|Quantity |* A single FileNAS file system supports up to 20 DataFlow policies.<br><br>* A single FileNAS file system directory path can only connect to one TOS bucket for DataFlow.<br><br>* Mapping nested FileNAS directories to TOS buckets is not supported. |
|TOS bucket restrictions |* Deleting objects<br><br>   TOS serves as the backend storage for DataFlow. Deleting files in TOS can result in data loss for FileNAS and cause errors when loading files on demand. Exercise extreme caution when deleting files in TOS and when using TOS lifecycle feature which automatically deletes files.<br><br>* Bucket type<br><br>   * Creating DataFlow policies for TOS HNS buckets is not supported.<br><br>   * DataFlow only supports the on\-demand loading, importing, and exporting of data stored in TOS **Standard Storage**. All other TOS storage types, including Archive and Cold Archive, are incompatible with DataFlow operations. If a DataFlow policy is associated with a TOS bucket containing Archive or Cold Archive data, you must fully restore the archived data. Failure to do so will result in:<br><br>      * Errors when attempting to load archived data on demand.<br><br>      * Failures to synchronize TOS data.<br><br>      * Additional charges for reading or writing TOS archived or cold archived data. |
|Data synchronization delay |After the import and export rules are enabled, FileNAS continuously monitors data changes. However, there is a minute\-level delay between a data change and the execution of import or export operations, which can vary with cluster workload. Therefore, we cannot guarantee the maximum synchronization delay. |


<span id="899321e9"></span>
## Creating DataFlow policies


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where you want to create a DataFlow policy.

3. In the left navigation pane, select **File System** \> **DataFlow**.

4. On the **Policy** tab, click **Create policy**.

5. On the **Create DataFlow policy** page, set the following parameters.

   
   |**Category** |**Parameter** |**Description** |
   |---|---|---|
   |Basic information |DataFlow policy name |Enter a name for the DataFlow policy. The name must:<br><br><br>* Not be empty.<br><br>* Not start with a number or a hyphen (\-).<br><br>* Contain only Chinese characters, letters, numbers, underscores (_), or hyphens (\-).<br><br>* Be between 1 and 128 characters long. |
   |File storage path |File System |Select the file system you wish to create a DataFlow policy for. Currently, only Cache FileNAS file systems are supported. |
   ||File System path |Specify the directory path in the file system where TOS data will be stored. The following constraints apply:<br><br><br>* The directory must be empty. Non\-empty directories are not allowed.<br><br>* The directory cannot be the root directory.<br><br>* The path must be an absolute path, which starts and ends with a forward slash (/).<br><br>* The parent directory must be an existing directory.<br><br>* The path cannot exceed 8 directory levels.<br><br>* The length should be between 3 and 1,024 characters.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Nested paths across DataFlow policies are not supported.</div><br> |
   |Object storage path |Bucket name |Select the TOS bucket with which you want to associate the file system. |
   ||Versioning status |Once you select a TOS bucket, its versioning status will be shown automatically. |
   ||Bucket prefix |Set a prefix for data transfers between the TOS bucket and the file system so that only files with this prefix are transferred to FileNAS. The prefix should:<br><br><br>* Start and end with a forward slash (/), for example `/prefix/`.<br><br>* Be between 2 and 1,024 characters long.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If no prefix is set, all data from the bucket flows to FileNAS by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot bind another DataFlow policy to any sub\-prefix under a prefix if a DataFlow policy is already bound to that prefix in the bucket.</div><br> |
   ||Cross service authorization |Before data can flow between FileNAS and TOS, you must complete cross\-service authorization. Once authorized, a service\-linked role named FileNASAccessTOSRole is automatically created to enable mutual access between TOS and FileNAS.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not change or turn off cross\-service authorization after you enable it. Otherwise, the DataFlow feature will not work properly.</div><br> |
   |Flow rules |File conflict policy |Select the file conflict policy for import or export tasks:<br><br><br>* **Keep the latest files**: For files with the same name, FileNAS compares the timestamps of the last modification between the TOS and FileNAS versions and only imports or exports the newer version. Overwritten files cannot be recovered. If both versions have the same timestamp, FileNAS skips the file.<br><br>* **Skip files with the same name**: FileNAS automatically skips files with the same name in TOS and FileNAS during import or export tasks. In other words, import or export operations are not performed on files with identical names. |
   ||Import rule |Set rules for automatic import from TOS to FileNAS:<br><br><br>* **Automatic import range**: Select **Only metadata** or **Metadata and data**.<br><br>* **Warm up trigger condition**: By default, imports are triggered when you **create and modify objects**. Optionally, you can enable import triggering for **object deletion** events.<br><br>* **File delete range**: If **Warm up trigger condition** is set to **Delete object**, select the range of files to be synchronized and deleted from file storage. Options:<br><br>   * **All documents (including complete and incomplete documents)** <br><br>   * **Incomplete files (files with metadata only)**  |
   ||Settlement rule |Set rules for automatic export from FileNAS to TOS:<br><br><br>* **Automatic settlement rule**: Select **non\-settling** or **immediate settlement**.<br><br>* **Settling trigger condition**: When you select **immediate settlement** for **Automatic settlement rule**, the Settling trigger condition option appears. **Create and modify files** and **Delete file** are selected by default.<br><br>* **Object version control**: When you select **Delete file** for **Settling trigger condition**, you have the following options:<br><br>   * **Only completely delete the latest version of the associated object**<br><br>   * **Only completely delete the specified version of the associated object**<br><br>   * **Completely delete all versions of associated objects** |
   ||Eviction rules |Set rules for automatically evicting data from FileNAS:<br><br><br>* **Automatic eviction rule**: Select **No eviction** or **Custom**.<br><br>* **Eviction metrics**: When you select **Custom** for **Automatic eviction rule**, you must configure **Eviction metrics**. There are two options available for the data eviction range:<br><br>   * **AccessTime** (Required): Files with a last access time **greater than or equal to** a specified value will be removed. The available time ranges are as follows:<br><br>      * **Hour**: Enter an integer between 1 and 8,760.<br><br>      * **Day**: Enter an integer between 1 and 365.<br><br>      * **Week**: Enter an integer between 1 and 52.<br><br>      * **Month**: Enter an integer between 1 and 12.<br><br>      * **Year**: Only the value 1 is supported.<br><br>   * **SubDirectory** (Optional): Click **add** and enter the directory path. Files that are older than the specified time and that are located outside the specified subdirectories will be deleted. The following constraints apply:<br><br>      * You can only enter subdirectories that already exist within the specified **File System path**.<br><br>      * The path must end with a forward slash (/).<br><br>      * The path cannot exceed 8 directory levels.<br><br>      * You can add up to 20 subdirectories.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If a file in FileNAS is updated and meets the eviction rules, it will first be exported to TOS and then deleted.</div><br> |
   |Log analysis |Torch Log Service Cross\-service authorization |After enabling and authorizing this feature, you can query and analyze data transfer records of the policy in real time. To view DataFlow logs, see [Viewing DataFlow logs](https://docs.byteplus.com/en/docs/nas/Viewing_DataFlow_logs).<br><br>If the page displays **Not activated**, you can click **Go activate** to enable Torch Log Service (TLS) and authorize FileNAS to access TLS. |
   |Log analysis |Log analysis |If cross\-service authorization for TLS is enabled, the log analysis feature will be activated automatically.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can use the toggle switch to turn this feature off at any time.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Activating log analysis is free. However, TLS will bill you separately for any usage generated after activation. For billing details, see <a href="https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode">TLS billing overview</a>.</div><br> |
   

6. After completing the settings, click **Confirm**.


<span id="7592501c"></span>
## Editing DataFlow policies


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region of the DataFlow policy you want to manage.

3. In the left navigation pane, select **File System** \> **DataFlow**.

4. On the **Policy** tab, click the name of the policy.

5. On the **Overview** tab, make the necessary changes.

   
   <Tabs>
   <Tab zoneid="BQMVfcLkBJ" title="Edit file conflict policy">
   <TabTitle>Edit file conflict policy</TabTitle>
   
   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="0">tip</div>
   
   
   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">Stop the import and export rules first before editing the file conflict policy. Otherwise, editing is not allowed.</div>
   
   
   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">Stop the import rule and wait 60 seconds before restarting it. The export rule supports immediate restart after stopping, with no cooldown period required.</div>
   
   
   1. Stop the import rule and export rule.
   
      1. Select the **Import rule** tab, and click **Stop** at **Rule status**.
   
      2. In the dialog box, click **OK**.
   
      3. Follow the above steps to stop the export rule under the **Export rule** tab.
   
   2. Edit the file conflict policy when the **Rule status** of both the import and export rules is **Stopped**.
   
      1. Click the edit icon next to **File conflict policy**.
   
      2. Select the policy in the dialog box and click **OK**.
   
   3. Enable the import rule or export rule to apply the configuration.
   
      1. Select the **Import rule** tab, and click **Enable** at **Rule status**.
   
      2. In the dialog box, click **OK**.
   
      3. Follow the above steps to enable the export rule under the **Export** rule tab.
   
   
   </Tab>
   <Tab zoneid="hLdQSz28oW" title="Edit DataFlow rules">
   <TabTitle>Edit DataFlow rules</TabTitle>
   
   Editing rules for import, export and eviction follows a similar process. This section explains the steps for editing DataFlow rules using import rules as an example.
   
   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="0">tip</div>
   
   
   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">Stop the rule before editing. Otherwise, editing is not allowed.</div>
   
   
   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">Stop the import rule and wait 60 seconds before restarting it. The export rule supports immediate restart after stopping, with no cooldown period required.</div>
   
   
   1. Stop the import rule.
   
      1. Select the **Import rule** tab, and click **Stop** at **Rule status**.
   
      2. In the dialog box, click **OK**.
   
   2. Modify the import rule when its **Rule status** is **Stopped**.
   
      1. Click the edit icon at **Import rule**.
   
      2. In the box that appears, make the necessary changes and click **OK**.
   
         After modification, FileNAS automatically starts the DataFlow rule without requiring manual intervention.
   
   
   </Tab>
   </Tabs>
   


<span id="e6fb08be"></span>
## Deleting DataFlow policies

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To delete a DataFlow policy, first stop all flow rules under it. Otherwise, deletion is not allowed.</div>


* <div data-tips="true" data-tips-type="warning">Currently, DataFlow only supports TOS Standard Storage. You cannot delete a DataFlow policy if files in the associated TOS bucket or with specified prefixes have been moved to a different TOS storage type.</div>


1. Stop all DataFlow rules.

   1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

   2. In the top menu bar, select the region of the DataFlow policy you want to manage.

   3. In the left navigation pane, select **File System \> DataFlow**.

   4. On the **Policy** tab of the **DataFlow** page, click **Stop** in the **Actions** column of the policy.

   5. In the **Stop DataFlow policy** dialog box, select all DataFlow rules, enter "confirm", and click **OK**.

2. Delete the DataFlow policy.

   1. On the **Policy** tab of the **DataFlow** page, click **Delete** in the **Actions** column of the policy.

   2. Set the following parameters in the dialog box.

      
      |**Parameter** |**Description** |
      |---|---|
      |Select delete rule |Select delete rules for files in the associated file system directory:<br><br><br>* **Warm up all files in the File System associated directory and delete policy**: After selecting this option, you can configure file retention ranges based on the last access timestamps. Files outside the retention range will be deleted and cannot be recovered.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Deleting a DataFlow policy automatically exports the latest versions of all files to be retained, including metadata\-only loaded files. Please delete unnecessary files before export to save storage space.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">DataFlow policy deletion will fail if the file system directory has a restricted directory quota and reaches its limit. Increase the directory quota limits before deleting the DataFlow policy. For more information, see <a href="https://docs.byteplus.com/docs/nas/Managing_directory_quotas#ec5b9ecb">Restricted directory quota</a>.   </div><br>   <br><br>* **Delete all files in the File System associated directory delete policy**: Selecting this option will delete the chosen DataFlow policy and all files in the associated file system directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Data cannot be recovered after deletion. Please create a new export task to save data to TOS before deleting.   </div><br>    |
      |Synchronize delete the policy for Torch Log Service TLS Projects and Topics |Select whether to delete the TLS project and topic associated with this policy at the same time. Log storage fees will keep adding up if you do not delete them. It's best to do it all at once. |
      |Delete confirm |Enter the ID of the DataFlow policy you want to delete in the input box. |
      

   3. Click **OK**.


<span id="2eeff267"></span>
## Other operations


|**Operation** |Steps |
|---|---|
|View DataFlow policy details |1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).<br><br>2. In the top menu bar, select the region of the DataFlow policy you want to manage.<br><br>3. In the left navigation pane, select **File System** \> **DataFlow**.<br><br>4. On the **Policy** tab of the **DataFlow** page, click the target policy to view the file system ID, file system path, bucket name, and other details. |
|Stop a DataFlow policy |1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).<br><br>2. In the top menu bar, select the region of the DataFlow policy you want to manage.<br><br>3. In the left navigation pane, select **File System** \> **DataFlow**.<br><br>4. On the **Policy** tab of the **DataFlow** page, click **Stop** in the **Actions** column of the policy.<br><br>5. In the **Stop DataFlow policy** dialog box, select the flow rule you wish to stop, enter **confirm**, and click **OK**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To stop a DataFlow rule, you can also go to the <strong>DataFlow</strong> page, click the target policy under the <strong>Policy</strong> tab, click <strong>Stop</strong> at <strong>Rule statu</strong>s under the rule tabs in the <strong>Flow rules</strong> section, then click <strong>OK</strong> in the dialog box.   </div><br>    |
|Start a DataFlow policy |1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).<br><br>2. In the top menu bar, select the region of the DataFlow policy you want to manage.<br><br>3. In the left navigation pane, select **File System** \> **DataFlow**.<br><br>4. On the **Policy** tab of the **DataFlow** page, click **Start** in the **Actions** column of the policy.<br><br>5. In the **Start DataFlow policy** dialog box, select the DataFlow rule to enable, enter **confirm**, and click **OK**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To activate a DataFlow rule, you can also go to the <strong>DataFlow</strong> page, click the target policy under the <strong>Policy</strong> tab, click <strong>Enable</strong> at <strong>Rule status</strong> under the rule tabs in the <strong>Flow rules</strong> section, then click <strong>OK</strong> in the dialog box.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the eviction rules are set to no eviction, customize them before enabling.   </div><br>    |


&nbsp;
