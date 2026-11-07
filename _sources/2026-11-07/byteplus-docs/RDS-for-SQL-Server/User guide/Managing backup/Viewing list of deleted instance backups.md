---
title: "Viewing list of deleted instance backups"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-list-of-deleted-instance-backups"
---

This article describes the steps to view the backup list of deleted instances.

<span id="background-information"></span>
## Background information

Manually deleted or unsubscribed, due to arrears or expiration of the recovery instance, will be deleted, unsubscribed or recycled according to the set **instance release after retaining backup file** retention policy, keep the backup file instance. These backup files appear in the **deleted instance backup** list. For more information about **keeping backup files after instance release** retention policies, see [Custom backup policies](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/custom-backup-policy).

<span id="precautions"></span>
## Precautions

Backups of incoming deleted instance backups do not support deletion and are automatically released if not rebuilt within seven days.

<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the target project and region.

3. Select **SQL Server** \> **Backup Management** in the left navigation bar.

4. On the **Backup Management** page, click **Deleted instance backups** .

5. On the **Deleted Instance Backups** tab, view the deleted instance backup information.

   Instance backup information includes backup ID, instance name and ID, instance type, database version, instance creation time, instance deletion time, backup file size, backup start time and end time, backup retention period. You can also rebuild an instance based on the backup file of the deleted instance. For details, see [Rebuilding an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/rebuilding-instance).
