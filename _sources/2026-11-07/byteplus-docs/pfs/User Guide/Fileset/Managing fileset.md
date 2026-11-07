---
title: "Managing fileset"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Managing-fileset"
---

This topic introduces the operation steps of managing Filesets on the PFS console, including creating, viewing, editing, and deleting Filesets.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Fileset is a small dataset for storing files in PFS, with its own independent inode space and management capabilities. You can use Fileset as the smallest unit to configure corresponding data policies and Quota settings.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Preconditions

Created file system, please refer to [Creating a file system](https://docs.byteplus.com/docs/pfs/Creating-a-file-system).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A PFS supports creating up to 10 Filesets.If you need to create more than 10 Filesets, please submit a ticket for application.

* The default inode limits in Fileset are as follows:

   * 100MB/s/TiB specification: 10 million inodes

* If the number of files or directories in Fileset reaches the inode limit, an error will be reported when writing data. We recommend configuring Fileset usage alerts. When the number of used files exceeds 80%, we suggest cleaning up files or submitting a ticket to increase the file limit to avoid impacting your normal business operations.

* Nested Filesets are not supported in Fileset.


<span id=".5Yib5bu6LWZpbGVzZXQ="></span>
## Create Fileset


1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region where the target file system is located.

3. Select **File System** \> **Instances** in the left navigation bar. On the Instance List page, click the target file system name.

4. On the instance details page, click **Fileset** tab.

5. On the **Fileset** tab, click **Create Fileset**.

6. Set the following parameters in the pop\-up dialog box.

   
   |Parameters |Description |
   |---|---|
   |Instance ID |Create a PFS system for Fileset, the system will automatically populate and cannot be modified. |
   |Fileset name |Set the Fileset name, naming convention is as follows:<br><br><br>* Can only start with English and Chinese.<br><br>* Can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* Length is between 1 and 128 characters. |
   |Fileset path |Set the path of Fileset in the PFS file system, with the following constraints:<br><br><br>* The input directory should be an absolute path in the file system, starting and ending with `/`.<br><br>* The path format should be `/<parent directory>/<subdirectory>/`, where:<br><br>   * The parent directory must be an existing directory.<br><br>   * The subdirectory is the directory name that needs to be created when creating the Fileset, and it will be automatically created by the system.<br><br>   * Example directory: `/dir/Filesetdir/`.<br><br>* The path depth should be no more than 8 layers.<br><br>* The length should be between 1 and 255 characters. |
   

7. Click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Creating a Fileset takes some time. Please be patient and wait.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the Fileset path you set is not reasonable, it will fail to create.   </div>
   


<span id=".5YW25LuW5pON5L2c"></span>
## Other operations


* **View Fileset list**

   On the **Fileset** tab, you can view detailed information about the Fileset, including Name, ID, State, Directory path, and Create time.

* **Edit Fileset**

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">PFS only supports modifying the Fileset name.   </div>
   

   1. On the **Fileset** tab, hover the mouse over the target Fileset name and click the edit button next to it.

   2. In the pop\-up dialog box, set the name of the Fileset that needs to be modified, and click **OK**.

* **Delete Fileset**

   1. On the **Fileset** tab, click **delete** corresponding to the target Fileset in the action column.

   2. Click **Delete** in the pop\-up dialog box.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After deleting the Fileset, all data in the directory will be permanently deleted and cannot be recovered. Please proceed with caution.      </div>
