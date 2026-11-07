---
title: "Editing database name"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/editing-database-name"
---

This article describes the steps to modify a database name using a stored procedure.

<span id="prerequisite"></span>
## prerequisite

The SQL Server instance is connected. For more information, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

<span id="precautions"></span>
## Precautions


* Modifying the database name removes the database from the high availability group, along with the availability group for the database.

* You can only modify the name of one database at a time.

* Statements with transactions cannot be inserted for execution.

* You cannot modify the name of the system library or rdsadmin.

* The target inventory is in and the status is Online.

* The new database name cannot duplicate an existing database name, and cannot use the system library name or rdsadmin.


<span id="operation-steps"></span>
## Operation steps

Execute the following command to modify the database name.

```sql
Exec [msdb].[dbo].[rds_modify_db_name] '@OldDBName','@NewDBName';
```



* @OldDBName: Specifies the database to operate on.

* @NewDBName: Specify the new database name.
