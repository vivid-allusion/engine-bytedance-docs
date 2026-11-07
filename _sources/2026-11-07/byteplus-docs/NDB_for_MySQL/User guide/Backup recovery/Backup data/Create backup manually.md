---
title: "Create backup manually"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_a_data_backup_manually"
---

This article describes the steps to manually create a backup.

<span id="前提条件"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance).

* There is currently no backup task in progress.


<span id="注意事项"></span>
## Precautions


* The maximum number of manual backup files is 10. After the number limit is exceeded, existing backup files need to be deleted to create a new manual backup task. For more information about deleting backup files, see [Deleting data backup files](https://www.byteplus.com/en/docs/NDB_for_MySQL/Deleting_data_backup_files).

* Manual backup files are saved permanently by default.


<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Backups** tab.

5. On the **Basic backup list** subtab, click **Manual backup**.

6. Click **OK** in the pop\-up dialog box.


<span id="相关-api"></span>
## Related APIs


|API |Description |
|---|---|
|[CreateBackup](https://www.byteplus.com/en/docs/NDB_for_MySQL/CreateBackup) |Call the CreateBackup to manually create a data backup. |
