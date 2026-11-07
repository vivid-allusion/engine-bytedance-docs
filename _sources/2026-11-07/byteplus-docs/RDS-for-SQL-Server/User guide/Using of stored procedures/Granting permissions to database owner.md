---
title: "Granting permissions to database owner"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/granting-permissions-to-database-owner"
---

This article describes how to use stored procedures to grant database owner permissions.

<span id="prerequisite"></span>
## prerequisite

The SQL Server instance is connected. For more information, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

<span id="precautions"></span>
## Precautions


* Only highly privileged accounts `veyun_user` have permissions give database owner permissions.

* You cannot grant an account that already has permissions to the database.

* The new database owner ( `login1`) you want to change to must be a valid SQL Server login and no corresponding user must be created in the target database.

* Changing the database owner may affect certain objects and permission configurations in the database, so when adjusting permissions, it is recommended to verify the effect of the relevant measures in the testing environment before applying them to the production environment to prevent inappropriate permission settings from affecting the normal function of the application.

* Currently only database owner privileges are supported on instances of the base version type.


<span id="operation-steps"></span>
## Operation steps

Execute the following command to grant the owner privileges of database `testdb1` to the database account `login1`:


* Directly execute the command to grant database owner privileges:

   ```sql
   EXEC [master].[dbo].[sp_rds_change_dbowner] 'testdb1', 'login1';
   ```
   

* Executing with parameter names confers database owner privileges:

   ```sql
   EXEC [master].[dbo].[sp_rds_change_dbowner] @db_name='testdb1', @login_name='login1';
   ```
   


The parameters in the command are described as follows:


* `@db_name`: Database name, such as `'testdb1'`.

* `@login_name`: The login name of the new database owner, such as `'login1'`.
