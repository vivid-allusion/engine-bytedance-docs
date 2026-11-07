---
title: "Managing DataFlow tasks"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Managing_DataFlow_tasks"
---

This topic explains how to manage DataFlow tasks, including how to create them and perform related operations.

<span id="fv0WjpQF"></span>
## Background information


* DataFlow tasks execute immediately upon creation and run only once.

* EFS allows three types of DataFlow tasks: Import, Export, and Eviction. Specifically:

   * **Import task**: Loads metadata and data from TOS to EFS. It proactively caches data that requires high\-performance file access into the file system.

   * **Export task**: Synchronizes data written to or modified in the file system to TOS. Running export tasks on a periodic basis supports data protection, aggregation, and transfer.

   * **Eviction task**: Removes rarely used data in the file system, freeing up space and lowering storage costs. After data eviction, the data blocks are cleared, while the metadata remains retained.


<span id="qiv1nZlS"></span>
## Prerequisites

An EFS file system has been created and is **Running**. For instructions, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems).

<span id="4KNP8nri"></span>
## Creating import tasks


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, click **DataFlow**.

6. On the **DataFlow** page, select the **Task** tab.

7. Click **Create task**, and configure the parameters in the **Create DataFlow task** panel.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Associated path |Configure the EFS\-TOS association paths using one of these two methods:<br><br><br>* **Policy\-Based**: This method uses the association paths defined in the existing DataFlow policies.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A DataFlow policy can have only one running task. That is, a DataFlow policy can create or run only one task at a time.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In the "Policy\-Based" scenario, only the path settings (<strong>File storage path</strong> and <strong>Object storage path</strong>, not <strong>Flow rules</strong>) from the selected DataFlow policy will be used to set up the association between EFS and TOS.   </div><br>   <br><br>* **Custom**: This option enables you to customize the association paths between EFS and TOS. After selecting it, configure the parameters for **File storage path** and **Object storage path**. |
      |Policy |If you select **Policy\-Based** for the **Associated path** option, you must choose a DataFlow policy. For more information about DataFlow policies, see [Managing DataFlow policies](https://docs.byteplus.com/en/docs/nas/efs_Managing_DataFlow_policies). |
      

   * **File** **storage** **path**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The following parameters only apply when the <strong>Associated path</strong> option is set to <strong>Custom</strong>.      </div>
      

      
      |**Parameter** |**Description** |
      |---|---|
      |File System |Displays the ID of the EFS file system for which you are creating a DataFlow task. This field is auto\-filled and non\-editable. |
      |File System path |Enter the file system directory path in which data synchronization will be performed. The following constraints apply:<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">Make sure that the directory path is correct. If the directory does not exist, EFS will automatically create it.</div><br><br><br><br>* The path must be an absolute path, which starts and ends with a forward slash (/).<br><br>* The directory cannot be the root directory.<br><br>* The parent directory must be an existing directory.<br><br>* The path cannot exceed 8 directory levels.<br><br>* The length must be between 3 and 1,024 characters.<br><br>* The path cannot overlap with the path of any other task. |
      

   * **Object storage path**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The following parameters only apply when the <strong>Associated path</strong> option is set to <strong>Custom</strong>.      </div>
      

      
      |**Parameter** |**Description** |
      |---|---|
      |Bucket list |Select the TOS bucket with which you want to associate the file system. |
      |Versioning status |Once you select a TOS bucket, its versioning status will be shown automatically. |
      |Bucket prefix |Specify a prefix in the selected TOS bucket for data synchronization with the file system. The prefix should:<br><br><br>* Start and end with a forward slash (/), for example `/prefix/`.<br><br>* Be between 2 and 1,024 characters long.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not specify a prefix, EFS uses the root directory of the TOS bucket.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot bind another DataFlow task to any sub\-prefix under a prefix if a DataFlow task is already bound to that prefix in the bucket.</div><br> |
      |TOS cross\-service authorization |Before data can flow between EFS and TOS, you must complete cross\-service authorization. Once authorized, a service\-linked role named `EFSAccessTOSRole` is automatically created to enable mutual access between TOS and EFS.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not change or turn off cross\-service authorization after you enable it. Otherwise, the DataFlow feature will not work properly.</div><br> |
      

   * **Task**

      
      |**Parameter** |**Description** |
      |---|---|
      |Task type |Select **Import**. |
      |File conflict policy |Set file conflict policy for import tasks:<br><br><br>* **Preserve Latest Files**: For files with the same name, EFS compares the timestamps of the last modification between the TOS and EFS versions and only imports the newer version. Overwritten files cannot be recovered. If both versions have the same timestamp, EFS skips the file.<br><br>* **Skip Existing Files**: EFS automatically skips files with the same name in TOS and EFS during import tasks. In other words, import operations are not performed on files with identical names.<br><br>* **Overwrite Existing Files**: EFS automatically overwrites files with the same name during import tasks, specifically replacing EFS files with TOS files. This change is permanent. |
      |TLS cross\-service authorization |After enabling and authorizing this feature, you can query and analyze data flow records of the task in real time. To view DataFlow logs, see [Viewing DataFlow logs](https://docs.byteplus.com/en/docs/nas/efs_Viewing_DataFlow_logs?lang=zh).<br><br>If the page says that Torch Log Service (TLS) is **Not yet open**, click **To open** to activate TLS and allow EFS access. |
      |Log analysis |If cross\-service authorization for TLS is enabled, the log analysis feature will be activated automatically.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can use the toggle switch to turn this feature off at any time.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Activating log analysis is free. However, TLS will bill you separately for any usage generated after activation. For billing details, see <a href="https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode">TLS billable items</a>.</div><br> |
      

   * **Metrics**

      
      |**Parameter** |**Description** |
      |---|---|
      |Filter range |Select filter range for import tasks. By default, both metadata and data are included. Details are as follows:<br><br><br>* **All**: This option imports all data.<br><br>* **Specify filter conditions**: This option only imports data within a specified directory.<br><br>* **Specify file list**: This option imports data from a specified list of files. |
      |Specify filter conditions |When you set **Filter range** to **Specify filter conditions**, you must add filter conditions. Click **Add metrics**, and set **Metrics type** to **Subdirectory**. Then, click **add** to enter the subdirectory. The following constraints apply:<br><br><br>* Only subdirectories within the file system data source path are supported. For example, if the **File System path** is `/aa/` and the **Bucket prefix** is `/bb/`, then data in `/bb/` links to `/aa/`. To import only data from `/bb/data/` of the bucket, you need to set the file system subdirectory to `data/`.<br><br>* Subdirectories must end with a forward slash (/).<br><br>* The parent directory must be an existing directory with the maximum path depth of 8.<br><br>* You can add up to 20 subdirectories. |
      |Specify file list |When you set **Filter range** to **Specify file list**, you can choose to **Upload file list** or **Working with file lists in TOS**. Specifically:<br><br><br>* **Upload file list**: Write the file paths in a `txt` file. Then, click **Click to upload txt file** to upload the file to the console. Restrictions:<br><br>   * File path restrictions:<br><br>      * Each line must contain only one file path. For multiple file paths, enter each on a separate line. Both directory and full file paths are supported.<br><br>      * Enter **full file paths** within the TOS bucket. However, do not include the bucket name.<br><br>   * File upload restrictions:<br><br>      * The file must be in `txt` format.<br><br>      * The file size must be less than 150 MB.<br><br>* **Working with file lists in TOS**: Enter the full TOS path where the file list is located manually. DataFlow will then import **all the listed files** and **all the files in the listed subdirectories**. Subdirectories must start and end with a forward slash (/). Restrictions:<br><br>   * File list restrictions:<br><br>      * Enter a full file path, including the file extension.<br><br>      * The file can be a text file from any TOS bucket or directory, or a non\-compressed `manifest.json` file generated from a TOS bucket inventory. For more information on manifest.json files, see [Bucket inventory](https://docs.byteplus.com/en/docs/tos/Bucket-inventory).<br><br>      * Only import tasks support manifest.json files.<br><br>   * Restrictions on importing a list of files:<br><br>      * Each line must contain only one file path. For multiple file paths, enter each on a separate line. Both directory and full file paths are supported.<br><br>      * Enter **full file paths** within the TOS bucket. However, omit the bucket name.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Caution      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the file path prefix you enter does not match the configured TOS <strong>Bucket prefix</strong>, the file will automatically be skipped and not imported.      </div><br>       |
      

6. After completing the settings, click **OK**.

   Once created, EFS immediately starts the import task, and the task status changes to **Running**. You can view the progress in the task list. When the task is done, the status changes to **Completed**.


<span id="KRkpdKRT"></span>
## Creating export tasks


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, click **DataFlow**.

6. On the **DataFlow** page, select the **Task** tab.

7. Click **Create task**, and configure the parameters in the **Create DataFlow task** panel.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Associated path |Configure the EFS\-TOS association paths using one of these two methods:<br><br><br>* **Policy\-Based**: This method uses the association paths defined in the existing DataFlow policies.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A DataFlow policy can have only one running task. That is, a DataFlow policy can create or run only one task at a time.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In the "Policy\-Based" scenario, only the path settings (<strong>File storage path</strong> and <strong>Object storage path</strong>, not <strong>Flow rules</strong>) from the selected DataFlow policy will be used to set up the association between EFS and TOS.   </div><br>   <br><br>* **Custom**: This option enables you to customize the association paths between EFS and TOS. After selecting it, configure the parameters for **File storage path** and **Object storage path**. |
      |Policy |If you select **Policy\-Based** for the **Associated path** option, you must choose a DataFlow policy. For more information about DataFlow policies, see [Managing DataFlow policies](https://docs.byteplus.com/en/docs/nas/efs_Managing_DataFlow_policies). |
      

   * **File** **storage** **path**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The following parameters only apply when the <strong>Associated path</strong> option is set to <strong>Custom</strong>.      </div>
      

      
      |**Parameter** |**Description** |
      |---|---|
      |File System |Displays the ID of the EFS file system for which you are creating a DataFlow task. This field is auto\-filled and non\-editable. |
      |File System path |Enter the file system directory path in which data synchronization will be performed. The following constraints apply:<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">Make sure that the directory path is correct. If the directory does not exist, EFS will automatically create it.</div><br><br><br><br>* The path must be an absolute path, which starts and ends with a forward slash (/).<br><br>* The directory cannot be the root directory.<br><br>* The parent directory must be an existing directory.<br><br>* The path cannot exceed 8 directory levels.<br><br>* The length must be between 3 and 1,024 characters.<br><br>* The path cannot overlap with the path of any other task. |
      

   * **Object storage path**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The following parameters only apply when the <strong>Associated path</strong> option is set to <strong>Custom</strong>.      </div>
      

      
      |**Parameter** |**Description** |
      |---|---|
      |Bucket list |Select the TOS bucket with which you want to associate the file system. |
      |Versioning status |Once you select a TOS bucket, its versioning status will be shown automatically. |
      |Bucket prefix |Specify a prefix in the selected TOS bucket for data synchronization with the file system. The prefix should:<br><br><br>* Start and end with a forward slash (/), for example `/prefix/`.<br><br>* Be between 2 and 1,024 characters long.<br><br>* Exist in the TOS bucket.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not specify a prefix, EFS uses the root directory of the TOS bucket.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot bind another DataFlow task to any sub\-prefix under a prefix if a DataFlow task is already bound to that prefix in the bucket.</div><br> |
      |TOS cross\-service authorization |Before data can flow between EFS and TOS, you must complete cross\-service authorization. Once authorized, a service\-linked role named `EFSAccessTOSRole` is automatically created to enable mutual access between TOS and EFS.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not change or turn off cross\-service authorization after you enable it. Otherwise, the DataFlow feature will not work properly.</div><br> |
      

   * **Task**

      
      |**Parameter** |**Description** |
      |---|---|
      |Task type |Select **Export**. |
      |File conflict policy |Set file conflict policy for export tasks:<br><br><br>* **Preserve Latest Files**: For files with the same name, EFS compares the timestamps of the last modification between the TOS and EFS versions and only exports the newer version. Overwritten files cannot be recovered. If both versions have the same timestamp, EFS skips the file.<br><br>* **Skip Existing Files**: EFS automatically skips files with the same name in TOS and EFS during export tasks. In other words, export operations are not performed on files with identical names.<br><br>* **Overwrite Existing Files**: EFS automatically overwrites files with the same name during export tasks, specifically replacing TOS files with EFS files. This change is permanent. |
      |TLS cross\-service authorization |After enabling and authorizing this feature, you can query and analyze data flow records of the task in real time. To view DataFlow logs, see [Viewing DataFlow logs](https://docs.byteplus.com/en/docs/nas/efs_Viewing_DataFlow_logs?lang=zh).<br><br>If the page says that Torch Log Service (TLS) is **Not yet open**, click **To open** to activate TLS and allow EFS access. |
      |Log analysis |If cross\-service authorization for TLS is enabled, the log analysis feature will be activated automatically.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can use the toggle switch to turn this feature off at any time.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Activating log analysis is free. However, TLS will bill you separately for any usage generated after activation. For billing details, see <a href="https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode">TLS billable items</a>.</div><br> |
      

   * **Metrics**

      
      |**Parameter** |**Description** |
      |---|---|
      |Filter range |Select filter range for export tasks:<br><br><br>* **All**: This option exports all data.<br><br>* **Specify filter conditions**: This option only exports data within a specified directory.<br><br>* **Specify file list**: This option exports data from a specified list of files. |
      |Specify filter conditions |When you set **Filter range** to **Specify filter conditions**, you must add filter conditions. Click **Add metrics**, and set **Metrics type** to **Subdirectory**. Then, click **add** to enter the subdirectory. The following constraints apply:<br><br><br>* Only subdirectories within the file system data source path are supported. For example, if the **File System path** is `/aa/` and the **Bucket prefix** is `/bb/`, then data in `/bb/` links to `/aa/`. If you export data from `/aa/data/` to TOS, it will be stored in the `/bb/data/` directory.<br><br>* Subdirectories must end with a forward slash (/).<br><br>* The parent directory must be an existing directory with the maximum path depth of 8.<br><br>* You can add up to 20 subdirectories. |
      |Specify file list |When you set **Filter range** to **Specify file list**, you can choose to **Upload file list** or **Working with file lists in TOS**. Specifically:<br><br><br>* **Upload file list**: Write the file paths in a `txt` file. Then, click **Click to upload txt file** to upload the file to the console. Restrictions:<br><br>   * File path restrictions:<br><br>      * Each line must contain only one file path. For multiple file paths, enter each on a separate line. Both directory and full file paths are supported.<br><br>      * Enter **full file paths** within the TOS bucket. However, do not include the bucket name.<br><br>   * File upload restrictions:<br><br>      * The file must be in `txt` format.<br><br>      * The file size must be less than 150 MB.<br><br>* **Working with file lists in TOS**: Enter the full TOS path where the file list is located manually. DataFlow will then export **all the listed files** and **all the files in the listed subdirectories**. Subdirectories must start and end with a forward slash (/). Restrictions:<br><br>   * File list restrictions:<br><br>      * Enter a full file path, including the file extension.<br><br>      * The file can be a text file from any TOS bucket or directory.<br><br>   * Restrictions on exporting a list of files:<br><br>      * Each line must contain only one file path. For multiple file paths, enter each on a separate line. Both directory and full file paths are supported.<br><br>      * Enter **full file or directory paths** within the file system. However, do not include the file system name.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Caution      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the file path prefix you enter does not match the configured <strong>File System path</strong>, the file will automatically be skipped and not exported.      </div><br>       |
      

6. After completing the settings, click **OK**.

   Once created, EFS immediately starts the export task, and the task status changes to **Running**. You can view the progress in the task list. When the task is done, the status changes to **Completed**.


<span id="KiDOCfGI"></span>
## Creating eviction tasks


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, click **DataFlow**.

6. On the **DataFlow** page, select the **Task** tab.

7. Click **Create task**, and configure the parameters in the **Create DataFlow task** panel.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Associated path |For eviction tasks, only the **Policy\-Based** option is supported. This option uses the association paths defined in the existing DataFlow policies.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">A DataFlow policy can have only one running task. That is, a DataFlow policy can create or run only one task at a time.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">In the "Policy\-Based" scenario, only the path settings (<strong>File storage path</strong> and <strong>Object storage path</strong>, not <strong>Flow rules</strong>) from the selected DataFlow policy will be used to set up the association between EFS and TOS.</div><br> |
      |Policy |If you select **Policy\-Based** for the **Associated path** option, you must choose a DataFlow policy. For more information about DataFlow policies, see [Managing DataFlow policies](https://docs.byteplus.com/en/docs/nas/efs_Managing_DataFlow_policies). |
      

   * **Task**

      
      |**Parameter** |**Description** |
      |---|---|
      |Task type |Select **Eviction**. |
      |TLS cross\-service authorization |After enabling and authorizing this feature, you can query and analyze data flow records of the task in real time. To view DataFlow logs, see [Viewing DataFlow logs](https://docs.byteplus.com/en/docs/nas/efs_Viewing_DataFlow_logs?lang=zh).<br><br>If the page says that Torch Log Service (TLS) is **Not yet open**, click **To open** to activate TLS and allow EFS access. |
      |Log analysis |If cross\-service authorization for TLS is enabled, the log analysis feature will be activated automatically.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You cannot turn this feature off for eviction tasks.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Activating log analysis is free. However, TLS will bill you separately for any usage generated after activation. For billing details, see <a href="https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode">TLS billable items</a>.</div><br> |
      

   * **metrics**

      
      |**Parameter** |**Description** |
      |---|---|
      |Filter range |Select filter range for eviction tasks:<br><br><br>* **All**: This option evicts all data.<br><br>* **Specify filter conditions**: This option only evicts data within a specified directory.<br><br>* **Specify file list**: This option evicts data from a specified list of files. |
      |Specify filter conditions |When you set **Filter range** to **Specify filter conditions**, click **Add metrics** to define the range for data eviction. This option allows you to define the range based on **AccessTime** and **Subdirectory**:<br><br><br>* **AccessTime**: Files with a last access time **greater than or equal to** a specified value will be removed. The available time ranges are as follows:<br><br>   * **Hour**: Enter an integer between 1 and 8,760.<br><br>   * **Day**: Enter an integer between 1 and 365.<br><br>   * **Week**: Enter an integer between 1 and 52.<br><br>   * **Month**: Enter an integer between 1 and 12.<br><br>   * **Year**: Only the value 1 is supported.<br><br>* **Subdirectory**: Only the data within the specified subdirectory will be deleted. The following constraints apply:<br><br>   * Only subdirectories within the file system data source path are supported.<br><br>   * Subdirectories must end with a forward slash (/).<br><br>   * The parent directory must be an existing directory with the maximum path depth of 8.<br><br>   * You can add up to 20 subdirectories. |
      |Specify file list |When you set **Filter range** to **Specify file list**, you can choose to **Upload file list** or **Working with file lists in TOS**. Specifically:<br><br><br>* **Upload file list**: Write the file paths in a `txt` file. Then, click **Click to upload txt file** to upload the file to the console. Restrictions:<br><br>   * File path restrictions:<br><br>      * Each line must contain only one file path. For multiple file paths, enter each on a separate line. Both directory and full file paths are supported.<br><br>      * Enter **full file paths** within the TOS bucket. However, do not include the bucket name.<br><br>   * File upload restrictions:<br><br>      * The file must be in `txt` format.<br><br>      * The file size must be less than 150 MB.<br><br>* **Working with file lists in TOS**: Enter the full TOS path where the file list is located manually. DataFlow will then evict **all the listed files** and **all the files in the listed subdirectories**. Subdirectories must start and end with a forward slash (/). Restrictions:<br><br>   * File list restrictions:<br><br>      * Enter a full file path, including the file extension.<br><br>      * The file can be a text file from any TOS bucket or directory.<br><br>   * Restrictions on evicting a list of files:<br><br>      * Each line must contain only one file path. For multiple file paths, enter each on a separate line. Both directory and full file paths are supported.<br><br>      * Enter **full file or directory paths** within the file system. However, do not include the file system name.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Caution      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the file path prefix you enter does not match the configured <strong>File System path</strong>, the file will be automatically skipped and will not be evicted.      </div><br>       |
      

6. After completing the settings, click **OK**.

   Once created, EFS immediately starts the eviction task, and the task status changes to **Running**. You can view the progress in the task list. When the task is done, the status changes to **Completed**.


<span id="3j4e4HM4"></span>
## Related operations


|Operation |Steps |
|---|---|
|View DataFlow task details |* On the DataFlow **Task** tab, view details about tasks, including **Task ID**, **Task type**, **Running status**, and **Completed Tasks**.<br><br>* On the DataFlow **Task** tab, click the **Task ID** of a task to access its **Overview** tab. There, you can view **Basic information** and **Task information**. |
|Cancel a DataFlow task |1. On the **Task** tab, click **Cancel** in the **Action** column of the task.<br><br>2. In the box that appears, click **Cancel task**.<br><br>   After canceling the task, its status will change to **Cancelled**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Task cancellation is only permitted when the DataFlow task is in <strong>Running</strong> status.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Canceling a running task takes longer. These tasks will be excluded from cancellation progress statistics, though the system continues processing cancellations in the background. This may cause discrepancies between the displayed and actual successful cancellation counts.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Exercise caution when canceling an import or export task, as this may result in data inconsistencies.</div><br> |
|Delete a DataFlow task |1. On the **Task** tab, click **Delete** in the **Action** column of the task.<br><br>2. In the **Delete task** dialog, click **Delete task**. |
