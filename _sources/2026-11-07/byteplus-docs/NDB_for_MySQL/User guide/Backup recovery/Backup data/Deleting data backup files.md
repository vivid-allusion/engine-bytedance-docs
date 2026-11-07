---
title: "Deleting data backup files"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Deleting_data_backup_files"
---

This article describes the steps for deleting a backup file created manually by an instance.

<span id="注意事项"></span>
## Precautions


* Manual backup of files while the instance is running. Manual backup files will be saved permanently. It is recommended that you delete the backup files in time when the number of manual backup files exceeds the limit or some manual backup files are no longer needed.

* The final backup file of a deleted instance cannot be manually deleted. It will be automatically deleted by the system after 7 days by default based on the completion time of the backup. You can view the estimated deletion time of the target instance backup in the deleted instance backup list. For details, see [Viewing the list of deleted instance backups](https://www.byteplus.com/en/docs/NDB_for_MySQL/Viewing_backups_of_deleted_instances).


<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Backups** tab.

5. On the **Basic backup list** subtab, locate the manual backup file that needs to be deleted, and in its **Actions** column click **Delete**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Manual backup files are created with the <strong>User</strong> type.   </div>
   

6. Enter the backup file ID in the **Confirm deletion** dialog box that pops up, and click **OK**.


<span id="相关-api"></span>
## Related APIs


|API |Description |
|---|---|
|[DeleteBackup](https://www.byteplus.com/en/docs/NDB_for_MySQL/DeleteBackup) |Call the DeleteBackup to delete the instance manual backup file. |
