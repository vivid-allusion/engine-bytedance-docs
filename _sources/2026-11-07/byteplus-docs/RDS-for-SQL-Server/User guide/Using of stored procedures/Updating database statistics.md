---
title: "Updating database statistics"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/updating-database-statistics"
---

This article describes how to use stored procedures to update database statistics and provide query performance.

<span id="prerequisite"></span>
## prerequisite

The SQL Server instance is connected. For more information, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

<span id="precautions"></span>
## Precautions


* Statements with transactions cannot be inserted for execution.

* Cannot update system library or rdsadmin statistics.


<span id="operation-steps"></span>
## Operation steps

Execute the following command to update the statistics for the specified library.

```sql
EXEC master.dbo.rds_sp_updatestats '@DBname' ；
```


Where `@DBname` represents the name of the database that needs to update statistics.

The execution example is as follows:

```sql
EXEC master.dbo.rds_sp_updatestats 'testdb1' ；
```


The output after successful execution is as follows:

```sql
Statistics for all tables have been updated.
```
