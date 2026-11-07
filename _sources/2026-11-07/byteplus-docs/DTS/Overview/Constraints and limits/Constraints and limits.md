---
title: "Constraints and limits"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Constraints_and_limits"
---

This topic outlines the limits and database contents for migrating or synchronizing Milvus databases, for example, BytePlus Milvus.

<span id="YLBhoUp8"></span>
## Supported databases


|**Source database** |**Target database** |**Supported versions** |**Synchronous** |
|---|---|---|---|
|* BytePlus RDS for MySQL<br><br>* BytePlus veDB for MySQL<br><br>* MySQL connected over public network<br><br>* MySQL connected over express network |* BytePlus Milvus<br><br>* Self\-built Milvus<br><br>* Milvus connected over express network |Milvus 2.5、2.6 |* Schema initialization<br><br>* Full initialization |
|BytePlus Milvus |BytePlus Milvus ||Full initialization |


<span id="TQy7wYQ3"></span>
## Limits


<Tabs>
<Tab zoneid="R3IJ5PmdlA" title="Milvus to Milvus">
<TabTitle>Milvus to Milvus</TabTitle>


|**Type** |**Description** |
|---|---|
|Source database limits |Milvus engine versions are 2.5 and 2.6. |
|Target database limits |Currently, only synchronization to BytePlus Milvus is supported, and the Milvus engine version must be 2.5. |
|Other limits |* Role/User permission synchronization is not currently supported.<br><br>* Synchronizing instances with SSL enabled is not supported.<br><br>* Milvus database supports Insert and Upsert write modes. For more details, refer to [Milvus primary fields and automatic recognition](https://milvus.io/docs/zh/primary-field.md#Overview). When synchronizing data, the differences and applicable scenarios of Insert and Upsert write modes are as follows.<br><br>   * Insert: Insert data directly using the Insert command. This applies when Collection has AutoID enabled, and data in the source and target ends (including primary key) are consistent. When DTS restarts or fetches data repeatedly, it may cause data redundancy in the destination.<br><br>   * Upsert: Insert data directly or update existing data using the Upsert command. This is suitable for updating existing data when Collection does not have AutoID enabled, or when Collection has AutoID enabled but business or verification does not rely on the primary key. When DTS restarts or fetches data repeatedly, it may lead to primary key inconsistency, affecting business or verification that depends on the primary key.<br><br>* During synchronization, do not change the instance configuration. Otherwise, the synchronization task will fail.<br><br>* When you want to achieve data synchronization through a dedicated line, you can [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |





</Tab>
<Tab zoneid="oOtXBkgrmS" title="MySQL to Milvus">
<TabTitle>MySQL to Milvus</TabTitle>


|**Type** |**Description** |
|---|---|
|**Source database limits**<br><br> |* Database version: RDS for MySQL 5.7 and 8.0 instances are supported.<br><br>* When the instance version of the source database is greater than or equal to 5.6, the parameter `gtid_mode` is set to `ON`.<br><br><br>When the MySQL version is earlier than 8.0 and the parameter `gtid_mode` is disabled, foreign key cascading deletion may fail during data migration, resulting in data differences.<br><br><br>* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal migration performance.<br><br>* Data migration supports storage engines including InnoDB, MyISAM, and RocksDB. During data migration, if the source database is not using the InnoDB storage engine, the system automatically converts it to InnoDB. MariaDB database engine is not supported currently.<br><br>* Partitioned tables are not supported when converting the MyISAM storage engine to the InnoDB storage engine.<br><br>* Tables to be migrated must have a primary key or a unique non\-null constraint, and their fields must be unique. Otherwise, data inconsistency may occur. If a table to be migrated is an extra\-large table and lacks a primary key or unique non\-null constraint, the data migration process may stall when the network is unstable.<br><br>* To perform incremental migration, the Binlog logs must meet the following requirements:<br><br>   * The Binlog feature must be enabled, and the parameter `binlog_format `set to` row`, `binlog_row_image` set to `full`. Otherwise, pre\-check will report an error, and data migration tasks can not start successfully.<br><br>   * Binlogs must be retained for at least 24 hours, and a retention period of more than seven days is recommended. Otherwise, the DTS task may fail because it can not obtain logs, potentially leading to data loss.<br><br>* Tables with foreign key dependencies must be migrated together, or data migration will fail.<br><br>* It is recommended that the number of tables in a single task should not exceed 20,000, and the number of databases should not exceed 1,000. When a large number of databases and tables need to be migrated, it is recommended to split them into multiple tasks. |
|**Target database limits** |Milvus engine versions are 2.5 and 2.6. |
|**Other limits**<br><br> |* Role/User permission synchronization is not currently supported.<br><br>* Prior to executing data synchronization, assess the performance of both source and target databases. It is also advised to perform synchronization during off\-peak business hours. Otherwise, during full data synchronization, DTS consumes certain read/write resources on both source and target databases, which may lead to an increase in database load.<br><br>* During synchronization, the target database may generate a large number of Binlog files, causing the target database disk usage to be much higher than that of the original instance. It is recommended to adjust the Binlog retention policy in the target database before migration or synchronization to prevent excessive storage usage by Binlog files.<br><br>* For data synchronization tasks with database or table name mapping, the mapping may not take effect after the stored procedure synchronization and function are synchronized.<br><br>* If the source database is RDS for MySQL 8.0, when configuring synchronization tasks, you must manually grant the relevant data synchronization permissions directly to the following accounts:<br><br>   * The accounts for the source or target database are granted relevant permissions through the Role.<br><br>   * The accounts that need to perform User synchronization are granted relevant permissions through the Role.<br><br>* Supports synchronization of tables, views, stored procedures, functions, triggers, and events only. |





</Tab>
</Tabs>


&nbsp;
