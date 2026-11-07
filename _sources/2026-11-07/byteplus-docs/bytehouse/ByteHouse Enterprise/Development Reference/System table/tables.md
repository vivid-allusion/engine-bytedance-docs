---
title: "tables"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/tables"
---

The system table `system.tables` is used for the implementation of the `SHOW TABLES` query and can be used to obtain metadata for tables known to the server. Tables which are detached by [DETACH statement](https://docs.byteplus.com/docs/bytehouse/ce-detach-statement) will not appear in `system.tables`. [Temporary tables](https://clickhouse.com/docs/sql-reference/statements/create/table#temporary-tables) are visible in `system.tables` only within the session in which they were created, with the `database` field left empty and the `is_temporary` flag set to 1 (enabled).

<span id="081c3756"></span>
## Column name


|**Field name** |**Data types** |**Explanation of field meanings** |
|---|---|---|
|database |String |The name of the database where the table is located. |
|name |String |Table name. |
|uuid |UUID |The persistent UUID of each table in an Atomic\-type database. |
|engine |String |Table engine name (without parameters). |
|is_temporary |UInt8 |It indicates whether the indicator table is a temporary marker. Supported values are as follows:<br><br><br>* 0: Not a temporary table.<br><br>* 1: Temporary table. |
|is_readonly |UInt8 |Flag indicating whether the table is read\-only. Supported values are as follows:<br><br><br>* 0: The table is in a readable and writable state (not read\-only).<br><br>* The table is in read\-only state. |
|data_paths |Array(String) |The path to table data in the file system. |
|metadata_path |String |The path to table metadata in the file system. |
|metadata_modification_time |DateTime |Latest modification time of table metadata. |
|dependencies_database |Array(String) |Database dependencies. |
|dependencies_table |Array(String) |Table dependencies (the current table's [Materialized view](https://docs.byteplus.com/docs/bytehouse/ce-materialized-view)). |
|create_table_query |String |A query for creating tables. |
|engine_full |String |Table engine parameters. |
|update_time |DateTime |It represents the last time the data in the table was updated. If the data is not modified after the Server starts, the time is the Attach table's timestamp at the moment the Server starts. |
|partition_key |String |The partition key expression specified in the table. |
|sorting_key |String |The sort key expression specified in the table. |
|primary_key |String |The primary key expression specified in the table. |
|unique_not_enforced |Array(String) |The optimizer assumes that the data is unique and does not check the data when inserting it. |
|foreign_key |Map(String, Tuple(String, String)) |Foreign key, used for optimizer tuning. |
|sampling_key |String |The sampling key expression specified in the table. |
|storage_policy |String |Storage polices:<br><br><br>* [HaMergeTree](https://docs.byteplus.com/docs/bytehouse/hamergetree)<br><br>* [HaUniqueMergeTree](https://docs.byteplus.com/docs/bytehouse/hauniquemergetree)<br><br>* [Distributed](https://docs.byteplus.com/docs/bytehouse/distributed) |
|total_rows |Nullable(UInt64) |Total number of rows. If the exact number of rows in the table can be quickly determined, that value is returned; otherwise, `NULL` is returned (including underlying `Buffer` tables). |
|total_bytes |Nullable(UInt64) |Total number of bytes. If the exact number of bytes for the table in storage can be quickly determined, that value is returned; otherwise, `NULL` is returned (excluding any underlying storage).<br><br><br>* If the table stores data on disk, the space used on disk is returned (that is, compressed).<br><br>* If the table stores data in memory, it returns an approximate value of the number of bytes used. |
|lifetime_rows |Nullable(UInt64) |Total number of rows inserted since the server started (applies only to the `Buffer` table). |
|lifetime_bytes |Nullable(UInt64) |Total number of bytes inserted since the server started (applies only to the `Buffer` table). |
|comment |String |Table annotations. |
|user |String |The creator of the table.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">ByteHouse Enterprise Engine versions 2.7 and later support the user column. You can view the engine version by navigating to <strong>ByteHouse Console</strong> \> <strong>Cluster List</strong> \> <strong>Cluster Name</strong> \> <strong>Basic Information</strong>.</div><br> |


<span id="e6fd1616"></span>
## **Example**

```SQL
SELECT * FROM system.tables where database = 'tpch' and name='lineitem' limit 1 format Vertical; 
```


```SQL
database:                   tpch
name:                       lineitem
uuid:                       00000000-0000-0000-0000-000000000000
engine:                     MergeTree
is_temporary:               0
is_readonly:                0
data_paths:                 ['/mnt/multi_disk_9000/disk01/clickhouse/data/data/tpch/lineitem/','/mnt/multi_disk_9000/disk02/clickhouse/data/data/tpch/lineitem/','/mnt/multi_disk_9000/disk03/clickhouse/data/data/tpch/lineitem/','/mnt/multi_disk_9000/disk04/clickhouse/data/data/tpch/lineitem/','/mnt/multi_disk_9000/disk05/clickhouse/data/data/tpch/lineitem/','/mnt/multi_disk_9000/disk06/clickhouse/data/data/tpch/lineitem/','/mnt/multi_disk_9000/disk07/clickhouse/data/data/tpch/lineitem/','/mnt/multi_disk_9000/disk08/clickhouse/data/data/tpch/lineitem/']
metadata_path:              /mnt/multi_disk_9000/disk01/clickhouse/data/metadata/tpch/lineitem.sql
metadata_modification_time: 2025-06-13 21:36:52
dependencies_database:      []
dependencies_table:         []
create_table_query:         CREATE TABLE tpch.lineitem (`l_orderkey` Int32, `l_partkey` Int32, `l_suppkey` Int32, `l_linenumber` Int32, `l_quantity` Decimal(15, 2), `l_extendedprice` Decimal(15, 2), `l_discount` Decimal(15, 2), `l_tax` Decimal(15, 2), `l_returnflag` String, `l_linestatus` String, `l_shipdate` Date, `l_commitdate` Date, `l_receiptdate` Date, `l_shipinstruct` String, `l_shipmode` String, `l_comment` String) ENGINE = MergeTree ORDER BY (l_orderkey, l_linenumber) SETTINGS index_granularity = 8192
engine_full:                MergeTree ORDER BY (l_orderkey, l_linenumber) SETTINGS index_granularity = 8192
update_time:                2025-06-13 21:47:34
partition_key:
sorting_key:                l_orderkey, l_linenumber
primary_key:                l_orderkey, l_linenumber
unique_not_enforced:        []
foreign_key:                {}
sampling_key:
storage_policy:             default
total_rows:                 600037902
total_bytes:                28682278543
lifetime_rows:              ᴺᵁᴸᴸ
lifetime_bytes:             ᴺᵁᴸᴸ
comment:
user:                       default
```
