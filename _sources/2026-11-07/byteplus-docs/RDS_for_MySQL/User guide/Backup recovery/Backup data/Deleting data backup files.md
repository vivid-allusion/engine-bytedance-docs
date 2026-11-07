---
title: "Deleting data backup files"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/manually_deleting_data_backup_files"
---

This topic describes the steps for deleting manually created data backup files.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can only delete backup files that are created manually (Executor: **User**). Backup files that are created automatically (Executor: **System**) cannot be deleted. They are automatically cleared upon the expiration of the backup retention policy.

* If the backup has cross\-regional backup enabled, deleting the local backup will also delete the cross\-regional backup.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click on the target instance name to enter the instance details page.

4. At the top of the page, click the **Backups** tab.

5. On the **Data backup** tab, click **Data backup** on the **Basic backup list** sub\-tab to go to the data backup list.

6. Click **Delete** in the **Actions** column of the target backup file.

7. In the dialog box that appears, confirm the backup file information and click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DeleteDataBackup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedatabackup) |Call the DeleteDataBackup API to delete manual backup files for a specified MySQL instance. |
