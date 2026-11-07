---
title: "Editing database status to online"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/editing-database-status-to-online"
---

This article describes the steps to modify the database state to Online using a stored procedure.

<span id="prerequisite"></span>
## **prerequisite**

The SQL Server instance is connected. For more information, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

<span id="precautions"></span>
## **Precautions**


* It can only be used to modify databases that are in the RESTORING or OFFLINE state.

* Statements with transactions cannot be inserted for execution.

* Only one database can be modified at a time.

* The state of the system library cannot be modified.

* Only highly privileged user accounts veyun_user have permission to modify the database state.


<span id="operation-steps"></span>
## **Operation steps**

Execute the following command to modify the status of the database to Online. Where `@DBName` is used to specify the database to be modified.

```sql
Exec [msdb].[dbo].[rds_modify_db_online] '@DBName'
```
