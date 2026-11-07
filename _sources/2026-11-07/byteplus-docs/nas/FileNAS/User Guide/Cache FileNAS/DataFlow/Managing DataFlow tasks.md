---
title: "Managing DataFlow tasks"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Managing_DataFlow_tasks"
---

This topic explains how to create a DataFlow task and related operations.

<span id="8APai5xv"></span>
## Background information


* DataFlow tasks execute immediately upon creation and run only once.

* FileNAS allows four types of DataFlow tasks: import, export, eviction, and delete. Specifically:

   * Import task: Loads metadata and data from TOS to FileNAS. It proactively caches data requiring high\-performance semantic file access into the file system.

   * Export task: Periodically synchronizes data writes and modifications with TOS, enabling data protection, aggregation, and transmission.

   * Eviction task: Removes rarely used data in the file system, freeing up space and lowering storage costs. The file's data blocks will be cleared, but metadata will be retained.

   * Delete task: Removes files from the file system, deleting both metadata and data. Once deleted, files cannot be recovered. You can choose to delete files concurrently from both FileNAS and TOS.


<span id="jsQYyXm3"></span>
## Prerequisites

A Cache FileNAS file system has been created and is **Running**. For more information, see [Creating file systems](https://docs.byteplus.com/docs/nas/Creating_file_systems).

<span id="gNpscdkH"></span>
## Steps


<Tabs>
<Tab zoneid="ULWiEWotf2" title="Create import tasks">
<TabTitle>Create import tasks</TabTitle>

1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where you want to create an import task.

3. In the left navigation pane, click **File System** \> **DataFlow**.

4. On the **DataFlow** page, click the **Task** tab.

5. On the **Task** tab, click **Create task**.

6. Set the following parameters on the **Create DataFlow task** page.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Configure association path |Configure the FileNAS\-TOS association paths using one of these two methods:<br><br><br>* **Based on policy**: This method uses the association paths defined in the existing DataFlow policies.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A DataFlow policy can have only one running task. That is, a DataFlow policy can create or run only one task at a time.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In the "Based on Policy" scenario, the association between FileNAS and TOS will be set up using only the path settings (<strong>File storage path</strong> and <strong>Object storage path</strong>, but not <strong>Flow rules</strong>) from the selected DataFlow Policy.   </div><br>   <br><br>* **Custom**: This option enables you to customize the association paths between FileNAS and TOS. After selecting it, configure the parameters for **File storage path** and **Object storage path**. |
      |DataFlow policy |If you choose to **configure association path** **based on policy**, you must select a DataFlow policy. For more information about DataFlow policies, see [Managing DataFlow policies](https://docs.byteplus.com/docs/nas/Managing_DataFlow_policies). |
      

   * **File storage path**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The following parameters only apply when the <strong>Configure association path</strong> option is set to <strong>Custom</strong>.      </div>
      

      
      |**Parameter** |**Description** |
      |---|---|
      |File System |Select the file system you wish to create a DataFlow task for. Only Cache FileNAS file systems are supported. |
      |File System path |Enter the file system directory path in which data synchronization will be performed. The following constraints apply:<br><br><br>* The path must be an absolute path, which starts and ends with a forward slash (/).<br><br>* The directory cannot be the root directory.<br><br>* The parent directory must be an existing directory.<br><br>* The path cannot exceed 8 directory levels.<br><br>* The length must be between 3 and 1,024 characters.<br><br>* The path cannot overlap with the path of any other DataFlow task. |
      

   * **Object storage path**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The following parameters only apply when the <strong>Configure association path</strong> option is set to <strong>Custom</strong>.      </div>
      

      
      |**Parameter** |**Description** |
      |---|---|
      |Bucket name |Select the TOS bucket with which you want to associate the file system. |
      |Bucket prefix |Specify a prefix in the selected TOS bucket for data synchronization with the file system. The prefix should:<br><br><br>* Start and end with a forward slash (/), for example `/prefix/`.<br><br>* Be between 2 and 1,024 characters long.<br><br>* Exist in the TOS bucket.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not specify a prefix, FileNAS uses the root directory of the TOS bucket.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot bind another DataFlow task to any sub\-prefix under a prefix if a DataFlow task is already bound to that prefix in the bucket.</div><br> |
      |Cross service authorization |Before data can flow between FileNAS and TOS, you must complete cross\-service authorization. Once authorized, a service\-linked role named `FileNASAccessTOSRole` is automatically created to enable mutual access between TOS and FileNAS.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not change or turn off cross\-service authorization after you enable it. Otherwise, the DataFlow feature will not work properly.</div><br> |
      

   * **Task**

      
      |**Parameter** |**Description** |
      |---|---|
      |Task type |Select **Import**. |
      |File conflict policy |Set file conflict policy for the import task:<br><br><br>* **Keep the latest files**: For files with the same name, FileNAS compares the timestamps of the last modification between the TOS and FileNAS versions and only imports the newer version. Overwritten files cannot be recovered. If both versions have the same timestamp, FileNAS skips the file.<br><br>* **Skip files with the same name**: FileNAS automatically skips files with the same name in TOS and FileNAS during import tasks. In other words, import operations are not performed on files with identical names.<br><br>* **Overwrite files with the same name**: FileNAS automatically overwrites files with the same name during import tasks, specifically replacing FileNAS files with TOS files. This change is permanent. |
      

   * **Settings file filter criteria**

      
      |**Parameter** |**Description** |
      |---|---|
      |Filter range |Select filter range for the import task. By default, both metadata and data are included. The options include:<br><br><br>* **All**: This option imports all data.<br><br>* **Specify filters**: This option only imports data within a specified directory.<br><br>* **Specify File List**: This option imports data from a specified list of files. |
      |Metrics rules |When you set **Filter range** to **Specify filters**, you must add filter conditions. Click **Add metrics**, and set **Metrics content** to **SubDirectory**. Then, click **add** to enter the subdirectory. The following constraints apply:<br><br><br>* Only subdirectories within the file system data source path are supported. For example, if the **File System path** is `/aa/` and the **Bucket prefix** is `/bb/`, then data in `/bb/` links to `/aa/`. To import only data from `/bb/data/` of the bucket, you need to set the file system subdirectory to `data/`.<br><br>* Subdirectories must end with a forward slash (/).<br><br>* The parent directory must be an existing directory with the maximum path depth of 8.<br><br>* You can add up to 20 subdirectories. |
      |Specify File List |When you set **Filter range** to **Specify File List**, you can choose to **Upload File List** or **Use File List in TOS**. Specifically:<br><br><br>* **Upload File List**: Write the file paths in a `txt` file. Then, click **Click to upload txt file** to upload the file to the console. Constraints:<br><br>   * File path restrictions:<br><br>      * Each line must contain only one file path. For multiple file paths, enter each on a separate line. Both directory and full file paths are supported.<br><br>      * Enter **full file paths** within the TOS bucket. However, do not include the bucket name.<br><br>   * File upload restrictions:<br><br>      * The file must be in `txt` format.<br><br>      * The file size must be less than 150 MB.<br><br>* **Use File List in TOS**: Enter the full TOS path where the file list is located manually. DataFlow will then import **all the listed files** and **all the files in the listed subdirectories**. Subdirectories must start and end with a forward slash (/). Constraints:<br><br>   * File list restrictions:<br><br>      * Enter a full file path, including the file extension.<br><br>      * The file can be a text file from any TOS bucket or directory, or a non\-compressed `manifest.json` file generated from a TOS bucket inventory. For more information on manifest.json files, see [Bucket inventory](https://docs.byteplus.com/en/docs/tos/Bucket-inventory).<br><br>      * Only import tasks support manifest.json files.<br><br>   * Restrictions on importing a list of files:<br><br>      * Each line must contain only one file path. For multiple file paths, enter each on a separate line. Both directory and full file paths are supported.<br><br>      * Enter **full file paths** within the TOS bucket. However, omit the bucket name.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the file path prefix you enter does not match the configured TOS <strong>Bucket prefix</strong>, the file will automatically be skipped and not imported.      </div><br>       |
      

7. After completing the settings, click **Confirm**.

   Once created, FileNAS immediately starts the import task, and the task status changes to **Running**. You can view the progress in the task list. When the task is done, the status changes to **Completed**.


</Tab>
<Tab zoneid="VSDKlFEkTo" title="Create export tasks">
<TabTitle>Create export tasks</TabTitle>

1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where you want to create an export task.

3. In the left navigation pane, click **File System** \> **DataFlow**.

4. On the **DataFlow** page, click the **Task** tab.

5. On the **Task** tab, click **Create task**.

6. Set the following parameters on the **Create DataFlow task** page.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Configure association path |Configure the FileNAS\-TOS association paths using one of these two methods:<br><br><br>* **Based on policy**: This method uses the association paths defined in the existing DataFlow policies.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A DataFlow policy can have only one running task. That is, a DataFlow policy can create or run only one task at a time.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In the "Based on Policy" scenario, the association between FileNAS and TOS will be set up using only the path settings (<strong>File storage path</strong> and <strong>Object storage path</strong>, but not <strong>Flow rules</strong>) from the selected DataFlow Policy.   </div><br>   <br><br>* **Custom**: This option enables you to customize the association paths between FileNAS and TOS. After selecting it, configure the parameters for **File storage path** and **Object storage path**. |
      |DataFlow policy |If you choose to **configure association path** **based on policy**, you must select a DataFlow policy. For more information about DataFlow policies, see [Managing DataFlow policies](https://docs.byteplus.com/docs/nas/Managing_DataFlow_policies). |
      

   * **File storage path**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The following parameters only apply when the <strong>Configure association path</strong> option is set to <strong>Custom</strong>.      </div>
      

      
      |**Parameter** |**Description** |
      |---|---|
      |File System |Select the file system you wish to create a DataFlow task for. Only Cache FileNAS file systems are supported. |
      |File System path |Enter the file system directory path in which data synchronization will be performed. The following constraints apply:<br><br><br>* The path must be an absolute path, which starts and ends with a forward slash (/).<br><br>* The directory cannot be the root directory.<br><br>* The parent directory must be an existing directory.<br><br>* The path cannot exceed 8 directory levels.<br><br>* The length must be between 3 and 1,024 characters.<br><br>* The path cannot overlap with the path of any other DataFlow task.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Nested paths across DataFlow policies are not supported.</div><br> |
      

   * **Object storage path**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The following parameters only apply when the <strong>Configure association path</strong> option is set to <strong>Custom</strong>.      </div>
      

      
      |**Parameter** |**Description** |
      |---|---|
      |Bucket name |Select the TOS bucket with which you want to associate the file system. |
      |Bucket prefix |Specify a prefix in the selected TOS bucket for data synchronization with the file system. The prefix should:<br><br><br>* Start and end with a forward slash (/), for example `/prefix/`.<br><br>* Be between 2 and 1,024 characters long.<br><br>* Exist in the TOS bucket.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not specify a prefix, FileNAS uses the root directory of the TOS bucket.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot bind another DataFlow task to any sub\-prefix under a prefix if a DataFlow task is already bound to that prefix in the bucket.</div><br> |
      |Cross service authorization |Before data can flow between FileNAS and TOS, you must complete cross\-service authorization. Once authorized, a service\-linked role named `FileNASAccessTOSRole` is automatically created to enable mutual access between TOS and FileNAS.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not change or turn off cross\-service authorization after you enable it. Otherwise, the DataFlow feature will not work properly.</div><br> |
      

   * **Task**

      
      |**Parameter** |**Description** |
      |---|---|
      |Task type |Select **Export**. |
      |File conflict policy |Set file conflict policy for export tasks:<br><br><br>* **Keep the latest files**: For files with the same name, FileNAS compares the timestamps of the last modification between the TOS and FileNAS versions and only exports the newer version. Overwritten files cannot be recovered. If both versions have the same timestamp, FileNAS skips the file.<br><br>* **Skip files with the same name**: FileNAS automatically skips files with the same name in TOS and FileNAS during export tasks. In other words, export operations are not performed on files with identical names.<br><br>* **Overwrite files with the same name**: FileNAS automatically overwrites files with the same name during export tasks, specifically replacing TOS files with FileNAS files. This change is permanent. |
      

   * **Settings file filter criteria**

      
      |**Parameter** |**Description** |
      |---|---|
      |Filter range |Select filter range for the export task:<br><br><br>* **All**: This option exports all data.<br><br>* **Specify filters**: This option only exports data within a specified directory.<br><br>* **Specify File List**: This option exports data from a specified list of files. |
      |Metrics rules |When you set **Filter range** to **Specify filters**, you must add filter conditions. Click **Add metrics**, and set **Metrics content** to **SubDirectory**. Then, click **add** to enter the subdirectory. The following constraints apply:<br><br><br>* Only subdirectories within the file system data source path are supported. For example, if the **File System path** is `/aa/` and the **Bucket prefix** is `/bb/`, then data in `/bb/` links to `/aa/`. If you export data from `/aa/data/` to TOS, it will be stored in the `/bb/data/` directory.<br><br>* Subdirectories must end with a forward slash (/).<br><br>* The parent directory must be an existing directory with the maximum path depth of 8.<br><br>* You can add up to 20 subdirectories. |
      |Specify File List |When you set **Filter range** to **Specify File List**, you can choose to **Upload File List** or **Use File List in TOS**. Specifically:<br><br><br>* **Upload File List**: Write the file paths in a `txt` file. Then, click **Click to upload txt file** to upload the file to the console. Constraints:<br><br>   * File path restrictions:<br><br>      * Each line must contain only one file path. For multiple file paths, enter each on a separate line. Both directory and full file paths are supported.<br><br>      * Enter **full file paths** within the TOS bucket. However, do not include the bucket name.<br><br>   * File upload restrictions:<br><br>      * The file must be in `txt` format.<br><br>      * The file size must be less than 150 MB.<br><br>* **Use File List in TOS**: Enter the full TOS path where the file list is located manually. DataFlow will then export **all the listed files** and **all the files in the listed subdirectories**. Subdirectories must start and end with a forward slash (/). Constraints:<br><br>   * File list restrictions:<br><br>      * Enter a full file path, including the file extension.<br><br>      * The file can be a text file from any TOS bucket or directory.<br><br>   * Restrictions on exporting a list of files:<br><br>      * Each line must contain only one file path. For multiple file paths, enter each on a separate line. Both directory and full file paths are supported.<br><br>      * Enter **full file or directory paths** within the file system. However, do not include the file system name.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the file path prefix you enter does not match the configured <strong>File System path</strong>, the file will automatically be skipped and not exported.      </div><br>       |
      

7. After completing the settings, click **Confirm**.

   Once created, FileNAS immediately starts the export task, and the task status changes to **Running**. You can view the progress in the task list. When the task is done, the status changes to **Completed**.


</Tab>
<Tab zoneid="XRLfhowaoP" title="Create eviction tasks">
<TabTitle>Create eviction tasks</TabTitle>

1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where you want to create an eviction task.

3. In the left navigation pane, click **File System** \> **DataFlow**.

4. On the **DataFlow** page, click the **Task** tab.

5. On the **Task** tab, click **Create task**.

6. Set the following parameters on the **Create DataFlow task** page.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Configure association path |For eviction tasks, only the **Based on policy** option is supported. This option uses the association paths defined in an existing DataFlow policy.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">A DataFlow policy can have only one running task. That is, a DataFlow policy can create or run only one task at a time.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">In the "Based on Policy" scenario, the association between FileNAS and TOS will be set up using only the path settings (<strong>File storage path</strong> and <strong>Object storage path</strong>, but not <strong>Flow rules</strong>) from the selected DataFlow Policy.</div><br> |
      |DataFlow policy |If you choose to **configure association path** **based on policy**, you must select a DataFlow policy. For more information about DataFlow policies, see [Managing DataFlow policies](https://docs.byteplus.com/docs/nas/Managing_DataFlow_policies). |
      

   * **Task**

      
      |**Parameter** |**Description** |
      |---|---|
      |Task type |Select **Eviction**. |
      

   * **Settings file filter criteria**

      
      |**Parameter** |**Description** |
      |---|---|
      |Filter range |Select filter range for the eviction task:<br><br><br>* **All**: This option evicts all data.<br><br>* **Specify filters**: This option only evicts data within a specified directory.<br><br>* **Specify File List**: This option evicts data from a specified list of files. |
      |Metrics rules |When you set **Filter range** to **Specify filters**, click **Add metrics** to define the range for data eviction. This option allows you to define the range based on **SubDirectory** and **AccessTime**.<br><br><br>* **SubDirectory**: Only the data within the specified subdirectory will be deleted. The following constraints apply:<br><br>   * Only subdirectories within the file system data source path are supported.<br><br>   * Subdirectories must end with a forward slash (/).<br><br>   * The parent directory must be an existing directory with the maximum path depth of 8.<br><br>   * You can add up to 20 subdirectories.<br><br>* **AccessTime**: Files with a last access time **greater than or equal to** a specified value will be removed. |
      |Specify File List |When you set **Filter range** to **Specify File List**, you can choose to **Upload File List** or **Use File List in TOS**. Specifically:<br><br><br>* **Upload File List**: Write the file paths in a `txt` file. Then, click **Click to upload txt file** to upload the file to the console. Constraints:<br><br>   * File path restrictions:<br><br>      * Each line must contain only one file path. For multiple file paths, enter each on a separate line. Both directory and full file paths are supported.<br><br>      * Enter **full file paths** within the TOS bucket. However, do not include the bucket name.<br><br>   * File upload restrictions:<br><br>      * The file must be in `txt` format.<br><br>      * The file size must be less than 150 MB.<br><br>* **Use File List in TOS**: Enter the full TOS path where the file list is located manually. DataFlow will then evict **all the listed files** and **all the files in the listed subdirectories**. Subdirectories must start and end with a forward slash (/). Constraints:<br><br>   * File list restrictions:<br><br>      * Enter a full file path, including the file extension.<br><br>      * The file can be a text file from any TOS bucket or directory.<br><br>   * Restrictions on evicting a list of files:<br><br>      * Each line must contain only one file path. For multiple file paths, enter each on a separate line. Both directory and full file paths are supported.<br><br>      * Enter **full file or directory paths** within the file system. However, do not include the file system name.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the file path prefix you enter does not match the configured <strong>File System path</strong>, the file will automatically be skipped and not removed.      </div><br>       |
      

7. After completing the settings, click **Confirm**.

   Once created, FileNAS immediately starts the eviction task, and the task status changes to **Running**. You can view the progress in the task list. When the task is done, the status changes to **Completed**.


</Tab>
<Tab zoneid="lbiHk2nEJh" title="Create delete tasks">
<TabTitle>Create delete tasks</TabTitle>

1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where you want to create a delete task.

3. In the left navigation pane, click **File System** \> **DataFlow**.

4. On the **DataFlow** page, click the **Task** tab.

5. On the **Task** tab, click **Create task**.

6. Set the following parameters on the **Create DataFlow task** page.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Configure association path |For delete tasks, only the **Based on policy** option is supported. This option uses the association paths defined in an existing DataFlow policy.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">A DataFlow policy can have only one running task. That is, a DataFlow policy can create or run only one task at a time.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">In the "Based on Policy" scenario, the association between FileNAS and TOS will be set up using only the path settings (<strong>File storage path</strong> and <strong>Object storage path</strong>, but not <strong>Flow rules</strong>) from the selected DataFlow Policy.</div><br> |
      |DataFlow policy |If you choose to **configure association path based on policy**, you must select a DataFlow policy. For more information about DataFlow policies, see [Managing DataFlow policies](https://docs.byteplus.com/docs/nas/Managing_DataFlow_policies). |
      

   * **Task**

      
      |**Parameter** |**Description** |
      |---|---|
      |Task type |Select **Delete**. |
      |Delete range |Select filter range for the delete task:<br><br><br>* **Only delete files in File System (force overwrite policy configuration: trigger condition that starts "delete file" in fallout rule)** <br><br>* **Only delete incomplete files in File System (forced overwrite policy configuration: trigger condition that starts "delete file" in fallout rule)** <br><br>* **Simultaneously delete associated files in File System and Object storage (forced overwrite policy in configuration: trigger condition in fallout rule that does not start "delete file")** <br><br>   * **When the object store starts multiple versions, delete the latest version of the associated object**<br><br>   * **When the object store starts multiple versions, delete all versions of the associated object (completely delete), no recovery** |
      

   * **Settings file filter criteria**

      
      |**Parameter** |**Description** |
      |---|---|
      |Filter range |Only the **Specify filters** option is available, meaning you can only delete data within a specified directory. |
      |Metrics rules |Click **Add metrics** to specify the file deletion range. You can filter by **SubDirectory**, **AllDirectories**, or **LastAccessTimeStamp**.<br><br><br>* **SubDirectory**: Enter a directory you want to include. Click **add** to enter directories you do not want to include. In this case, only data in the **Include only** directories will be deleted, while data in the **Do not include** directories will remain. Requirements:<br><br>   * Only subdirectories within the file system data source path are supported.<br><br>   * The path must end with a forward slash (/).<br><br>   * The parent directory must be an existing directory with the maximum path depth of 8.<br><br>* **AllDirectories**: Click **add** to enter directories you do not want to include. In this case, all files within the **AllDirectories** scope will be deleted, except those in the **Do not include** directories. Requirements:<br><br>   * Only subdirectories within the DataFlow policy data source path are supported.<br><br>   * The path must end with a forward slash (/).<br><br>   * The parent directory must be an existing directory with the maximum path depth of 8.<br><br>* **LatestAccessTimeStamp**: Select a date next to **specified time**. This removes files that were last accessed **before** the specified time. |
      

7. After completing the settings, click **Confirm**.

   Once created, FileNAS immediately starts the delete task, and the task status changes to **Running**. You can view the progress in the task list. When the task is done, the status changes to **Completed**.


</Tab>
</Tabs>


<span id="XPoGVBYP"></span>
## Related operations


|Operation |**Steps** |
|---|---|
|View DataFlow task details |1. On the **Task** tab, click a task's ID.<br><br>2. On the **Overview** page, view **Basic information** and **Task rules** for the task. |
|Copy a DataFlow task |You can copy DataFlow tasks to avoid repetitive operations.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Copying a task creates a new task with a different task ID, but all other parameters stay the same as the original task.</div><br><br><br><br>1. On the **Task** tab, click **Copy** in the **Actions** column of the task.<br><br>2. In the **Copy task** dialog box, verify the details and click **Copy task**. |
|Cancel a DataFlow task |1. On the **Task** tab, click **Cancel** in the **Actions** column of the task.<br><br>2. In the **Cancel Task** dialog box, click **Cancel task**.<br><br>   After cancellation, the task status changes to **Cancelled**. You can re\-execute the task by copying the **Cancelled** task.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Task cancellation is only permitted when the DataFlow task is in <strong>Running</strong> status.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Canceling a running task takes longer. These tasks will be excluded from cancellation progress statistics, though the system continues processing cancellations in the background. This may cause discrepancies between the displayed and actual successful cancellation counts.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Canceling an import or export task can cause file inconsistencies.</div><br> |
|Delete a DataFlow task |1. On the **Task** tab, click **Delete** in the **Actions** column of the task.<br><br>2. In the **Delete task** dialog box, click **Delete task**. |
