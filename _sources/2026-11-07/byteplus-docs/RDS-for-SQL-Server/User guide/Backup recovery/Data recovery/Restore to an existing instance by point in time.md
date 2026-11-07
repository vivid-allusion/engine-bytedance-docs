---
title: "Restore to an existing instance by point in time"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/recovering-to-existing-instance-by-time-point"
---

This topic describes the steps to restore data to an existing instance by point in time.

<span id=".6IOM5pmv5L-h5oGv"></span>
## **Background Information**

SQL Server provides the following restore methods:


* Restore from a backup set: This method allows you to restore an entire instance or specific databases to a new or existing instance from a specified backup set. The data in the restored instance is consistent with the data from the backup file. For more information, see [Restore to a new instance from a backup Set](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/recovery-to-new-instances-by-using-backup-set) and [Restore to an existing instance from a backup set](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/recovery-to-existing-instances-by-using-backup-set).

* Restore to a point in time: This method allows you to restore an entire instance or specific databases to a new or existing instance as they were at a specified point in time. The data in the restored instance is consistent with the data at the specified point in time. For more information, see [Restore a new instance to a point in time](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/recovering-to-new-instance-by-time-point) and [Restore an existing instance to a point in time](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/recovering-to-existing-instance-by-time-point).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* The target instance has been created and its status is **Running**. For detailed operations, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* The source instance must have at least one full backup and a differential or log backup that corresponds to the selected point in time.


<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* You can only select a restore point within the retention period configured in the retention policy. The earliest available point is the end time of the first system full backup, and the latest is the start time of the most recent log backup.

* During the restoration process, the status of the target instance is **Recovering**.

* The recovery process will impose a certain amount of pressure on the target instance. It is recommended to perform backup recovery during off\-peak business hours.

* Restoring system databases and the rdsadmin database is not currently supported.

* During a restore, modifying a database or table that was renamed to match the name of an object being restored can cause data conflicts or restore failure.

* If you restore to the original instance, the restored database name cannot be the same as the original database name or any existing database names in the instance. If you restore to an existing non\-original instance, the restored database name can be the same as the original one, but it cannot be the same as any existing database names in the target instance. By default, the restored database is named `DBName_bak{date}{minute}{second}`, for example, `DBName_bak20230718152102`. You can also customize the database name.

* When restoring to an existing instance, you can only select an instance with the same or a higher compatible version than the original instance. You cannot select an instance with a lower compatible version.

* The number of databases to restore must be less than or equal to the remaining database quota of the target instance.


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the target project and region.

3. In the left navigation pane, click **Instances**.

4. On the **Instances** page, click the name of the target instance.

5. On the Summary page, click **Backups**.

6. On the **Backups** tab, click **Restore to existing instances**.

7. On the **Recovery to Existing Instances** page, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Restore method** |Select **By point in time**. |
   |**Recovery time point** |Select a target recovery time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After you select a specific time, the <strong>All databases</strong> section displays all restorable databases for that point in time, excluding system and rdsadmin databases.</div><br> |
   |**Select instance** |Select the original instance or another existing instance to restore the backup to. Fuzzy search for instances is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When restoring to an existing instance, you can only select an instance with the same or a higher compatible version than the original instance. You cannot select an instance with a lower compatible version. The year version and product edition of the compatible version must both be no lower than those of the original instance:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Year version: 2019 < 2022</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Product edition: Web Edition < Standard Edition < Enterprise Edition</div><br><br><br><br><div data-tips="true" data-tips-type="tip">For example:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the compatible version of the original instance is 2022 Standard Edition, you can select an instance with a compatible version of 2022 Standard Edition, 2022 Enterprise Edition.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the compatible version of the original instance is 2019 Enterprise Edition, you can select an instance with a compatible version of 2019 Enterprise Edition, 2022 Enterprise Edition.</div><br> |
   |**Select database** |You can choose to restore a single database, multiple databases, or all databases to the instance. Select the databases to restore in the **All databases** area, and then confirm the selected databases and their restored database names in the **Selected database** area.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you restore to the original instance, the restored database name cannot be the same as the original database name or any existing database names in the instance. If you restore to an existing non\-original instance, the restored database name can be the same as the original one, but it cannot be the same as any existing database names in the target instance. By default, the restored database is named <code>DBName_bak{date}{minute}{second}</code>, for example, <code>DBName_bak20230718152102</code>. In the <strong>Selected database</strong> area, you can rename the restored database. The name must follow these naming conventions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with a letter and end with a letter or digit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length must be between 2 and 60 characters.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Consists of letters, numbers, and underscores (_).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can not use reserved words, such as <strong><code>master</code></strong>, <strong><code>msdb</code></strong>, <strong><code>model</code></strong>, <strong><code>tempdb</code></strong>,<strong><code>resource</code></strong>, <strong><code>rdsadmin</code></strong>, and <strong><code>distribution</code></strong>.</div><br> |
   

8. Click **Submit**.
