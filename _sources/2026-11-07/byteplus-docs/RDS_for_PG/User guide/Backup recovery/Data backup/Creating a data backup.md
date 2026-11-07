---
title: "Creating a data backup"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/creating_manual_backup"
---

This topic describes how to create a data backup.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Backups are retained for 7 to 365 days, after which they will be deleted. If you need to keep backups for a long time, you can download them locally. For more details about downloading backups, see [Downloading data backup files](https://docs.byteplus.com/en/docs/RDS_for_PG/Downloading_a_data_backup).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL](https://console.byteplus.com/db/rds-pg) console.

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name to enter the instance details page.

5. At the top of the page, click the **Backups** tab.

6. Under the **Data backup** page, click **Manual backup**.

7. On the pop\-up **Manual backup** page, after completing the following settings, click **OK**.

   
   |**Configuration item** |**Required?**  |**Description** |
   |---|---|---|
   |Backup object |Yes |Set the backup target. You can select **Entire instance** or **Specified databases**. |
   |Backup type<br><br> |Yes |Set the backup type. You can choose **Physical** or **Logical**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When you select the backup target as the <strong>Specified databases</strong>, the backup type can only be selected as <strong>Logical</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the instance does not have a database, creating a logical backup is not supported.</div><br> |
   |Database<br><br> |Yes |Select the database that needs to be backed up.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Settings are supported only when the backup target is selected as the <strong>Specified databases</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can choose up to 2000 databases.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A single backup can support up to 50,000 tables (the sum of all tables in the selected database).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Backing up databases with more than 1000 tables is not supported yet.</div><br> |
   |Backup set description |No |Add a description of the backup set for subsequent management of backups. Supports up to 256 characters. |
   


<span id=".5ZCO57ut5q2l6aqk"></span>
## Next steps

<span id=".5p-l55yL5aSH5Lu96L-b5bqm"></span>
### Viewing data backup progress

After the backup is created, refresh the backup list to view the newly created backup. In the **Status** column of the **Backup** list, the status of the backup is displayed. If a backup is in progress, the **Status** column shows **In progress** and the backup progress as a percentage.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You need to manually refresh the list to view the latest backup progress.</div>


<span id=".5p-l55yL5aSH5Lu95paH5Lu2"></span>
### Viewing backup

In the backup list of the **Backups** page, the backup ID, backup status, backup method, backup size, start time and end time of the backup are displayed. Backups can be filtered through **Method**.

In the backup list, click **Restore** in the **Actions** column of the backup list to restore from the corresponding backup. For more information about recovery, see [Restoring to a new instance](https://docs.byteplus.com/en/docs/RDS_for_PG/recovery_from_a_backup_set).

<span id="1ZGquNTB"></span>
## Related APIs


|API |Note |
|---|---|
|[CreateBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/createbackup) |Call the CreateBackup API to create a data backup. |
