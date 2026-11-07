---
title: "Create a new database/table: Based on the DDL template"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/create-a-database-table-based-on-ddl-template"
---

This article lists the DDL templates supported by ByteHouse Enterprise Edition, and you can refer to [Create Table with DDL Template](https://docs.byteplus.com/docs/bytehouse/create-a-new-database-table#cf3cc783) to quickly create tables.

<span id="def8e904"></span>
# Database engine

<span id="fd3114d5"></span>
## Atomic [Standard]

Description: Default database engine of ByteHouse.

```SQL
   CREATE DATABASE [IF NOT EXISTS] <db_name> ON CLUSTER <cluster_name>
      [ ENGINE = Atomic];
```


<span id="4a860ee1"></span>
## MaterializeMySQL [Experimental]

Description: Supports real\-time synchronization of MySQL databases to ByteHouse.

```SQL
CREATE DATABASE [IF NOT EXISTS] <db_name> ON CLUSTER <cluster_name>
ENGINE = MaterializeMySQL('host:port', ['database'], 'user', 'password') 
[SETTINGS 
    [shard_mode=1],...] -- After switching on shard_mode, data will be stored in different shards;
[TABLE OVERRIDE <table_name> (
    [COLUMNS (
        [col_name [datatype], ...]
    )]
    [ORDER BY expr]
    [PARTITION BY expr]
    [TTL expr]
), ...]
```


<span id="d2c736da"></span>
# Table Engine

Currently, only the HaMergeTree and HaUniqueMergeTree table engines support two table creation modes: the common table mode and the non\-common table mode. All other engines only support the non\-common table mode. For an introduction to these two table modes and a comparison of their differences, please refer to [Table creation mode](https://docs.byteplus.com/docs/bytehouse/table-creation-mode).

<span id="d28ebfe8"></span>
## HaMergeTree [Standard]

Description: ByteHouse's default table engine, optimized for performance, supports high\-performance import and query, and multiple copies for high availability.

<span id="8a33c008"></span>
### Non\-common table mode

```SQL
CREATE TABLE [IF NOT EXISTS] [<db_name>.]<local_table_name> ON CLUSTER <cluster_name>
(
    name1 [type1],
    name2 [type2],
    ...
) ENGINE = HaMergeTree('/clickhouse/tables/{shard}/{database}/local_table_name', '{replica}')
ORDER BY expr
[PARTITION BY expr]
[TTL expr]
[SETTINGS
    [index_granularity=8192],...] -- don't change this setting in normal occasion; Only set index_granularity to 128 if this table is usually used to query a single row。

CREATE TABLE [db.]<table_name> ON CLUSTER <cluster_name>
    AS <db>.<local_table_name>
    ENGINE = Distributed(<cluster_name>, <db>, <local_table_name>, <sharding_key>);
```


<span id="1bfe69a0"></span>
### Common table mode

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The "common table mode" function must be activated before usage. Administrators have the permission to activate the function, and once activated, it cannot be terminated. Please choose carefully according to your business situation. For actions to activate the feature, please refer to <a href="https://docs.byteplus.com/docs/bytehouse/table-creation-mode#a796c1ec">Activate General Table Creation Mode</a>.</div>


```SQL
CREATE TABLE [IF NOT EXISTS] [<db_name>.]<table_name>
(
    name1 [type1],
    name2 [type2],
    ...
) ENGINE = HaMergeTree('/clickhouse/tables/{shard}/{database}/table_name', '{replica}')
ORDER BY expr
[PARTITION BY expr]
[TTL expr]
[SETTINGS
    enable_common_table_mode = 1,
    cluster_name = <cluster_name>,
    sharding_key = <sharding_key>
    [index_granularity=8192],...] -- don't change this setting in normal occasion; Only set index_granularity to 128 if this table is usually used to query a single row。
```


<span id="64e44947"></span>
## HaUniqueMergeTree [Standard]

Description: ByteHouse's efficient deduplication table engine supports real\-time deduplication (Merge\-on\-write), real\-time data deletion, and partial column updates. Supports multiple copies for high availability.

<span id="6a581783"></span>
### Non\-common table mode

```SQL
CREATE TABLE [IF NOT EXISTS] [<db_name>.]<local_table_name> ON CLUSTER <cluster_name>
(
    name1 [type1],
    name2 [type2],
    ...
) ENGINE = HaUniqueMergeTree('/clickhouse/tables/{shard}/{database}/local_table_name', '{replica}'[，version_column])
ORDER BY expr
UNIQUE KEY expr
[PARTITION BY expr]
[TTL expr]
[SETTINGS
    [index_granularity=8192],...] -- The default value is 8192. Only set index_granularity to 128 if this table is usually used to query a single row. Otherwise, don't change this setting in normal occasion;

CREATE TABLE [db.]<table_name> ON CLUSTER <cluster_name>
    AS <db>.<local_table_name>
    ENGINE = Distributed(<cluster_name>, <db>, <local_table_name>, <sharding_key>)
    SETTINGS remote_table_is_ha_unique = 1 [,...];
```


<span id="0a9d8d7e"></span>
### Common table mode

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The "common table mode" function must be activated before usage. Administrators have the permission to activate the function, and once activated, it cannot be terminated. Please choose carefully according to your business situation. For actions to activate the feature, please refer to <a href="https://docs.byteplus.com/docs/bytehouse/table-creation-mode#a796c1ec">Activate General Table Creation Mode</a>.</div>


```SQL
CREATE TABLE [IF NOT EXISTS] [<db_name>.]<table_name>
(
    name1 [type1],
    name2 [type2],
    ...
) ENGINE = HaUniqueMergeTree('/clickhouse/tables/{shard}/{database}/table_name', '{replica}'[，version_column])
ORDER BY expr
UNIQUE KEY expr
[PARTITION BY expr]
[TTL expr]
[SETTINGS
    enable_common_table_mode = 1,
    cluster_name = <cluster_name>,
    sharding_key = <sharding_key>
    [index_granularity=8192],...] -- The default value is 8192. Only set index_granularity to 128 if this table is usually used to query a single row. Otherwise, don't change this setting in normal occasion;
```


<span id="2a7b767f"></span>
## HaAggregatingMergeTree [Standard]

Description: An aggregate table engine used to store aggregated data in such tables through materialized views for high\-performance queries.

```SQL
CREATE TABLE [IF NOT EXISTS] [<db_name>.]<local_table_name> ON CLUSTER <cluster_name>
(
    name1 [type1],
    name2 [type2], -- Type Allows to be AggregateFunction(<agg_funcition_name>, <type>)
    ...
) ENGINE = HaAggregatingMergeTree('/clickhouse/tables/{shard}/{database}/local_table_name', '{replica}')
ORDER BY expr
[PARTITION BY expr]
[TTL expr]
[SETTINGS
    [index_granularity=8192],...] -- The default value is 8192. Only set index_granularity to 128 if this table is usually used to query a single row. Otherwise, don't change this setting in normal occasion;

CREATE TABLE [db.]<table_name> ON CLUSTER <cluster_name>
    AS <db>.<local_table_name>
    ENGINE = Distributed(<cluster_name>, <db>, <local_table_name>, <sharding_key>);
```


<span id="d067fbe4"></span>
## MergeTree [Community]

Note: A basic table engine provided by the community, not supporting multi\-copy high availability.

```SQL
CREATE TABLE [IF NOT EXISTS] [<db_name>.]<local_table_name> ON CLUSTER <cluster_name>
(
    name1 [type1],
    name2 [type2],
    ...
) ENGINE = MergeTree
ORDER BY expr
[PARTITION BY expr]
[TTL expr]
[SETTINGS
    [index_granularity=8192],...] -- don't change this setting in normal occasion; Only set index_granularity to 128 if this table is usually used to query a single row。

CREATE TABLE [db.]<table_name>
    ON CLUSTER <cluster_name>
    AS <db>.<local_table_name>
    ENGINE = Distributed(<cluster_name>, <db>, <local_table_name>, <sharding_key>);
```


<span id="155ce461"></span>
## ReplicatedMergeTree [Community]

Description: Table engine provided by the community, supporting multi\-copy high availability.

```SQL
CREATE TABLE [IF NOT EXISTS] [<db_name>.]<local_table_name> ON CLUSTER <cluster_name>
(
    name1 [type1],
    name2 [type2],
    ...
) ENGINE = ReplicatedMergeTree('/clickhouse/tables/{shard}/{database}/local_table_name', '{replica}')
ORDER BY expr
[PARTITION BY expr]
[TTL expr]
[SETTINGS
    [index_granularity=8192],...] -- The default value is 8192. Only set index_granularity to 128 if this table is usually used to query a single row. Otherwise, don't change this setting in normal occasion;


CREATE TABLE [db.]<table_name> ON CLUSTER <cluster_name>
    AS <db>.<local_table_name>
    ENGINE = Distributed(<cluster_name>, <db>, <local_table_name>, <sharding_key>);
```


<span id="bfef3d85"></span>
# External table engine

External table engines only support the non\-common table mode.

<span id="8a160372"></span>
## MySQL [Community]

Description: External table engine used to connect to MySQL tables.

```SQL
CREATE TABLE [IF NOT EXISTS] [<db_name>.]<table_name> ON CLUSTER <cluster_name> 
(
    name1 [type1],
    name2 [type2],
    ...
) ENGINE = MySQL('host:port', 'database', 'table', 'user', 'password'
    [, replace_query, -- Flag that converts INSERT INTO queries to REPLACE INTO. If replace_query=1, the query is substituted.
    'on_duplicate_clause']) --The ON DUPLICATE KEY on_duplicate_clause expression that is added to the INSERT query.
SETTINGS
    [connection_pool_size=16, ]
    [connection_max_tries=3, ]
    [connection_auto_close=true ]
;
```


<span id="f9af6c8b"></span>
## HDFS [Community]

Description: External table engine used to connect to HDFS files.

```SQL
CREATE TABLE [IF NOT EXISTS] [<db_name>.]<table_name> ON CLUSTER <cluster_name> 
(
    name1 [type1],
    name2 [type2], 
    ...
) 
HDFS(URI, format) -- Supported format: JSON,CSV,Parquet,ORC,etc。
```


<span id="d39fb444"></span>
## S3 [Community]

Description: An external table engine for connecting to object storage compatible with the S3 protocol (such as ToS).

```SQL
CREATE TABLE [IF NOT EXISTS] [<db_name>.]<local_table_name> ON CLUSTER <cluster_name> 
(
    name1 [type1],
    name2 [type2], 
    ...
) 
ENGINE = S3(path, [aws_access_key_id, aws_secret_access_key,] 
    format, --Supported values: JSON,CSV,Parquet,ORC,etc。
    [compression]) --Supported values: none, gzip/gz, brotli/br, xz/LZMA, zstd/zst
```


<span id="4915d5f6"></span>
## HiveCluster [Experimental]

Description: An external table engine for connecting to Hive.

```SQL
CREATE TABLE [IF NOT EXISTS] [<db_name>.]<table_name> ON CLUSTER <cluster_name> 
(
    name1 [type1],
    name2 [type2], 
    ...
) 
ENGINE = HiveCluster(cluster, path, hive_database, hive_table);
PARTITION BY expr
SETTINGS [
    endpoint = <s3_endpoint>, 
    ak_id = 'access_key', 
    ak_secret = 'secret_key'
    -- for hive table on S3]
;
```


<span id="2c7ea4f6"></span>
# Views & materialized views

<span id="867b5095"></span>
## View [Standard]

Description: Executes the SQL statement defining the view in real\-time during a query, does not store data, and allows for rapid initiation of sub\-queries based on the view.

```SQL
CREATE VIEW [IF NOT EXISTS] [<db_name>.]<view_name> ON CLUSTER <cluster_name> 
AS SELECT ...;
```


<span id="e2a4e2f7"></span>
## MaterializedView [Standard]

Description: Used to store the query result data, eliminating the need for further calculation and aggregation during subsequent queries. Thus, it accelerates queries by trading space for time, thereby achieving query acceleration and simplification of query logic.

```SQL
CREATE MATERIALIZED VIEW [IF NOT EXISTS] [<db_name>.]<view_name> ON CLUSTER <cluster_name> 
    [TO [db.]target_table_name]
    [ENGINE = engine]
    [ORDER BY order_by_key]
    [PARTITION BY partition_key]
    [TTL ttl_expr]
    [POPULATE]
AS SELECT ...;
```


<span id="e9a893f9"></span>
# Column projection

<span id="6542c4e3"></span>
## Projection

Description: Typically used to speed up query performance on MergeTree tables at the expense of storage. It features the following characteristics:


* **Part\-level storage**. Compared with a normal materialized view, which is an independent table, the data materialized by the Projection is stored in the partition directory of the original table, supporting both normal Projection and pre\-aggregated Projection of detailed data;

* **Transparent use, automatic hit**. Multiple Projections can be created on a MergeTree table. When executing a Select statement, the most optimal Projection can be automatically matched according to the query range to provide accelerated querying. If a Projection is not hit, the base table is queried directly.

* **Data are co\-born and co\-die with the same source.**  Since the physical data is stored in the original table's partition, updates and merges are done with the same source, and hence; inconsistencies will not occur


**ADD PROJECTION**

Add column projection metadata to the table.

```SQL
ALTER TABLE [db.]name [ON CLUSTER cluster] ADD PROJECTION [IF NOT EXISTS] name ( SELECT <COLUMN LIST EXPR> [GROUP BY] [ORDER BY] )
```


**DROP PROJECTION**

Delete projection metadata from the table and remove projection data files from the disk. The data is deleted asynchronously.

```SQL
ALTER TABLE [db.]name [ON CLUSTER cluster] DROP PROJECTION [IF EXISTS] name
```


**MATERIALIZE PROJECTION**

Build projection data in the partition named partition_name.

```SQL
ALTER TABLE [db.]table [ON CLUSTER cluster] MATERIALIZE PROJECTION [IF EXISTS] name [IN PARTITION partition_name]
```


**CLEAR PROJECTION**

Remove projection data files from the disk without deleting the projection metadata. The process data is deleted asynchronously.

```SQL
ALTER TABLE [db.]table [ON CLUSTER cluster] CLEAR PROJECTION [IF EXISTS] name [IN PARTITION partition_name]
```
