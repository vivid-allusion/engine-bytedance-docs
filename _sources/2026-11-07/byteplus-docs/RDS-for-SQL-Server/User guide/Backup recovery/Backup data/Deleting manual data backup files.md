---
title: "Deleting manual data backup files"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deleting-manual-data-backup-files"
---

This article describes how to delete manually backed up data files in the SQL Server Edition console of a cloud database.

<span id="prerequisite"></span>
## prerequisite


* The instance has been created and the instance status is running. For more details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* A manual backup file has been created. For more information, see [Creating a manual backup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-data-backup-manually).


<span id="precautions"></span>
## Precautions

Only manually created backup files are supported for deletion.

<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instance list** page, click the target instance name.

4. At the top of the page, click the **Backup recovery** tab.

5. On the **Data backup** tab, click Delete in the Destination Backup ID Action column.

6. Are you **Sure to delete the selected backup file?**  Dialog box, click **Delete**.
