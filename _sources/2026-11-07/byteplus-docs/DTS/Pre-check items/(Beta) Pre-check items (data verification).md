---
title: "(Beta) Pre-check items (data verification)"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/beta-pre-check-items-data-verification"
---

Database Transmission Service (DTS) performs various checks on databases when creating data verification tasks. This topic introduces the details of check items.


|**Database type** |**Check item** |**Verification method** |**Level** |**Check content** |**Remarks** |
|---|---|---|---|---|---|
|MySQL |Environment detection |* Increment verification<br><br>* Full data verification<br><br>* Schema verification<br><br>* Full row verification |Warning |Environment check. |None |
||Database connection and architecture wildcard rule check |* Increment verification<br><br>* Full data verification<br><br>* Schema verification<br><br>* Full row verification |Error |Database connection and structure wildcard rule verification. |None |
||Source database connectivity check |* Increment verification<br><br>* Full data verification<br><br>* Schema verification<br><br>* Full row verification |Error |Check whether the data transmission server can connect to the source database. |None |
||Source database version detection |* Increment verification<br><br>* Full data verification<br><br>* Schema verification<br><br>* Full row verification |Error |Check whether the source database version is supported. |None |
||Source database permission detection |Increment verification |Error |Check whether the account privileges of the source database meet the migration requirements. |* Check if the source database has `REPLICATION SLAVE` and `REPLICATION CLIENT` permissions.<br><br>* The password for the source database account can not exceed 32 characters. |
||Source database binlog enablement check |Increment verification |Error |Check whether the source database has enabled binlog. |Binlog parameters must meet the following requirements simultaneously:<br><br><br>* `log_bin` value is `ON`.<br><br>* `binlog_format` value is `ROW`.<br><br>* For RDS for MySQL 5.6.2 and later, `binlog_row_image` value is `FULL`. |
||Source database ServerID check |Increment verification |Warning |Check whether the ServerID of the source database is 1. If it is 1, the system can not confirm whether ServerID is configured. |If the ServerID of the source database is 1, the system can not confirm whether ServerID is configured. You need to confirm it by yourself. |
||Check source database log_slave_updates |Increment verification |Warning |Check source database log_slave_updates. |None |
||Source database gtid mode enablement check |Increment verification |Error |Check whether the source database has enabled gtid mode. |The parameter `gtid mode` of the source database instance must be set to `ON`. |
||Target database connectivity check |* Increment verification<br><br>* Full data verification<br><br>* Schema verification<br><br>* Full row verification |Error |Check whether the data transmission server can connect to the target database. |None |
||Target database version detection |* Increment verification<br><br>* Full data verification<br><br>* Schema verification<br><br>* Full row verification |Error |Check whether the target database version is supported. |None |
||Target database permission check |Increment verification |Error |Check whether the account privileges of the target database meet the migration requirements. |* Check if the target database has `REPLICATION SLAVE` and `REPLICATION CLIENT` permissions.<br><br>* The password for the target database account can not exceed 32 characters. |
||Target database binlog enablement check |Increment verification |Error |Check whether the target database has enabled binlog. |Binlog parameters must meet the following requirements simultaneously:<br><br><br>* `log_bin` value is `ON`.<br><br>* `binlog_format` value is `ROW`.<br><br>* For RDS for MySQL 5.6.2 and later, `binlog_row_image` value is `FULL`. |
||Target database ServerID check |Increment verification |Warning |Check whether the ServerID of the target database is 1. If it is 1, the system can not confirm whether ServerID is configured. |If the ServerID of the target database is 1, the system can not confirm whether ServerID is configured. You need to confirm it by yourself. |
||Check the target database log_slave_updates. |Increment verification |Warning |Check the target database log_slave_updates. |None |
||Target database gtid mode enablement check |Increment verification |Error |Check whether the target database has enabled gtid mode |The incremental verification task must be enabled. |
|MongoDB |Environment detection. |* Full data verification<br><br>* Increment verification<br><br>* Full row verification<br><br>* Full primary key verification |Error |Environment detection. |* Replica set instance type<br><br>* Sharded cluster instance type |
||Database connection and architecture wildcard rule check |* Full data verification<br><br>* Increment verification<br><br>* Full row verification<br><br>* Full primary key verification |Error |Database connection and schema wildcard rule check. |* Replica set instance type<br><br>* Sharded cluster instance type |
||Source database connectivity check |* Full data verification<br><br>* Increment verification<br><br>* Full row verification<br><br>* Full primary key verification |Error |Check whether the data transmission server can connect to the source database. |* Replica set instance type<br><br>* Sharded cluster instance type |
||Target database connectivity check |* Full data verification<br><br>* Increment verification<br><br>* Full row verification<br><br>* Full primary key verification |Error |Check whether the data transmission server can connect to the target database. |* Replica set instance type<br><br>* Sharded cluster instance type |
||Existence check of source synchronization objects |* Full data verification<br><br>* Increment verification<br><br>* Full row verification<br><br>* Full primary key verification |Error |Check whether the source synchronization objects exist. |* Replica set instance type<br><br>* Sharded cluster instance type |
||Source end mongos connection check |* Full data verification<br><br>* Increment verification<br><br>* Full row verification<br><br>* Full primary key verification |Error |Check whether the source mongos address is correct. |Sharded cluster instance type |
||Destination mongos connection check |* Full data verification<br><br>* Increment verification<br><br>* Full row verification<br><br>* Full primary key verification |Error |Check whether the target mongos address is correct. |Sharded cluster instance type |
||Source database oplog enablement check |Increment verification |Error |Check whether the source database has enabled oplog. |* Replica set instance type<br><br>* Sharded cluster instance type |
||Target database oplog enablement check |Increment verification |Error |Check whether the target database has enabled oplog. |* Replica set instance type<br><br>* Sharded cluster instance type |
|PostgreSQL |Environment detection |Full data verification |Warning |Environment detection |None |
||Database connection and schema wildcard rule check |Full data verification |Error |Database connection and schema wildcard rule check. |None |
||Source database connectivity check |Full data verification |Error |Check whether the data transmission server can connect to the source database. |None |
||Source database version detection |Full data verification |Error |Check whether the source database version is RDS for PostgreSQL 10, RDS for PostgreSQL 11, RDS for PostgreSQL 12, RDS for PostgreSQL 13, or RDS for PostgreSQL 14. |None |
||Check whether the source database and table schema have a uniqueness constraint |Full data verification |Warning |Check whether the source database and table schema have a uniqueness constraint. |None |
||Target database connectivity check |Full data verification |Error |Check whether the DTS can connect to the target database. |None |
||Target database version detection |Full data verification |Error |Check whether the target database version is RDS for PostgreSQL 10, RDS for PostgreSQL 11, RDS for PostgreSQL 12, RDS for PostgreSQL 13, or RDS for PostgreSQL 14. |None |
||Database & table nonexistence check for the target database |Full data verification |Error |During full migration, check whether the databases and tables in the target database do not exist. |None |
||Source\-target database LC_MONETARY consistency check |Full data verification |Warning |Check whether the LC_MONETARY of the source database and the target database are consistent. |None |
||Character set encoding check |Full data verification |Warning |Check whether the character set encoding of the source database and the target database is consistent. |None |
