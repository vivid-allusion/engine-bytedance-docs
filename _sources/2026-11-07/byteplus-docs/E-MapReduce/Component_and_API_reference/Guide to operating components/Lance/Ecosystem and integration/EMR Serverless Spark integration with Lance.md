---
title: "EMR Serverless Spark integration with Lance"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_Spark_integration_with_Lance"
---

Currently, Lance supports both Spark and Ray compute engines. Ray's compute capabilities are primarily encapsulated and implemented through the pylance module. To fully demonstrate the synergy between compute engines and data warehouses, as well as the advantages of SQL language in implementing complex business logic, this document focuses on the Spark compute engine, detailing its integration process with Hive tables and SQL use cases.

<span id="c983491f"></span>
## Prerequisites

<span id="1665d386"></span>
### Enable EMR Serverless queue

Verify that the user has permission for the [EMR Serverless queue](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/serverless/).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/056b53a7027145be96d50a77f3aaa4b0~tplv-goo7wpa0wc-image.image) </span>

<span id="09ffb6c4"></span>
### Enable Metadata Permissions

Verify that the user has operation permissions for the relevant Catalog. For detailed instructions, refer to: [Permission management](https://www.volcengine.com/docs/6492/1264534).

<span id="16125fd8"></span>
## Limits


1. Currently, a single SQL statement or Spark task accessing a Lance table must be within the same las catalog.

2. Tables in the Lance Catalog can perform join operations with Hive tables in the Hive Catalog. Caution: This feature currently does not support join operations across multiple Lance Catalogs.

3. Lance tables required by a single task must only be stored in a fixed TOS bucket.

4. Currently, only access via PySpark and custom jobs is supported.

5. The images referenced in the following documentation are only supported in the Beijing region. For other regions, please contact the Volcano Engine Technical Team for custom images.

6. Access operations for Spark compute groups are currently not supported, including access via the Kyubbi component.

7. alter table add/drop column is currently not supported.


<span id="6bce70d6"></span>
## SparkSQL operation guide

<span id="f6664ebe"></span>
### Parameter configuration

The following parameters are required to operate Lance tables:

```SQL
--{} section should be completed according to your actual situation.

-- Fixed value
set tqs.query.engine.type = sparkcli;
set spark.sql.storeAssignmentPolicy = ANSI;

-- las catalog configuration
set spark.hadoop.hive.hms.client.is.public.cloud=true;
set spark.hadoop.hive.metastore.execute.setugi=false;
set spark.hadoop.hive.client.las.region.name=cn-beijing;
set spark.hadoop.hive.client.las.ak={your ak};
set spark.hadoop.hive.client.las.sk={your sk};
set spark.hadoop.hive.metastore.uris=thrift://lakeformation.las.cn-beijing.ivolces.com:48869;
set spark.hadoop.metastore.catalog.default={las_catalog_name};

-- lance configuration
set serverless.spark.lance.enabled=true;
set emr.serverless.spark.custom.parse.enabled = true;
set spark.sql.catalog.lance=com.lancedb.lance.spark.LanceNamespaceSparkCatalog;
set spark.sql.extensions=com.lancedb.lance.spark.extensions.LanceSparkSessionExtensions;
set spark.sql.catalog.lance.impl=las2;
set spark.sql.catalog.lance.storage.virtual_hosted_style_request=true;
set spark.sql.catalog.lance.storage.enable_virtual_host_style=true;
set spark.sql.catalog.lance.storage.transform_tos_to_s3=true;
set spark.sql.catalog.lance.storage.aws_region=cn-beijing;
set spark.sql.catalog.lance.storage.aws_endpoint=https://{bucket}.tos-s3-cn-beijing.ivolces.com;
set spark.sql.catalog.lance.storage.access_key_id={your ak};
set spark.sql.catalog.lance.storage.secret_access_key={your sk};
```


Parameter description:


|spark.hadoop.hive.client.las.region.name |The region where your current service is located |
|---|---|
|spark.hadoop.hive.client.las.ak |The AK that can access the LAS AI Data Lake |
|spark.hadoop.hive.client.las.sk |The SK that can access the LAS AI Data Lake |
|spark.hadoop.hive.metastore.uris |The service address of the LAS AI Data Lake |
|spark.hadoop.metastore.catalog.default |The default LAS Catalog accessed in the job |
|serverless.spark.lance.enabled |Fixed value true, indicates that the Lance feature is enabled |
|emr.serverless.spark.custom.parse.enabled |Fixed value true, supports Lance's Spark SQL extension |
|spark.sql.catalog.lance |Fixed value com.lancedb.lance.spark.LanceNamespaceSparkCatalog |
|spark.sql.extensions |Fixed value com.lancedb.lance.spark.extensions.LanceSparkSessionExtensions |
|spark.sql.catalog.lance.impl |Fixed value las2 |
|spark.sql.catalog.lance.storage.virtual_hosted_style_request |Fixed value true |
|spark.sql.catalog.lance.storage.enable_virtual_host_style |Fixed value true |
|spark.sql.catalog.lance.storage.transform_tos_to_s3 |Fixed value true |
|spark.sql.catalog.lance.storage.aws_region |The region where your TOS Bucket is located.<br><br>Currently, Lance uses the S3 protocol to access TOS, so the aws_region parameter is used here. |
|spark.sql.catalog.lance.storage.aws_endpoint |The service address of your TOS Bucket using the S3 protocol. |
|spark.sql.catalog.lance.storage.access_key_id |Your TOS AK |
|spark.sql.catalog.lance.storage.secret_access_key |Your TOS SK |


<span id="6b034c3d"></span>
### Create table

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In Serverless Spark, you can reference directly using the three\-part format <code>lance.{db_name}.{tbl_name}</code>. The parameters are as follows:</div>



* <div data-tips="true" data-tips-type="tip">db_name: The database name where the Lance table is stored.</div>


* <div data-tips="true" data-tips-type="tip">tbl_name: The table name where the Lance table is stored.</div>



Assume that there is a lance_db database under the hive catalog.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78077eb0ee4a457ba6915fb9ac08732a~tplv-goo7wpa0wc-image.image) </span>

In the [EMR Serverless console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/serverless/)  **\> Queue \> Job submission \> SparkSQL editor**, submit the following job:

```SQL
-- Configure required parameters

create table lance.lance_db.my_table (id int);
```


This operation will create a table named my_table in the lance_db database.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9372365a021240f588b538b2049f2078~tplv-goo7wpa0wc-image.image) </span>

<span id="2e0c380f"></span>
### Write data

In the [EMR Serverless console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/serverless/)  **\> Queue \> Job submission \> SparkSQL editor**, submit the following job:

```SQL
-- Configure required parameters

insert into lance.lance_db.my_table values(1);
```


<span id="3281a9d5"></span>
### Query data

In the [EMR Serverless console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/serverless/)  **\> Queue \> Job submission \> SparkSQL editor**, submit the following job:

```SQL
-- Configure required parameters

select * from lance.lance_db.my_table;
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5f39dabba7d4d26b8934fffa157d6ce~tplv-goo7wpa0wc-image.image) </span>

<span id="ffa89045"></span>
## Configuration template for other regions

If your configuration is in the East China region, you can use the following configuration template and replace cn\-beijing with cn\-shanghai. For example, the SQL template changes are as follows.

```SQL
--{} section should be completed according to your actual situation.

-- Fixed value
set tqs.query.engine.type = sparkcli;
set spark.sql.storeAssignmentPolicy = ANSI;

-- las catalog configuration
set spark.hadoop.hive.hms.client.is.public.cloud=true;
set spark.hadoop.hive.metastore.execute.setugi=false;
set spark.hadoop.hive.client.las.region.name=cn-shanghai;
set spark.hadoop.hive.client.las.ak={your ak};
set spark.hadoop.hive.client.las.sk={your sk};
set spark.hadoop.hive.metastore.uris=thrift://lakeformation.las.cn-shanghai.ivolces.com:48869;
set spark.hadoop.metastore.catalog.default={las_catalog_name};

-- lance configuration
set serverless.spark.lance.enabled=true;
set emr.serverless.spark.custom.parse.enabled = true;
set spark.sql.catalog.lance=com.lancedb.lance.spark.LanceNamespaceSparkCatalog;
set spark.sql.extensions=com.lancedb.lance.spark.extensions.LanceSparkSessionExtensions;
set spark.sql.catalog.lance.impl=las2;
set spark.sql.catalog.lance.storage.virtual_hosted_style_request=true;
set spark.sql.catalog.lance.storage.enable_virtual_host_style=true;
set spark.sql.catalog.lance.storage.transform_tos_to_s3=true;
set spark.sql.catalog.lance.storage.aws_region=cn-shanghai;
set spark.sql.catalog.lance.storage.aws_endpoint=https://{bucket}.tos-s3-cn-shanghai.ivolces.com;
set spark.sql.catalog.lance.storage.access_key_id={your ak};
set spark.sql.catalog.lance.storage.secret_access_key={your sk};
```
