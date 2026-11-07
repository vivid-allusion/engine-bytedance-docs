---
title: "Pre-check items (RDS for SQL Server)"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/pre-check-items-rds-for-sql-server"
---

Database Transmission Service (DTS) performs various checks on databases when creating RDS for SQL Server migration tasks. This topic introduces detailed instructions for each check item.


|**Check item** |**Database type** |**Check scope** |**Level** |**Check content** |**Remarks** |
|---|---|---|---|---|---|
|Environment detection. |* Source database<br><br>* Target database |* All logical migrations<br><br>* Physical backup |Warning |Check the running environment. |None |
|Target database connectivity check |Target database |* All logical migrations<br><br>* Physical backup |Error |Check whether the data transmission server can connect to the target database. |None |
|Target database existence check |Target database |Physical backup |Warning |Check whether the specified table or database exists in the target database. |None |
|Database connection and schema wildcard rule check |* Source database<br><br>* Target database |All logical migrations |Error |Check the database connection and schema wildcard rules. |None |
|Source database connectivity check |Source database |All logical migrations |Error |Check whether the data transmission server can connect to the source database. |None |
|Source database version detection |Source database |All logical migrations |Error |Check whether the source database version is RDS for SQL Server 2019. |None |
|Target database version detection |Target database |All logical migrations |Error |Check whether the target database version is RDS for SQL Server 2019. |None |
|Source database account privileges check |Source database |All logical migrations |Error |Check whether the account privileges of the source database meet the migration requirements. |None |
|Target database account privileges check |Target database |All logical migrations |Error |Check whether the account privileges of the target database meet the migration requirements. |None |
|Check the existence of target tables/databases |Target database |Schema migration |Warning |Check whether the specified table or database exists in the target database. |None |
|Target table/database existence check |Target database |Full migration |Error |Check whether the specified table or database exists in the target database. |None |
|Source and target same\-name table existence check |Target database |Full migration |Warning |Check whether there are tables with the same name on the source and target ends. |None |
|Check the existence of target tables/databases |Target database |Incremental migration |Warning |Check whether the specified table or database exists in the target database. |None |
|Source database full recovery mode check |Source database |Incremental migration |Error |Check whether the source database has started the full recovery mode. |None |
|SQL Server migration database count limit check |Source database |Incremental migration |Error |Check whether the RDS for SQL Server databases being migrated exceeds the limit. |None |
|RDS for SQL Server table\-level CDC count limit check |Source database |Incremental migration |Error |Check whether the number of tables with table\-level CDC enabled exceeds the scope. |None |
|Source instance name consistency check |Source database |Incremental migration |Error |Check whether the `srvname` field in the `sys.sysservers` view is consistent with the return value of the `SERVERPROPERTY` function. |None |
|Source parameter max text repl size check |Source database |Incremental migration |Error |Check whether the source parameter `max text repl size` equals `-1`. |None |
|Check tables in the same instance and database on the source and target ends |* Source database<br><br>* Target database |All logical migrations |Error |Check whether the source and target ends are the same instance and database & table. |None |
