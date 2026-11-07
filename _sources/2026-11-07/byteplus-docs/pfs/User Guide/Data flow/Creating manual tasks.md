---
title: "Creating manual tasks"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Creating_manual_tasks"
---

This topic introduces how to create manual tasks using the  console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The file system has been created, and the Data Flow bandwidth has been configured. For more information, see [Creating file systems](https://docs.byteplus.com/en/docs/pfs/Creating-a-file-system) and [Configuring Data Flow bandwidth](https://docs.byteplus.com/en/docs/pfs/Configure_data_flow_bandwidth).

* The directory has been created in the file system. This directory can be either a fileset or a subdirectory. If it is a fileset, first create the fileset using the console. For more information, see [Create Fileset](https://docs.byteplus.com/en/docs/pfs/Managing-fileset#.5Yib5bu6LWZpbGVzZXQ=).

* The TOS bucket has been created. For more information, see [Creating a Bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).


<span id="2c7332b1"></span>
## Notice


* You cannot nest the fileset (subdirectory), directory, or bucket prefix configured in a task with those in tasks that are in the **Creating**, **Running**, or **Cancelling** state.

* Make sure that the directory is correct. If the directory doesn't exist,  will automatically create it.


<span id=".5Yib5bu65pWw5o2u5rWB5Yqo5Lu75Yqh"></span>
## Steps


1. Log in to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File** **System** \> **File** **System** **List**.

4. On the File System page, click the file system you want to manage.

5. On the **Overview** page, click the **Data flow** tab.

6. On the **Data flow** tab, click **Data Flow Task** \> **manual task**.

7. On the **manual task** tab, click **Create task**.

8. Set the following parameters on the **Create Data Flow Task** page.

   * **Data Flow path**

      
      |Parameter |Note |
      |---|---|
      |Configuration path |Select **custom** to manually enter information in the **File storage path** and **Object storage path** sections. |
      

   * **File storage path**

      
      |Parameter |Note |
      |---|---|
      |File System ID | The PFS file system ID for creating the data flow task is automatically populated by the system and cannot be modified. |
      |File System path |Set the path in the current file system for which you want to enable data synchronization. Select either a Fileset or a directory and enter the subdirectory, if necessary.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">We recommend selecting a fileset, as the Fileset feature supports quota and Quality of Service (QoS) mechanisms.</div><br><br><br><br>* If you don't specify a subdirectory,  uses the **File system root directory** or the **Fileset** that you previously selected.<br><br>* Requirements for subdirectories, if necessary:<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Make sure that the directory path is correct. If the directory doesn't exist,  will automatically create it.   </div><br>   <br><br>   * Enter the absolute path of the subdirectory in the file system. It must begin and end with a forward slash (/).<br><br>   * Can contain letters, numbers, periods (.), underscores (_), hyphens (\-), and forward slashes (/).<br><br>   * Length of the complete path string must not exceed 1,024 characters, and each subpath segment must be limited to 255 characters or fewer.<br><br>   * Cannot nest with the fileset (subdirectory), or directory configured in tasks that are in the **Creating**, **Running**, or **Cancelling** state. |
      

   * **Object storage path**

      
      |**Parameter** |**Note** |
      |---|---|
      |TOS bucket |Select the TOS bucket for which you want to enable data synchronization. The TOS bucket must be in the same region as the current file system.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The interface automatically displays the versioning status of the selected bucket. If versioning is disabled or suspended, click <strong>Settings</strong> to enable it. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/tos/docs-enabling-and-suspending-versioning">Enabling and suspending versioning</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">We recommend enabling versioning for the selected TOS bucket. This allows you to restore files to any previous version when files in the bucket are overwritten.</div><br> |
      |TOS bucket prefix |Specify a prefix in the selected TOS bucket for data transfers with the file system. Requirements:<br><br><br>* Must start and end with a forward slash (/).<br><br>* Cannot contain consecutive forward slashes (//).<br><br>* Length must be between 3 and 1,024 characters.<br><br>* Cannot nest with prefixes configured in policies or manual tasks that are in the **Creating**, **Running**, or **Cancelling** state.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you don't specify a prefix,  uses the root directory of the bucket.</div><br> |
      

   * **Data Flow Task**: **Import**, **Export ** and **Inventory**. The parameters are described below.

      * **Import**: Imports data from TOS to PFS.

         
         |Parameter |Note |
         |---|---|
         |File conflict policy |Configure how files with the same name in the file system and the TOS bucket are handled during data transfer. The options are as follows:<br><br><br>* **Keep the latest files up to date**: Compare the last modified times of the two files and keep the latest version. If the last modified times are the same, skip the file with the same name.<br><br>* **Skip the file with the same name**: Skips files with the same name in TOS and PFS. In other words, no actions are taken on files with identical names.<br><br>* **Overwrite file with same name**: Uses TOS files to overwrite PFS files. |
         |Data type |**Metadata and data** are selected by default. A Import task loads both metadata and data. |
         

      * **Export**: Exports data from PFS to TOS.

         
         |Parameter |Note |
         |---|---|
         |File conflict policy |Configure how files with the same name in the file system and the TOS bucket are handled during data transfer. The options are as follows:<br><br><br>* **Keep the latest files up to date**: Compare the last modified times of the two files and keep the latest version. If the last modified times are the same, skip the file with the same name.<br><br>* **Skip the file with the same name**: Skips files with the same name in TOS and PFS. In other words, no actions are taken on files with identical names.<br><br>* **Overwrite file with same name**: Uses PFS files to overwrite TOS files. |
         |Symbolic Link handling policy |Set the parameters for handling Symbolic Link during data transfer. The options are as follows:<br><br><br>* **Skip Symbolic Link file**: Symbolic Link won't be exported to TOS.<br><br>* **Export as a separate file**: Symbolic Link are exported as new files to TOS, and are stored independently with no link to the original files. |
         |Data type |**Metadata and data** are selected by default. A Export task exports both metadata and data. |
         

      * **Inventory**: Only verifies files within the designated directories of  file systems and TOS buckets. It doesn't execute any import or export operations.

         
         |Parameter |Note |
         |---|---|
         |Data type |**Metadata and data** are selected by default. |
         

   * **Settings file filter criteria**: This determines the data range for Data Flow tasks.

      
      |Parameter |Note |
      |---|---|
      |Filter range |Available options include **All files**, **Specify file list**, and **Specify filter conditions**. The details are as follows:<br><br><br>* **All files**: Executes tasks on all files within the configured path.<br><br>* **Specify file list**: Executes tasks on files listed in the file list.<br><br>* **Specify filter conditions**: Executes tasks on all files that match the specified filter conditions.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Filtering parameters are task\-dependent. Please check the console for supported selection ranges.</div><br> |
      |Specify file list |If you set the **Task type** to **Import ** or **Export**, and **Filter range** is **Specify file list**, you must specify the file list. Available file lists include:<br><br><br>* **Specify file list**: Click **Click upload txt list** to upload a `.txt`  file containing multiple prefixes and import all files listed in the txt file.<br><br>* **Working with file lists in TOS**: Enter a file path in TOS to import all files listed in this file.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">In warm\-up and Export tasks, all files listed in the file list, as well as all files in listed subdirectories, will be processed. Subdirectories must start and end with a forward slash (/).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Prefix requirements for files listed in the document:</div><br><br><br>   * <div data-tips="true" data-tips-type="default">For Import tasks:</div><br><br><br>      * <div data-tips="true" data-tips-type="default">Specify subprefixes of the <strong>TOS bucket prefix</strong> in the <strong>Object storage path</strong> section.</div><br><br><br>      * <div data-tips="true" data-tips-type="default">Enter the full prefix excluding the TOS bucket name.</div><br><br><br>      * <div data-tips="true" data-tips-type="default">Separate multiple prefixes using line breaks.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">For Export tasks:</div><br><br><br>      * <div data-tips="true" data-tips-type="default">Specify subdirectories of the fileset or directory in the <strong>File storage path</strong> section.</div><br><br><br>      * <div data-tips="true" data-tips-type="default">If it is a subdirectory of Fileset, enter the Fileset path + subdirectory path; otherwise, enter the absolute path of the directory in the file system.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">For more information, see <a href="https://docs.byteplus.com/en/docs/pfs/Best_practices_for_configuring_vePFS_Data_Flow_directories">Best practices for configuring PFS Data Flow directories</a>.</div><br> |
      |Filter rules |When **Task type** is **Export**, and **Filter range** is **Specify filter conditions**, you must configure filter rules. Optional **Filter conditions** are as follows:<br><br><br>* **AllDirectories**: You can choose to exclude a directory under the root of the file system, with the following constraints:<br><br>   * The directory must be a subdirectory under the source path of the data flow policy.<br><br>   * You must enter the absolute path of the directory in the file system, starting and ending with a forward slash (/).<br><br>   * The parent directory must be an existing directory, with a maximum path depth of 8 levels.<br><br>   * You can add up to 20 directories.<br><br>* **LastestAccessTimeStamp**: You can specify a last accessed time in the time picker to filter files accessed before this date. |
      

   * **Log analysis**: After enabling this feature, you can query and analyze transfer records of the Data Flow policy in real time.

      * You can choose to enable log analysis for Import or Export tasks. This function is not available for Inventory tasks.

      * To enable this feature, activate log services and authorize  to access the log service. 

9. Click **Confirm** to save your choices and create a task.
