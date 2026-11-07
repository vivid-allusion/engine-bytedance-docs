---
title: "Import data via MaterializedMySQL"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/import-via-materializedmysql"
---

To enhance real\-time data warehousing capabilities and facilitate the mapping of tables from MySQL to ByteHouse Enterprise, ByteHouse has introduced the MaterializedMySQL database engine. The ByteHouse service acts as a MySQL replica, allowing it to read the Binlog and execute DDL and DML requests. This enables real\-time synchronization of business databases based on the MySQL Binlog mechanism, making it suitable for scenarios where MySQL business data needs to be synchronized in real time to ByteHouse Enterprise for analysis. This tutorial describes the syntax, operation steps, and considerations for importing MySQL data into ByteHouse Enterprise using the MaterializedMySQL engine.

<span id="e4ee6487"></span>
# Function overview

When implementing MaterializedMySQL in ByteHouse Enterprise, the underlying engine uses a self\-developed [HaUniqueMergeTree](https://docs.byteplus.com/docs/bytehouse/hauniquemergetree) Engine that supports customizable version fields and the function of real\-time data deletion based on UNIQUE KEY, without introducing any additional fields. Additionally, ByteHouse has enhanced the stability and usability of the MaterializedMySQL engine.

Compared with the community\-native MaterializedMySQL engine, the MaterializedMySQL database engine in ByteHouse offers the following advantages:


1. **Simplify processes**: Data is deduplicated and updated in real time, simplifying business logic.

2. **A precise range**: The data synchronization range can be selected and modified, making it more convenient in practical applications.

3. **Stable synchronization**: It can optimize exception handling to minimize the risk of synchronization tasks being interrupted by unexpected issues.

4. **Source\-side pressure reduction**: Data can be sharded and stored across all nodes, with each database synchronized only once, reducing synchronization pressure on the source side.

5. **Intuitive operations and maintenance**: It can provide a visualized operation and maintenance module, enable real\-time monitoring of synchronization status, and support online repair of synchronization anomalies, and restarting synchronization tasks.


<span id="aec303ef"></span>
# Usage restrictions


* The currently supported MySQL versions are 5.6, 5.7, and 8.0.

* **Base table operations**: **Direct operations on tables in the MaterializedMySQL engine database are disabled by default.**  To adjust table contents, you can perform query operations (such as INSERT, ALTER, and so on) in ByteHouse. By setting the session\-level parameter `set force_manipulate_materialize_mysql_table = 1, distributed_ddl_entry_format_version = 2`, you can operate on the underlying table. After the adjustment, only tables in the ByteHouse MaterializedMySQL engine database are affected; MySQL source tables are not affected.

* **Creating base table replicas is prohibited**: In the MaterializedMySQL engine database, the ZooKeeper path for a table is `/clickhouse/[database_name]/[table_name]/UUID`, the replica is `{replica}`, and UUID is generated randomly. Tables in MaterializedMySQL exist as a single replica by default. It is prohibited to create additional replicas of these tables to form multiple replicas, as operations on newly added replicas may indirectly affect the tables in MaterializedMySQL and potentially cause data consistency issues.


<span id="eacde622"></span>
# Cautions


* ByteHouse supports connecting to MySQL source tables over public or private networks. Before performing the import operation, ensure that the network between ByteHouse and the MySQL source is reliable and stable.

* If you access via the public network, you may incur related charges. The specific billing rules should be based on each product's official documentation and actual bills. Please confirm the billing model in advance.


<span id="7986dff3"></span>
# Prerequisites


* If you are using a MySQL cloud database, you usually need to configure an access whitelist before you can connect to an external database. Please add the IP addresses of ByteHouse cluster nodes to the whitelist in the MySQL cloud database. If you are using a service such as [BytePlus RDS for MySQL](https://www.byteplus.com/en/product/rds-mysql), see [Configure an allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_allowlist_1) for details.

   The IP address of ByteHouse nodes can be obtained by navigating to **ByteHouse Enterprise Console** \> **Cluster management** \> **Cluster list** \> **Nodes**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86adac4e8de440a49a2217938fba722a~tplv-goo7wpa0wc-image.image) </span>

* Please ensure that the MySQL user you are using has the following MySQL database privileges:

   * RELOAD

   * REPLICATION SLAVE

   * REPLICATION CLIENT

   * SELECT PRIVILEGE

   * The `SELECT` privilege on the `mysql.user` table


<span id="69ee4438"></span>
# Basic syntax

<span id="c43fcd91"></span>
## Create a MaterializedMySQL database

When you create a new database in ByteHouse with the MaterializedMySQL engine, the system will automatically read the source data after the database is created. The syntax is as follows:

```SQL
CREATE DATABASE [IF NOT EXISTS] db_name [ON CLUSTER cluster]
ENGINE = MaterializeMySQL('host:port', ['database' | database], 'user', 'password')
[SETTINGS ...]
[TABLE OVERRIDE table_name (
    [COLUMNS (
        [name1 [type1] [DEFAULT|MATERIALIZED|ALIAS expr1] [TTL expr1], ...]
        [INDEX index_name1 expr1 TYPE type1(...) GRANULARITY value1, ...]
        [PROJECTION projection_name_1 (SELECT <COLUMN LIST EXPR> [GROUP BY] [ORDER BY]), ...]
        )]
        [ORDER BY expr]
        [PRIMARY KEY expr]
        [PARTITION BY expr]
        [SAMPLE BY expr]
        [TTL expr]
), ...]
```


<span id="fee24371"></span>
### Parameter description


|**Parameters** |**Required** |**Note** |
|---|---|---|
|IF NOT EXISTS |No |Determine whether the database to be created already exists. If the `db_name` database already exists, ByteHouse will not create a new database and:<br><br><br>* If a clause is specified, no exception is thrown.<br><br>* An exception is thrown if no clause is specified. |
|db_name |Yes |Customize your database name. |
|ON CLUSTER |No |Specify the cluster name, and create a database on the specified cluster.<br><br>To prevent database corruption, specify the cluster using `ON CLUSTER` when creating the database. If you execute SQL statements in the ByteHouse Enterprise console, you can also directly check **All nodes**. |
|host:port |Yes |URL and port number of the MySQL database. |
|database |Yes |MySQL database name. |
|user |Yes |MySQL database account. |
|password |Yes |MySQL database account password. |
|SETTINGS |No |See [Settings parameter descriptions](https://docs.byteplus.com/docs/bytehouse/import-via-materializedmysql#c879a9fe). |
|TABLE OVERRIDE |No |See [Custom schema (table override: TABLE OVERRIDE)](https://docs.byteplus.com/docs/bytehouse/import-via-materializedmysql#dbb5ca07). |


<span id="c879a9fe"></span>
### Settings parameter descriptions

You can configure the following settings as needed:


|**Settings** |**Type** |**Default value** |**Note** |
|---|---|---|---|
|max_rows_in_buffer |UInt64 |65505 |Maximum number of rows of data that can be cached in memory for a single table (cached data cannot be queried). When this number is exceeded, the data will be materialized and written to persistent storage. Default value: 65505. |
|max_bytes_in_buffer |UInt64 |1048576 |Maximum number of bytes of data that can be cached in memory for a single table (cached data cannot be queried). When this number is exceeded, the data will be materialized and then persistently written to storage. Default value: 1048576. |
|max_flush_data_time |UInt64 |1000 |The maximum duration for which data can be cached in memory at the database level, in milliseconds (cached data cannot be queried). When this duration is exceeded, the data will be materialized and persistently written to storage. Default value: 1000. |
|max_wait_time_when_mysql_unavailable |Int64 |1000 |Retry interval when MySQL is unavailable, in milliseconds. A negative value disables retries; setting the value to 0 triggers an immediate retry. Default value: 1000. |
|allows_query_when_mysql_lost |Bool |true |It defines whether querying materialized tables is allowed when the MySQL connection is disconnected. It can be set to true (allowed) or false (not allowed). Default value: true. |
|skip_error_count |Int64 |0 |Number of skipped DML and DDL errors during MaterializedMySQL data synchronization. Negative values indicate that all errors are skipped, while other values indicate that a specified number of errors are skipped. Default value: 0. |
|include_tables |String |'' |If this parameter is configured, the system synchronizes only tables that meet the conditions. Table names are separated by commas; regular expressions are supported.<br><br>You can only set one of the parameters: `include_tables` or `exclude_tables`. If both parameters are set at the same time, the system will throw an error. If both parameters are not set, the database will synchronize all tables. Default: ''.<br><br>If you adjust this parameter at the database level, the system will then check whether there are any new tables that need to be synchronized. |
|exclude_tables |String |'' |If this parameter is configured, all eligible tables will not be synchronized. Table names are separated by commas; regular expressions are supported.<br><br>You can only set one of the parameters: `include_tables` or `exclude_tables`. If you set both parameters at the same time, the system will throw an error. If neither of these parameters is set, the database will synchronize all tables. Default: ''.<br><br>If you adjust this parameter at the database level, the system will then check whether there are any new tables that need to be synchronized. |
|skip_ddl_patterns |String |'' |If this parameter is configured, all qualifying DDL queries will not be executed. DDL mode is comma\-separated, supports regular expressions, and is case\-insensitive. If this parameter is not set or is empty, all DDL queries will be executed. |
|skip_unsupported_ddl |Bool |true |It defines whether to skip unsupported DDL operations except for CREATE, DROP, RENAME, and TRUNCATE TABLE. See [DDL](https://docs.byteplus.com/docs/bytehouse/import-via-materializedmysql#b3bc0d28) for the DDL operations currently supported by ByteHouse MaterializedMySQL. |
|skip_unsupported_tables |Bool |true |Whether to skip unsupported tables, such as tables without a primary key. |
|skip_sync_failed_tables |Bool |false |It defines whether tables that failed to synchronize should be skipped to avoid blocking the entire synchronization process. |
|resync_table_task_schedule_time_ms |UInt64 |1000 |Scheduling interval for the resynchronize table task, in milliseconds. |
|resync_table_task_fail_retry_time |UInt64 |5 |Number of retry attempts when table resynchronization fails. |
|max_insert_wait_seconds_for_unique_table_leader |UInt64 |30 |Maximum wait time for the unique key table to become the leader (leader), measured in seconds. |
|shard_mode |Bool |false |It defines whether the MaterializedMySQL database will synchronize MySQL data to ByteHouse in a distributed manner. You can set the value to false or true. Alternatively, you can set the value to 0 (corresponding to false) or 1 (corresponding to true), and the system will convert it accordingly. This value cannot be modified after the database is created. |
|zookeeper_session_expiration_check_period_s |UInt64 |60 |ZooKeeper session expiration check interval in sharding mode, in seconds. |
|execute_dml_fail_max_retry_timeout_s |UInt64 |600 |Retry timeout when a DML operation fails, in seconds. For the DML operations currently supported by ByteHouse MaterializedMySQL, see [DML](https://docs.byteplus.com/docs/bytehouse/import-via-materializedmysql#b802cb60). |
|retry_execute_dml_sleep_ms |UInt64 |2000 |Wait time between retry executions of DML commands, in milliseconds. |
|inner_query_distributed_ddl_task_timeout |UInt64 |30 |The timeout period for all hosts in the cluster to respond to DDL queries.<br><br>If a DDL request is not completed on all hosts, the response will contain a timeout error, and the request will continue to execute in asynchronous mode. A negative value indicates that there is no timeout limit, while 0 indicates direct execution in asynchronous mode. |
|max_concurrent_resync_task_num |UInt64 |5 |The maximum number of resynchronization (resync) tasks that can be executed concurrently at the database level.<br><br>When the number of tasks in the MaterializedMySQL database reaches the limit, newly added tables pending resync will wait for other tasks to complete. |
|resync_table_per_task |UInt64 |5 |The maximum number of tables to be resynchronized contained in a single MaterializedMySQLResyncTask (resynchronization task). At each scheduling cycle, a task is created by selecting `resync_table_per_task` tables from the MaterializedMySQL database, and table synchronization is performed. |
|parallel_in_resync_task |Bool |false |It defines whether the full synchronization of multiple tables can be performed in parallel within the same resynchronization task. |
|resync_position_diff |UInt64 |15000 |Position difference when a resynchronization task ends or merges into the main synchronization thread (for synchronization progress alignment). |
|merge_resync_task_sleep_ms |UInt64 |1000 |The waiting time interval when merging a resynchronization task into the main synchronization thread (unit: milliseconds). |


<span id="dbb5ca07"></span>
### Custom schema (TABLE OVERRIDE)

Table override can be used to customize ByteHouse DDL queries, allowing you to adjust the table structure rules within the MaterializedMySQL engine database in ByteHouse without modifying the original MySQL source data.

When the table structure or partitioning of MySQL source data does not meet ByteHouse performance requirements, you can use `TABLE OVERRIDE` to specifically modify the rules for certain tables when creating a ByteHouse MaterializedMySQL database. This operation does not affect MySQL source data and does not require modifying all synchronized tables. You can specify target tables and configure rules as needed.

A common use case for this feature is partition management. For example, if the source data in MySQL is not partitioned, after syncing to ByteHouse, you can partition by time to improve query efficiency. You can use `TABLE OVERRIDE...PARTITION BY` to specify partitioning and enhance query performance.

You can perform the following operations on schema conversion for rewritten MaterializedMySQL tables:


* Modify column type: The type must be compatible with the original type, otherwise the copy will fail. For example, you can change the **UInt32** column to **UInt64**, but you cannot change the **String** column to **Array(String)** . See [Data types](https://docs.byteplus.com/docs/bytehouse/import-via-materializedmysql#2a3cbe27) below for the mapping relationship between MySQL and ByteHouse data types.

* Modify column\-level TTL

* Modify the column compression codec

* Add alias columns

* Add skipping indices

* Add projections

* Modify partition key (PARTITION BY)

* Modify the sort key (ORDER BY)

* Modify the primary key (PRIMARY KEY)

* Add sampling rules (SAMPLE BY)

* Add a table\-level TTL (table TTL)


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If used improperly, table overwrite will interrupt data synchronization between MySQL and ByteHouse. For example:</div>



* <div data-tips="true" data-tips-type="warning">If a field is first added to ByteHouse by rewriting the table, and then a field with the same name is later added to the source table in MySQL, the following scenario may occur. At this point, ByteHouse will synchronize the 'add column' operation from MySQL and automatically execute the corresponding <code>ALTER TABLE</code> statement. This statement will fail because the column already exists, which also blocks subsequent data synchronization.</div>


* <div data-tips="true" data-tips-type="warning">Currently, ByteHouse does not check whether a field is nullable. For example, if your table rewrite rules use nullable fields as sort keys (<code>ORDER BY</code>) or partition keys (<code>PARTITION BY</code>), but ByteHouse actually requires non\-null fields for sort keys and partition keys, data queries will encounter issues after synchronization.</div>



<span id="57fa1570"></span>
### **Usage example**

```SQL
CREATE DATABASE demo_db_mysql
ENGINE = MaterializeMySQL('localhost:3306', 'db', 'user', '***')
SETTINGS parallel_in_resync_task = true, shard_mode = 1
TABLE OVERRIDE table1 (
    COLUMNS (
        userid UUID,
        category LowCardinality(String),
        timestamp DateTime CODEC(Delta, Default)
    )
    PARTITION BY toYear(timestamp)
),
TABLE OVERRIDE table2 (
    COLUMNS (
        ip_hash UInt32 MATERIALIZED xxHash32(client_ip),
        client_ip String TTL created + INTERVAL 72 HOUR
    )
    SAMPLE BY ip_hash
);
```


<span id="13a699cd"></span>
## Modify library parameters

After the ByteHouse MaterializedMySQL engine database is created, you can modify the database configuration parameters using the `ALTER` statement.


<Tabs>
<Tab zoneid="gLNcSftjj5" title="Distributed (shard_mode = 1)">
<TabTitle>Distributed (shard_mode = 1)</TabTitle>

**Grammar**:

```SQL
ALTER DATABASE db_name ON CLUSTER cluster_name MODIFY SETTING setting_name=value [, ...] 
```


**Example**:

```SQL
ALTER DATABASE demo_db_mysql ON CLUSTER bytehouse_demo_cluster MODIFY SETTING exclude_tables = 'table1,table2';
```



</Tab>
<Tab zoneid="bSPCpR5NNw" title="Non-distributed (shard_mode = 0)">
<TabTitle>Non-distributed (shard_mode = 0)</TabTitle>

**Grammar**:

```SQL
ALTER DATABASE db_name MODIFY SETTING setting_name=value [, ...]
```


**Example**:

```SQL
ALTER DATABASE demo_db_mysql MODIFY SETTING exclude_tables = 'table1,table2';
```



</Tab>
</Tabs>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Setting both <code>include_tables</code> and <code>exclude_tables</code> at the same time is not supported.</div>


* <div data-tips="true" data-tips-type="warning">The engine will check whether there are new tables that need to be synchronized after the parameters are adjusted. If new tables require synchronization, you can resynchronize them by following the steps in the table synchronization section below.</div>


* <div data-tips="true" data-tips-type="warning">Modification of the <code>shard_mode</code> parameter in this way is prohibited.</div>



<span id="17e29661"></span>
## Manually start, stop, or restart repository synchronization

ByteHouse allows you to manually start, stop, or restart database synchronization tasks.


<Tabs>
<Tab zoneid="WHTnXXbTBS" title="Distributed (shard_mode = 1)">
<TabTitle>Distributed (shard_mode = 1)</TabTitle>

**Grammar**:

```SQL
system start/stop/restart sync materialize mysql on cluster cluster_name db 
```


**Example 1**: Manually start a synchronization task

```SQL
system start sync materialize mysql on cluster bytehouse_demo_cluster demo_db_mysql
```


**Example 2**: Stop the synchronization task

```SQL
system stop sync materialize mysql on cluster bytehouse_demo_cluster demo_db_mysql
```


**Example 3**: Restart the synchronization task

```SQL
system restart sync materialize mysql on cluster bytehouse_demo_cluster demo_db_mysql
```



</Tab>
<Tab zoneid="EcyaiKo8Wn" title="Non-distributed (shard_mode = 0)">
<TabTitle>Non-distributed (shard_mode = 0)</TabTitle>

**Grammar**:

```SQL
system start/stop/restart sync materialize mysql db
```


**Example 1**: Manually start a synchronization task

```SQL
system start sync materialize mysql demo_db_mysql
```


**Example 2**: Stop a synchronization task

```SQL
system stop sync materialize mysql demo_db_mysql
```


**Example 3**: Restart the synchronization task

```SQL
system restart sync materialize mysql demo_db_mysql
```



</Tab>
</Tabs>


<span id="9653b060"></span>
## Table synchronization

ByteHouse supports restarting and canceling the restart process for full sync tables. If a table exception occurs during synchronization, the task status changes to sync_failed. You can execute the table synchronization command to restore the synchronization process for the table. The ByteHouse MaterializedMySQL engine maintains a list of tables pending resynchronization (resync table), and has a background thread to ***asynchronously*** perform the resynchronization process. You can use the `system.materialize_mysql_status` system table to query the list of tables that failed to synchronize and tables that are pending resynchronization. For details on how to query this system table, see [system.materialize_mysql_status](https://docs.byteplus.com/docs/bytehouse/import-via-materializedmysql#4a499da4).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When this command is executed, tables in the FullSync state will skip this command.</div>



<Tabs>
<Tab zoneid="nnTxmDmVW2" title="Distributed (shard_mode = 1)">
<TabTitle>Distributed (shard_mode = 1)</TabTitle>

**Grammar**:

```SQL
system [stop] resync materialize mysql table on cluster cluster_name db.table
```


**Example 1**: Cancel synchronization

```SQL
system stop resync materialize mysql table on cluster bytehouse_demo_cluster demo_db_mysql.demo_table
```


**Example 2**: Resynchronize

```SQL
system resync materialize mysql table on cluster bytehouse_demo_cluster demo_db_mysql.demo_table
```



</Tab>
<Tab zoneid="cUPAg3lWrF" title="Non-distributed (shard_mode = 0)">
<TabTitle>Non-distributed (shard_mode = 0)</TabTitle>

**Grammar**:

```SQL
system [stop] resync materialize mysql table db.table
```


**Example 1**: Cancel synchronization

```SQL
system stop resync materialize mysql table demo_db_mysql.demo_table
```


**Example 2**: Resynchronize

```SQL
system resync materialize mysql table demo_db_mysql.demo_table
```



</Tab>
</Tabs>


<span id="84cbe72f"></span>
# Steps

<span id="8ed4924a"></span>
## Step 1: Preparation

On the MySQL server, ensure that the following parameters are configured: Binlog is enabled, `binlog_format` is set to ROW, and GTID mode (Global Transaction ID) is enabled.


1. Log in to MySQL and check whether the binary log is enabled.

   ```SQL
   [root@node1 ~]# mysql -u root -password
   mysql> show variables like 'log_%';
   ```
   

   If the query result for the `log_bin` field is `off`, it means that the binary log is not enabled.

   
   |**Parameters** |**Parameter values** |
   |---|---|
   |log_bin |ON |
   

2. If binlog is enabled, please confirm that `binlog_format` and `binlog_row_image` are configured as follows:

   ```SQL
   mysql> show variables like 'binlog_format';
   mysql> show variables like 'binlog_row_image';
   ```
   

   
   |**Parameters** |**Parameter values** |
   |---|---|
   |binlog_format |ROW |
   |binlog_row_image |FULL |
   

3. Check whether the default authentication plugin setting is `mysql_native_password`.

   ```SQL
   mysql> show variables like 'default_authentication_plugin';
   ```
   

   
   |**Parameters** |**Parameter values** |
   |---|---|
   |default_authentication_plugin |mysql_native_password |
   

4. Confirm whether GTID mode is enabled.

   ```SQL
   mysql> show variables like 'gtid_mode';
   mysql> show variables like 'enforce_gtid_consistency';
   ```
   

   
   |**Parameters** |**Parameter values** |
   |---|---|
   |gtid_mode |ON |
   |enforce_gtid_consistency |ON |
   


If none of the above parameters are configured, you can refer to the following configuration example to set the parameters:

In the MySQL `/etc/my.cnf` file, under `[mysqld]`, write the following configuration.

```JavaScript
[mysqld]
# Specify a unique server-id
server-id=123
# Configure the log directory for Binlog
log-bin=/var/lib/mysql/mysql-bin
# Set the Binlog format to Row
binlog_format=ROW
binlog_row_image=FULL
# Set the default authentication plugin to mysql_native_password
default_authentication_plugin=mysql_native_password
# Enable GTID mode
gtid_mode=on
enforce_gtid_consistency=1
```


After completing the configuration, restart the MySQL service. You can then execute the above query commands one by one to check whether the binary log and the configuration of other parameters meet the requirements.

```SQL
[root@node1 ~]# service mysqld restart
[root@node1 ~]# mysql -u root -password
mysql> show variables like 'log_%';
mysql> show variables like 'binlog_format';
mysql> show variables like 'binlog_row_image';
mysql> show variables like 'default_authentication_plugin';
mysql> show variables like 'gtid_mode';
mysql> show variables like 'enforce_gtid_consistency';
```


<span id="04e8a81d"></span>
## Step 2: Create a source repository

Execute the following SQL statements in MySQL to create the MySQL source database and tables.

```SQL
mysql> CREATE DATABASE mysql_source;
mysql> CREATE TABLE mysql_source.test (a INT PRIMARY KEY, b INT);
```


<span id="37ec846f"></span>
## Step 3: Connect ByteHouse to MySQL

Create a MaterializedMySQL database in ByteHouse and query the database. At this point, you can query the tables synchronized from the MySQL source database in ByteHouse. When using the command, replace the placeholders in the command examples with actual parameter values. For parameter configuration instructions, see [Parameter description](https://docs.byteplus.com/docs/bytehouse/import-via-materializedmysql#fee24371).

```SQL
CREATE DATABASE demo_db_mysql
ENGINE = MaterializeMySQL('192.xx.xx.xxx:3306', 'mysql_source', 'user_name', 'password')
SETTINGS shard_mode = 1;

SHOW TABLES FROM demo_db_mysql;

-- Query result:
┌─name─┐
│ test │
└──────┘
```


<span id="c1640121"></span>
## Step 4: Test MySQL data synchronization


* Test table creation and data insertion

   Create tables and insert data in MySQL:

   ```SQL
   mysql> INSERT INTO mysql_source.test VALUES (1, 11), (2, 22);
   ```
   

   When querying synchronization status in ByteHouse, the results are consistent with those from the MySQL source table.

   ```SQL
   SELECT * FROM demo_db_mysql.test;
   
   -- Query result:
   ┌─a─┬──b─┐ 
   │ 1 │ 11 │ 
   │ 2 │ 22 │ 
   └───┴────┘
   ```
   

* Test deleting data, adding columns, and updating data

   Delete data, add columns, and update data in the MySQL source table.

   ```SQL
   mysql> DELETE FROM mysql_source.test WHERE a=1;
   mysql> ALTER TABLE mysql_source.test ADD COLUMN c VARCHAR(16);
   mysql> UPDATE mysql_source.test SET c='Wow!', b=222;
   mysql> SELECT * FROM mysql_source.test;
   
   -- Query result:
   +---+------+------+
   | a |    b |    c |
   +---+------+------+
   | 2 |  222 | Wow! |
   +---+------+------+
   ```
   

   When checking synchronization status in ByteHouse, the results are consistent with those from querying the MySQL source table.

   ```SQL
   SELECT * FROM demo_db_mysql.test;
   
   -- Query result:
   ┌─a─┬───b─┬─c────┐ 
   │ 2 │ 222 │ Wow! │ 
   └───┴─────┴──────┘
   ```
   


<span id="48a9b4a7"></span>
## Advanced usage: View system tables

You can view system tables to obtain synchronization information, synchronization task status, resynchronization task status, error information, logs, and more for the MaterializedMySQL database to assist with troubleshooting. For details, refer to the relevant sections below:


* [system.materialize_mysql_status](https://docs.byteplus.com/docs/bytehouse/import-via-materializedmysql#4a499da4): View the status of the MaterializedMySQL database.

* [system.materialize_mysql_resync_task_status](https://docs.byteplus.com/docs/bytehouse/import-via-materializedmysql#9390f6dd): View resynchronization task statuses.

* [system.materialize_mysql_log](https://docs.byteplus.com/docs/bytehouse/import-via-materializedmysql#804eb9dd): View log information.


<span id="304756b1"></span>
# Reference: Supported ByteHouse MaterializedMySQL engine

<span id="2a3cbe27"></span>
## Data types

All data types support being set to **nullable**.


|**MySQL** |**ByteHouse Enterprise** |
|---|---|
|TINY |Int8 |
|SHORT，SMALLINT |Int16 |
|MEDIUMINT，INT，INTEGER，INT32 |Int32 |
|BIGINT |Int64 |
|LONG |UInt32 |
|LONGLONG |UInt64 |
|FLOAT |Float32 |
|DOUBLE |Float64 |
|DECIMAL，NEWDECIMAL |Decimal |
|DATE，NEWDATE |Date |
|DATETIME，TIMESTAMP |DateTime |
|DATETIME2，TIMESTAMP2 |DateTime64 |
|ENUM |Enum |
|STRING |String |
|VARCHAR，VAR_STRING |String |
|BLOB |String |
|BINARY |FixedString |


<span id="b3bc0d28"></span>
## DDL


|**MySQL DDL** |**ByteHouse Enterprise** |
|---|---|
|CREATE TABLE |✔️ |
|DROP TABLE | **✔️**  |
|RENAME TABLE |✔️ |
|ADD COLUMN |✔️ |
|DROP COLUMN |✔️ |
|RENAME COLUMN |✔️ (ByteHouse Enterprise engine version must be 2.4 or above) |
|MODIFY COLUMN |✔️ (ByteHouse Enterprise engine version must be 2.4 or above) |


`RENAME COLUMN` and `MODIFY COLUMN` depend on the ByteHouse Enterprise engine version, which must be 2.4 or above. You can log in to the ByteHouse Enterprise console and check whether the engine version meets the requirements via the path **Cluster management** \> **Cluster list** \> **Cluster Name** \> **Basic information**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f03bcc227e734637b7e09095a0029ce9~tplv-goo7wpa0wc-image.image) </span>

<span id="b802cb60"></span>
## DML

The underlying engine of ByteHouse Enterprise Edition uses the HaUniqueMergeTree engine, and therefore directly supports INSERT, UPDATE, and DELETE operations.

<span id="d2a850d3"></span>
# Relevant reference: The system operations table

<span id="4a499da4"></span>
## system.materialize_mysql_status

You can use this system table to query the status of the MaterialMySQL database.

```SQL
SELECT * FROM system.materialize_mysql_status
```


In distributed mode (shard_mode=1), **only the leader node can query this information**. If you need to obtain information from this system table, you need to execute the following SQL:

```SQL
SELECT * FROM CLUSTER('<cluster_name>', system.materialize_mysql_status, (1,2))
```


**Column name description**


|**Column name** |**Type** |**Note** |
|---|---|---|
|mysql_info |String |MySQL connection information, in the format `ip:port`. |
|mysql_database |String |Synchronized MySQL database name. |
|database |String |Name of the database synchronized in ByteHouse. |
|shard_mode |UInt8 |Whether it is in distributed mode. |
|cluster_name |String |Specified cluster name. |
|zookeeper_path |String |ZooKeeper paths |
|sync_type |String |The possible values for synchronization status are as follows:<br><br><br>1. PreparingSync: Synchronization preparation phase;<br><br>2. FullSync: Full synchronization phase;<br><br>3. IncrementSync: incremental synchronization phase;<br><br>4. ManualStopSync: Synchronization is manually stopped;<br><br>5. ExceptionStopSync: Synchronization is stopped due to exception;<br><br>6. MergeResyncTaskSync: Execute the merging of resync tasks into the main sync thread. |
|include_tables |Array |Table names included in synchronization. |
|exclude_tables |Array |Table names excluded from synchronization. |
|resync_tables |Array |Tables being resynced. |
|seconds_behind_mysql |Int64 |Replication lag in MySQL has the same meaning as [Seconds_Behind_Master](https://dev.mysql.com/doc/refman/5.7/en/show-slave-status.html). When the library is not in the IncrementSync state, the value is \-1. |
|last_committed_position |String |The binlog position of the last commit. |
|last_executed_event |String |Content of the last executed binlog event. |
|total_position |String |The latest position of the binlog in MySQL. |
|error_count |UInt64 |Number of errors during synchronization. |
|already_skip_errors |UInt64 |Number of skipped errors. |
|last_error_msg |String |The last error message. |
|last_error_time |DataTime |The time of the last error occurrence. |
|sync_failed_tables |Array |Tables that failed to synchronize. |
|skipped_unsupported_tables |Array |Unsupported tables that have already been skipped. |


<span id="9390f6dd"></span>
## system.materialize_mysql_resync_task_status

You can use this system table to query the status of data synchronization tasks in the MaterialMySQL database.

```SQL
SELECT * FROM system.materialize_mysql_resync_task_status
```


In distributed mode (shard_mode=1), **only the leader node can query this information**. To obtain information from this system table, you need to execute the following SQL:

```SQL
SELECT * FROM CLUSTER('<cluster_name>', system.materialize_mysql_resync_task_status, (1,2))
```


**Column name description**

Among them, some columns have the same semantics as `system.materialize_mysql_status`, but they refer to different scopes. For example `error_count`:


* The `error_count` in `system.materialize_mysql_status` contains the number of errors for the main sync thread and resync tasks.

* `system.materialize_mysql_resync_task_status` error_count only includes the number of errors for the current resync task.



|**Column names** |**Type** |**Note** |
|---|---|---|
|mysql_info |String |MySQL connection information, in the format `ip:port`. |
|mysql_database |String |Name of the synchronized MySQL database. |
|database |String |The name of the synchronized database in the ByteHouse cloud database. |
|shard_mode |UInt8 |Whether it is in distributed mode. |
|cluster_name |String |The specified cluster name. |
|zookeeper_path |String |ZooKeeper path. |
|sync_type |String |Synchronization status: The possible values are as follows:<br><br><br>1. PreparingSync: Synchronization preparation stage;<br><br>2. FullSync: Full synchronization phase;<br><br>3. IncrementSync: It specifically refers to the incremental synchronization phase. |
|last_committed_position |String |The binlog position of the last commit. |
|last_executed_event |String |Content of the last executed binlog event. |
|total_position |String |The latest position of binlog in MySQL |
|error_count |UInt64 |Number of errors during synchronization. |
|already_skip_errors |UInt64 |Number of skipped errors. |
|last_error_msg |String |The last error information. |
|last_error_time |DataTime |Time of last error occurrence. |
|resync_tables_in_task |Array |Tables pending resync in the MaterializedMySQLResyncTask task. |
|sync_failed_tables_in_task |Array |Tables that failed to synchronize in the task. |
|skipped_unsupported_tables_in_task |Array |Unsupported tables skipped in the task. |


<span id="804eb9dd"></span>
## system.materialize_mysql_log

You can use this system table to query the logs of data synchronization tasks in the MaterialMySQL database.

Before use, you need to configure the following in the config.xml file. For details, refer to [Modify configuration parameters](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters).

```SQL
<materialize_mysql_log>
    <database>system</database>
    <table>materialize_mysql_log</table>
    <partition_by>toYYYYMM(event_date)</partition_by>
    <flush_interval_milliseconds>7500</flush_interval_milliseconds>
</materialize_mysql_log>
```


Query method:

```SQL
SELECT * FROM system.materialize_mysql_log ORDER BY event_time DESC limit 10;
```


In distributed mode (shard_mode=1), **the log is recorded only on the leader node**. To obtain information from this system table, you need to execute the following SQL:

```SQL
SELECT * FROM CLUSTER('<cluster_name>', system.materialize_mysql_log, (1,2)) ORDER BY event_time DESC limit 10;
```


**Column name description**


|**Column names** |**Type** |**Note** |
|---|---|---|
|database |String |Databases synchronized in the ByteHouse cloud database. |
|event_type |String |Log type, possible values are as follows:<br><br><br>1. Error: error log;<br><br>2. START_SYNC: Start synchronization;<br><br>3. MANUAL_STOP_SYNC: Synchronization is manually stopped;<br><br>4. EXCEPTION_STOP_SYNC: Abnormal stop of synchronization;<br><br>5. Resynchronize the table. |
|event_date |Date |The occurrence date. |
|event_time |DateTime |Time of occurrence. |
|resync_table |String |Resync the table name. |
|exception |String |Detailed exception information. |
|exception_source |String |Source of exception information to assist in determining the cause of `sync_failed_tables/skipped_unsupported_tables`:<br><br><br>1. `""`: The exception originates from some shared functions.<br><br>2. `MAIN_SYNC_TASK`: The exception originates from the main sync thread of the library.<br><br>3. `RESYNC_TASK`: The exception originates from the resync task. |
