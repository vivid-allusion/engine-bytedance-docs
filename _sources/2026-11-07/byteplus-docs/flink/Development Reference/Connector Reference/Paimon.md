---
title: "Paimon"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Connector_Paimon"
---

Paimon is a real\-time data lake solution based on stream and batch processing, combining efficient storage and flexible computing, specially designed for handling large\-scale real\-time data and streaming data. Paimon achieves efficient real\-time updates and querying capabilities by integrating the Log\-Structured Merge Tree (LSM Tree) structure, supporting a unified data processing model for streaming and batch operations. Its advantages include low latency, strong consistency, and easy scalability.

<span id="9e386cfe"></span>
# Features Highlights

Paimon offers the following features, for more details refer to the community [official documentation](https://paimon.apache.org/docs/0.8/concepts/overview/):

<span id="7e70744e"></span>
## Unified Storage

Paimon provides table abstraction, supporting data read and write operations in both batch and streaming processing modes.


* In batch processing mode, Paimon is similar to a Hive table, supporting various batch processing SQL operations and querying the latest snapshot.

* In streaming mode, Paimon is similar to a message queue, allowing queries for stream data similar to change logs in a message queue, and historical data does not expire.


<span id="9af09441"></span>
## Rich Ecosystem Support

**Multi\-Engine Ecosystem Support**: In addition to deep integration with Apache Flink, Paimon also supports other computing engines such as Apache Hive, Apache Spark, Trino, and StarRocks, offering flexible data read and write capabilities.

<span id="e5d399c8"></span>
## Efficient Storage and Query


* Paimon stores data in a columnar file format on file systems or object storage, with metadata kept in manifest files, supporting large\-scale storage and data skipping features to enhance query performance.

* For primary key tables, Paimon uses an LSM tree structure, supporting large\-scale data updates and high\-performance queries.


<span id="2b550d62"></span>
## **Flexible Data Read and Write Modes**


* **Reading Mode**: Supports reading data from historical snapshots (batch mode), the latest offset (streaming mode), or in a mixed mode for incremental snapshots.

* **Writing Mode**: Supports stream synchronization from database change logs (CDC) and batch insertion or overwrite of offline data.


<span id="dc23f16e"></span>
## Comprehensive Lake Management Capabilities


* Paimon's data storage is built on object storage TOS; based on these low\-cost, highly available distributed remote storage and scalable metadata management designs, Paimon offers complete data lake capabilities: including ACID, Schema Evolution, version rollback, Tags, and Branches.


<span id="3d589577"></span>
# Feature Details

<span id="6cf89227"></span>
## Data Table Types

**Primary Key Table:** 

The primary key table is the default table type in Paimon, allowing records to be inserted, updated, and deleted. Primary keys consist of columns, and the primary key values must be unique. Paimon sorts primary keys within storage buckets to ensure ordered data and high\-performance when filtering by primary key. The primary key table uses an LSM tree structure for data storage, supporting efficient read and write operations. It also supports partitioning and bucket mechanisms to enhance data management and query efficiency.

**Non\-Primary Key Table:** 


* **Append Table:** 


If a primary key is not defined for the table, it defaults to being an append table. In stream processing, append tables only support inserting complete records and are suitable for use cases like log data synchronization that do not require stream updates. By default, there's no concept of storage buckets, similar to Hive tables, where data files are organized and sorted by partitions to accelerate queries. In streaming write jobs, append tables have an automatic small file merging mechanism, facilitated by the Compact Coordinator and Compact Worker components, scanning and merging small files to enhance storage efficiency and query performance.


* **Append Queue:** 


Append queues are organized by storage buckets. Within the same storage bucket, records are arranged in the order they are written, and streaming reads are delivered downstream in this order, suitable for scenarios requiring data order preservation like log processing and event tracing. By default, all data enter a single storage bucket forming one queue, but users can increase parallelism and distribute loads by defining parameters. Append Queue supports automatic file compression to control the number of files, enhancing storage and query efficiency; during streaming reads, Paimon ensures data is delivered in the expected order based on partition and bucket sequence.

<span id="0b24e3d6"></span>
## Merge\-Engine

Paimon provides a variety of merging engines, supports different merging mechanisms, and is suitable for various scenarios. Here are the main merging engine mechanisms:

Detailed introductions to these merging engines are as follows:


|Merge Engine Types |Description |Applicable Scenarios |
|---|---|---|
|**Deduplication** |The default merge engine. Paimon only retains the latest record with the same, discarding the others. Specifically, if the latest record is an `DELETE` record, then all records with the same primary key will be deleted. You can ignore the delete operation by configuring `ignore-delete`. |Suitable for scenarios where it is necessary to ensure the uniqueness of the primary key and only care about the latest data. |
|**Partial Update** |Allows for the gradual perfection of each column of a record through multiple updates, i.e., updating the latest values of fields with the same primary key individually, but not overwriting non\-null values. By default, the partial update engine does not accept delete records; you can ignore deletion records by configuring `ignore-delete`, or manage partial columns by configuring `sequence-group`. |Suitable for scenarios that require gradual updates to parts of a record without affecting other fields. Suitable for scenarios involving multiple stream joins with primary keys. |
|**Aggregation** |Users are only concerned with aggregation results. According to the specified aggregation function, perform field\-level aggregation on records with the same primary key Each non\-primary key field can specify an aggregation function; fields without a specified function will default to use `last_non_null_value` aggregation |Suitable for scenarios that require data aggregation calculations, such as summing and counting |
|**First Row** |Preserves the first record with the same primary key, unlike the deduplication engine, the first row engine preserves the earliest record In this mode, the output changelog is an INSERT stream |Suitable for scenarios that require preserving the first appearance of a record, while ignoring subsequent updates |


<span id="79d03b88"></span>
## Changelog output mechanism

`changelog-producer` parameters control how tables generate changelogs when writing data. Different modes are suitable for different application scenarios; here are the main `changelog-producer` modes, their functions, and suitable scenarios:


|Mode Name |Function |Applicable Scenarios |
|---|---|---|
|**None** |Default mode, no additional change logs generated. Paimon sources can only see changes merged across snapshots and cannot form a complete change log. |Suitable for consumers who do not need a complete change log, such as database systems. It is important to note that Flink's built\-in "Normalize" operator persists the value of each key in the state, but this operation is costly and should be avoided as much as possible. |
|**Input** |Consider the input as a complete change log source; all input records will be saved in separate change log files and provided to consumers through Paimon sources. |Applicable when the input itself is a complete change log, such as Change Data Capture data from databases, or data generated by stateful computations in Flink. |
|**Lookup** |Generate change logs by looking up before data submission is committed. Paimon caches data on both memory and local disk to generate a complete change log. |This is suitable for cases where input cannot generate a complete change log and aims to avoid costly "Normalize" operations. It should be noted that the Lookup operation consumes certain resources and is more applicable to scenarios with high real\-time requirements (minute\-level). |
|**Full Compaction** |By comparing the results between full compactions, differences are generated as a change log. The delay of the change log is influenced by the frequency of full compaction. |This is suitable for scenarios with high latency that wish to decouple data writing from change log generation, such as generating a change log at intervals (e.g., hourly). This mode can reduce resources consumption but will increase the latency of the change log. |


<span id="63b245ee"></span>
# Restrictions


* Paimon connector currently only supports usage in **Flink 1.16\-byted** and higher engine versions.

* If using object storage TOS as the storage destination, it is necessary to pre\-build the storage Bucket, refer to [the documentation](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).


<span id="be3123d4"></span>
# Detailed SQL Syntax

<span id="99fb3bf6"></span>
## CREATE Catalog

Paimon engine supports multiple types of meta\-storages, here are the methods to create Filesystem Catalog and LAS Catalog:

<span id="080773de"></span>
### Filesystem Catalog

In this mode, both metadata and table files are stored in the filesystem.

```SQL
CREATE CATALOG my_catalog WITH (
  'type' = 'paimon',
  'warehouse' = 'tos://<bucket-name>/path/to/warehouse'
);
```


The above SQL statement creates a Paimon Catalog named `my_catalog`, with the data warehouse path as `tos://<bucket-name>/path/to/warehouse`.

<span id="3816cb24"></span>
### LAS Catalog

In this mode, the metadata is stored in the metadata storage service of LAS Catalog, and the table files are stored at the specified filesystem path.

```SQL
CREATE CATALOG my_hive WITH (
  'type' = 'paimon',
  'metastore' = 'hive',
  -- The Thrift endpoint of the LAS metadata service. Please ensure that the Region information is correctly configured.
  'uri' = 'thrift://lakeformation.las.cn-beijing.byteplus.com:48869',
  -- The Hive configuration directory, uploaded through the file module of the Flink job development interface.
  'hive-conf-dir' = '/opt/tiger/workdir', 
  -- The storage bucket directory path
  'warehouse' = 'tos://<bucket-name>/path/to/warehouse'
);
```


The above SQL statement creates a Paimon Catalog named`my_hive`, with metadata stored in the LAS Catalog, and the data warehouse path as `tos://<bucket-name>/path/to/warehouse`.

Additionally, when creating a job, you need to upload the corresponding hive.xml file on the job development interface:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26dc01ad6fcd435485470c0c11816ee0~tplv-goo7wpa0wc-image.image) </span>

The content of the hive.xml file is as follows:

```XML
      
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
  <property>
    <name>hive.server2.max.start.attempts</name>
    <value>5</value>
  </property>
  <property>
    <name>hive.client.las.region.name</name>
    <value>cn-shanghai</value>
  </property>
  <property>
    <name>hive.metastore.uris</name>
    <value>thrift://lakeformation.las.cn-shanghai.byteplus.com:48869</value>
  </property>
  <property>
    <name>hive.hms.client.is.public.cloud</name>
    <value>true</value>
  </property>
  <property>
    <name>hive.client.las.ak</name>
    <value>__LAS_ACCESS_KEY__</value>
  </property>
  <property>
    <name>hive.client.las.sk</name>
    <value>__LAS_ACCESS_KEY_SECRET__</value>
  </property>
</configuration>
```


Note that you must fill in the specific LAS Catalog and account AK/SK information. Then upload the hive.xml file through Job Development \- Dependencies.

Moreover, if you are using Flink\-1.16\-byted, the engine does not have a built\-in LAS Catalog connector and you need to manually upload the following JAR package to the dependencies:

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8188e4d3043544249fe41f1dff773c75~tplv-goo7wpa0wc-image.image" name="flink-sql-connector-hive-las-formation-3_2.12-1.16-byted-connector-SNAPSHOT.jar">flink-sql-connector-hive-las-formation-3_2.12-1.16-byted-connector-SNAPSHOT.jar</Attachment>


<span id="14e2c4c3"></span>
## CREATE TABLE

In the specified Catalog, you can use SQL statements to create a data table. Below is an example of creating a table with a primary key and partitions:

```SQL
-- Create Catalog
CREATE CATALOG `paimon_test` WITH (
  'type' = 'paimon',
  'warehouse' = 'tos://<bucket-name>/path/to/warehouse'
);

-- Create Database
CREATE DATABASE IF NOT EXISTS `paimon_test`.`test_db`;

-- Create DataTable
CREATE TABLE IF NOT EXISTS `paimon_test`.`test_db`.`doc_result` (
    word varchar,
    cnt bigint,
    PRIMARY KEY (word) NOT ENFORCED
) WITH (
    'bucket' = '4',  -- Control the number of buckets; it is recommended to store around 2GB of data per bucket.
    'changelog-producer' = 'input' -- Generate a changelog to enable downstream streaming reads.
);
```


With the above SQL syntax, users can create different types of Catalogs and data tables in Paimon to meet various business needs.

<span id="b07a12bf"></span>
## SQL INSERT

Paimon supports data writing to tables through Flink SQL, which mainly includes the following methods:


1. **Insert data (INSERT INTO):** 


By using the `INSERT INTO` statement, data can be inserted into the specified table. This operation is suitable for batch and stream processing jobs.

```SQL
INSERT INTO my_table
SELECT ...
```


In stream mode, by default, Paimon performs data compression, snapshot expiration, and even partition expiration (if configured) in Flink Sink.


2. **Overwrite the entire table (INSERT OVERWRITE):** 


For non\-partitioned tables, the `INSERT OVERWRITE` statement can be used to overwrite the entire table's data.

```SQL
INSERT OVERWRITE my_table
SELECT ...
```



3. **Overwrite partition data:** 


For partitioned tables, the `INSERT OVERWRITE` statement can be used to overwrite data in specific partitions.

```SQL
INSERT OVERWRITE my_table PARTITION (key1 = value1, key2 = value2, ...)
SELECT ...
```



4. **Dynamic partition overwrite:** 


Flink by default adopts the dynamic partition overwrite mode, which only deletes the partitions that appear in the overwritten data. You can switch to the static overwrite mode by configuring the `dynamic-partition-overwrite` parameter.

```SQL
-- Dynamic overwriting
INSERT OVERWRITE my_table
SELECT ...
-- Static overwriting (overwriting the entire table)
INSERT OVERWRITE my_table /*+ OPTIONS('dynamic-partition-overwrite' = 'false') */
SELECT ...
```



5. **Empty table data:** 


You can use the `INSERT OVERWRITE` statement to insert null values and empty the table data.

```SQL
INSERT OVERWRITE my_table /*+ OPTIONS('dynamic-partition-overwrite'='false') */
SELECT * FROM my_table WHERE false;
```



6. **Delete partition data:** 


Currently, Paimon supports two methods for deleting partition data:


1. Use the `INSERT OVERWRITE` statement to insert null values into a specific partition to empty its data.


```SQL
INSERT OVERWRITE my_table /*+ OPTIONS('dynamic-partition-overwrite'='false') */
PARTITION (key1 = value1, key2 = value2, ...)
SELECT selectSpec FROM my_table WHERE false;
```



2. For the need to delete multiple partitions, you can achieve this by submitting a `drop_partition` job.


<span id="37c2278d"></span>
## SQL QUERY

Paimon supports querying tables through Flink SQL, mainly including the following methods:

**Batch Query:** 

In batch processing mode, Paimon returns specific snapshot data of a table, by default returning the latest snapshot.

```SQL
-- Configure the job mode to run as a batch job.
-- Query the latest snapshot, where print_sink is a sink table with the connector set to print.
INSERT INTO print_sink
SELECT * FROM my_table;
```


> **Note**: Due to the current lack of support for direct use of SELECT statements for query debugging in the streaming compute Flink product, if you need to debug Query statements in the job development interface, you must include `INSERT INTO print_sink` and `print_sink create table statement` to print the data.

> **Additionally, for the ease of discussion in the following text, we universally omit related debugging statements of** **`INSERT INTO`** **. Please adjust the statements appropriately based on actual conditions in practical applications.** 


**Time Travel Query:** 

Paimon supports time travel queries based on time or snapshot ID, allowing users to read the state of a table at a specific time point or snapshot.

```SQL
-- Query by snapshot ID
SELECT * FROM my_table /*+ OPTIONS('scan.snapshot-id' = '1') */;
-- Query by timestamp (Unix time in milliseconds)
SELECT * FROM my_table /*+ OPTIONS('scan.timestamp-millis' = '1678883047356') */;
-- Query by tags
SELECT * FROM my_table /*+ OPTIONS('scan.tag-name' = 'my-tag') */;
-- Query by watermark timestamp
SELECT * FROM my_table /*+ OPTIONS('scan.watermark' = '1678883047356') */;
```


**Batch Incremental Query:** 

Paimon supports batch incremental queries, allowing users to read the change data of a table within a specific snapshot range.

```SQL
-- Query incremental data within the snapshot ID range
SELECT * FROM my_table /*+ OPTIONS('incremental-between' = '12,20') */;

-- Query incremental data within the timestamp range
SELECT * FROM my_table /*+ OPTIONS('incremental-between-timestamp' = '1692169000000,1692169900000') */;
```


For cases requiring viewing of deleted records, the `audit_log` system table can be queried:

```SQL
SELECT * FROM my_table$audit_log /*+ OPTIONS('incremental-between' = '12,20') */;
```


**Streaming Query:** 

In stream processing mode, Paimon supports real\-time reading of the latest changes to tables. By default, streaming queries read the latest snapshot of a table at startup and continuously read subsequent changes.

```SQL
-- Set Flink SQL job to streaming mode
-- Perform a streaming query on table data
SELECT * FROM my_table;
```


Additionally, Paimon also supports specifying a starting point for consumption in streaming queries, such as starting from a specific snapshot or time point:

```SQL
-- Consume starting from the specified snapshot ID
SELECT * FROM my_table /*+ OPTIONS('scan.mode' = 'from-snapshot', 'scan.snapshot-id' = '1') */;

-- Consume starting from the specified timestamp
SELECT * FROM my_table /*+ OPTIONS('scan.mode' = 'from-timestamp', 'scan.timestamp-millis' = '1678883047356') */;
```


Through these features, Paimon provides flexible support for Flink SQL queries, meeting the data query needs of different scenarios.

<span id="1784f4a4"></span>
## Lookup Join

Paimon supports the use of Lookup Join in Flink to enrich the data in streaming queries. The process for using Paimon's dimension table feature can be referenced as follows:

**Preparation:** 

First, create a Paimon table and update the data in real\-time.

```SQL
-- Create Paimon Catalog
CREATE CATALOG my_catalog WITH (
  'type'='paimon',
  'warehouse'='tos://<bucket-name>/path/to/warehouse' 
);

USE CATALOG my_catalog;

-- Create a table in the Paimon Catalog
CREATE TABLE customers (
    id INT PRIMARY KEY NOT ENFORCED,
    name STRING,
    country STRING,
    zip STRING
);

-- Start a streaming job to update the customers' tables
INSERT INTO customers ...

-- Create a temporary left table, for example, data from Kafka
CREATE TEMPORARY TABLE orders (
    order_id INT,
    total INT,
    customer_id INT,
    proc_time AS PROCTIME()
) WITH (
    'connector' = 'kafka',
    'topic' = '...',
    'properties.bootstrap.servers' = '...',
    'format' = 'csv'
    ...
);
```


**2. Basic Lookup Join:** 

After preparing the tables mentioned above, you can use Lookup Join in the query to associate real\-time order data with customer information.

```SQL
-- Enrich each order with customer information
SELECT o.order_id, o.total, c.country, c.zip
FROM orders AS o
JOIN customers
FOR SYSTEM_TIME AS OF o.proc_time AS c
ON o.customer_id = c.id;
```


In the above query, the `orders` table is a streaming data source, and the `customers` table is a dimensional table. The association based on processing time is realized through the `FOR SYSTEM TIME AS OF` clause.

**3. Lookup Join with Retry Mechanism:** 

If the record in the `orders` table fails to associate due to data not yet ready in the `customers` table during Lookup Join, you may consider using Flink's delay retry strategy (only applicable to Flink\-1.16\-byted and above versions).

```SQL
-- Enrich each order with customer information and retry on join failure
SELECT /*+ LOOKUP('table'='c', 'retry-predicate'='lookup_miss', 'retry-strategy'='fixed_delay', 'fixed-delay'='1s', 'max-attempts'='600') */
o.order_id, o.total, c.country, c.zip
FROM orders AS o
JOIN customers
FOR SYSTEM_TIME AS OF o.proc_time AS c
ON o.customer_id = c.id;
```


In the above query, Flink's Lookup Hint is used to specify the retry strategy, such as a fixed delay of 1 second and a maximum of 600 retries, to cope with the temporary unavailability of dimensional table data.

<span id="5712637f"></span>
## Procedure

Procedure syntax is designed to implement advanced lake management functions such as Compaction, creating branches, Tag, Rollback, etc. Supported in Flink\-1.17\-byted and above versions.

> Note: The current syntax only supports **Flink\-1.17\-byted** and above versions.



|**Command** |**Usage** |**Explanation** |**Example** |
|---|---|---|---|
|compact |CALL [catalog.]sys.compact('table')<br><br>CALL [catalog.]sys.compact('table', 'partitions')<br><br>CALL [catalog.]sys.compact('table', 'partitions', 'order_strategy', 'order_by')<br><br>CALL [catalog.]sys.compact('table', 'partitions', 'order_strategy', 'order_by', 'options')<br><br>CALL [catalog.]sys.compact('table', 'partitions', 'order_strategy', 'order_by', 'options', 'where')<br><br>CALL [catalog.]sys.compact('table', 'partitions', 'order_strategy', 'order_by', 'options', 'where', 'partition_idle_time') |Compact the data table. The parameters are as follows:<br><br><br>* table (required): Target table identifier.<br><br>* partitions (optional): Partition filter.<br><br>* order_strategy (optional): "order", "zorder", "hilbert", or "none".<br><br>* order_by (optional): Columns to be sorted. If "order_strategy" is "none", this item should be left blank.<br><br>* options (optional): Additional dynamic options for the table.<br><br>* where (optional): Partition predicate (cannot be used with "partitions"). Note: Because "where" is a keyword, it must be enclosed in backticks like "`where`".<br><br>* partition_idle_time (optional): Used for full compaction of partitions that have not received any new data within the duration of "partition_idle_time". And only these partitions will be compressed. This parameter cannot be used with sequential compression. |\-\- Use the partition selection feature<br><br>CALL sys.compact('default.T', 'p=0', 'zorder', 'a,b', 'sink.parallelism=4')<br><br>\-\- Use partition filtering conditions<br><br>CALL sys.compact('default.T', 'dt\>10 and h<20', 'zorder', 'a,b', 'sink.parallelism=4') |
|compact_database |CALL [catalog.]sys.compact_database()<br><br>CALL [catalog.]sys.compact_database('includingDatabases')<br><br>CALL [catalog.]sys.compact_database('includingDatabases', 'mode')<br><br>CALL [catalog.]sys.compact_database('includingDatabases', 'mode', 'includingTables')<br><br>CALL [catalog.]sys.compact_database('includingDatabases', 'mode', 'includingTables', 'excludingTables')<br><br>CALL [catalog.]sys.compact_database('includingDatabases', 'mode', 'includingTables', 'excludingTables', 'tableOptions')<br><br>CALL [catalog.]sys.compact_database('includingDatabases', 'mode', 'includingTables', 'excludingTables', 'tableOptions', 'partitionIdleTime') |Compact the database. Parameters are as follows:<br><br><br>* includingDatabases (Databases Included): Used to specify databases. Regular expressions can be used.<br><br>* mode (Mode): Compression mode. "divided" (Segmented): Launches a receiver for each table, requires restarting the job when a new table is detected; "combined" (Merged, default mode): Starts a merged receiver for all tables, new tables will be automatically detected.<br><br>   includingTables (included tables): Used to specify the tables. Regular expressions can be used.<br><br>   excludingTables (excluded tables): Used to specify tables that will not be compressed. Regular expressions can be used.<br><br>   tableOptions (table options): Additional dynamic options for the table.<br><br>   partition_idle_time (partition idle time): This parameter is used to fully compress partitions that have not received any new data within the "partition_idle_time" duration. And only these partitions will be compressed. |CALL sys.compact_database('db1 |
|create_tag |\-\- Based on the specified snapshot<br><br>CALL [catalog.]sys.create_tag('identifier', 'tagName', snapshotId)<br><br>\-\- Based on the latest snapshot<br><br>CALL [catalog.]sys.create_tag('identifier', 'tagName') |Create a tag based on the given snapshot. Parameters are as follows:<br><br><br>* identifier: The identifier of the target table, which cannot be empty.<br><br>* tagName: The name of the new tag.<br><br>* snapshotId (long type): The ID of the snapshot that the new tag is based on.<br><br>* time_retained: The maximum duration to retain the newly created tag. |CALL sys.create_tag('default.T', 'my_tag', 10, '1 d') |
|delete_tag |CALL [catalog.]sys.delete_tag('identifier', 'tagName') |Delete the tag. The parameters are as follows:<br><br><br>* identifier (identifier): The identifier of the target table; it cannot be empty.<br><br>* tagName (tag name): The name of the tag to be deleted. If multiple tags are specified, the separator is a comma (,). |CALL sys.delete_tag('default.T', 'my_tag') |
|merge_into |CALL [catalog.]sys.merge_into('identifier','targetAlias',<br><br>'sourceSqls','sourceTable','mergeCondition',<br><br>'matchedUpsertCondition','matchedUpsertSetting',<br><br>'notMatchedInsertCondition','notMatchedInsertValues',<br><br>'matchedDeleteCondition') |Execute "MERGE INTO" syntax. Refer to the [Paimon community merge_into action](https://paimon.apache.org/how-to/writing-tables#merging-into-table) documentation for specific usage. |\-\- For matched order rows, increase the price, and if there are no matches, insert orders from the source table.<br><br>CALL sys.merge_into('default.T', 'default.S', '[T.id](http://t.id/)=S.order_id', 'price=T.price+20', '\*') |
|remove_orphan_files |CALL [catalog.]sys.remove_orphan_files('identifier')<br><br>CALL [catalog.]sys.remove_orphan_files('identifier', 'olderThan')<br><br>CALL [catalog.]sys.remove_orphan_files('identifier', 'olderThan', 'dryRun') |Delete orphaned data files and metadata files. The parameters are as follows:<br><br><br>* identifier: the identifier of the target table, which cannot be empty. You can use the form `db_name.*` to clean up the entire database.<br><br>* olderThan: to avoid deleting newly written files, by default, this operation only deletes orphan files older than 1 day. This parameter can be used to modify the time interval.<br><br>* dryRun: when set to "true," only orphan files are viewed, without actually deleting the files. The default value is "false." |CALL remove_orphan_files('default.T', '2023\-10\-31 12:00:00')<br><br>CALL remove_orphan_files('default.\*', '2023\-10\-31 12:00:00')<br><br>CALL remove_orphan_files('default.T', '2023\-10\-31 12:00:00', true) |
|reset_consumer |\-\- Reset the consumer to the next snapshot<br><br>CALL [catalog.]sys.reset_consumer('identifier', 'consumerId', nextSnapshotId)<br><br>\-\- Delete the consumer<br><br>CALL [catalog.]sys.reset_consumer('identifier', 'consumerId') |Reset or delete the consumer. Parameters are as follows:<br><br><br>* identifier (Identifier): The identifier of the target table, cannot be empty.<br><br>* consumerId (消费者 ID): The consumer to be reset or deleted.<br><br>* nextSnapshotId (Long): The new next snapshot ID for the consumer. |CALL sys.reset_consumer('default.T', 'myid', 10) |
|rollback_to |\-\- Rollback to the specified snapshot<br><br>CALL sys.rollback_to('identifier', snapshotId)<br><br>\-\- Rollback to the specified tag<br><br>CALL sys.rollback_to('identifier', 'tagName') |Roll back to a specific version of the target table. Parameters:<br><br>Identifier (标识符): Identifier of the target table, cannot be empty.<br><br>SnapshotId (长整型): ID of the snapshot to Rollback to.<br><br>TagName (标签名): Name of the tag to Rollback to. |CALL sys.rollback_to('default.T', 10)<br><br>CALL sys.rollback_to('default.T', 'my_tag') |
|expire_snapshots |\-\- Community Flink version 1.18 style<br><br>CALL sys.expire_snapshots(table, retain_max) |Expire the snapshot. Parameters:<br><br>table (identifier): Identifier of the target table, cannot be empty.<br><br>retain_max (maximum retain count): The maximum number of completed snapshots to retain.<br><br>retain_min (minimum retain count): The minimum number of completed snapshots to retain.<br><br>order_than (timestamp older than): Snapshots before this timestamp will be removed.<br><br>max_deletes (maximum delete count): The maximum number of snapshots that can be deleted at one time. |CALL sys.expire_snapshots('default.T', 2) |


<span id="fbf6f510"></span>
# Explanation of the WITH Parameter


|Parameter |Default Value |Type |Explanation |
|---|---|---|---|
|auto\-create |false |Boolean |Whether to create the underlying file/folder when reading and writing tables. |
|bucket |\-1 |Integer |The number of buckets for file storage.<br><br>It should be set to \-1 (dynamic bucket mode), or it must be greater than 0 (fixed bucket mode). |
|bucket\-key |(none) |String |Specify Paimon data distribution strategy. Data is allocated to each bucket based on the hash value of the `bucket-key`.<br><br>If multiple fields are specified, the delimiter is ",".<br><br>If not specified, the Primary Key will be used; if no Primary Key exists, the entire row of data will be used. |
|cache\-page\-size |64 kb |MemorySize |Page size of the memory pages used for caching |
|changelog\-producer |none |Enum |Whether to duplicate writes to the changelog file. This changelog file records detailed data changes that can be used directly during stream reading. This feature is applicable to tables with a primary key.<br><br>Possible values:<br><br><br>* "None": Do not generate a changelog file.<br><br>* "Input": Duplicate writes to the changelog file when flushing the in\-memory table, with the changelog originating from the input data.<br><br>* "Full\-compaction": Generate a changelog file on each full compaction.<br><br>* "Lookup": Generate a changelog file through "lookup" before submitting data writes. |
|changelog\-producer.row\-deduplicate |false |Boolean |Whether to generate changelogs of type `-U` and `+U` for the same record. This setting is only effective when `changelog-producer` is `lookup` or `full-compaction`. |
|changelog.num\-retained.max |(none) |Integer |Maximum number of retained completed changelogs. Should be greater than or equal to `changelog.num-retained.min`. |
|changelog.num\-retained.min |(none) |Integer |The minimum number of retained completed changelogs. Should be greater than or equal to 1. |
|changelog.time\-retained |(none) |Duration |The maximum retention time for completed changelogs. |
|commit.callback.#.param |(none) |String |(none) |
|commit.callbacks |(none) |String |commit.force\-compact (none) |
|commit.force\-compact |false |Boolean |Perform compaction forcefully before submission. |
|commit.force\-create\-snapshot |false |Boolean |Create a snapshot forcefully before submission. |
|compaction.max\-size\-amplification\-percent |200 |Integer |For the change log mode table, the additional storage (in percentage) required to store single\-byte data in the merged tree. |
|compaction.max.file\-num |50 |Integer |For the file set [f_0,...,f_N], even if the total (size(f_i)) is less than the target file size, this triggers the compaction of the maximum number of files for append\-only tables. This value can prevent too many small files from hanging, thereby enhancing performance. |
|compaction.min.file\-num |5 |Integer |For the file set [f_0,...,f_N], for append\-only tables, the minimum number of files required to meet the total (size(f_i)) \>= target file size to trigger compaction. This value prevents nearly full files from being compacted, which is uneconomical. |
|compaction.optimization\-interval |(none) |Duration |The frequency of optimizing compaction operations, this configuration is used to ensure the timeliness of querying read\-optimized system tables. |
|compaction.size\-ratio |1 |Integer |Percentage flexibility when comparing sorted run sizes for change log mode tables. If the size of the candidate sorted runs is less than 1% smaller than the size of the next sorted run, then include the next sorted run in this candidate set. |
|consumer\-id |(none) |String |Consumer ID used for recording offset consumption in storage. |
|consumer.expiration\-time |(none) |Duration |Consumer file expiration interval. If the lifetime exceeds this value since the last modification, the consumer file will expire. |
|consumer.ignore\-progress |false |Boolean |Ignore consumer progress for newly started jobs. |
|consumer.mode |exactly\-once |Enum |Specify the consumer consistency mode for the table.<br><br>Possible values:<br><br><br>* "exactly\-once": Readers consume data at snapshot granularity and strictly ensure that the snapshot ID recorded in consumers is the next consecutive snapshot ID that all readers have exactly consumed `ID + 1`.<br><br>* "at\-least\-once": Each reader consumes snapshots at different rates, and the slowest snapshot progress among all readers is recorded in the consumers. |
|continuous.discovery\-interval |10 s |Duration |Default interval to discover file changes is 10 seconds, which checks for file modifications. |
|cross\-partition\-upsert.bootstrap\-parallelism |10 |Integer |Parallelism of bootstrap in a single task for cross\-partition upserts. |
|cross\-partition\-upsert.index\-ttl |(none) |Duration |Cross\-partition updates and insertions (where the primary key does not include all partition fields) in RocksDB indices have a TTL to avoid maintaining excessive indices and degrading performance, but note that this may also lead to data duplication. |
|delete.force\-produce\-changelog |false |Boolean |Force the generation of a changelog in delete SQL, or you can use "streaming\-read\-overwrite" to read the changelog from overwrite commits. |
|deletion\-vectors.enabled |false |Boolean |Enable deletion vector mode. In this mode, when writing data, an index file containing a delete vector is generated, marking the data to be deleted. During the read operation, these index files can be applied to avoid merging. |
|dynamic\-bucket.assigner\-parallelism |(none) |Integer |The parallelism of the assigner operation in dynamic bucket mode is related to the number of buckets initialized; too few can lead to insufficient processing speed of the assigner. |
|dynamic\-bucket.initial\-buckets |(none) |Integer |The initial number of buckets in a partition during assigner operations in dynamic bucket mode. |
|dynamic\-bucket.target\-row\-num |2000000 |Long |If the bucket is \-1, for a Primary Key table, it's dynamic bucket mode, this option controls the target number of rows per bucket. |
|dynamic\-partition\-overwrite |true |Boolean |Whether to only overwrite the dynamic partitions when overwriting a partitioned table that has dynamic partition columns. Only effective when the table has partition keys. |
|file\-index.in\-manifest\-threshold |500 bytes |MemorySize |Threshold for storing file index bytes in the list. |
|file\-index.read.enabled |true |Boolean |Enable reading file index. |
|file\-reader\-async\-threshold |10 mb |MemorySize |Threshold for asynchronous file reading. |
|file.compression |(none) |String |Default file compression format<br><br><br>* orc uses lz4<br><br>* parquet uses snappy. It can be overridden by file.compression.per.level |
|file.compression.per.level | |Map |Define different compression strategies for different levels by adding this configuration: 'file.compression.per.level' = '0:lz4,1:zstd'. |
|file.format |orc |Enum |Specify the message format of the data file, currently supporting orc, parquet, and avro formats.<br><br>Possible values:<br><br><br>* "orc": ORC file format.<br><br>* "parquet": Parquet file format.<br><br>* "avro": Avro file format. |
|file.format.per.level | |Map |To define different file formats for different levels, you can add configurations like this: 'file.format.per.level' = '0:avro,3:parquet'. If no file format is provided for the level, the default format set by `file.format` will be used. |
|full\-compaction.delta\-commits |(none) |Integer |Full Compaction will be scheduled after a certain number of delta commits. By default, this behavior will not occur. |
|ignore\-delete |false |Boolean |Whether to ignore delete actions; defaulted to not ignore. |
|incremental\-between |(none) |String |Read incremental changes between the start snapshot (exclusive) and end snapshot, for example, '5,10' indicates changes between snapshot 5 and snapshot 10. |
|incremental\-between\-scan\-mode |auto |Enum |Type of scan when reading incremental changes between the start snapshot (exclusive) and end snapshot.<br><br>Possible values:<br><br><br>* "auto": Generates a changelog file by scanning tables for changelog files of changes. Otherwise, scan for newly changed files.<br><br>* "delta": Scan files changed between snapshots.<br><br>* "changelog": Scan the changelog files between snapshots. |
|incremental\-between\-timestamp |(none) |String |Read incremental changes between a starting timestamp (exclusive) and an ending timestamp, for example, 't1,t2' means changes between timestamp t1 and timestamp t2. |
|local\-merge\-buffer\-size |(none) |MemorySize |Local merging will buffer and merge data before sorting records into buckets and writing them to the receiver. When the buffer is full, it will be flushed. Mainly used to address skew issues on the Primary Key. We recommend starting with 64 megabytes (64mb) when trying out this feature. |
|local\-sort.max\-num\-file\-handles |128 |Integer |The maximum fan\-in for external merge sorting. It limits the number of file handles. If it's too small, it may lead to mid\-way merging. But if it's too large, it may result in too many files being opened simultaneously, consuming memory and causing random reads. |
|lookup.cache\-file\-retention |1 h |Duration |Retention time of cache files for lookup. After the file expires, if access is needed, it will be read again from DFS to build an index on the local disk. |
|lookup.cache\-max\-disk\-size |infinite |MemorySize |The maximum disk size of the Lookup cache. You can use this option to limit the use of the local disk. |
|lookup.cache\-max\-memory\-size |256 mb |MemorySize |The maximum memory size of the Lookup cache. |
|lookup.cache\-spill\-compression |"lz4" |String |Compression of Lookup cache spill files, currently supports `none`, `lz4`, `lzo`, and `zstd`. |
|lookup.cache.bloom.filter.enabled |true |Boolean |Enable Bloom Filter for Lookup Cache. |
|lookup.cache.bloom.filter.fpp |0.05 |Double |Define the default false positive probability for the lookup cache Bloom filter. |
|lookup.hash\-load\-factor |0.75 |Float |Search index load factor. |
|manifest.format |avro |Enum |Specify the message format for the manifest file.<br><br>Possible values:<br><br><br>* "orc": ORC file format.<br><br>* "parquet": Parquet file format.<br><br>* "avro": Avro file format. |
|manifest.full\-compaction\-threshold\-size |16 mb |MemorySize |The size threshold that triggers a full compaction of the manifest. |
|manifest.merge\-min\-count |30 |Integer |To avoid frequent merges of the manifest files, this parameter specifies the minimum number of ManifestFileMeta to merge. |
|manifest.target\-file\-size |8 mb |MemorySize |Recommended manifest file size. |
|merge\-engine |deduplicate |Enum |Specify the merge engine for tables with primary keys.<br><br>Possible values:<br><br><br>* Deduplication (`deduplicate`): Deduplicate and keep the last row.<br><br>* Partial column update (`partial-update`): Partially update non\-empty fields.<br><br>* Pre\-aggregation (`aggregation`): Pre\-aggregate fields with the same primary key.<br><br>* First row (`first-row`): Deduplicate and keep the first row. |
|metadata.stats\-mode |"truncate(16)" |String |Mode of metadata statistics collection. Available modes include `none`, `counts`, `truncate(16)`, `full`.<br><br><br>* "none": Indicates that metadata statistics collection is disabled.<br><br>* "counts" means only collecting null value counts.<br><br>* "full": Indicates collecting null value counts, minimum/maximum values.<br><br>* "truncate(16)": Indicates collecting null value counts, minimum/maximum values with truncation at length 16.<br><br>* Field\-level statistics modes can be specified through fields.{field_name}.stats\-mode |
|metastore.partitioned\-table |false |Boolean |Whether to create this table as a partitioned table in the metastore. For example, if you want to list all partitions of the Paimon table in Hive, you need to create this table as a partitioned table in the Hive metastore. This configuration option does not affect the default file system metastore. |
|metastore.tag\-to\-partition |(none) |String |Whether to create a partitioned table in the metastore for this table to map non\-partitioned table tags. This allows the Hive engine to view the table as a partitioned table and read specific partitions (specific tags) using the partition fields. |
|metastore.tag\-to\-partition.preview |none |Enum |Preview the tags of the snapshot generated in the metastore. This allows the Hive engine to query specific tags before they are created.<br><br>Possible values:<br><br><br>* "none": No auto\-created tags.<br><br>* "process\-time": Tags are created when the processing time exceeds the cycle time plus delay, based on device time.<br><br>* "watermark": Tags are created when the watermark exceeds the cycle time plus delay, based on the input watermark.<br><br>* "batch": In batch processing scenarios, labels corresponding to the current snapshot are generated after the task is completed. |
|num\-levels |(none) |Integer |Total number of levels, for example, there are 3 levels including level 0, level 1, and level 2. |
|num\-sorted\-run.compaction\-trigger |5 |Integer |Number of sorted runs that trigger the compaction operation. Includes level 0 files (each file is a sorted run) and higher level files (each level is a sorted run). |
|num\-sorted\-run.stop\-trigger |(none) |Integer |Number of sorted runs allowed before triggering a stop, with the default value set to 'num\-sorted\-run.compaction\-trigger' + 3. |
|page\-size |64 kb |MemorySize |Memory page size. |
|parquet.enable.dictionary |(none) |Integer |Disable dictionary encoding for all fields in the parquet. |
|partition |(none) |String |Define partitions through table options; partitions cannot be defined simultaneously on both DDL and table options. |
|partition.default\-name |"**DEFAULT_PARTITION**" |String |Default partition name when the dynamic partition column value is null or an empty string. |
|partition.expiration\-check\-interval |1 h |Duration |Interval for checking partition expiration. |
|partition.expiration\-time |(none) |Duration |Interval for partition expiration. If the lifespan of the partition exceeds this value, the partition will expire. Partition time is extracted from the partition value. |
|partition.timestamp\-formatter |(none) |String |Formatter for formatting timestamps from string formats. It can be used with 'partition.timestamp\-pattern' to create a formatter using the specified values.<br><br><br>* The default formatter is 'yyyy\-MM\-dd HH:mm:ss' and 'yyyy\-MM\-dd'.<br><br>* Supports multiple partition fields, such as '$year\-$month\-$day $hour:00:00'.<br><br>* The timestamp formatter is compatible with Java's DateTimeFormatter. |
|partition.timestamp\-pattern |(none) |String |You can specify a pattern to retrieve timestamps from partitions. The formatter mode is defined by 'partition.timestamp\-formatter'.<br><br><br>* By default, data is read from the first field.<br><br>* If the timestamp in the partition is a single field named 'dt', you can use '$dt'.<br><br>* If it is distributed across multiple fields for year, month, day, and hour, you can use '$year\-$month\-$day $hour:00:00'.<br><br>* If the timestamp is in the fields dt and hour, you can use '$dt $hour:00:00'. |
|primary\-key |(none) |String |Define the primary key through the table options; you cannot define the primary key simultaneously in DDL and table options. |
|read.batch\-size |1024 |Integer |The read batch size for orc and parquet. |
|record\-level.expire\-time |(none) |Duration |The record\-level expiration time for primary key tables; expires during compaction, and timely expiration of records cannot be guaranteed. You must also specify 'record\-level.time\-field'. |
|record\-level.time\-field |(none) |String |The field for record\-level expiration time should be of type INT in seconds |
|rowkind.field |(none) |String |Generate field types for the primary key table, where the row type determines which data are '+I', '\-U', '+U', or '\-D'. |
|scan.bounded.watermark |(none) |Long |End condition for bounded stream mode: "watermark". Stream read will end when a large watermark snapshot is encountered. |
|scan.file\-creation\-time\-millis |(none) |Long |After configuring this time, only data files created after this time are read. It is independent of the snapshot, but it is an imprecise filter (depending on whether compression occurs). |
|scan.manifest.parallelism |(none) |Integer |The parallelism of scanning list files, default value is the size of the CPU processor. Note: Extension |
|scan.max\-splits\-per\-task |10 |Integer |The maximum split size a task should cache during scanning. If the split size cached in the enumerator exceeds the task size multiplied by this value, the scanner will pause scanning. |
|scan.mode |default |Enum |Designated source scanning behavior.<br><br>Possible values:<br><br><br>* "default": Determined by other table properties, defines the actual startup mode. If "scan.timestamp\-millis" is set, the actual startup mode will be "from\-timestamp"; if "scan.snapshot\-id" or "scan.tag\-name" is set, the actual startup mode will be "from\-snapshot". Otherwise, the actual startup mode will be "latest\-full".<br><br>* "latest\-full": For streaming data sources, generates the latest snapshot on the table at startup and continues reading the latest changes. For batch sources, only the latest snapshot is generated, but new changes are not read.<br><br>* "full": Deprecated. Same as "latest\-full".<br><br>* "latest": For streaming data sources, does not generate a snapshot at the start and continuously reads the latest changes. For batch sources, the behavior is the same as the "latest\-full" start mode.<br><br>* "compacted\-full": For streaming data sources, generates a snapshot after the latest compact at the first start and continues to read the latest changes. For batch sources, generates a snapshot only after the latest compact, but does not read new changes. When scheduled full compact is enabled, select the snapshot after the full compact.<br><br>* "from\-timestamp": For streaming data sources, continuously reads changes starting from the timestamp specified by "scan.timestamp\-millis", without generating a snapshot at the start. For batch sources, generates a snapshot at the timestamp specified by "scan.timestamp\-millis", but does not read new changes.<br><br>* "from\-file\-creation\-time": For both streaming and batch sources, generates a snapshot and filters data files by creation time. For streaming data sources, does not generate a snapshot at the first start and continues to read the latest changes.<br><br>* "from\-snapshot": For streaming data sources, continuously reads changes starting from the snapshot specified by "scan.snapshot\-id", without generating a snapshot at the start. For batch data sources, generate snapshots specified by "scan.snapshot\-id" or "scan.tag\-name", but do not read new changes.<br><br>* "from\-snapshot\-full": For streaming data sources, generate a snapshot from the table specified by "scan.snapshot\-id" at initial startup, and continuously read changes thereafter. For batch data sources, generate snapshots specified by "scan.snapshot\-id", but do not read new changes.<br><br>* "incremental": Read incremental changes between the start and end snapshots or timestamps. |
|scan.plan\-sort\-partition |false |Boolean |Whether to sort the plan files by partition fields, allowing you to read in partition order, even if your partition writing is unordered.<br><br>It is recommended to use this for streaming read operations on 'append\-only' tables. By default, stream reading starts by reading the complete snapshot. To avoid disordered reads of partitions, you can enable this option. |
|scan.snapshot\-id |(none) |Long |Optional snapshot ID used in "from\-snapshot" or "from\-snapshot\-full" scan mode. |
|scan.tag\-name |(none) |String |Optional tag name used in "from\-snapshot" scan mode. |
|scan.timestamp\-millis |(none) |Long |from\-timestamp" scan mode uses an optional timestamp. If there is no snapshot earlier than this time, the earliest snapshot will be selected. |
|scan.watermark |(none) |Long |Optional watermark used in "from\-snapshot" scan mode. If there are no snapshots later than this watermark, an exception will be thrown. |
|sequence.field |(none) |String |Generate sequence numbers for the fields of the Primary Key table; the sequence numbers determine which data is the latest. |
|sink.watermark\-time\-zone |"UTC" |String |Parse the watermark value as a TIMESTAMP value's timezone. The default value is 'UTC', which means the watermark is defined on the TIMESTAMP column or is undefined. If the watermark is defined on the TIMESTAMP_LTZ column, the timezone of the watermark is the user\-configured timezone, and this value should be the user\-configured local timezone. The option value can be a full name such as 'America/Los_Angeles,' or a custom timezone ID, such as 'GMT\-08:00'. |
|snapshot.expire.clean\-empty\-directories |true |Boolean |When snapshots expire, try to clean up empty directories. Please note that attempting to clean directories may throw exceptions in the filesystem, but this usually doesn't cause problems. |
|snapshot.expire.execution\-mode |sync |Enum |Specify the execution mode for snapshot expiration.<br><br>Possible values:<br><br><br>* "sync": Synchronous execution expired. If there are too many files, it may take a long time and block the stream processing.<br><br>* "async": Asynchronous execution expired. If the snapshot generation surpasses deletion, there will be a backlog of files. |
|snapshot.expire.limit |10 |Integer |The maximum number of snapshots allowed to expire at one time. |
|snapshot.num\-retained.max |infinite |Integer |The maximum number of completed snapshots to retain. Should be greater than or equal to the minimum number. |
|snapshot.num\-retained.min |10 |Integer |The minimum number of completed snapshots to retain. Should be greater than or equal to 1. |
|snapshot.time\-retained |1 h |Duration |The maximum retention time for completed snapshots. |
|snapshot.watermark\-idle\-timeout |(none) |Duration |In watermarks, if the source remains idle for the specified timeout duration, it triggers the snapshot advancement and facilitates labeling. |
|sort\-compaction.local\-sample.magnification |1000 |Integer |Multiplication factor for the local sample of sort compaction. The size of the local sample is the receiver parallelism \* magnification. |
|sort\-compaction.range\-strategy |QUANTITY |Enum |The default range strategy for sort\-compaction is quantity. If the data size allocated to the sorting task is uneven, it may cause a performance bottleneck; the configuration can be set to size.<br><br>Possible values:<br><br><br>* "SIZE"<br><br>* "QUANTITY" |
|sort\-engine |loser\-tree |Enum |Specify the sorting engine for tables with a Primary Key.<br><br>Possible values:<br><br><br>* "min\-heap": Uses a min heap for multi\-way sorting.<br><br>* "loser\-tree": Uses a loser tree for multi\-way sorting. Compared to heap sort, loser tree has fewer comparisons and is more efficient. |
|sort\-spill\-buffer\-size |64 mb |MemorySize |The amount of data recorded to disk in a spill disk sort for spill. |
|sort\-spill\-threshold |(none) |Integer |If the maximum number of sort readers exceeds this value, an attempt to spill will be made. This can prevent excessive readers from consuming too much memory and causing memory spills. |
|source.split.open\-file\-cost |4 mb |MemorySize |The open file cost of the source file. To avoid using source splits to read too many files, which can be very slow. |
|source.split.target\-size |128 mb |MemorySize |The target size for source splits when scanning buckets. |
|spill\-compression |"LZ4" |String |Compression for spills, currently supports lz4, lzo, and zstd. |
|streaming\-read\-mode |(none) |Enum |Mode of streaming reads, specifying data from either a table file or a log<br><br>Possible values:<br><br><br>* log": Read from log storage.<br><br>* File": Read from file storage. |
|streaming\-read\-overwrite |false |Boolean |Read changes during the overwrite in stream mode. When the change log generator is set for complete compression or lookup, it should not be set to true as this reads duplicate changes. |
|tag.automatic\-creation |none |Enum |Whether to automatically create tags and how to generate them.<br><br>Possible values:<br><br><br>* "none": Do not automatically create tags.<br><br>* "process\-time": Based on machine time, create tags once the processing time exceeds the cycle time plus delay.<br><br>* "watermark": Based on the input watermark, create tags once the watermark exceeds the cycle time plus delay.<br><br>* "batch": In batch scenarios, generate tags corresponding to the current snapshot after the task is completed. |
|tag.callback.#.param |(none) |String |The parameter string of the constructor for class #. The callback class should parse the parameter itself. |
|tag.callbacks |(none) |String |A set of commit callback classes to be invoked after successful creation of a Tag. Class names are connected by commas (for example: com.test.CallbackA, com.sample.CallbackB). |
|tag.creation\-delay |0 ms |Duration |Delay time before creating a tag after the period ends. This allows some late data to enter the tag. |
|tag.creation\-period |daily |Enum |Frequency of generating tags.<br><br>Possible values:<br><br><br>* "daily": A tag is generated daily.<br><br>* "hourly": A tag is generated every hour.<br><br>* "two\-hours": A tag is generated every two hours. |
|tag.default\-time\-retained |(none) |Duration |The default maximum retention time for newly created Tags. It affects Tags created automatically and those created manually (through the process). |
|tag.num\-retained\-max |(none) |Integer |Maximum number of tags to retain. It only affects automatically created tags. |
|tag.period\-formatter |with_dashes |Enum |Date format of the tag period.<br><br>Possible values:<br><br><br>* "with_dashes": Date and hour with dashes, e.g., 'yyyy\-MM\-dd HH'<br><br>* "without_dashes": Date and hour without dashes, e.g., 'yyyyMMdd HH' |
|target\-file\-size |128 mb |MemorySize |The target size of the file. |
|write\-buffer\-for\-append |false |Boolean |This option is only applicable to Append Tables. Writing uses a write buffer to avoid out of memory errors. |
|write\-buffer\-size |256 mb |MemorySize |The amount of data accumulated in memory before it is converted to sorted disk files. |
|write\-buffer\-spill.max\-disk\-size |infinite |MemorySize |The maximum disk size for write buffer overflow. Only valid when write buffer overflow is enabled. |
|write\-buffer\-spillable |(none) |Boolean |Can the write buffer overflow. Enabled by default when using object storage. |
|write\-manifest\-cache |0 bytes |MemorySize |Cache size for reading manifest files during write initialization. |
|write\-max\-writers\-to\-spill |5 |Integer |When batch appending, if the number of writers exceeds this option, we will enable buffer caching and overflow functions to prevent memory shortage. |
|write\-only |false |Boolean |If set to true, compaction and snapshot expiration will be skipped. Once this option is enabled, it is recommended to set a dedicated compaction job to complete the compaction work. |
|zorder.var\-length\-contribution |8 |Integer |The number of bytes for types (CHAR, VARCHAR, BINARY, VARBINARY) used in zorder sorting. |


This section of the document mainly references [Apache Paimon's official documentation](https://paimon.apache.org/docs/master/maintenance/configurations/). For more detailed information, please see the original document.

<span id="769ed7dc"></span>
# Reference Documents

Paimon is an active and rapidly evolving community. We strongly recommend that you follow the [Apache Paimon community documentation](https://paimon.apache.org/docs/master/) to stay updated with the latest changes.
