---
title: "Deleting database"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deleting-database"
---

This article describes the steps to delete a database using a stored procedure.

<span id="prerequisite"></span>
## prerequisite

The SQL Server instance is connected. For more information, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

<span id="precautions"></span>
## Precautions


* Statements with transactions cannot be inserted for execution.

* Only one database can be deleted at a time.

* The system library or rdsadmin cannot be deleted.

* Only highly privileged user accounts veyun_user have permission to delete the database.


<span id="operation-steps"></span>
## Operation steps

Execute the following command to modify the database name. Where @DBName is used to specify the database to be deleted.

```sql
Exec [msdb].[dbo].[rds_drop_database] '@DBName'
```
