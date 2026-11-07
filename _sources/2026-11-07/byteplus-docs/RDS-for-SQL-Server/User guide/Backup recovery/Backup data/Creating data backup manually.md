---
title: "Creating data backup manually"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-data-backup-manually"
---

This article describes the steps to create a manual backup.

<span id="prerequisite"></span>
## prerequisite


* The [instance was created](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide) and the instance state is **running**.

* The status of the target library to be backed up is `Online`, and you need to confirm that the high availability group is healthy.


<span id="precautions"></span>
## Precautions


* When backing up a single library, backing up the system library and the rdsadmin library is not supported.

* Under a single instance, no more than 100 single\-library backups can be performed, and they cannot be duplicated.

* Instance\-level backup means that only one backup task is supported when all databases are selected.


<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name.

4. At the top of the page, click the **Backup Recovery** tab.

5. On the **Data Backup** tab, click **Manual Backup**.

6. Set the following parameters in the **manual backup** dialog box.



|**Parameters** |**Description** |
|---|---|
|**Backup method** |Currently only **physical backup** is supported, no need to select. |
|**Backup Type** |Currently only **full backups** are supported, no need to select. |
|**Backup Objects** |Select backup objects on demand, currently supports selecting to backup **the entire instance** and **specify libraries**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When selecting a specified library, the number of single library backups being performed in a single instance cannot exceed 100 and cannot be repeated.</div><br> |
|**Select Database** |In the Select Database area, check the database that needs to be backed up. Also, support fuzzy search database. |



8. Click **OK** to complete manual backup creation.


<span id="follow-up-operation"></span>
## follow\-up operation

[Database backup download](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloading-data-backup-files)
