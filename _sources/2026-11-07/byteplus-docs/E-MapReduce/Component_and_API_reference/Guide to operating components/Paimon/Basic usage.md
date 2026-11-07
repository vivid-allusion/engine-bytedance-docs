---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/pamon_basic_usage"
---

Currently, in Volcano Engine E\-MapReduce (EMR3.9.0) clusters, the supported version of Paimon is 0.6\-release.

<span id="_1-paimon安装"></span>
## Step 1: Paimon installation

Paimon is installed as an optional component during the creation of a Hadoop cluster. After the cluster is created, ensure that the Paimon component is visible and its status is normal. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456). If Paimon was not installed during cluster initialization, you can also add Paimon to an existing cluster by adding the Paimon component. For details, see [Add/restart services](https://docs.byteplus.com/docs/E-MapReduce/105409).

<span id="_2-功能矩阵"></span>
## Step 2: Feature matrix


|Engine |Version |Batch read |Batch write |Create a table |Modify a table |Streaming write |Streaming read |Batch overwrite write |
|---|---|---|---|---|---|---|---|---|
|Flink |1.16.1 |✅ |✅ |✅ |❌ |✅ |✅ |✅ |
|Spark |3.5.0 |✅ |✅ |✅ |✅ |✅ |✅ |❌ |
|Hive |3.1.3 |✅ |✅ |✅ |❌ |❌ |❌ |❌ |
|Presto |0.280 |✅ |❌ |✅ |✅ |❌ |❌ |❌ |


<span id="_3-通过flink-sql快速上手"></span>
## Step 3: Quick start with Flink SQL

Step 3.1: Start a Flink session cluster

```sql
<FLINK_HOME>/bin/yarn-session.sh -d
```


Step 3.2: Use Flink sql\-client to execute Flink SQL

```sql
<FLINK_HOME>/bin/sql-client.sh
```


<span id="_3-1-catalog"></span>
### 3.1 Catalog

Before using Paimon databases and tables, you need to create a catalog for Paimon.

Currently, Paimon supports two types of catalogs: FileSystem or Hive.

**FileSystem**

This type of catalog stores Paimon database and table metadata in the file system, such as HDFS.

The method for creating a FileSystem\-type catalog with Flink is as follows:

```sql
CREATE CATALOG my_catalog WITH (
'type' = 'paimon',
'warehouse' = 'hdfs://nn:8020/path/to/warehousee'
);

USE CATALOG my_catalog;
```


**Hive**

This type of catalog stores Paimon database and table metadata in the Hive metastore, allowing users to access these Paimon tables through Hive.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using Hive metastore as the catalog, it depends on the Flink Hive bundle. Please ensure that the Flink Hive bundle has been added to the relevant Flink dependencies.</div>


The method for creating an HMS\-type catalog with Flink is as follows:

```sql
CREATE  CATALOG my_hive  WITH  (
    'type' = 'paimon',
    'metastore' = 'hive',
    -- 'uri' = 'thrift://<hive-metastore-host-name>:<port>', default use 'hive.metastore.uris' in HiveConf
    -- 'hive-conf-dir' = '...', this is recommended in the kerberos environment
    -- 'hadoop-conf-dir' = '...', this is recommended in the kerberos environment
    -- 'warehouse' = 'hdfs://nn:8020/path/to/warehouse', this parameter specifies the warehouse address. By default, it uses the value of the hive.metastore.warehouse.dir parameter in hive-site, but you can also customize the path. TOS paths are supported.
);

USE CATALOG my_hive;
```


<span id="_3-2-创建表"></span>
### Step 3.4: Create a table

**Primary key table (主键表)** 

```sql
CREATE TABLE word_count (
    word STRING PRIMARY KEY NOT ENFORCED,
    cnt BIGINT
);
```


**Append\-only table (non\-primary key table)** 

```sql
CREATE TABLE word_count_nonkey (
    word STRING,
    cnt BIGINT
);
```


<span id="_3-3-流式写入"></span>
### Step 3.5: Streaming write

```sql
-- First, create a streaming data source table
CREATE TEMPORARY TABLE word_table (
    word STRING
) WITH (
     'connector' = 'datagen',
     'fields.word.length' = '1'
);

-- When writing to Paimon in streaming mode, you need to set the checkpoint interval
SET 'execution.checkpointing.interval' = '10 s';

-- Stream the source table into Paimon
INSERT INTO word_count SELECT word, COUNT(*) FROM word_table GROUP BY word;
```


<span id="_3-4-流式读取"></span>
### Step 3.6: Streaming read

```sql
-- Switch to streaming mode
SET 'execution.runtime-mode' = 'streaming';

SELECT `interval`, COUNT(*) AS interval_cnt FROM(
SELECT cnt / 10000 AS `interval` FROM word_count
) GROUP BY `interval`;
```


<span id="_3-5-批式写入"></span>
### Step 3.7: Batch write

```sql
INSERT INTO word_count_nonkey VALUES
('a', 1),
('b', 2),
('c', 3);
```


<span id="_3-6-批式读取"></span>
### Step 3.8: Batch read

```sql
-- Switch to batch mode
SET 'execution.runtime-mode' = 'batch';

SELECT * FROM word_count_nonkey;
```


<span id="_4-通过spark-快速上手"></span>
## Step 4: Quick start with Spark

<span id="_4-1-catalog"></span>
### 4.1 Catalog

**Hive catalog**

The method for creating an HMS\-type catalog with Spark is as follows:

```sql
spark-sql ... \
    --conf spark.sql.catalog.paimon=org.apache.paimon.spark.SparkCatalog \
    --conf spark.sql.catalog.paimon.metastore=hive \
    --conf spark.sql.catalog.paimon.warehouse=hdfs://nn:8020/path/to/warehouse \ #This parameter specifies the warehouse address. By default, it uses the value of the hive.metastore.warehouse.dir parameter in hive-site, but you can also customize the path. TOS paths are supported.
    --conf spark.sql.extensions=org.apache.paimon.spark.extensions.PaimonSparkSessionExtensions
```


Use paimon catalog

```sql
use paimon;
```


<span id="_4-2-创建表"></span>
### Step 4.2: Create a table

```sql
create table test_table (
    k int,
    v string
) tblproperties (
    'primary-key' = 'k'
);
```


<span id="_4-3-批式写入"></span>
### Step 4.3: Batch write

```sql
INSERT INTO test_table VALUES (1, 'Hi'), (2, 'Hello');
```


<span id="_4-4-批式查询"></span>
### Step 4.4: Batch query

```sql
SELECT * FROM test_table;
```


<span id="_5-通过hive-快速上手"></span>
## Step 5: Quick start with Hive

<span id="_5-1-首先借助flink-sql创建catalog和库表"></span>
### Step 5.1: First, use Flink SQL to create the catalog and databases/tables

```sql
CREATE CATALOG my_hive WITH (
    'type' = 'paimon',
    'metastore' = 'hive',
    -- 'uri' = 'thrift://<hive-metastore-host-name>:<port>', default use 'hive.metastore.uris' in HiveConf
  -- 'hive-conf-dir' = '...', this is recommended in the kerberos environment
  -- 'hadoop-conf-dir' = '...', this is recommended in the kerberos environment
  -- 'warehouse' = 'hdfs://nn:8020/path/to/table/store/warehouse', default use 'hive.metastore.warehouse.dir' in HiveConf
);

USE CATALOG my_hive;

CREATE TABLE test_table (
    a int,
    b string
);

INSERT INTO test_table VALUES (1, 'Table'), (2, 'Store');

SELECT * FROM test_table;
```


**Hive SQL accesses Paimon tables that already exist in the Hive metastore**

```sql
SHOW TABLES;

SELECT * FROM test_table;

-- The Tez engine does not support writing to Paimon. You need to switch to the MR engine
SET hive.execution.engine=mr;

INSERT INTO test_table VALUES (3, 'a');

SELECT * FROM test_table;
```


<span id="_5-2-创建表"></span>
### Step 5.2: Create a table

```sql
CREATE TABLE hive_test_table(
    a INT COMMENT 'The a field',
    b STRING COMMENT 'The b field'
)STORED BY 'org.apache.paimon.hive.PaimonStorageHandler';
```


<span id="_5-3-以外表的方式访问paimon"></span>
### Step 5.3: Access Paimon as an external table

```sql
-- Caution: The location here points to the address of test_table created above by Flink SQL
CREATE EXTERNAL TABLE external_test_table
STORED BY 'org.apache.paimon.hive.PaimonStorageHandler'
LOCATION '/path/to/table/store/warehouse/default.db/test_table';

SELECT a, b FROM external_test_table ORDER BY a;

INSERT INTO external_test_table VALUES (3, 'Paimon');

SELECT a, b FROM external_test_table ORDER BY a;
```


<span id="a793d86b"></span>
## Step 6: Quick start with Doris

<span id="79c1d8db"></span>
### 5.1 Catalog

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Doris version in use is subject to the following restrictions:</div>



* <div data-tips="true" data-tips-type="warning">Version 2.x: Doris supports this starting from version 2.1.11.</div>


* <div data-tips="true" data-tips-type="warning">Version 3.x: Doris supports this starting from version 3.0.8.</div>


1. Create a catalog.

   
   <Tabs>
   <Tab zoneid="u9Mjcl6I8L" title="HMS Catalog">
   <TabTitle>HMS Catalog</TabTitle>
   
   ```SQL
   CREATE CATALOG IF NOT EXISTS paimon_hms_catalog PROPERTIES (
       'type' = 'paimon',
       'paimon.catalog.type' = 'hms',
       'hive.metastore.uris' = '<hms_url>',
       'warehouse' = '<tos_bucket_warehouse>',
       'las.tos.endpoint' = '<tos_endpoint>',
       'aws.s3.region'= '<region>',
       'aws.s3.endpoint' = '<tos_s3_endpoint>',
       'aws.s3.access_key' = '<ak>',
       'aws.s3.secret_key' = '<sk>'
   );
   ```
   
   
   Details:
   
   
      * `las.tos.endpoint`: The endpoint for proton to access tos.
   
      * `aws.s3.endpoint`: The endpoint for the backend to access s3.
   
   
   </Tab>
   <Tab zoneid="tBHyndhbVo" title="FileSystem Catalog">
   <TabTitle>FileSystem Catalog</TabTitle>
   
   ```SQL
   CREATE CATALOG IF NOT EXISTS paimon_filesystem_catalog PROPERTIES (
       'type' = 'paimon',
       'paimon.catalog.type' = 'filesystem',
       'warehouse' = '<tos_bucket_warehouse>',
       'las.tos.endpoint' = '<tos_endpoint>',
       'aws.s3.region'= '<region>',
       'aws.s3.endpoint' = '<tos_s3_endpoint>',
       'aws.s3.access_key' = '<ak>',
       'aws.s3.secret_key' = '<sk>'
   );
   ```
   
   
   Details:
   
   
      * `las.tos.endpoint`: The endpoint for proton to access tos.
   
      * `aws.s3.endpoint`: The endpoint for the backend to access s3.
   
   
   </Tab>
   <Tab zoneid="tthdc0ScCr" title="LAS Catalog">
   <TabTitle>LAS Catalog</TabTitle>
   
   For more information, please refer to [Doris 访问 LAS Catalog](https://docs.byteplus.com/docs/undefined/698008803c928c0509be188b).
   
   
   </Tab>
   </Tabs>
   

2. Switch catalog and view databases

   ```SQL
   switch ${已创建catalog名称};
   show databases;
   use ${数据库名};
   ```
   

3. Query existing Paimon tables

   ```SQL
   show tables;
   select * from ${表名称};
   ```
