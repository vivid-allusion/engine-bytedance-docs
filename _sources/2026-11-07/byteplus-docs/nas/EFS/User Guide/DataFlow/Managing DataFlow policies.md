---
title: "Managing DataFlow policies"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Managing_DataFlow_policies"
---

This topic explains how to manage DataFlow policies, including how to create, edit, and delete them.

<span id="530cBX2J"></span>
## Background information

DataFlow policies enable automatic metadata and data import, data export, and data eviction. Specifically:


|Feature |Description |Trigger condition |
|---|---|---|
|Import |This feature synchronizes TOS write and delete operations with EFS. It allows you to import data with high\-performance semantic file access requirements into the file system beforehand. |Once the **Import rule** is set in the DataFlow policy, EFS continuously monitors data and triggers import tasks for any TOS actions—writes, modifications, or deletions—automatically synchronizing these changes. |
|Export |This feature automatically synchronizes write, modify, and delete operations in the file system with the TOS bucket, enabling data protection, aggregation, and transmission. |When the **Export rule** is set to **Immediate export** or **Periodic export** in the DataFlow policy, EFS continuously monitors data and triggers export tasks for any EFS actions—including writes, modifications, or deletions—synchronizing these changes either immediately or at regular intervals. |
|Eviction |This feature removes rarely used data in the file system, freeing up space and lowering storage costs. The file's data blocks will be cleared, but metadata will be retained. |Once the **Eviction rules** are set in the DataFlow policy, EFS continuously monitors data and triggers eviction tasks for any data meeting the specified conditions. |


<span id="hgQLhtsU"></span>
## Creating DataFlow policies

<span id="hgQLhtsU"></span>
### Prerequisites


* You have created an EFS file system. For details, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems).

* You have created a TOS bucket in the same region as the file system. For instructions, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).


<span id="gFBKodJ0"></span>
### Steps


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the File System page, click the file system you want to manage.

5. In the left navigation pane, click **DataFlow**.

6. On the **DataFlow** page, select the **Policy** tab.

7. Click **Create policy**, and configure the parameters in the **Create DataFlow policy** panel.

   * **Basic information**

      
      |Parameter |Description |
      |---|---|
      |DataFlow Name |Enter a name for your DataFlow policy. The policy name must:<br><br><br>* Start with letters or Chinese characters.<br><br>* Contain only letters, Chinese characters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* Be between 1 and 128 characters long. |
      

   * **File storage path**

      
      |**Parameter** |**Description** |
      |---|---|
      |File System |Displays the ID of the EFS file system for which you are creating a DataFlow policy. This field is auto\-filled and non\-editable. |
      |File System path |Set the path in the current file system for which you want to enable data synchronization. The following constraints apply:<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">Make sure that the directory path is correct. If the directory does not exist, EFS will automatically create it.</div><br><br><br><br>* The path must be an absolute path, which starts and ends with a forward slash (/).<br><br>* The directory cannot be the root directory.<br><br>* The parent directory must be an existing directory.<br><br>* The path cannot exceed 8 directory levels.<br><br>* The length must be between 3 and 1,024 characters.<br><br>* The path cannot overlap with the path of any other policy. |
      

   * **Object storage path**

      
      |**Parameter** |**Description** |
      |---|---|
      |Bucket list |Select the TOS bucket for which you want to enable data synchronization. |
      |Versioning status |Once you select a TOS bucket, its versioning status will be shown automatically. |
      |Bucket prefix |Specify a prefix in the selected TOS bucket for data synchronization with the file system. This ensures that only the data under this prefix is synchronized with EFS. The prefix should:<br><br><br>* Start and end with a forward slash (/).<br><br>* Be between 2 and 1,024 characters long.<br><br>* Not be nested within prefixes defined by other policies.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not specify a prefix, EFS uses the root directory of the TOS bucket.</div><br> |
      |TOS cross\-service authorization |Before data can flow between EFS and TOS, you must complete cross\-service authorization. Once authorized, a service\-linked role named `EFSAccessTOSRole` is automatically created to enable mutual access between TOS and EFS.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not change or turn off cross\-service authorization after you enable it. Otherwise, the DataFlow feature will not work properly.</div><br> |
      

   * **Flow rules**

      
      |**Parameter** |**Description** |
      |---|---|
      |File conflict policy |**Preserve Latest Files**. EFS compares the timestamps of the last modification between the TOS and EFS versions when importing or exporting files with the same name. Only the newer version is retained. Overwritten files cannot be recovered. If both versions have the same timestamp, EFS skips the file. |
      |Import rule |Set rules for automatic import from TOS to EFS:<br><br><br>* **Automatic import range**: **Metadata**, or **metadata and data**.<br><br>* **Import trigger condition**: By default, imports are triggered when you **create and modify objects**. Optionally, you can enable import triggering for **Delete** **object** events.<br><br>* **File delete range**: If **Import trigger condition** is set to **Delete object**, select the range of files to be synchronized and deleted from file storage. Options:<br><br>   * **All documents (including complete and incomplete documents)** <br><br>   * **Incomplete files (files with metadata only)**  |
      |Export rule |Set **rules for automatic export** from EFS to TOS:<br><br><br>* **No export**: No export operation is performed.<br><br>* **Immediate export**: EFS immediately synchronizes write and modify actions in the specified file system path to TOS. Options for **Export trigger condition**:<br><br>   * **Create and modify files** (Default)<br><br>   * **Delete file**: When you select this option, the system will check the file version. The export operation is only triggered if the file version in the file system is newer than the version in the TOS bucket. Options:<br><br>      * **Only completely delete the latest version of the associated object**<br><br>      * **Only completely delete the specified version of the associated object**<br><br>      * **Completely delete all versions of associated objects**<br><br>* **Periodic export**: EFS synchronizes write and modify actions in the specified file system path at set intervals with TOS.<br><br>   * **Export period**: Set the export interval. The available time ranges are as follows:<br><br>      * **Hour**: Enter an integer between 4 and 8,760.<br><br>      * **Day**: Enter an integer between 1 and 365.<br><br>      * **Week**: Enter an integer between 1 and 52.<br><br>      * **Month**: Enter an integer between 1 and 12.<br><br>      * **Year**: Only the value 1 is supported.<br><br>   * **First settlement time**: Choose the first export time.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The selected time must be on the hour.      </div><br>      <br><br>   * **Export directory**: Select the directories that should be included in the periodic export. Options:<br><br>      * **All**: Exports all data under the file system directory path.<br><br>      * **Include**: Exports only the data in the specified directories.<br><br>      * **Exclude**: Exports all data except for that in the specified directories.<br><br>      When selecting **Include** or **Exclude**, click **Add subdirectory** and enter the directory path. The following constraints apply:<br><br>      * You can only enter subdirectories that already exist within the specified **File System path**.<br><br>      * The path must end with a forward slash (/).<br><br>      * The path cannot exceed 8 directory levels.<br><br>      * You can add up to 20 subdirectories. |
      |Eviction rule |Set rules for automatically evicting data from EFS:<br><br><br>* **No eviction**: Data stays in the file system and will not be evicted.<br><br>* **Custom**: There are two options available for data eviction range:<br><br>   * **Last access time** (Required): Files with a last access time **greater than or equal to** a specified value will be removed. The available time ranges are as follows:<br><br>      * **Hour**: Enter an integer between 1 and 8,760.<br><br>      * **Day**: Enter an integer between 1 and 365.<br><br>      * **Week**: Enter an integer between 1 and 52.<br><br>      * **Month**: Enter an integer between 1 and 12.<br><br>      * **Year**: Only the value 1 is supported.<br><br>   * **Subdirectory not included** (Optional): Click **Add subdirectory** and enter the directory path. Files that are older than the specified time and that are located outside the specified subdirectories will be deleted. The following constraints apply:<br><br>      * You can only enter subdirectories that already exist within the specified **File System path**.<br><br>      * The path must end with a forward slash (/).<br><br>      * The path cannot exceed 8 directory levels.<br><br>      * You can add up to 20 subdirectories.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a file in EFS is updated and meets the eviction rules, it will first be exported to TOS and then deleted.   </div><br>    |
      

   * **Log analysis**

      
      |Parameter |Description |
      |---|---|
      |TLS cross\-service authorization |After enabling and authorizing this feature, you can query and analyze data flow records of the policy in real time. To view DataFlow logs, see [Viewing DataFlow logs](https://docs.byteplus.com/en/docs/nas/efs_Viewing_DataFlow_logs?lang=en).<br><br>If the page says that Torch Log Service (TLS) is **Not yet open**, click **To open** to activate TLS and allow EFS access. |
      |Log analysis |If cross\-service authorization for TLS is enabled, the log analysis feature will be activated automatically.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can use the toggle switch to turn this feature off at any time.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Activating log analysis is free. However, TLS will bill you separately for any usage generated after activation. For billing details, see <a href="https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode">TLS billable items</a>.</div><br> |
      

8. Click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Creating the DataFlow policy may take a few minutes. Thank you for your patience.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you enter an invalid path, the DataFlow policy cannot be created.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Once you have successfully created a policy, you can view its details on the <strong>DataFlow</strong> \> <strong>Policy</strong> tab.   </div>
   

   <span id="aLlbAXhd"></span>
   ## Enabling DataFlow policy rules

   <span id="DxqmdEls"></span>
   ### Prerequisites

   You have created a DataFlow policy with the corresponding rule, and the rule is **Disabled**.

   <span id="uIIOX16D"></span>
   ### Steps

   1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, click **DataFlow**.

6. On the **DataFlow** page, select the **Policy** tab.

7. Click **Enable** in the **operation** column of the DataFlow policy you want to manage.

8. In the **Enable DataFlow rule** dialog, configure the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Import |This option only applies when an import rule is configured and is currently **Disabled**.<br><br>Once you enable it, any updates to the TOS bucket will automatically be synchronized with the file system. If directory quotas are active, be sure to manage capacity as needed. |
   |Export |This option only applies when an export rule is configured and is currently **Disabled**.<br><br>Once you enable it, any updates to the file system will automatically be synchronized with the TOS bucket. |
   |Evict |This option only applies when an eviction rule is configured and is currently **Disabled**.<br><br>When enabled, data in the file system will be deleted according to that rule. |
   |Confirm |After selecting the rule(s) you want, enter **Confirm** in the input box. |
   

9. Click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can only enable a DataFlow rule after all ongoing tasks associated with the corresponding file system directory have been completed.   </div>
   

   <span id="GBQYsbFV"></span>
   ## Disabling DataFlow policy rules

   <span id="wbiQRvaO"></span>
   ### Prerequisites

   You have created a DataFlow policy with the corresponding rule, and the rule is **Running**.

   <span id="MiEKW7Lt"></span>
   ### Steps

   1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, click **DataFlow**.

6. On the **DataFlow** page, select the **Policy** tab.

7. Click **Disable** in the **operation** column of the DataFlow policy you want to manage.

8. In the **Disable DataFlow rule** dialog, configure the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Import |This option only applies when an import rule is configured and is currently **Running**.<br><br>Disabling it will stop updates to the TOS bucket from being synchronized with the file system. |
   |Export |This option only applies when an export rule is configured and is currently **Running**.<br><br>Disabling it will stop updates to the file system from being synchronized with the TOS bucket. |
   |Evict |This option only applies when an eviction rule is configured and is currently **Running**.<br><br>When disabled, data in the file system will not be deleted according to that rule. If directory quotas are active, be sure to manage capacity as needed. |
   |Confirm |After selecting the rule(s) you want, enter **Confirm** in the input box. |
   

9. Click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can only disable a DataFlow rule after all ongoing tasks associated with the corresponding file system directory have been completed.   </div>
   

   <span id="aLlbAXhd"></span>
   ## Editing DataFlow policies

   <span id="etds1aDA"></span>
   ### Prerequisites

   You have created a DataFlow policy and all its corresponding rules are **Disabled**.

   <span id="LDSjcbXZ"></span>
   ### Steps

   1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, click **DataFlow**.

6. On the **DataFlow** page, select the **Policy** tab.

7. Click the name of the policy you want to edit. This will open its details page.

8. On the **Overview** tab, make the necessary changes.

   
   |Operation |Steps |
   |---|---|
   |Edit a DataFlow rule |These operations are only available when the rule is **Disabled**:<br><br><br>2. In the **Flow rules** area, click **edit** in the **operation** column of the rule.<br><br>3. Adjust the settings in the edit panel.<br><br>4. Click **OK**. |
   |Enable or disable a DataFlow rule |In the **Flow rules** area, click **Running** or **Disabled** in the **Rule status** column of the rule.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">If you have not set up the corresponding rule when creating the policy, click <strong>Disabled</strong>. You can then adjust the settings in the edit panel to enable the rule.</div><br> |
   

   <span id="QAZgoNqe"></span>
   ## Deleting DataFlow policies

<span id="gw0MYkKu"></span>
### Notes

Currently, DataFlow only supports TOS Standard Storage. Do not move files within the associated TOS bucket or files with the specified prefix to other TOS storage types. Otherwise, deleting the DataFlow policy may result in the forcible removal of these files from EFS.

<span id="gw0MYkKu"></span>
### Prerequisites


* You have created a DataFlow policy and all its corresponding rules are **Disabled**.

* There are no ongoing tasks associated with the corresponding file system directory.


<span id="s55q2bFG"></span>
### Steps


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, click **DataFlow**.

6. On the **DataFlow** page, select the **Policy** tab.

7. Click **Delete** in the **operation** column of the DataFlow policy you want to remove. Then, configure the following parameters in the box that appears.

   
   |Parameter |Description |
   |---|---|
   |Select delete rule |Select the rule for deleting files within the file system associated directory:<br><br><br>* **Retain all files in the File System associated directory**: This option configures file retention ranges based on the last access timestamps. Files outside the retention range will be deleted and cannot be recovered.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Deleting a DataFlow policy automatically exports all files to be retained to their latest versions, including metadata\-only loaded files. Please delete unnecessary files before export to save storage space.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">DataFlow policy deletion will fail if the file system directory has restrictive directory quotas and reaches its limit. Increase the directory quota limits before deleting the DataFlow policy. For more information, see <a href="https://docs.byteplus.com/en/docs/nas/efs_Managing_directory_quotas">Managing directory quotas</a>.   </div><br>   <br><br>* **Delete all files in the File System associated directory**: Selecting this option will delete the chosen DataFlow policy and all files in the file system associated directory.<br><br>   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Deleting files is a high\-risk operation that permanently removes both metadata and data. This action is irreversible, and deleted files cannot be recovered. Therefore, we recommend exporting any data you wish to keep to TOS before deleting.   </div><br>    |
   |Only retain the AccessTime less than |If you set the delete rule to **Retain all files in the File System associated directory**, you can select a time range and keep only the files that were last accessed before the specified time. All other files will be permanently deleted and cannot be recovered. The available time range is as follows:<br><br><br>* **Hour**: Enter an integer between 4 and 8,760.<br><br>* **Day**: Enter an integer between 1 and 365.<br><br>* **Week**: Enter an integer between 1 and 52.<br><br>* **Month**: Enter an integer between 1 and 12.<br><br>* **Year**: Only the value 1 is supported. |
   |Delete confirm |Enter the ID of the DataFlow policy you want to delete in the input box. |
   

8. Click **OK**.

   <span id="aLlbAXhd"></span>
   ## Related operations


|**Operation** |**Steps** |
|---|---|
|View DataFlow policy details |* On the DataFlow **Policy** tab, view details about policies, including **Policy name/ID**, **Status**, **File System path**, and **Running associated tasks**.<br><br>* On the DataFlow **Policy** tab, click the name of a policy to access its **Overview** tab. There, you can view **Basic information**, **Conflict policy**, and **Flow rules**. |
|Rename a DataFlow policy |After creating a DataFlow policy, you can change its name. Steps:<br><br><br>1. On the DataFlow **Policy** tab, hover over the policy name, and click the edit icon that appears.<br><br>2. In the box that appears, enter the new policy name.<br><br>3. Click **Save**. |
