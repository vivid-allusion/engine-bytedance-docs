---
title: "Read LAS data"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Read_LAS_data"
---

This article describes how to use External Catalog to read LAS data. By creating an LAS Catalog, you can query data in LAS directly without performing data import.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the function for reading LAS data requires allowlist access. To operate, please contact Volcano Engine technical support by <a href="https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D">submitting a ticket</a>.</div>


<span id="09859ae2"></span>
# context

**LAS (Lakehouse Analytics Service)**  is a data lake solution designed to simplify and accelerate the construction and management of data lakes. By providing unified metadata management, data access control, metadata discovery, and data integration, it helps organizations break down data silos, strengthen the lakehouse architecture, and better organize, share, access, and analyze large\-scale enterprise data. For detailed information, refer to [LAS official documentation](https://docs.byteplus.com/en/docs/Byteplus_LAS/What_is_AI_data_lake_service).

<span id="7ea4d13e"></span>
# Limits


* The StarRocks cluster and the LAS Catalog must be in the same region. For related operations, refer to [StarRocks-Hive Catalog](https://docs.starrocks.io/zh/docs/data_source/catalog/hive_catalog/).

* Supported StarRocks versions for this capability: StarRocks 3.3.20 and later.

* Only supported by Serverless StarRocks.


<span id="ff81794d"></span>
# Integrate LAS Catalog

<span id="_2-配置core-site"></span>
## Integrate Hive Catalog on LAS

The following example uses data stored in TOS.

<span id="9adcedc1"></span>
### Syntax

```SQL
CREATE EXTERNAL CATALOG <catalog_name>
[COMMENT <comment>]
PROPERTIES
(
  "type"  =  "hive",
  "hive.metastore.type"  =  "las",
  "hive.metastore.uris"  =  "thrift://<LAS_HMS_IP>:48869",
-- Optional: Specify which user-defined catalog under LAS to use; if not specified, defaults to hive
  "hive.metastore.catalog.default" = "<las_catalog_name>",

  -- LAS authentication
  "las.hive.metastore.service"   = "catalog_service",
  "las.hive.metastore.region"    = "<las_region>",
  "las.hive.metastore.access.key"= "<your_access_key>",
  "las.hive.metastore.secret.key"= "<your_secret_key>",

-- Required for HNS buckets only; optional for FNS buckets
  "las.tos.endpoint" = "tos-cn-beijing.ivolces.com",

  -- TOS (S3 protocol) access configuration
  "aws.s3.enable_ssl"                  = "false",
  "aws.s3.region"                      = "<tos_region>",
  "aws.s3.use_instance_profile"        = "false",
  "aws.s3.use_aws_sdk_default_behavior"= "false",
  "aws.s3.endpoint"                    = "<tos_s3_endpoint>",
  "aws.s3.access_key"                  = "<your_access_key>",
  "aws.s3.secret_key"                  = "<your_secret_key>"
);
```


<span id="40c80858"></span>
### Note


|**Parameters** |**Required** |Note |
|---|---|---|
|catalog_name |Yes |The name of the catalog attached to the LAS Catalog. Naming requirements are as follows:<br><br><br>* Must consist of letters (a\-z or A\-Z), digits (0\-9), or underscores (_), and must begin with a letter.<br><br>* The total length must not exceed 1023 characters.<br><br>* Catalog names are case\-sensitive. |
|comment |No |Description of the catalog attached to the LAS Catalog. |
|hive.metastore.type |Yes |Set to `las` to trigger access to Hive Metastore using the LAS client |
|hive.metastore.uris |Yes |Thrift address of LAS Hive Metastore. Format: `thrift://<LAS_HMS_IP>:48869`.<br><br>For example: `thrift://lakeformation.las.cn-beijing.ivolces.com:48869` |
|hive.metastore.catalog.default |No |Used to specify which LAS Catalog to use in multi\-catalog scenarios; the default value is `hive`, or you can enter a user\-defined catalog name on LAS. |
|las.hive.metastore.service |Yes |Set to `catalog_service`. |
|las.hive.metastore.region |Yes |Region of the LAS Catalog instance. For example, `cn-beijing`. |
|las.hive.metastore.access.key |Yes |AK for accessing LAS metadata. LAS Catalog\-related database and table permissions are required. |
|las.hive.metastore.secret.key |Yes |SK for accessing LAS metadata. LAS Catalog\-related database and table permissions are required. |
|las.tos.endpoint |Required for HNS buckets / optional for FNS buckets |Endpoint used by Proton to access TOS, for example `tos-cn-beijing.ivolces.com`. |
|aws.s3.region |Yes |Region where the TOS bucket instance is located. which is generally the same address as las.hive.metastore.region above. |
|aws.s3.endpoint |Yes |Region where the TOS bucket instance is located. Caution: You need to enter the s3 Endpoint here. Additionally, if tos and lasformation are in the same region, it is recommended to use the internal network address. |
|aws.s3.access_key |Yes |AK used by TOS. |
|aws.s3.secret_key |Yes |SK used by TOS. |
|aws.s3.enable_ssl |No |Whether to enable SSL; default is `false` |
|aws.s3.use_instance_profile |No |Whether to use instance profile; default is `false` |
|aws.s3.use_aws_sdk_default_behavior |No |Whether to use AWS SDK default behavior; default is `false` |


<span id="b4407229"></span>
## Integrate Paimon Catalog on LAS

StarRocks supports using LAS as the Hive Metastore for Paimon tables through PaimonConnector and the LAS client.

<span id="908d4347"></span>
### Syntax

```SQL
CREATE EXTERNAL CATALOG <catalog_name> PROPERTIES (
  -- Let StarRocks use PaimonConnector
  "type" = "paimon",
  -- The Metastore type for Paimon is fixed as hive (do not use paimon)
  "paimon.catalog.type" = "hive",
  -- Thrift address of LAS Hive Metastore
  "hive.metastore.uris" = "thrift://<LAS_HMS_IP>:48869",
  -- Triggers the LAS client branch
  "hive.metastore.type" = "las",
  -- Optional: Specify which user-defined catalog under LAS to use; if not specified, defaults to hive
  "hive.metastore.catalog.default" = "<las_catalog_name>",

  -- Paimon warehouse path (TOS)
  "paimon.catalog.warehouse" = "tos://<bucket>/<prefix>/",

  -- LAS authentication
  "las.hive.metastore.service"   = "catalog_service",
  "las.hive.metastore.region"    = "<las_region>",
  "las.hive.metastore.access.key"= "<your_access_key>",
  "las.hive.metastore.secret.key"= "<your_secret_key>",

  -- HNS bucket required
  "las.tos.endpoint" = "tos-cn-beijing.ivolces.com",

  -- TOS (S3 protocol) access configuration (using Paimon's s3 FileIO)
  "aws.s3.enable_ssl"                  = "false",
  "aws.s3.region"                      = "<tos_region>",
  "aws.s3.use_instance_profile"        = "false",
  "aws.s3.use_aws_sdk_default_behavior"= "false",
  "aws.s3.endpoint"                    = "tos-s3-cn-beijing.ivolces.com",
  "aws.s3.access_key"                  = "<your_access_key>",
  "aws.s3.secret_key"                  = "<your_secret_key>"
);
```


<span id="e0d906e4"></span>
### Note


|**Parameters** |**Required** |Note |
|---|---|---|
|`type` |Yes |Set to `paimon` |
|`paimon.catalog.type` |Yes |Set to `hive` to enable Paimon to use Hive Metastore as the metadata backend |
|`paimon.catalog.warehouse` |Yes |Paimon warehouse path, must be an object storage path (for example, `tos://hns-test-xxx/test1/`); do not use a thrift address |
|Other parameters: All other LAS / TOS / S3 related parameters are consistent with the Hive Catalog parameter description. |||


<span id="8c43a6a2"></span>
## Integrate Iceberg Catalog on LAS

<span id="3ae0fd95"></span>
### Syntax

```SQL
CREATE EXTERNAL CATALOG <catalog_name> PROPERTIES
(
  "type" = "iceberg",
  -- Key switch for Iceberg integration with LAS
  "iceberg.catalog.type" = "las",
  -- Thrift address of LAS Hive Metastore
  "hive.metastore.uris" = "thrift://<LAS_HMS_IP>:48869",
  "hive.metastore.type" = "las",
  -- Optional: Specify which user-defined catalog under LAS to use
  "hive.metastore.catalog.default" = "<las_catalog_name>",

  -- Iceberg warehouse path (TOS)
  "iceberg.catalog.warehouse" = "tos://<bucket>/<prefix>/",

  -- LAS authentication
  "las.hive.metastore.service"   = "catalog_service",
  "las.hive.metastore.region"    = "<las_region>",
  "las.hive.metastore.access.key"= "<your_access_key>",
  "las.hive.metastore.secret.key"= "<your_secret_key>",

  -- HNS bucket required
  "las.tos.endpoint" = "tos-cn-beijing.ivolces.com",

  -- TOS (S3 protocol) access configuration
  "aws.s3.enable_ssl" = "false",
  "aws.s3.region"     = "<tos_region>",
  "aws.s3.endpoint"   = "tos-s3-cn-beijing.ivolces.com",
  "aws.s3.access_key" = "<your_access_key>",
  "aws.s3.secret_key" = "<your_secret_key>"
);
```


<span id="a6e88523"></span>
### Note


|**Parameters** |**Required** |Note |
|---|---|---|
|`type` |Yes |Set to `iceberg` |
|`iceberg.catalog.type` |Yes |Set to `las` to enable Iceberg to use the LAS client to access metadata |
|`iceberg.catalog.warehouse` |Yes |Iceberg warehouse path, must be an object storage path (for example, `tos://hns-test-xxx/test1/`) |
|Other parameters: All other LAS / TOS / S3 related parameters are consistent with the Hive Catalog parameter description. |||


<span id="fdd3d10f"></span>
# Delete Catalog

You can delete a specified catalog attached to the LAS Catalog using DROP CATALOG.

```SQL
DROP CATALOG <catalog_name>
```


<span id="537f2e34"></span>
# Query data

After creating a catalog attached to the LAS Catalog, you can use it to access LAS data.


1. Set the current catalog. Assume the catalog_name we created is `las`.

   ```SQL
   set catalog las;
   ```
   

2. Switch the database. For example, using the `sr_demo` database, users need to replace `sr_demo` with the actual database.

   ```SQL
   USE sr_demo;
   ```
   

3. View the table schema. For example, using the `sr_demo_test` table, users need to replace `sr_demo_test` with the actual table.

   ```SQL
   DESC sr_demo_test;
   SHOW CREATE TABLE sr_demo_test;
   ```
   

4. Query data in the table. For example, using the `sr_demo_test` table, users need to replace `sr_demo_test` with the actual table.

   ```SQL
   SELECT * FROM sr_demo_test LIMIT 10;
   ```
   

5. Import data into an internal table.

   Assume there is an OLAP table under the `olap_db` database, with the table name `olap_tbl`. You can convert the data in this table and import it into StarRocks as follows:

   ```SQL
   INSERT INTO default_catalog.olap_db.olap_tbl SELECT * FROM las.sr_demo.sr_demo_test;
   ```
   

6. Delete Catalog.

   ```SQL
   DROP CATALOG las;
   ```
   


<span id="0f9ef747"></span>
# Metadata cache

Consistent with the logic of the open\-source Hive catalog, StarRocks currently caches metadata. See [StarRocks文档](https://docs.byteplus.com/docs/E-MapReduce/109132#%E6%89%8B%E5%8A%A8%E6%88%96%E8%87%AA%E5%8A%A8%E6%9B%B4%E6%96%B0%E5%85%83%E6%95%B0%E6%8D%AE%E7%BC%93%E5%AD%98). To manually refresh the cache when needed, execute the following statement.

```SQL
refresh external table <table_name>;
```


<span id="26b4ace1"></span>
# Application examples

The following provides complete SQL for several typical combinations of "Spark write + StarRocks read", covering common combinations of (Paimon / Hive / Iceberg) × (HNS / FNS) × (user\-defined catalog / default catalog / filesystem mode).

> The placeholders `tos://hns-test-xxx/test1/`, `<your_access_key>`, and `<your_secret_key>` in the examples must be replaced with your actual values.


<span id="6298f98a"></span>
## Paimon

<span id="6336dfa0"></span>
### Paimon + LAS + HNS + user\-defined catalog

**Spark side (data construction)** 

```SQL
-- Default parameters
SET spark.sql.catalog.spark_paimon_catalog=org.apache.paimon.spark.SparkCatalog;
SET spark.sql.catalog.spark_paimon_catalog.metastore=hive;
SET spark.sql.storeAssignmentPolicy=ansi;
-- Custom warehouse
SET spark.sql.catalog.spark_paimon_catalog.warehouse=tos://hns-test-xxx/test1/;
USE spark_paimon_catalog;
-- Specify LAS custom catalog
SET spark.hadoop.hive.metastore.catalog.default=my_hns_catalog;

CREATE DATABASE IF NOT EXISTS test_paimon_db;
CREATE TABLE IF NOT EXISTS test_paimon_db.test_tb2(id INT, name STRING);
INSERT INTO TABLE test_paimon_db.test_tb2 VALUES(1, 'paimon'),(2, 'paimon');
```


**StarRocks side (query)** 

```SQL
DROP CATALOG IF EXISTS my_hns_catalog;
CREATE EXTERNAL CATALOG my_hns_catalog PROPERTIES (
  "type" = "paimon",
  "paimon.catalog.type" = "hive",
  "hive.metastore.uris" = "thrift://lakeformation.las.cn-beijing.ivolces.com:48869",
  "hive.metastore.type" = "las",
  "hive.metastore.catalog.default" = "my_hns_catalog",
  "paimon.catalog.warehouse" = "tos://hns-test-xxx/test1/",
  "las.hive.metastore.service"   = "catalog_service",
  "las.hive.metastore.region"    = "cn-beijing",
  "las.hive.metastore.access.key"= "<your_access_key>",
  "las.hive.metastore.secret.key"= "<your_secret_key>",
  "las.tos.endpoint" = "tos-cn-beijing.ivolces.com",
  "aws.s3.enable_ssl"                  = "false",
  "aws.s3.region"                      = "cn-beijing",
  "aws.s3.use_instance_profile"        = "false",
  "aws.s3.use_aws_sdk_default_behavior"= "false",
  "aws.s3.endpoint"                    = "tos-s3-cn-beijing.ivolces.com",
  "aws.s3.access_key"                  = "<your_access_key>",
  "aws.s3.secret_key"                  = "<your_secret_key>"
);

SET CATALOG my_hns_catalog;
SHOW DATABASES;
USE test_paimon_db;
SELECT * FROM test_tb2;
```


<span id="bd3d44d0"></span>
### Paimon + filesystem mode + HNS

No Hive Metastore required; access HNS buckets directly in Paimon Filesystem Catalog mode.

```SQL
DROP CATALOG IF EXISTS paimon_fs_catalog;
CREATE EXTERNAL CATALOG paimon_fs_catalog PROPERTIES (
  "type" = "paimon",
  "paimon.catalog.type" = "filesystem",
  "paimon.catalog.warehouse" = "tos://hns-test-xxx/test1/",
  "las.tos.endpoint" = "tos-cn-beijing.ivolces.com",
  "aws.s3.region"     = "cn-beijing",
  "aws.s3.endpoint"   = "tos-s3-cn-beijing.ivolces.com",
  "aws.s3.access_key" = "<your_access_key>",
  "aws.s3.secret_key" = "<your_secret_key>"
);
SET CATALOG paimon_fs_catalog;
SHOW DATABASES;
USE test_paimon_db;
SHOW TABLES;
SELECT * FROM test_tb;
```


<span id="bd099f88"></span>
### Paimon + LAS + HNS + default catalog (`hive`)

Usage is basically the same as 11.1, except that `hive.metastore.catalog.default` uses the default value `hive`, and Spark writes data to the LAS default catalog.

**Spark side (data construction)** 

```SQL
SET spark.sql.catalog.spark_paimon_catalog=org.apache.paimon.spark.SparkCatalog;
SET spark.sql.catalog.spark_paimon_catalog.metastore=hive;
SET spark.sql.storeAssignmentPolicy=ansi;
SET spark.sql.catalog.spark_paimon_catalog.warehouse=tos://hns-test-xxx/test1/;
USE spark_paimon_catalog;

CREATE DATABASE IF NOT EXISTS demo_paimon_default;
CREATE TABLE IF NOT EXISTS demo_paimon_default.t2(id INT, name STRING);
INSERT INTO TABLE demo_paimon_default.t2 VALUES(1, 'hehe'),(777, 'haha');
```


**StarRocks side (query)** 

```SQL
DROP CATALOG IF EXISTS paimon_default_catalog;
CREATE EXTERNAL CATALOG paimon_default_catalog PROPERTIES (
  "type" = "paimon",
  "paimon.catalog.type" = "hive",
  "hive.metastore.uris" = "thrift://lakeformation.las.cn-beijing.ivolces.com:48869",
  "hive.metastore.type" = "las",
  "hive.metastore.catalog.default" = "hive",
  "paimon.catalog.warehouse" = "tos://hns-test-xxx/test1/",
  "las.hive.metastore.service"   = "catalog_service",
  "las.hive.metastore.region"    = "cn-beijing",
  "las.hive.metastore.access.key"= "<your_access_key>",
  "las.hive.metastore.secret.key"= "<your_secret_key>",
  "las.tos.endpoint" = "tos-cn-beijing.ivolces.com",
  "aws.s3.enable_ssl"                  = "false",
  "aws.s3.region"                      = "cn-beijing",
  "aws.s3.endpoint"                    = "tos-s3-cn-beijing.ivolces.com",
  "aws.s3.access_key"                  = "<your_access_key>",
  "aws.s3.secret_key"                  = "<your_secret_key>"
);

SET CATALOG paimon_default_catalog;
USE demo_paimon_default;
SELECT * FROM t2;
```


<span id="affb73b1"></span>
## Hive

<span id="031f7162"></span>
### Hive + self\-built HMS + HDFS

Comparison scenario for non\-LAS and non\-TOS: access HDFS tables on a self\-built Hive Metastore in an EMR cluster.

```SQL
DROP CATALOG IF EXISTS hive_hdfs_catalog;
CREATE EXTERNAL CATALOG hive_hdfs_catalog PROPERTIES (
  "type" = "hive",
  "hive.metastore.uris" = "thrift://<emr-master>:9083",
  "hadoop.username"     = "doris",
  "fs.defaultFS"        = "hdfs://<emr-master>:8320"
);
SET CATALOG hive_hdfs_catalog;
USE hive_demo_db;
SELECT * FROM hive_demo_t1;
```


<span id="579f604e"></span>
### Hive + LAS + HNS + user\-defined catalog

**Spark side (data construction)** 

```SQL
SET spark.hadoop.hive.metastore.catalog.default=my_hns_catalog;

CREATE DATABASE IF NOT EXISTS hive_lll_fns_1;
CREATE TABLE IF NOT EXISTS hive_lll_fns_1.hive_lll_fns_table_1(id INT, name STRING);
INSERT INTO TABLE hive_lll_fns_1.hive_lll_fns_table_1 VALUES(1, 'hehe'),(2, 'haha'),(3, 'mary');
```


**StarRocks side (query)** 

```SQL
DROP CATALOG IF EXISTS hive_hns_user_catalog;
CREATE EXTERNAL CATALOG hive_hns_user_catalog
PROPERTIES
(
  "type"  =  "hive",
  "hive.metastore.type"  =  "las",
  "hive.metastore.uris"  = "thrift://lakeformation.las.cn-beijing.ivolces.com:48869",
  "hive.metastore.catalog.default" = "my_hns_catalog",

  "las.hive.metastore.service"   = "catalog_service",
  "las.hive.metastore.region"    = "cn-beijing",
  "las.hive.metastore.access.key"= "<your_access_key>",
  "las.hive.metastore.secret.key"= "<your_secret_key>",
  "las.tos.endpoint"             = "tos-cn-beijing.ivolces.com",

  "aws.s3.enable_ssl"                  = "true",
  "aws.s3.region"                      = "cn-beijing",
  "aws.s3.use_instance_profile"        = "false",
  "aws.s3.use_aws_sdk_default_behavior"= "false",
  "aws.s3.endpoint"                    = "tos-s3-cn-beijing.ivolces.com",
  "aws.s3.access_key"                  = "<your_access_key>",
  "aws.s3.secret_key"                  = "<your_secret_key>"
);
SET CATALOG hive_hns_user_catalog;
USE hive_lll_fns_1;
SELECT * FROM hive_lll_fns_table_1;
```


<span id="01ca0206"></span>
### Hive + LAS + FNS + default catalog

For FNS buckets, `las.tos.endpoint` can be omitted, in which case s3a is used; if `las.tos.endpoint` is specified, Proton is used uniformly.

```SQL
DROP CATALOG IF EXISTS hive_fns_default_catalog;
CREATE EXTERNAL CATALOG hive_fns_default_catalog
PROPERTIES
(
  "type"  =  "hive",
  "hive.metastore.type"  =  "las",
  "hive.metastore.uris"  = "thrift://lakeformation.las.cn-beijing.ivolces.com:48869",

  "las.hive.metastore.service"   = "catalog_service",
  "las.hive.metastore.region"    = "cn-beijing",
  "las.hive.metastore.access.key"= "<your_access_key>",
  "las.hive.metastore.secret.key"= "<your_secret_key>",
  -- Optional: To unify FNS bucket access via the Proton channel, keep the following line; to use s3a, delete it
  "las.tos.endpoint"             = "tos-cn-beijing.ivolces.com",

  "aws.s3.enable_ssl"                  = "false",
  "aws.s3.region"                      = "cn-beijing",
  "aws.s3.use_instance_profile"        = "false",
  "aws.s3.use_aws_sdk_default_behavior"= "false",
  "aws.s3.endpoint"                    = "tos-s3-cn-beijing.ivolces.com",
  "aws.s3.access_key"                  = "<your_access_key>",
  "aws.s3.secret_key"                  = "<your_secret_key>"
);
SET CATALOG hive_fns_default_catalog;
USE demo_hive_db;
SELECT * FROM demo_hive_t;
```


<span id="53026892"></span>
## Iceberg

<span id="1ed263e4"></span>
### Iceberg + self\-built HMS + TOS (FNS)

Example of Iceberg integration without LAS:

```SQL
DROP CATALOG IF EXISTS iceberg_hms_catalog;
CREATE EXTERNAL CATALOG iceberg_hms_catalog PROPERTIES (
  "type" = "iceberg",
  "iceberg.catalog.type" = "hive",
  "hive.metastore.uris" = "thrift://<emr-master>:9083",
  "las.tos.endpoint" = "tos-cn-beijing.ivolces.com",
  "aws.s3.region"     = "cn-beijing",
  "aws.s3.endpoint"   = "tos-s3-cn-beijing.ivolces.com",
  "aws.s3.access_key" = "<your_access_key>",
  "aws.s3.secret_key" = "<your_secret_key>"
);
SET CATALOG iceberg_hms_catalog;
USE iceberg_demo;
SELECT * FROM demo_table;
```


<span id="9fca133f"></span>
### Iceberg + LAS + HNS + user\-defined catalog

**Spark side (data construction)** 

```SQL
SET spark.sql.catalog.spark_iceberg_catalog=org.apache.iceberg.spark.SparkCatalog;
SET spark.sql.catalog.spark_iceberg_catalog.type=hive;
SET spark.sql.storeAssignmentPolicy=ansi;
USE spark_iceberg_catalog;
SET spark.hadoop.hive.metastore.catalog.default=my_hns_catalog;

CREATE DATABASE IF NOT EXISTS test_iceberg_db;
CREATE TABLE IF NOT EXISTS test_iceberg_db.test_tb(id INT, name STRING);
INSERT INTO TABLE test_iceberg_db.test_tb VALUES(1, 'hehe'),(2, 'haha');
```


**StarRocks side (query)** 

```SQL
DROP CATALOG IF EXISTS iceberg_hns_user_catalog;
CREATE EXTERNAL CATALOG iceberg_hns_user_catalog
PROPERTIES
(
  "type" = "iceberg",
  "iceberg.catalog.type" = "las",
  "hive.metastore.uris" = "thrift://lakeformation.las.cn-beijing.ivolces.com:48869",
  "hive.metastore.type" = "las",
  "hive.metastore.catalog.default" = "my_hns_catalog",
  "iceberg.catalog.warehouse" = "tos://hns-test-xxx/test1/",
  "las.hive.metastore.service"   = "catalog_service",
  "las.hive.metastore.region"    = "cn-beijing",
  "las.hive.metastore.access.key"= "<your_access_key>",
  "las.hive.metastore.secret.key"= "<your_secret_key>",
  "las.tos.endpoint"             = "tos-cn-beijing.ivolces.com",
  "aws.s3.enable_ssl"                  = "false",
  "aws.s3.region"                      = "cn-beijing",
  "aws.s3.use_instance_profile"        = "false",
  "aws.s3.use_aws_sdk_default_behavior"= "false",
  "aws.s3.endpoint"                    = "tos-s3-cn-beijing.ivolces.com",
  "aws.s3.access_key"                  = "<your_access_key>",
  "aws.s3.secret_key"                  = "<your_secret_key>"
);
SET CATALOG iceberg_hns_user_catalog;
USE test_iceberg_db;
SELECT * FROM test_tb;
```


<span id="7adb9100"></span>
### Iceberg + LAS + FNS + default catalog

```SQL
DROP CATALOG IF EXISTS iceberg_fns_default_catalog;
CREATE EXTERNAL CATALOG iceberg_fns_default_catalog PROPERTIES (
  "type" = "iceberg",
  "iceberg.catalog.type" = "las",
  "hive.metastore.uris" = "thrift://lakeformation.las.cn-beijing.ivolces.com:48869",
  "iceberg.catalog.warehouse" = "tos://<bucket>/<prefix>/",
  "las.hive.metastore.service"   = "catalog_service",
  "las.hive.metastore.region"    = "cn-beijing",
  "las.hive.metastore.access.key"= "<your_access_key>",
  "las.hive.metastore.secret.key"= "<your_secret_key>",
  "aws.s3.enable_ssl"                  = "false",
  "aws.s3.region"                      = "cn-beijing",
  "aws.s3.endpoint"                    = "tos-s3-cn-beijing.ivolces.com",
  "aws.s3.access_key"                  = "<your_access_key>",
  "aws.s3.secret_key"                  = "<your_secret_key>"
);
SET CATALOG iceberg_fns_default_catalog;
USE iceberg_demo_db;
SELECT COUNT(*) FROM iceberg_demo_db.demo_table;
SELECT * FROM iceberg_demo_db.demo_table LIMIT 10;
```
