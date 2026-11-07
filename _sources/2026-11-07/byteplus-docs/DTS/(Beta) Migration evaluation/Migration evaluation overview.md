---
title: "Migration evaluation overview"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Migration_evaluation_overview"
---

Before the actual data migration, Database Transmission Service (DTS) supports a comprehensive evaluation and analysis of the source database, including pre\-check evaluation of instance status, migration task dependencies, etc., which improves the success rate and efficiency of the data migration task, helps to identify and solve potential problems in advance, reduce risks, control costs, and helps you efficiently and comprehensively migrate from other databases to BytePlus database, ensure the smooth completion of the migration process.

<span id=".5LyY5Yq_"></span>
## Advantages


* **Reduce risks**: By pre\-assessing and identifying potential problems, you can reduce the risks during the data migration process and ensure data integrity and smooth advancement of the migration process.

* **Improve efficiency**: Estimating migration time and resource requirements helps optimize the migration process, allocate resources reasonably, and improve migration efficiency.

* **Ensure business continuity**: The evaluation helps to select the optimal migration time window, minimize the impact on business, and ensure the continuous development of business.

* **Cost control**: By accurately assessing resource requirements, you can effectively control migration costs and avoid waste of resources.

* **Source database data analysis and target database configuration recommendations**: Assist in analyzing source database data and other information before going to the cloud, and provide configuration recommendations for the target database.

* **Identify obstacles to data migration**: Identify obstacles that will affect data migration in advance.

* **Solve compatibility issues**: Data migration evaluation can check the compatibility of source data and target environment in terms of system parameter configuration, time zone, character set, etc., to ensure that data can be migrated smoothly and ensure the normal operation of business.


<span id=".6LS555So"></span>
## Billing

No billing is charged during the promotion period.

<span id=".5b2x5ZON"></span>
## Impact

The migration evaluation task basically has no impact on the business.

<span id=".5pSv5oyB55qE5Zyw5Z-f"></span>
## Supported region

The following regions are currently supported for migration evaluation tasks:


|**Region** ||**RegionId** |
|---|---|---|
|China |China (Shanghai) |cn\-shanghai |
||China (Beijing) |cn\-beijing |
||China (Guangzhou) |cn\-guangzhou |
||China (Hong Kong) |cn\-hongkong |
|Overseas |Asia Pacific (Johor) |ap\-southeast\-1 |
||Asia Pacific (Jakarta) |ap\-southeast\-3 |


<span id=".5pSv5oyB55qE5pWw5o2u5rqQ"></span>
## Supported data source


|**Database type** |**Source database** |**Target database** |
|---|---|---|
|MySQL |* MySQL connected over public network<br><br>* MySQL connected over express network |* BytePlus RDS for MySQL<br><br>* NDB for MySQL |


<span id=".6L-B56e76K-E5Lyw5Yqf6IO9"></span>
## Migration evaluation function

When performing migration evaluation, Database Transmission Service (DTS) conducts evaluations based on evaluation types such as basic information, system configuration, migration dependency, object compatibility, specifications recommended, and migration duration. In addition, specific reasons are provided for items with evaluation risks and those that did not pass the evaluation.

<span id=".5Z-65pys5L-h5oGv"></span>
### Basic information


|**Evaluation item** |**Evaluation content** |
|---|---|
|Source instance TDE check |Check whether the source instance contains tables with TDE encryption enabled. |
|Source instance and target instance versions |Whether to support migration from source version to target version. |
|Source instance metadata read permissions |Whether the source instance account can query `information_schema` database data. |
|View the permissions to define the source instance table |Whether the source instance account can execute the `show create table` statement. |
|View the permissions defined by the source instance view |Can the `Source` instance account execute the show create view statement? |
|Check the permissions to view the programmable object definitions of the source instance |Whether the source instance account can execute the `show create function/trigger/procedure` statement. |
|Source instance log reading permission |Whether the source instance account can execute the `show binary logs` statement. |


<span id=".57O757uf6YWN572u"></span>
### System configuration


|**Evaluation item** |**Evaluation content** |
|---|---|
|Whether the time zones of the source and target instances are consistent |The `time_zone` parameter of MySQL is used to set the time zone of the database server, control the return value of time functions (such as `NOW()`, `CURTIME()`), and the storage and display of `TIMESTAMP` type data. If not explicitly specified, it may cause time inconsistency between the application and the database. During master\-slave replication, ensure that the time zones of the master and slave nodes are consistent to avoid differences in the `TIMESTAMP` field due to time zone conversion. Supports global or session\-level configuration. It is recommended to align with the application time zone to ensure accurate and reliable time data processing. |
|Whether the default character set of the target is compatible with the source database |MySQL `character_set_database` parameters define the default character set for the database, which is automatically used to store data when a new table or column is not explicitly specified. It affects the encoding method of data writing and query, and needs to be consistent with the configuration of the connection character set to avoid garbled characters. If the database character set is not explicitly set, inherit this parameter value. It is recommended to align with the global character set (such as utf8mb4) to ensure data compatibility and multi\-language support. |
|Whether the default collation of the target is compatible with the source database |MySQL's `collation_database` parameter defines the default collation for the database, specifying rules for character comparison, sorting, and indexing (e.g., case sensitivity, accent handling, etc.). If the collation for a table or column is not explicitly set, this value is automatically inherited. It must be compatible with the character set (such as utf8mb4) to ensure the correctness of data query and Index optimization, and avoid resulting abnormal or performance problems caused by rule mismatch. It is recommended to be consistent with the global configuration. |
|Whether the case sensitivity settings of the table names of the source and target instances are consistent |MySQL's `lower_case_table_names` parameter controls how table names and database names are stored and compared:<br><br><br>* `0`: (default) case sensitive, stored by creation name.<br><br>* `1`: Case\-insensitive, and table names are stored in lowercase.<br><br>* `2`: (Only applicable to Windows) Retains the case upon creation but converts to lowercase during comparison.<br><br><br>It is used to solve the problem that the table cannot be recognized due to case\-sensitive differences in file names during migration across operating systems (such as Linux and Windows). It needs to be configured before initialization to avoid data conflicts. |
|Whether the transaction isolation level between the source and target is consistent |The `tx_isolation` parameter (renamed to `transaction_isolation` in the current version) of MySQL is used to set the default `isolation` level of transactions and control the `data` visibility and concurrent conflict handling methods between transactions, such as `READ UNCOMMITTED` and `REPEATABLE READ`. Different levels balance data consistency and concurrent performance, which needs to be adjusted according to the business scenario to avoid dirty reads, phantom reads, and other problems. It is recommended to configure based on application requirements and database load. |
|Whether the InnoDB_strict_mode of the Source and the Target is consistent |MySQL's `InnoDB_strict_mode` parameters enable the strict mode of the InnoDB storage engine to perform stricter syntax and configuration checks on DDL operations such as creating and modifying tables. If incompatible options are detected (such as invalid row format or excessive index key length), an error is reported directly instead of a warning to avoid potential data inconsistency or performance issues. It is recommended to enable it to ensure configuration compliance, especially during migration or upgrades to prevent implicit errors. |
|Whether the source and target InnoDB_large_prefix is consistent |MySQL's `InnoDB_large_prefix` parameter (5.7.7 + enabled by default) allows InnoDB tables to use longer Index prefixes (up to 3072 bytes), breaking through the default 767\-byte limit, and needs to be used with `ROW_FORMAT=DYNAMIC` or `COMPRESSED` and `InnoDB_file_format=Barracuda`. It is suitable for large field Index scenarios such as UTF8MB4 and other multi\-byte character sets to solve the `“index column size too large”` error. This parameter has been deprecated in higher versions because it is supported by default. |
|Are the source and target log_bin_trust_function_creators the same? |The `log_bin_trust_function_creators` parameter of MySQL is used to control whether to trust the creator of the Stored procedure or Trigger, so as to avoid errors caused by the Function not declaring attributes such as `DETERMINISTIC` and `NO SQL`. After it is enabled (set to `1`), users without SUPER permissions are allowed to create functions, but it is necessary to ensure that the function logic is secure, otherwise it may cause inconsistent master\-slave copy data due to non\-deterministic operations. It is recommended to enable it only in a trusted environment, or after strictly reviewing the function logic. |
|Whether the event_scheduler of the source and target are consistent |The `event_scheduler` parameter of MySQL is used to control the start and stop of the event scheduler (ON/OFF/DISABLED), and determines whether to automatically execute predefined event tasks (such as timed execution of SQL statements or stored procedures). When enabled (set to ON), automated operations such as data maintenance and statistics can be triggered periodically; when turned off (OFF or DISABLED), all event tasks are suspended. Make sure that the user has EVENT authority and the event status is ACTIVE. Applicable to scenarios such as scheduled log cleanup and data backup. Pay attention to the configuration of global variables and resource usage. |
|Are the sql_mode of the source and the target consistent |The `sql_mode` parameter of MySQL is used to define the syntax rule, data verification, and compatibility behavior when the server executes SQL statements. The combination of adjusted mode can control strictness, fault tolerance, and function support. Common modes include:<br><br><br>* Strict mode (such as `STRICT_TRANS_TABLES` or `STRICT_ALL_TABLES`): Prohibits illegal data insertion (such as overlength strings and invalid dates), and reports errors directly instead of truncating or filling default values.<br><br>* Traditional mode (`TRADITIONAL`): Combines strict mode with other restrictions (such as disabling division by zero and invalid dates) to simulate the strict verification of traditional databases.<br><br>* ANSI compatible (`ANSI`): Enables standard SQL behavior (such as quotation mark processing and function name resolution).<br><br>* Function control: For example, `ONLY_FULL_GROUP_BY` requires the `GROUP BY` clause to contain all non\-aggregated columns, and `NO_ZERO_IN_DATE` prohibits zero values in dates.<br><br><br>Reasonable configuration of `sql_mode` can ensure data consistency and avoid implicit errors, but note the default value differences in different MySQL versions (such as 5.7 + which contains strict mode by default). It is recommended to set it explicitly according to the application scenario to avoid compatibility issues during migration or upgrade due to mode changes. |


<span id=".6L-B56e75L6d6LWW"></span>
### Migration dependency


|**Evaluation item** |**Evaluation content** |
|---|---|
|Whether the binlog_format of the source instance is in row format |When the `binlog_format` of MySQL is set to `ROW`, the binary log records the change details of each row of data instead of the `SQL` statement execute, which ensures that the primary\-secondary copy data is strictly consistent and avoids logical errors in the secondary database caused by uncertain function (such as NOW(), `UUID()`) or trigger. This mode supports row\-level replication, reducing lock conflicts, but with a large log volume, it is suitable for scenarios that require high data accuracy. |
|Whether the source instance binlog_row_image is in full mode. |When the `binlog_row_image` of MySQL is set to `FULL`, the binary log records all column data of the modified row (complete row information before and after the change), ensuring that the data is absolutely consistent when the leader/follower replicates. This mode is suitable for scenarios that rely on full row data, such as triggers, foreign key constraints, or complex stored procedures, to avoid logic errors or recovery failures caused by some columns not being recorded. Although the log volume increases, the data security and reliability are higher, which is especially important for systems with strict consistency requirements. |
|Whether log_slave_updates is enabled for the source instance |When `log_slave_updates` of MySQL is set to `ON`, the replica database records the update operations synchronization from the primary database to its own binary logs, so that the replica database can be used as the primary database of other instances, and supports multi\-level copy architectures (such as chain or tree topology). This setting ensures that data changes in cascading copy are transmitted level by level. At the same time, it is convenient to establish a new copy link directly based on the replica database during disaster preparedness or adding a new replica database, which enhances the flexibility of the architecture, but will slightly increase the I/O and log storage overhead of the replica database. |
|Whether gtid_mode is enabled for the source instance |When the instance version of the source database is greater than or equal to 5.6, the parameter `gtid_mode` is set to `ON`.<br><br>When the MySQL version is earlier than 8.0 and the parameter `gtid_mode` is disabled, foreign key cascading deletion may fail during data migration, resulting in data differences.<br><br>When the primary database is down, the secondary database quickly locates unsynchronized transactions through GTID, reducing the risk of data loss. |
|Does the source instance contain tables without primary key? |Data consistency can not be guaranteed, and the target may have more data. |


<span id=".5a-56LGh5YW85a655oCn"></span>
### Object compatibility


|**Evaluation item** |**Evaluation content** |
|---|---|
|Migration object information |Number of tables/views/functions/ stored procedure/trigger/event. |
|Are the table character set and the collation compatible? |Whether the destination is compatible with the character set and verification set settings of the source table. |
|Whether the table contains the Memory engine |The memory engine can not guarantee data integrity. All data in its tables is lost when the instance restarts or during a switch between primary and secondary nodes.<br><br>Volcano RDS only supports the InnoDB storage engine, and Volcano InnoDB has many kernel optimizations and obvious performance advantages.<br><br>DTS will automatically convert it to InnoDB. |
|Does it contain a table with the MyISAM engine |MyISAM uses a table\-level locking mechanism, while InnoDB uses a row\-level locking mechanism. Therefore, InnoDB typically offers higher write efficiency.<br><br>MyISAM's data integrity protection is flawed, which can lead to data corruption or even loss. Most of these flaws are design issues that cannot be fixed without breaking compatibility.<br><br>Volcano InnoDB has done a lot of kernel optimization and has obvious performance advantages.<br><br>DTS will automatically convert it to InnoDB. |
|Whether to include tables of the MGRMyISAM engine |Volcano RDS does not support this engine. |
|Whether tables of other engines are included |Volcano RDS does not support non\-InnoDB engines, and DTS will automatically convert to the InnoDB engine. |
|Do table and column names contain the new keywords added in 8.0? |If the table name or column name is a keyword newly added in 8.0, use ```` to enclose it when using SQL. Otherwise, a syntax error will be reported in version 8.0. |


<span id=".6KeE5qC85o6o6I2Q"></span>
### Specifications recommended


|**Evaluation item** |**Evaluation content** |
|---|---|
|InnoDB buffer pool size |The InnoDB buffer pool is used to cache table data, indexes and auxiliary structures, reduce disk I/O operations, and significantly improve database read and write efficiency. Its size is set by `InnoDB_buffer_pool_size` parameters, which directly affects the data caching capacity. It is recommended to set it to 60%~80% of the physical memory (memory should be reserved for the system and other processes). If it is too small, frequent disk access will occur. If it is too large, memory resource competition may occur. |
|instance connection settings |The `max_connections` parameter of MySQL defines the maximum number of concurrent client connections allowed by the database. Reasonable settings can balance resource utilization and concurrency requirements: If the value is too low, connection requests will be rejected (such as the `“too many connections”` error). If the value is too high, memory or CPU resources may be exhausted, causing performance degradation. It needs to be adjusted according to the server configuration (memory, thread processing capability) and the actual load, and the resource reuse can be optimized through connection pool management to avoid the overhead of frequently creating connections. |
|Threadrunning number of active threads in the thread pool |It is used to indicate the number of active threads that are currently executing queries or transactions, reflecting the real\-time concurrent load of the database. Excessive levels of this metric may indicate lock contention, resource bottlenecks, or slow query build\-up, which requires optimizing connection pool configuration or troubleshooting performance issues in combination with other state parameters. |
|TPS and QPS metrics of the current source database |The current number of updates and queries executed per second. |
|Size of the source instance data space |The data space and index space of the database selected by the source instance. |
|Specifications recommended for the target |Based on the above performance indicators of the source instance, the Volcano RDS specifications recommended that meet the conditions are recommended. |


<span id=".6L-B56e75pe26ZW_"></span>
### Migration duration


|**Evaluation item** |**Evaluation content** |
|---|---|
|Size of the source instance data space |Only data space, excluding index space. |
|Source and target network latency |The network delay between the machine where the migration task is located and the source and target machines affects the read and write throughput. |
|Estimate the DTS migration speed. |The estimated migration speed is configured based on network latency, source, and target performance parameters. Bandwidth and other configurations are not considered here, and the actual migration speed may vary. |
|Estimated DTS Migration duration |The estimated migration duration is calculated based on the space occupied by the current table data and the estimated speed. The actual migration duration will be affected by the performance, load, and bandwidth of the source and destination machines. |


<span id=".55u45YWz5paH5qGj"></span>
## Relevant document


* [Creating a migration evaluation task](https://docs.byteplus.com/en/docs/DTS/Creating_a_migration_evaluation_task)

* [Managing migration evaluation tasks](https://docs.byteplus.com/en/docs/DTS/Managing_migration_evaluation_tasks)
