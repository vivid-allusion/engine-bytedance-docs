---
title: "Hive external tables"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-hive-external-table"
---

Bytehouse Enterprise Edition supports federated queries using external tables, allowing users to query data in Hive directly without data import. This provides flexibility and convenience in data processing. This article introduces the details on using Hive external tables.

<span id="55f5e60d"></span>
# Background information

ByteHouse offers multiple ways to integrate with external systems, including table engines. Like all other table engines, configurations can be done by using `CREATE TABLE` or `ALTER TABLE` statements, and from the user's perspective, the integrated setting looks like querying a normal table, but effectively, the queries are delegated to the external system. This type of transparent query is one of the main advantages of external tables, such as external dictionaries or table functions that require custom query methods each time they are used.

<span id="80b0e637"></span>
# Usage restrictions


* ByteHouse Enterprise Edition version 2.5 and above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Starting from version 2.5, ByteHouse Enterprise Edition supports Hive external table functionality.</div>



* Currently, only `SELECT` and `ALERT` query operations on Hive external tables are supported; currently, only Hive tables are supported, not views, View, or bucket tables.

* Currently, only the following input formats are supported:

   * ORC: Supports simple scalar column types other than `char`; complex types only support `array`

   * Parquet


<span id="4755d27e"></span>
# Create external table

When creating Hive external tables, ByteHouse provides you with a universal table creation DDL command. Additionally, if integrating with LasFormation’s Hive tables, you can also refer to the LasFormation integration method for external table creation. Introductions to both methods are as follows.

<span id="246148c0"></span>
## Universal table creation DDL


* Versions 2.6 and above (recommended)


Versions 2.6 and above support automatic derivation of table structures, eliminating the need to specify columns and partition keys when creating tables.

```SQL
CREATE TABLE table_name [ON CLUSTER cluster]
ENGINE = HiveCluster(cluster, 'thrift://host:port', 'hive_database_name', 'hive_table_name')
SETTINGS 
    endpoint = 'http://tos-s3-{REGION}.ibytepluses.com', 
    ak_id = 'access_key', 
    ak_secret = 'secret_key'
;   
```



|Parameters |Configuration Description |
|---|---|
|Create Table Description |Column names and types for the Hive table, as well as Partition By key and Cluster By key, will be automatically deduced and established during table creation. **Columns are established by default as Nullable types**, see the **Column Type Mapping** section below for the mapping rules of column types.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When creating an external Hive table, you can also specify column names, types, and partition keys among other descriptions (not recommended). When specifying:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Column names must correspond one\-to\-one with the Hive table; column types must be identical to those in the Hive table; the order of the columns need not correspond one\-to\-one with Hive</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When creating an external table, you can select only part of the columns from a Hive table, but all partition columns must be included.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The partitions of external table columns must be specified using a partition by statement and must be defined in the description list like normal columns.</div><br> |
|Engine Parameters (Engine) |* thrift://hive_metastore:port: Address of the hivemetastore<br><br>* hive_database_name: Specifies the database in Hive<br><br>* hive_table_name: Specifies the table in Hive, does not support views or bucket tables |
|Settings (SETTINGS) |* Endpoint: The connection address of external data sources, taking BytePlus LAS as an example, connection information can be found in [Las Help Document](https://www.volcengine.com/docs/6492/1264542#%E8%BF%9E%E6%8E%A5%E5%9C%B0%E5%9D%80).<br><br>* ak_id/ak_secret: Keys with Hive access permissions (including Hive Metastore and the corresponding object storage) |



* Version 2.5


Version 2.5 does not support automatic derivation of table structures; specifying columns and partition keys is required when creating tables.

```SQL
CREATE TABLE [db.]table_name [ON CLUSTER cluster]
(
    name1 [type1] [ALIAS expr1],
    name2 [type2] [ALIAS expr2],
    ...
) ENGINE = HiveCluster(cluster, 'thrift://host:port', 'hive_database', 'hive_table');
PARTITION BY expr
-- for hive table on S3
SETTINGS 
    endpoint = 'http://tos-s3-{REGION}.ibytepluses.com', 
    ak_id = 'access_key', 
    ak_secret = 'secret_key';   
```


Table creation parameters are similar to those described above.

<span id="1c8b1a30"></span>
## LasFormation integration

<span id="241b2fef"></span>
### Create a Hive table

```SQL
create table las_t 
Engine = HiveCluster('cluster_name', 'cache_key', 'las_database','las_table')
settings 
meta_type = 'lf',
lf_metastore_url = 'las_addr',
lf_metastore_ak_id = 'ak',
lf_metastore_ak_secret = 'sk',
lf_metastore_region = '{REGION}',
endpoint = 'tos-s3-{REGION}.ibytepluses.com',
ak_id = 'ak', 
ak_secret = 'sk'
```



|Parameters |Configuration Description |
|---|---|
|Create Table Descriptions |Hive table column names and types, as well as Partition By key, Cluster By key, will be automatically deduced and established during table creation **Columns default to being created as Nullable types**. See the **column type mapping** section below for column type mapping rules.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When creating an external Hive table, you can also specify column names, types, and partition keys among other descriptions (not recommended). When specifying:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Column names must correspond one\-to\-one with the Hive table; column types must be identical to those in the Hive table; the order of the columns need not correspond one\-to\-one with Hive</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When creating an external table, you can select only part of the columns from a Hive table, but all partition columns must be included.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The partition columns must be specified by the partition by statement and like normal columns, they need to be defined in the description list.</div><br> |
|Engine parameters (Engine) |* cluster_name: The cluster name of ByteHouse.<br><br>* cache_key: The name cached in memory for the last client. You can customize the cache_key; try to keep it consistent within the same LasFormation environment (same lf_metastore_url).<br><br>* las_database: The database name in LasFormation.<br><br>* las_table: The table name in LasFormation. |
|Settings (SETTINGS) |* meta_type: The external data source type, set to a fixed value 'lf'.<br><br>* lf_metastore_url: The connection address for the external data source, for example, in the Johor region: `thrift://lakeformation.las.ap-southeast-1.ibytepluses.com:48869`. For connection addresses in more regions, refer to the [LAS help documentation](https://www.volcengine.com/docs/6492/1264542#%E8%BF%9E%E6%8E%A5%E5%9C%B0%E5%9D%80).<br><br>* lf_metastore_ak_id/lf_metastore_ak_secret: Keys with Hive access permissions (including Hive Metastore and the corresponding object storage).<br><br>* LF Metastore Region: The region of LasFormation.<br><br>* Endpoint: The TOS access domain name for data storage in LasFormation, which should be configured as an internal network S3 address. Taking Johor as an example: `tos-s3-ap-southeast-1.ibytepluses.com`. For details on accessing domain names for other regions, please see [TOS Help Document](https://www.volcengine.com/docs/6349/107356).<br><br>* ak_id/ak_secret: Access ak/sk for TOS. |


<span id="94791b13"></span>
### Create a Hive database

When integrating with LasFormation, you can also directly create a Hive database. Once created, tables under the external hive database will be automatically mapped. The DDL to create the database is as follows.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only ByteHouse Enterprise version 2.7 and above supports the creation of Hive databases.</div>


```SQL
CREATE DATABASE hive_db [ON CLUSTER cluster_name]
ENGINE = Hive(cluster_name, 'thrift://host:port', 'hive_database')
settings 
meta_type = 'lf',
lf_metastore_url = 'las_addr',
lf_metastore_ak_id = 'ak',
lf_metastore_ak_secret = 'sk',
lf_metastore_region = '{REGION}',
endpoint = 'tos-s3-{REGION}.ibytepluses.com',
ak_id = 'ak', 
ak_secret = 'sk'
```


The parameters for building tables are similar to those discussed above; they include:


* lf_metastore_url: The external data source's connection address, taking the Johor region as an example: `thrift://lakeformation.las.ap-southeast-1.ibytepluses.com:48869`, for more regional connection address information, please refer to the [Las help documentation](https://www.volcengine.com/docs/6492/1264542#%E8%BF%9E%E6%8E%A5%E5%9C%B0%E5%9D%80).

* endpoint: The TOS access domain name for LasFormation data storage needs to be configured to an internal network S3 address, with Johor region as an example: `tos-s3-ap-southeast-1.ibytepluses.com`, for more details on regional access domain names, please refer to the [TOS help documentation](https://www.volcengine.com/docs/6349/107356).


<span id="0eba3464"></span>
# Query table

Query the created external hive table using SELECT statements. The specifics of the SELECT statement can be found in [SQL Syntax](https://docs.byteplus.com/en/docs/bytehouse/sql-syntax).

```SQL
select * from [db.]table_name  ... [SETTINGS ...]
```


When querying the external Hive table, the following Setting options are available:


* use_local_cache_for_remote_storage: Whether to enable disk cache, default is true.

* Enable optimizer: Whether to enable the optimizer.


The 'use_local_cache_for_remote_storage' option is enabled by default, indicating that the local cache is used for remote file systems, which can speed up query execution.

<span id="e3753227"></span>
# Modify table schema


* View table schema


```SQL
DESCRIBE TABLE table_name;
```



* Modify table schema


After changes to the Hive schema, you can manually update the schema of tables in CE to keep it synchronized with the modified Hive schema.

```SQL
ALTER TABLE table_name [ON CLUSTER cluster] REFRESH SCHEMA SETTINGS mutations_sync=1
```


<span id="1fb18125"></span>
# Usage example


* General DDL


```SQL
--Create hive external table
   
CREATE TABLE hivetable ON CLUSTER ch_qa_cluster1
ENGINE = HiveCluster('ch_qa_cluster1', 'thrift://localhost:9083', 'hive_database_name', 'hive_table_name')
PARTITION BY date;
   
--Query hive external table
select * from hivetable where xxx settings use_local_cache_for_remote_storage=true,enable_optimizer=true;
```



* LasFormation integration


```SQL
create table las_t 
Engine = HiveCluster('cluster_name', 'cache_key', 'las_database','las_table')
settings 
meta_type = 'lf',
lf_metastore_url = 'las_addr',
lf_metastore_ak_id = 'ak',
lf_metastore_ak_secret = 'sk',
lf_metastore_region = '{REGION}',
endpoint = 'tos-s3-{REGION}.ibytepluses.com',   
ak_id = 'ak', 
ak_secret = 'sk' 
```


<span id="8b174fac"></span>
# Column type mapping

When creating schemas, you can refer to the following type mapping table.


|Hive Data Types |ByteHouse Data Types |Remarks |
|---|---|---|
|tinyint |Tinyint/Int8 |Case Sensitive |
|smallint |Smallint/Int16 |case sensitive |
|int |int |case insensitive |
|int |Int32 |case sensitive |
|bigint |Int64 |Case sensitive |
|float |Float32 |Case sensitive |
|double |Float64 |Case sensitive |
|bigint |Bigint |Case insensitive |
|string |String |Case sensitive |
|varchar(N) |FixedString(N) |Case sensitive |
|char(N) |FixedString(N) |Case sensitive |
|binary |String |Case sensitive |
|boolean |UInt8 |Case sensitive |
|decimal(P,S) |Decimal(P,S) |Case insensitive |
|date |Date |Case Sensitivity |
|timestamp |DateTime |Case Sensitivity |
|array |Array(xxx) |Case Sensitive, Parentheses |
|map |Map(xxx, xxx) |Case Sensitivity and Parentheses |
