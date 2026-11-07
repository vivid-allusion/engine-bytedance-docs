---
title: "Copying database"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/copying-database"
---

This article describes how to replicate a database using stored procedures.

<span id="prerequisite"></span>
## prerequisite

The SQL Server instance is connected. For more information, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

<span id="precautions"></span>
## Precautions


* Only highly privileged accounts `veyun_user` have permission to replicate the database. However, the highly privileged account of the read\-only instance `veyun_user` not have permission to replicate the database.

* The target library already exists and its status is Online.

* The process of executing the command cannot be interrupted, otherwise the execution will not be successful.

* Before executing a command, ensure that the target instance has enough storage space for the replicated database.

* If the database is large, it is recommended to perform it during low peak periods to reduce the impact of internet bandwidth usage on other services.


<span id="operation-steps"></span>
## Operation steps

Select the following command to copy the database:


* Directly replicate the database:

   ```sql
   EXEC [master].[dbo].[sp_rds_copy_database] 'testdb1', 'testdb2';
   ```
   

* Execute the command to copy the database with the parameter name:

   ```sql
   EXEC [master].[dbo].[sp_rds_copy_database] @dbname_source = 'testdb1', @dbname_target = 'testdb2';
   ```
   


Example of expected output:

After executing the above command, the system will display the result and status information. If the output is as follows, it indicates that the database was successfully copied.

```sql
Database 'testdb1' has been successfully copied to 'testdb2'.
```


The parameters in the command are described as follows:


* `@dbname_source`: Source database name.

* `@dbname_target`: The target database name, the length of the target database name should be within 2~ 60 characters.
