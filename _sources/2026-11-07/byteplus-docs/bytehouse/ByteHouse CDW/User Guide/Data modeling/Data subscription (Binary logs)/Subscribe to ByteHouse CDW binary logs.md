---
title: "Subscribe to ByteHouse CDW binary logs"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/subscribe-to-bytehouse-cdw-binary-logs"
---

When you need to capture database events in ByteHouse Cloud Data Warehouse Edition (CDW) to enable data replication, synchronization, or to forward these events as message streams to different consumers for processing, ByteHouse provides the binary log (binlog) feature. Consuming ByteHouse CDW binlog can enhance data reuse capability and detect insert, delete, and update operations on related ByteHouse CDW tables. This tutorial introduces how to subscribe to binlog in ByteHouse and other related operations.

<span id="57e4fb00"></span>
# Introduction to binary log

ByteHouse CDW binary log, like MySQL binary log, supports recording event logs of all data changes in the database by means of binlog. ByteHouse CDW binlog enables highly convenient and flexible replication and synchronization between data sources. However, ByteHouse CDW binlog is generally used only for data synchronization, while MySQL binlog is also used for master\-slave instance synchronization, data recovery, and other high availability scenarios. Therefore, there are certain differences in the implementation of the two, which are mainly reflected in the following aspects:


* ByteHouse CDW binlog does not record DDL operations.

* ByteHouse CDW binlog is relatively flexible, operating at the table level. It can be enabled as needed, and different binlog TTL (time to live) values can be configured for individual tables.

* It is very convenient to query ByteHouse CDW binlog.


At the same time, in big data scenarios, the system supports Flink in directly consuming ByteHouse CDW binlog. Compared with traditional data warehouse layering, Flink and ByteHouse CDW binlog enable fully event\-driven processing, supporting real\-time data transformation from the operational data store (ODS) to the data warehouse dimension layer (DWD), and from DWD to the data warehouse service layer (DWS). This approach achieves unified storage while maintaining layered governance, enhances data reuse, and reduces end\-to\-end data processing latency, providing users with a one\-stop real\-time data warehouse solution.

Recommended use cases for ByteHouse CDW binlog are as follows:


* Target scenario: ByteHouse binlog supports downstream subscriptions. For example, ByteHouse ELT computation results flow back to the TP database, and together with Flink, support complete event\-driven architecture.

* Non\-target scenarios: ByteHouse's own data synchronization or cross\-region replication.


<span id="9d948ee5"></span>
# Usage restrictions


1. This feature is in Beta. Before using it, please submit a support ticket or contact the ByteHouse team to obtain whitelist access.

2. Please ensure that the ByteHouse CDW engine version you use is v2.3.1 or above. Log in to the ByteHouse CDW console, click the **Tenant management** tab at the top, and view the engine version in **Basic info**. Enabling the binlog feature on engine versions lower than this version will result in an error. If you need to upgrade, please submit a support ticket.

3. Currently, only CnchMergeTree is supported. For new tables, set the `ENGINE` to `CnchMergeTree` when creating the table; for existing tables, you can use the following command to check the table engine in use.

   ```SQL
   SHOW CREATE TABLE your_table_name;
   ```
   

4. ByteHouse CDW binary log operates at the table level and does not record DDL operations.

5. Once ByteHouse CDW binlog is enabled, it cannot be disabled. Please evaluate your business requirements before enabling this feature. If you need to disable this feature after it has been enabled, please submit a ticket to contact the ByteHouse team.

6. List of features that support (✅) and do not support (❌) binary log output.

   
   |Statement |Non\-unique key table |Unique key tables |
   |---|---|---|
   |INSERT |✅ ||
   |UPSERT and partial column updates |❌ |✅ |
   |UPDATE、DELETE |❌ |✅ |
   |DDL<br><br><br>1. CREATE TABLE<br><br>2. DROP/UNDROP TABLE<br><br>3. ADD/DROP/MODIFY COLUMN<br><br>4. TRUNCATE<br><br>5. ALTER PARTITION / PART (ATTACH/DETACH/DROP) |❌ ||
   |TTL expression |❌<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Data deleted by a TTL expression does not generate a binary log.</div><br> ||
   

7. Currently, ByteHouse CDW binlog only supports incremental data consumption and does not yet support scenarios where full and incremental consumption are integrated.


<span id="8bd21f10"></span>
# Binlog format and principles

<span id="53aa96cc"></span>
## Binlog release and data storage

After binlog is enabled, when data manipulation language (DML) operations are performed, ByteHouse executes write, delete, update, and other operations on the original table. At the same time, it writes to the binlog, converts the generated data into binlog format, and assigns a BSN (Binary Log Sequence Number).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa91f7cac2184109b8e8aea995d5b7d8~tplv-goo7wpa0wc-image.image) </span>


* Data written to ByteHouse is organized into parts (data segments), with each part containing a portion of the data. Binlog data is also stored in the form of parts, and both Binlog data and the data in the original table have independent TTL and GC (garbage collection).

* Binlog publishing operates asynchronously, with background tasks periodically converting table data updates into binlog, publishing them, and assigning BSN. After a data change occurs in the table, the corresponding Binlog message is generally visible after 500 ms to 5 s.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After binlog is enabled, DML operations must write to both the original table and the binlog, which may affect write performance to some extent. In addition, binlog data itself also occupies a certain amount of storage space. Enable binlog as needed, and configure an appropriate time to live (TTL).</div>


<span id="54dcb40a"></span>
## Binlog field descriptions

A binlog record consists of binlog system fields and user table fields. The specific field definitions are shown in the following table.


|Column names |Data types |Note |
|---|---|---|
|`_binlog_bsn` & `_part_row_number` |UInt64 |The system field of binlog indicates the BSN of the binlog to which the current Record belongs and the row number within that BSN.<br><br><br>* `_binlog_bsn` and `_part_row_number` can uniquely identify a row in the binlog.<br><br>* `_binlog_bsn` starts at 1 and increments continuously; `_part_row_number` starts at 0 and increments continuously.<br><br>* Both columns are virtual columns and do not occupy storage space. By default, they are not displayed in query results; to include them in a query, you must specify them explicitly. |
|`binlog_shard_id` |UInt16 |A system field in binlog that indicates the shard number to which the current record belongs. This field is used to support parallel consumption by multiple consumers, with each consumer thread consuming data within its own `binlog_shard_id`.<br><br><br>* The number of `binlog_shard_id` is determined by the table\-level configuration `binlog_shard_num` (for details on the parameters, see [Parameter description (table-level configuration)](https://docs.byteplus.com/docs/bytehouse/subscribe-to-bytehouse-cdw-binary-logs#a98328de)).<br><br>   * For tables with a defined unique key, `binlog_shard_id` is obtained by taking the hash value of the **unique key** modulo `binlog_shard_num`.<br><br>   * For tables without a defined unique key, `binlog_shard_id` is obtained by taking the hash value of the **sorting key** modulo `binlog_shard_num`.<br><br>* The data in the binlog part is sorted in ascending order based on the values of this column. This sorting improves the speed of reading data for a specific shard during queries. |
|`binlog_event_type` |Enum8 |A system field in binlog that indicates the type of modification represented by the current Record. There are four possible values as follows:<br><br><br>* "I": Insert. It indicates that the current record is a new record.<br><br>* 'D': Delete. It indicates that the current record represents the deletion of an existing record.<br><br>* 'U\-': Update Before. It indicates that the current record represents the state of an existing record before it is updated.<br><br>* 'U+': Update After. It indicates that the current record represents the state after an existing record has been updated.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An update operation generates two binlog records, representing the state before and after the update (<code>'U-'</code> and <code>'U+'</code>). The ByteHouse binlog feature will ensure that these two records belong to the same BSN, are consecutive, and that U\- comes before U+.</div><br> |
|`user_table_column_1` |User\-defined |User Table fields. |
|... |... |... |
|`user_table_column_n` |User customization |User table fields. |


<span id="26bb6951"></span>
# Configure and enable binlog

<span id="a98328de"></span>
## Parameter description (table\-level configuration)

ByteHouse binlog allows you to configure the following parameters:


|Configure |Required |Default value |Note |
|---|---|---|---|
|enable_binlog |Yes |0 |It specifies whether to enable binlog. When this parameter is set to 1, binlog is enabled. When it is set to 0, Binlog is not enabled. Once enabled, binlog cannot be disabled. |
|binlog_lifetime |No |86400 |TTL for binlog, in seconds. |
|binlog_shard_num |No |64 |The number of binlog shards, used to increase binlog consumption parallelism and support parallel consumption by multiple Flink consumers. This parameter must be set either before enabling binlog via the `enable_binlog` parameter or at the same time as enabling binlog. After binlog is enabled, this parameter cannot be modified independently. |
|binlog_row_deduplicate |No |false |After it is enabled, binlogs will no longer be generated for records where the values before and after the update ('U\-' and 'U+') are identical.<br><br>This feature does not affect write performance. After filtering out a large amount of redundant data, it may lead to some improvement in write performance by reducing disk I/O.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After this configuration change, it only takes effect for newly generated binlog files and does not modify historical binlog files.</div><br> |


<span id="f584687d"></span>
## Enable the binlog


* Example 1: Enable binlog when creating a table

   ```SQL
   CREATE TABLE binlog_test(
       `id` Int32,
       `a` Int64,
       `b` String
   )
   ENGINE = CnchMergeTree
   ORDER BY a
   UNIQUE KEY id
   SETTINGS
   enable_binlog = 1, -- Required: enable binlog
   binlog_lifetime = 86400, -- Optional
   binlog_shard_num = 4, -- Optional
   binlog_row_deduplicate = false; -- Optional 
   ```
   

* Example 2: Enable binlog for existing tables

   ```SQL
   ALTER TABLE binlog_test MODIFY SETTING binlog_lifetime = 3600; -- Optional, adjust TTL
   ALTER TABLE binlog_test MODIFY SETTING binlog_shard_num = 4; --Optional, adjust shard count
   ALTER TABLE binlog_test MODIFY SETTING enable_binlog = 1; -- Required: enable binlog 
   ```
   


<span id="1b116554"></span>
# Modify the binlog configuration

After enabling binlog, you can use `ALTER TABLE` to modify the binlog configuration.

<span id="94238f7f"></span>
## Adjust binlog TTL

```SQL
ALTER TABLE binlog_test MODIFY SETTING binlog_lifetime = 7200; 
```


<span id="e3a45d19"></span>
## Records with identical values before and after an update are not written to the binlog

```SQL
ALTER TABLE binlog_test MODIFY SETTING binlog_row_deduplicate = true; 
```


<span id="7f2559b8"></span>
# Query binlog

ByteHouse supports viewing all binlog data for a table, and also supports querying only binlog data within a specified BSN range. If you are unsure about the BSN range, you can first query the system table [system.cnch_table_info](https://docs.byteplus.com/docs/bytehouse/subscribe-to-bytehouse-cdw-binary-logs#5ab8bc50) to identify the required BSN range. You can also retrieve detailed information about the corresponding binlog part by querying the system table [system.cnch_binlogs](https://docs.byteplus.com/docs/bytehouse/subscribe-to-bytehouse-cdw-binary-logs#470ed477). For example, you can query the number of Shard records in the current binlog part in advance and customize your reading behavior accordingly to improve query efficiency.

After enabling binlog, you can query the binlog of the table by adding `$binlog` after the table name. For example, you can use the following SQL statement to query the binlog of `db_test.binlog_test`.

```SQL
SELECT * FROM db_test.binlog_test$binlog; 
```


ByteHouse supports querying only binlogs within a specified BSN range. To do this, you need to add a hint in the form of `bsn(table_name$binlog, A, B)` to the query, which indicates that the query will retrieve binlogs for the table where the BSN range is within  **(A,B]** . For example, you can use the following command to query binlog entries in `db_test.binlog_test` where the BSN is 2 or 3.

```SQL
SELECT /*+ bsn(db_test.binlog_test$binlog, 1, 3) */ * FROM db_test.binlog_test$binlog; 
```


The following examples demonstrate the query methods for several common Binlog scenarios.

Suppose we have already performed some DML operations on the `db_test.binlog_test` table:

```Java
INSERT INTO binlog_test VALUES (1,2,'string1-1'),(2,1,'string2-1'),(3,3,'string3-1');
INSERT INTO binlog_test VALUES (1,1,'string1-1'),(2,1,'string2-2'),(4,2,'string4-1');
DELETE FROM binlog_test WHERE id < 3; 
```


<span id="ae5af96b"></span>
## Example 1: Query all binlogs in the table

Query all binlog entries for table `db_test.binlog_test`.

```SQL
SELECT
    _binlog_bsn,
    _part_row_number,
    *
FROM `db_test.binlog_test$binlog`
ORDER BY _binlog_bsn ASC 
```


Sample query results are as follows:

```SQL
┌─_binlog_bsn─┬─_part_row_number─┬─binlog_shard_id─┬─binlog_event_type─┬─id─┬─a─┬─b─────┐
│           1  │                0  │               1   │ I                  │  1   │ 2  │ string1-1 │
│           1  │                1  │               2   │ I                  │  2   │ 1  │ string2-1 │
│           1  │                2  │               3   │ I                  │  3   │ 3  │ string3-1 │
└────────┴────────────┴───────────┴────────────┴────┴──┴───────┘
┌─_binlog_bsn─┬─_part_row_number─┬─binlog_shard_id─┬─binlog_event_type─┬─id─┬─a─┬─b─────┐
│           2  │                0   │               1  │ U-                 │  1   │ 2  │ string1-1 │
│           2  │                1   │               1  │ U+                 │  1   │ 1  │ string1-1 │
│           2  │                2   │               1  │ I                  │  4   │ 2  │ string4-1 │
│           2  │                3   │               2  │ U-                 │  2   │ 1  │ string2-1 │
│           2  │                4   │               2  │ U+                 │  2   │ 1  │ string2-2 │
└────────┴─────────────┴──────────┴────────────┴────┴──┴───────┘
┌─_binlog_bsn─┬─_part_row_number─┬─binlog_shard_id─┬─binlog_event_type─┬─id─┬─a─┬─b─────┐
│           3  │                0  │               1   │ D                  │  1   │ 1  │ string1-1 │
│           3  │                1  │               2   │ D                  │  2   │ 1  │ string2-2 │
└────────┴────────────┴───────────┴────────────┴────┴──┴───────┘
```


<span id="9e41189f"></span>
## Example 2: Query binlogs within the specified BSN range in the table

Query the table `db_test.binlog_test` for binlog records where BSN is 2 or 3.

```SQL
SELECT /*+ bsn(db_test.binlog_test$binlog, 1, 3) */
    _binlog_bsn,
    _part_row_number,
    *
FROM `db_test.binlog_test$binlog`
ORDER BY _binlog_bsn ASC 
```


An example of the query result is as follows:

```SQL

┌─_binlog_bsn─┬─_part_row_number─┬─binlog_shard_id─┬─binlog_event_type─┬─id─┬─a─┬─b─────┐
│           2  │                0   │               1  │ U-                  │  1  │ 2  │ string1-1 │
│           2  │                1   │               1  │ U+                  │  1  │ 1  │ string1-1 │
│           2  │                2   │               1  │ I                   │  4  │ 2  │ string4-1 │
│           2  │                3   │               2  │ U-                  │  2  │ 1  │ string2-1 │
│           2  │                4   │               2  │ U+                  │  2  │ 1  │ string2-2 │
└────────┴─────────────┴──────────┴─────────────┴───┴──┴───────┘
┌─_binlog_bsn─┬─_part_row_number─┬─binlog_shard_id─┬─binlog_event_type─┬─id─┬─a─┬─b─────┐
│           3  │                0   │               1  │ D                  │  1   │ 1  │ string1-1 │
│           3  │                1   │               2  │ D                  │  2   │ 1  │ string2-2 │
└────────┴────────────┴───────────┴────────────┴────┴──┴───────┘
```


<span id="cc755f2c"></span>
## Example 3: Query binlogs in the table within the specified BSN range for the specified shard ID

Query binlog in the `db_test.binlog_test` table where BSN is 2 or 3 and `binlog_shard_id` is 2.

```SQL
SELECT /*+ bsn(db_test.binlog_test$binlog, 1, 3) */
    _binlog_bsn,
    _part_row_number,
    *
FROM `db_test.binlog_test$binlog`
WHERE binlog_shard_id = 2
ORDER BY _binlog_bsn ASC 
```


An example of query results is as follows:

```SQL
┌─_binlog_bsn─┬─_part_row_number─┬─binlog_shard_id─┬─binlog_event_type─┬─id─┬─a─┬─b─────┐
│           2  │                3  │               2   │ U-                 │  2  │ 1   │ string2-1 │
│           2  │                4  │               2   │ U+                 │  2  │ 1   │ string2-2 │
└────────┴────────────┴───────────┴────────────┴───┴───┴───────┘
┌─_binlog_bsn─┬─_part_row_number─┬─binlog_shard_id─┬─binlog_event_type─┬─id─┬─a─┬─b─────┐
│           3  │                1   │               2  │ D                   │  2  │ 1  │ string2-2 │
└────────┴────────────┴───────────┴─────────────┴───┴──┴───────┘
```


<span id="5df920f7"></span>
## Example 4: Query the binlog for newly inserted data

Query all newly inserted data in table `db_test.binlog_test` where `binlog_event_type` is `'I'`, and do not output binlog system fields.

```SQL
SELECT * EXCEPT (binlog_event_type, binlog_shard_id)
FROM `db_test.binlog_test$binlog`
WHERE binlog_event_type = 'I'
```


An example of the query results is as follows:

```SQL
┌─id─┬─a─┬─b─────┐
│  1  │ 2  │ string1-1 │
│  2  │ 1  │ string2-1 │
│  3  │ 3  │ string3-1 │
└───┴──┴───────┘
┌─id─┬─a─┬─b─────┐
│  4  │ 2   │ string4-1 │
└───┴───┴───────┘
```


<span id="3c25417d"></span>
# Consume binlog in real time

ByteHouse CDW currently supports consuming ByteHouse CDW binlog via Flink. For details, see [Use BytePlus Flink to consume ByteHouse CDW binary log data in real time](https://docs.byteplus.com/docs/bytehouse/flink-consume-bytehouse-cdw-binary-logs-in-real-time).

<span id="b419b41a"></span>
# Query binlog system tables

ByteHouse provides two system tables, `system.cnch_table_info` and `system.cnch_binlogs`, to display the status information of the binlog for a specific table.


|System tables |Applications |Speed |Recommended use cases |
|---|---|---|---|
|`system.cnch_table_info` |It displays the current maximum and minimum BSN of a table. |Fast |Only the maximum and minimum BSN in the table need to be queried. |
|`system.cnch_binlogs` |It displays detailed information for each binlog part of a table. |Slow |You can query detailed information before reading the binlog part and use this information to customize the reading method. |


<span id="5ab8bc50"></span>
### system.cnch_table_info

Display the current maximum and minimum BSN for a table.


|Column names |Data types |Note |
|---|---|---|
|database |String |Library name |
|table |String |Table name |
|min_bsn |Nullable(UInt64) |The minimum BSN within TTL. For tables where binlog is not enabled or binlog has not yet been created, this field is NULL. |
|max_bsn |Nullable(UInt64) |The maximum BSN within TTL. For tables where binlog is not enabled or tables do not yet have binlog, this field is NULL. |


Example: Query the maximum and minimum BSN in table `db_test.binlog_test`.

```SQL
SELECT
    database,
    table,
    min_bsn,
    max_bsn 
FROM system.cnch_table_info
WHERE (database = 'db_test') AND (table = 'binlog_test')
```


An example of the query results is as follows:

```SQL
┌─database─┬─table───┬─min_bsn─┬─max_bsn─┐
│ db_test   │ binlog_test│       10 │    20     │
└──────┴────────┴──────┴──────┘
```


<span id="470ed477"></span>
### system.cnch_binlogs

Display detailed information for each binlog part of a table. When querying this system table, you must use equality filter conditions for both database and table.


|Column names |Data types |Note |
|---|---|---|
|database |String |Name of the database being queried. |
|table |String |Name of the table to query. |
|part_name |String |Name of the current binlog part. |
|bsn |UInt64 |The BSN of the current binlog part. |
|rows |UInt64 |Current number of rows in the binlog part. |
|bytes |UInt64 |Current storage size (in bytes) of the binlog part. |
|txn_id |UInt64 |Generate the transaction ID for the current binlog part. |
|commit_time |DateTime |Generate the commit time for transactions in the current binlog part. |
|published_time |DateTime |The time when the current binlog part was published. |
|active |UInt8 |Whether the current binlog part is valid (within the TTL and already published). |
|is_staged |UInt8 |Whether the current binlog part has been published. |
|shard_stats |String |The number of rows recorded for each Shard in the current binlog part. |


Example: Query information about all binlog parts of the table `db_test.binlog_test`.

```SQL
SELECT
    database,
    table,
    bsn,
    rows,
    bytes,
    active,
    shard_stats
FROM system.cnch_binlogs
WHERE (database = 'db_test') AND (table = 'binlog_test') 
```


The following are example query results:

```SQL
┌─database─┬─table───┬─bsn─┬─rows─┬─bytes─┬─active─┬─shard_stats────┐
│ db_test   │ binlog_test │   1 │    3  │  1416   │      1 │ [ 0, 1, 1, 1 ]     │
│ db_test   │ binlog_test │   2 │    5  │  1437   │      1 │ [ 0, 3, 2, 0 ]     │
│ db_test   │ binlog_test │   3 │    2  │  1403   │      1 │ [ 0, 1, 1, 0 ]     │
└──────┴────────┴───┴────┴──────┴─────┴────────────┘
```
