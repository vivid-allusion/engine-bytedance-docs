---
title: "Account permission description"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Account_permission_description"
---

The NDB for MySQL instance supports super accounts and normal accounts. After the account is created, the account type cannot be switched.

## Account type description

|Account type |Description |
|---|---|
|Super account |The super account has all permissions for all databases under the specified instance, and can manage all normal accounts and databases. Meet personalized and granular rights management requirements, such as assigning query permissions to different tables by user.<br><br><br>* Super accounts can be created synchronously when an instance is created, or they can be created after an instance is created. An instance can only create one super account.<br><br>* Super accounts can disconnect from other normal accounts in the current instance. |
|Normal account |Normal accounts do not have any permissions for any database by default, and need to manually grant permissions for specific databases to normal accounts. Normal accounts cannot create and manage other accounts, nor can they disconnect from other accounts.<br><br><br>* You can create and manage normal accounts through the console, API, or SQL statements.<br><br>* An instance can create multiple normal accounts, and the specific number depends on the instance kernel. |

## Precautions

* Normal accounts created after August 31, 2026 have `PROCESS`, `REPLICATION SLAVE`, and `REPLICATION CLIENT` permissions by default. To view them, log in to the DBW workbench and run `SHOW GRANTS;`. Normal accounts created before this date do not have these three permissions. Use a Super account to log in to the DBW workbench and execute the following statements to grant the corresponding permissions to the Normal account.

   ```SQL
   GRANT PROCESS, REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'username'@'host';
   ```

* The `SHOW_ROUTINE` permission only applies to instances compatible with community MySQL 8.0.20 and later. This permission is not available for MySQL 5.7. For detailed information about veDB MySQL versions, refer to [Version management](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Version_number_management).

* Super accounts on older version instances do not have the `SHOW_ROUTINE` permission. If an instance lacks this permission, reset the Super account permissions in the console to grant the `SHOW_ROUTINE` permission. For details, refer to [Resetting super account permissions](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Resetting_super_account_permissions).

* Granting the `SHOW_ROUTINE` permission to a Normal account is not supported in the console. Use a Super account to log in to the DBW workbench and execute the following statements to grant the permission.

   ```SQL
   GRANT SHOW_ROUTINE ON *.* TO 'test_user'@'%'; FLUSH PRIVILEGES; 
   ```

## Account permission list

|**Account type** |**Authorization type** |**Privilege** |
|---|---|---|
|**Super account** |**All permissions** |`SELECT`、`INSERT`、`UPDATE`、`DELETE`、`CREATE`、`DROP`、`RELOAD`、`PROCESS`、`REFERENCES`、`INDEX`、`ALTER`、`CREATE TEMPORARY TABLES`、`LOCK TABLES`、`EXECUTE`、`REPLICATION SLAVE`、`REPLICATION CLIENT`、`CREATE VIEW`、`SHOW VIEW`、`CREATE ROUTINE`、`ALTER ROUTINE`、`EVENT`、`TRIGGER`、`CREATE USER`、`SHOW_ROUTINE` |
|**Normal account** |**Read/Write (DDL+DML)**  |`SELECT`、`INSERT`、`UPDATE`、`DELETE`、`CREATE`、`DROP`、`REFERENCES`、`INDEX`、`ALTER`、`CREATE TEMPORARY TABLES`、`LOCK TABLES`、`EXECUTE`、`CREATE VIEW`、`SHOW VIEW`、`CREATE ROUTINE`、`ALTER ROUTINE`、`EVENT`、`TRIGGER`、`PROCESS`、`REPLICATION SLAVE`、`REPLICATION CLIENT` |
||**Read\-only** |`SELECT`、`LOCK TABLES`、`SHOW VIEW`、`PROCESS`、`REPLICATION SLAVE`、`REPLICATION CLIENT` |
||**DDL only** |`CREATE`、`DROP`、`INDEX`、`ALTER`、`CREATE TEMPORARY TABLES`、`LOCK TABLES`、`CREATE VIEW`、`SHOW VIEW`、`CREATE ROUTINE`、`ALTER ROUTINE`、`PROCESS`、`REPLICATION SLAVE`、`REPLICATION CLIENT` |
||**DML only** |`SELECT`、`INSERT`、`UPDATE`、`DELETE`、`CREATE TEMPORARY TABLES`、`LOCK TABLES`、`SHOW VIEW`、`EXECUTE`、`EVENT`、`TRIGGER`、`PROCESS`、`REPLICATION SLAVE`、`REPLICATION CLIENT` |
||**Custom privilege** |You can customize the authorization of any one or more of the following permissions:<br><br>`SELECT`、`INSERT`、`UPDATE`、`DELETE`、`CREATE`、`DROP`、`REFERENCES`、`INDEX`、`ALTER`、`CREATE TEMPORARY TABLES`、`LOCK TABLES`、`EXECUTE`、`CREATE VIEW`、`SHOW VIEW`、`CREATE ROUTINE`、`ALTER ROUTINE`、`EVENT`、`TRIGGER`<br><br>> **tip**<br><br><br>> Includes `PROCESS`, `REPLICATION SLAVE`, and `REPLICATION CLIENT` permissions by default.<br> |
