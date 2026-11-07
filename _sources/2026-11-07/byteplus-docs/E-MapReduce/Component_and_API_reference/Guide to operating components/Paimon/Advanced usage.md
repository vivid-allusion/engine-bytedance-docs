---
title: "Advanced usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/paimon_advanced_usage"
---

Volcano Engine E\-MapReduce (EMR) supports writing to Paimon tables via Spark SQL, and supports querying Paimon tables using Hive and Presto engines. For queries, the Paimon version of EMR is adapted for Presto and is directly integrated into Presto without additional configuration.

<span id="_1-paimon-spark集成"></span>
## Paimon \- Spark integration

This section describes how to configure Spark ThriftServer to connect to Paimon.


1. Log in to [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar, navigate to **Cluster Management \> Cluster List \> Cluster Details \> Service List \> Spark Service Parameters**.

3. After installing Paimon, go to the sparkthriftserver configuration page and in spark\-defaults

   1. Modify the spark.sql.extensions configuration to add org.apache.paimon.spark.extensions.PaimonSparkSessionExtensions (separate existing values with commas)

   2. Add spark.sql.catalog.paimon=org.apache.paimon.spark.SparkCatalog

   3. Add spark.sql.catalog.paimon.metastore=hive


Use beeline to connect to sparkthriftserver for testing. Refer to [Overview](https://docs.byteplus.com/docs/E-MapReduce/109349) and [Ksana for SparkSQL](https://docs.byteplus.com/docs/undefined/69aa394cc85d87051aff3c1d) to configure the username and password for sparkthriftserver connection.

```sql
beeline -u jdbc:hive2://emr-30f8q2lxxxxxxxxxx-master-1:10000/default -n xxxx -p xxxxx
```


You can then use standard SparkSQL to operate Paimon tables.

<span id="_2-paimon-presto集成"></span>
## Paimon \- Presto integration

Modify the warehouse parameter in paimon.properties to point to the actual Hive warehouse path, for example:

`hdfs://emr-cluster/user/hive/warehouse`

Restart all Presto components

View catalog

```sql
SHOW CATALOGS;
```


Create schema

```sql
CREATE SCHEMA paimon.test_db;
```


Query data

```sql
SELECT * FROM paimon.test_db.test_table;
```


<span id="_3-paimon-starrocks集成"></span>
## Paimon \- StarRocks integration

<span id="_3-1-环境集成"></span>
### Environment integration

Copy the core\-site.xml and hdfs\-site.xml configuration files from the Hadoop cluster to the StarRocks cluster, and restart the StarRocks service.

<span id="_3-2-starrocks查询paimon表"></span>
### StarRocks query Paimon table

Create catalog

```sql
CREATE EXTERNAL CATALOG <catalog_name>
[COMMENT <comment>]
PROPERTIES
(
    "type" = "paimon",
    "paimon.catalog.type" = "hive",
    "paimon.catalog.warehouse" = "hdfs://nn:8020/path/to/warehouse",
    "hive.metastore.uris" = "thrift://master-1-1.xxx.emr-volces.com:9083"
)
```


View databases under the catalog

```sql
SHOW DATABASES FROM <catalog_name>;
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c8fac9c1bbb26fbb542517442471b177.png) </span>

Use catalog

```sql
SET CATALOG <catalog_name>;
```


Query Paimon table

```sql
SELECT * FROM <table_name>;
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9a2c8443aef9719bb56b1cd1926ea687.png) </span>

<span id="4a4c6e74"></span>
## Paimon \- Doris integration

<span id="3a0e128c"></span>
### Data preparation

Create a Hadoop cluster and install necessary components such as Spark and Paimon. Select **Hive root path** as HDFS.

Log in to the Hadoop cluster, use spark\-sql to create a Paimon data table and insert data.

```SQL
-- spark-sql
-- Create data table
CREATE TABLE IF NOT EXISTS paimon.default.order_detail (
    order_id BIGINT NOT NULL,
    user_id BIGINT,
    order_amount DECIMAL(10,2),
    order_status STRING,
    create_time TIMESTAMP,
    dt STRING
)
USING paimon
PARTITIONED BY (dt)
OPTIONS (
    'file.format' = 'orc',
    'merge.engine' = 'deduplicate',
    'bucket' = '4'
);
-- Insert test data
INSERT OVERWRITE paimon.default.order_detail 
VALUES 
  (1001, 101, 99.90, 'PAID', TIMESTAMP('2025-01-01 10:00:00'), '20250101'),
  (1002, 102, 199.90, 'UNPAID', TIMESTAMP('2025-01-01 11:00:00'), '20250101'),
  (1003, 103, 299.80, 'PAID', TIMESTAMP('2025-01-01 12:00:00'), '20250101'),
  (1004, 104, 399.70, 'REFUNDED', TIMESTAMP('2025-01-01 13:00:00'), '20250101'),
  (1005, 105, 499.60, 'PAID', TIMESTAMP('2025-01-01 14:00:00'), '20250101'),
  (1006, 106, 599.50, 'UNPAID', TIMESTAMP('2025-01-01 15:00:00'), '20250101'),
  (1007, 107, 699.40, 'PAID', TIMESTAMP('2025-01-01 16:00:00'), '20250101'),
  (1008, 108, 799.30, 'CLOSED', TIMESTAMP('2025-01-01 17:00:00'), '20250101'),
  (1009, 109, 899.20, 'PAID', TIMESTAMP('2025-01-01 18:00:00'), '20250101'),
  (1010, 110, 999.10, 'UNPAID', TIMESTAMP('2025-01-01 19:00:00'), '20250101');
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/569408b0786f4a0e956b71fdf0362b6c~tplv-goo7wpa0wc-image.image" width="1614px" /></div>


<span id="60cecb47"></span>
### Doris query Paimon table

Create catalog

```SQL
-- <hadoop cluster address> like master-1-1.emr-ac4d37aae27728b54792.cn-beijing.emr-volces.com
DROP CATALOG IF EXISTS <catalog_name>;
CREATE CATALOG <catalog_name> 
PROPERTIES 
(
    'type' = 'paimon',
    'paimon.catalog.type' = 'hms',
    'hive.metastore.uris' = 'thrift://<hadoop cluster address>:9083',
    'warehouse' = 'hdfs://<hadoop cluster address>:8020/warehouse/tablespace/managed/hive',
    'hadoop.username' = 'doris',
    'fs.defaultFS' = 'hdfs://<hadoop cluster address>:8020'
);
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8344e177edc4620b001f8a9dea13ec9~tplv-goo7wpa0wc-image.image" width="1318px" /></div>


View databases under the catalog

```SQL
SWITCH <catalog_name>;
SHOW databases;
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02ce7288dee549d2823e2709d1b2087c~tplv-goo7wpa0wc-image.image" width="1030px" /></div>


Query Paimon table

```SQL
USE <database name>;
SHOW tables;
SELECT * FROM <table name>;
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/976ecd4e72ba4b54a0ad5a79d334a533~tplv-goo7wpa0wc-image.image" width="1308px" /></div>


<span id="e008ec01"></span>
## Paimon \- Dateleap usage

<span id="0901e0dc"></span>
### Flink uses HMS catalog

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using Hive metastore as the catalog, Flink Hive bundle is required. Ensure that the Flink Hive bundle has been added to the relevant Flink dependencies.</div>


<span id="77c58fae"></span>
### Spark jobs

In the console, modify the parameter `spark.driver.extraClassPath` to add the path to Spark jars, such as `/usr/lib/emr/current/spark3/jars/*`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">As paths may vary between versions, enter the path as appropriate for your environment.</div>
