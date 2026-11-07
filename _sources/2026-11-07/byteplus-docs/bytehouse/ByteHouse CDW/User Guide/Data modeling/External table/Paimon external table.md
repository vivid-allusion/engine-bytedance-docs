---
title: "Paimon external table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/paimon-external-table"
---

ByteHouse Cloud Data Warehouse Edition supports federated queries using the method of Paimon external tables, allowing users to directly query data in Paimon using Paimon external tables without needing data import. This provides flexibility and convenience in data handling.

<span id="a45bc946"></span>
# Background

<span id="988b34ba"></span>
## Billing

The function of external tables aims to provide processing capabilities for data other than the internal tables within ByteHouse. By a simple DDL statement, an external table can be created on ByteHouse, establishing a link between ByteHouse tables and the external data source.


* External tables only generate computation costs on the ByteHouse side, following the ByteHouse computing resources billing rules.

* I use the external table feature, the data in the external table is **not** copied to ByteHouse and does not incur storage fees. For storage fees, please refer to the billing rules on the storage side of the external data source.

* When using ByteHouse external tables to access an external data source, the external data source may incur costs such as computation, access, and data transfer. Please refer to the specific billing method of the external data source and follow the relevant product descriptions.


<span id="9f450b29"></span>
## Paimon data mapping methods

For Paimon Tables, ByteHouse currently supports two methods to map data between ByteHouse and Paimon: **creating Paimon external tables** and **creating Paimon databases**.


|Data Mapping Methods |Data Mapping Description |
|---|---|
|Create External Tables in Paimon |Create a mapping from ByteHouse tables to Paimon tables at the table dimension. Changes to the source table schema will not sync directly. If there are changes, it is necessary to delete the external table in ByteHouse and recreate it. |
|Create an external database in Paimon |Create a mapping from Bytehouse Database to Paimon Database at the Database dimension. After establishing the database mapping, there is no need to manually establish table mapping; it can automatically sync table mappings under the database, can sense the addition and deletion of Paimon tables, and source table schema changes can directly sync to ByteHouse. |


<span id="ded41070"></span>
# Usage restrictions


|Sub\-items |Restriction Description |
|---|---|
|Alter Actions |Currently, it is not possible to carry on Alter actions on Bytehouse External Datasources, Bytehouse DB, such as the external database does not support `Add Column`, Remove Column, or rename columns; External database does not support RENAME DATABASE. |
|Write/Import Actions |Write/Import actions are currently not supported. |
|Time Travel |The current implementation hides the version information in the table name, i.e., `tbl$version$`. Other types of Native\-supported Version descriptions are not currently supported by Paimon, such as:<br><br><br>* Timestamp (String, for example: 2024\-12\-01)<br><br>* snapshotId (Integer)<br><br>* Branch Name or Tag Name, which can be any string content<br><br><br>**At ByteHouse, can only be:** <br><br><br>* snapshotId (Integer)<br><br>* String that meets identifier naming rules |
|Automatically detects table structure changes |* Database method: Automatically detects table structure changes and adds or deletes tables<br><br>* Table method: Automatically detects table structure changes |
|Complex data types |Currently, complex data types are not supported as Nullable. |


<span id="ef55929e"></span>
# Create external tables

By creating ByteHouse external tables, establish a mapping from ByteHouse tables to Paimon tables on a table dimension. Paimon's data can be stored on different distributed storage systems, such as HDFS, S3. The following specifically introduces the table creation statements on different distributed storage systems:

<span id="92a4accd"></span>
## Paimon on HDFS

When creating an external table, you need to specify the associated external database table details, currently supporting either specified column information or automatic derivation of column information.


* Specified column information: All designated column names must exist in the corresponding Paimon table, and the types must be equivalent or compatible; otherwise, an error will occur.

* Automatic derivation of column information: This can be controlled through the parameter `enable_schema_covert_fault_tolerance`. When a type in Paimon cannot find a compatible type in Bytehouse, value `1` signifies ignore; `0` signifies error; the default value is `1`.


<span id="a982caa4"></span>
### Manually specifying column information

```SQL
CREATE TABLE `{tableName}` (
    `col_boolean` BOOLEAN,
    `col_tinyint` Int8,
    `col_smallint` Int16,
    `col_int` Int32,
    `col_bigint` Int64,
    `col_float` Float32,
    `col_double` Float64,
    `col_decimal` DECIMAL(10, 2),
    `col_date` DATE32,
    `col_time` DateTime,
    `col_timestamp` DateTime64(6),
    `col_char` FixedString(10),
    `col_varchar` String,
    `col_binary` FixedString(50),
    `col_varbinary` String,
    `col_array_int` Array(Int32),
    `col_map` Map(String, Int32),
    `col_struct` Tuple(`field_smallint` Int16, `field_varchar` String, `field_time` DateTime, `field_decimal` DECIMAL(28, 6), `field_varbinary` String)
) 
ENGINE = CnchPaimon('filesystem:HDFS', '{warehouse}', '{paimonDatabaseName}', '{paimonTableName}');
```



|Parameters |Configuration description |
|---|---|
|Create Table Description |Paimon table's column names and types are described in the **Column Type Mapping** section below.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When specifying column names and types, as well as partitions and other descriptions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Column names need to correspond one\-to\-one with the Paimon table; however, the order of columns does not need to correspond.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When creating an external table, the external table columns can select only part of the columns from the Paimon table, but all partition columns must be included.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The partitioning of external table columns needs to be specified by the "partition by" statement, and needs to be defined in the description list just like normal columns.</div><br> |
|Engine Parameters |* `filesystem:HDFS`: Fixed parameter.<br><br>* Warehouse: Configured as the address for Paimon's data warehouse connection, for example: `hdfs://haruna/home/byte_flink_test/table_store/bytehouse_test`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This is filled in with the top\-level directory of Paimon.</div><br><br><br><br>* paimonDatabaseName: Specifies the database in Paimon.<br><br>* paimonTableName: Specifies the table in Paimon. |


<span id="29cd3716"></span>
### Automatic derivation of column information

```SQL
CREATE TABLE `{tableName}`
ENGINE = CnchPaimon('filesystem:HDFS', '{warehouse}', '{paimonDatabaseName}', '{paimonTableName}')
SETTINGS enable_schema_covert_fault_tolerance = 0;
```



|Parameters |Configuration Description |
|---|---|
|Build table description |tableName: The name of the external table. The column names and types of the Paimon table, as well as the `Partition By` key, will be automatically inferred and established when creating the table. See the "Column Type Mapping" section below for the column type mapping rules. |
|Engine Parameters |* Fixed parameter in `filesystem:HDFS`.<br><br>* Warehouse: Configured as Paimon's data warehouse connection address, for example: `hdfs://haruna/home/byte_flink_test/table_store/bytehouse_test`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This is filled in with the top\-level directory of Paimon.</div><br><br><br><br>* Database name in Paimon: Specifies the database within Paimon.<br><br>* paimonTableName: Specifies the table in Paimon. |
|Settings (SETTINGS) |enable_schema_covert_fault_tolerance: Controls the handling method when type inference does not exist.<br><br>When types in Paimon cannot find compatible types in ByteHouse: taking `1` means ignore; `0` means error; the default value is `1`. |


<span id="7413d82c"></span>
## Paimon on S3

<span id="2a7bc448"></span>
### Manually specifying column information

```SQL
CREATE TABLE `{tableName}` (
    `col_boolean` BOOLEAN,
    `col_tinyint` Int8,
    `col_smallint` Int16,
    `col_int` Int32,
    `col_bigint` Int64,
    `col_float` Float32,
    `col_double` Float64,
    `col_decimal` DECIMAL(10, 2),
    `col_date` DATE32,
    `col_time` DateTime,
    `col_timestamp` DateTime64(6),
    `col_char` FixedString(10),
    `col_varchar` String,
    `col_binary` FixedString(50),
    `col_varbinary` String,
    `col_array_int` Array(Int32),
    `col_map` Map(String, Int32),
    `col_struct` Tuple(`field_smallint` Int16, `field_varchar` String, `field_time` DateTime, `field_decimal` DECIMAL(28, 6), `field_varbinary` String)
)
ENGINE = CnchPaimon('filesystem:S3', '${warehouse}', '{paimonDatabaseName}', '{paimonTableName}')
SETTINGS region='{region}', 
endpoint='{endpoint}', 
ak_id='{accessKey}', 
ak_secret='{accessSecretKey}'，
s3_extra_options='fs.s3a.connection.maximum=1000';
```



|Parameter |Configuration Description |
|---|---|
|Table Description |Column names and types in Paimon tables, see the **Column Type Mapping** section below for column type mapping rules. |
|Engine Parameters (Engine) |* Fixed parameter: `filesystem:S3`.<br><br>* Warehouse: The address connected to the Paimon data warehouse, for example: `s3://test-dev-hcf/paimon`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This is filled in with the top\-level directory of Paimon.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If Paimon's data storage system is BytePlus TOS, it should also be configured here with a domain name beginning with <code>s3://</code>.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, after copying the storage path of the external data source, it becomes: <code>bhlasinfo/paimon</code>.</div><br><br><br><div data-tips="true" data-tips-type="warning">Then, the address to be configured after splicing is: <code>s3://bhlasinfo/paimon</code>.</div><br><br><br><br>* paimonDatabaseName: Specifies the database in Paimon.<br><br>* paimonTableName: Specifies the table in Paimon. |
|Settings (SETTINGS) |* Region: The region of the external data source service. You can fill it in according to your available zone. For example, if you are using BytePlus services, please refer to the [region list](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint) for filling examples.<br><br>* Endpoint: The connection address of the external data source. For example, if you are using BytePlus Object Storage Service (TOS), you can log in to the TOS console, go to **Buckets** \> **Bucket Name** \> **Overview** \> **Access Domain** path to view the required Endpoint.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d89d9b0888d847c29e08e08ff129faf6~tplv-goo7wpa0wc-image.image) </span><br><br>* ak_id/ak_secret, keys with S3 access permission. |
|S3 parameter settings |* s3_extra_options: Optional parameters for S3 tuning settings, which can be configured following the Format below:<br><br><br>```SQL```<br>```s3_extra_options='s3.xxx=value1,s3.yyy=value2,s3.zzz=value3'```<br><br><br>`fs.s3a.connection.maximum` is a common tuning parameter (Default Value is 500) for setting the Max size of the connection pool when establishing a connection with the S3 Service. For all parameters, refer to [Help Documentation of Hadoop](https://hadoop.apache.org/docs/stable/hadoop-aws/tools/hadoop-aws/performance.html). |


<span id="b22413dd"></span>
### Automatic derivation of column information

```SQL
CREATE TABLE `{tableName}`
ENGINE = CnchPaimon('filesystem:S3', '${warehouse}', '{paimonDatabaseName}', '{paimonTableName}')
SETTINGS region='{region}', 
endpoint='{endpoint}', 
ak_id='{accessKey}', 
ak_secret='{accessSecretKey}',
s3_extra_options='fs.s3a.connection.maximum=1000'，
enable_schema_covert_fault_tolerance = 0;
```



|Parameter |Configuration Description |
|---|---|
|Create Table Description |Customize Paimon External Table Name. Column names and Types, as well as Partition By Key, will be automatically deduced and established during table creation. See the section on **Column Type Mapping** Rules below for column type mapping rules. |
|Engine Parameters (Engine) |* `filesystem:S3`: Fixed parameter.<br><br>* Warehouse: Configured as the address connected to Paimon warehouse, for example: `s3://test-dev-hcf/paimon`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This is the top\-level directory of Paimon.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If Paimon's data is stored in the BytePlus TOS distributed storage system, this should also be configured with a Domain Name starting with <code>s3://</code>.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, after copying the storage path of the external data source, it becomes: <code>bhlasinfo/paimon</code>.</div><br><br><br><div data-tips="true" data-tips-type="warning">Then, the address to be configured after splicing is: <code>s3://bhlasinfo/paimon</code>.</div><br><br><br><br>* paimonDatabaseName: Specifies the database in Paimon.<br><br>* paimonTableName: Specifies the table in Paimon. |
|Parameter Setting |* enable_schema_covert_fault_tolerance: Controls the handling method when the automatically inferred type does not exist.<br><br><br>When types in Paimon cannot find a compatible type in ByteHouse: Value `1` means to ignore; `0` means to report an error; the default value is `1`.<br><br><br>* Region: The region of the external data source service. You can fill it in according to your available zone. For example, if you are using BytePlus services, please refer to the [region list](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint) for filling examples.<br><br>* Endpoint: The connection address of the external data source. For example, if you are using BytePlus Object Storage Service (TOS), you can log in to the TOS console, go to **Buckets** \> **Bucket Name** \> **Overview** \> **Access Domain** path to view the required Endpoint.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d89d9b0888d847c29e08e08ff129faf6~tplv-goo7wpa0wc-image.image) </span><br><br>* ak_id/ak_secrent, a key with S3 access permissions. |
|S3 parameter settings |* s3_extra_options: Optional parameters for setting S3 tuning parameters, which can be set in the following format:<br><br><br>```SQL```<br>```s3_extra_options='s3.xxx=value1,s3.yyy=value2,s3.zzz=value3'```<br><br><br>`fs.s3a.connection.maximum` is a common tuning parameter (default value is 500) used to set the maximum size of the connection pool when establishing connections with the S3 storage service; for all parameters, refer to [Hadoop Help Documentation](https://hadoop.apache.org/docs/stable/hadoop-aws/tools/hadoop-aws/performance.html). |


<span id="118b710e"></span>
# Creating Paimon external database

Create a mapping from Bytehouse Database to Paimon Database in the Database dimension by creating an external ByteHouse database. After establishing the database mapping, there is no need to manually create table mappings, as table mappings under the database can synchronize automatically.

Paimon's data can be stored on different distributed storage systems, such as HDFS and S3. Below is a detailed introduction to the statements for creating tables on different distributed storage systems:

<span id="442581c9"></span>
## Paimon on HDFS

```SQL
CREATE DATABASE {databaseName}
engine = Paimon('filesystem:HDFS', '{warehouse}', '{paimonDatabaseName}')
SETTINGS enable_schema_covert_fault_tolerance = 1;
```



|Parameter |Configuration description |
|---|---|
|Database description |Customize external database name. |
|Engine parameters (Engine) |* `filesystem:HDFS`: Fixed parameter.<br><br>* Warehouse: The address configured for the warehouse connection in Paimon, such as: `hdfs://haruna/home/byte_flink_test/table_store/bytehouse_test`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This is the top\-level directory of Paimon.</div><br><br><br><br>* paimonDatabaseName: Specifies the database in Paimon. |
|Parameter Settings |* enable_schema_convert_fault_tolerance: Controls the handling method when an inferable type is not found.<br><br><br>When a type in Paimon cannot find a compatible type in ByteHouse: Value `1` means ignore; `0` means error.<br><br><br>* The default value is `1`.<br><br>* When set to `0`, tables with type compatibility issues will not be displayed. |


<span id="3adecbdf"></span>
## Paimon on S3

```SQL
CREATE DATABASE {databaseName}
ENGINE = Paimon('filesystem:S3', '{warehouse}', '{paimonDatabaseName}')
SETTINGS enable_schema_covert_fault_tolerance = 1,
region='{region}', 
endpoint='{endpoint}', 
ak_id='{accessKey}', 
ak_secret='{accessSecretKey}',
s3_extra_options='fs.s3a.connection.maximum=1000'; 
```



|Parameter |Configuration Description |
|---|---|
|Database Description |Customize External Database Name. |
|Engine Parameters (Engine) |* `filesystem:S3`: Fixed Parameter.<br><br>* warehouse: Configured as the connection address for the Paimon warehouse, for example: `s3://test-dev-hcf/paimon`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This is the top\-level directory of Paimon.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If Paimon's data distribution system were BytePlus TOS, here it should also be configured with a domain name starting with <code>s3://</code>.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For instance, after copying, the storage path of the external data source becomes: <code>bhlasinfo/paimon</code>.</div><br><br><br><div data-tips="true" data-tips-type="warning">Then, the address to be configured after concatenation is: <code>s3://bhlasinfo/paimon</code>.</div><br><br><br><br>* paimonDatabaseName: Specifies the database in Paimon. |
|Create MVT versions using Visual Editor |* enable_schema_covert_fault_tolerance: Controls how to handle the absence of an automatically derived type.<br><br><br>When a compatible type cannot be found in ByteHouse for types in Paimon: Value `1` means ignore; `0` means report an error.<br><br><br>* The default value is `1`.<br><br>* When set to `0`, tables with type compatibility issues will not be displayed.<br><br>* Region: The region of the external data source service. You can fill it in according to your available zone. For example, if you are using BytePlus services, please refer to the [region list](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint) for filling examples.<br><br>* Endpoint: The connection address of the external data source. For example, if you are using BytePlus Object Storage Service (TOS), you can log in to the TOS console, go to **Buckets** \> **Bucket Name** \> **Overview** \> **Access Domain** path to view the required Endpoint.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d89d9b0888d847c29e08e08ff129faf6~tplv-goo7wpa0wc-image.image) </span><br><br>* ak_id/ak_secret, keys with S3 access permissions. |
|S3 parameter setting |s3_extra_options: Optional parameters for S3 tuning, you can refer to the following format for setting tuning parameters:<br><br>```SQL```<br>```s3_extra_options='s3.xxx=value1,s3.yyy=value2,s3.zzz=value3'```<br><br><br>`fs.s3a.connection.maximum` is a common tuning parameter (default value is 500), used to set the maximum size of the connection pool when establishing a connection with the S3 storage service; for all parameters, refer to [Hadoop Help Documentation](https://hadoop.apache.org/docs/stable/hadoop-aws/tools/hadoop-aws/performance.html). |


<span id="a5af6bd9"></span>
# Search external tables

The query of external tables is consistent with the query operations of normal tables.


* General method.

   ```SQL
   select * from  t where xxx;
   ```
   


<span id="fe171fd4"></span>
# Delete external library tables

Deleting operations of external tables are consistent with normal table deletion actions.


* Delete the external database.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After deleting the external database, all external tables under the external database will also be deleted, please proceed with caution.   </div>
   

   ```SQL
   DROP DATABASE example_db
   ```
   

* Delete the external table.

   ```SQL
   DROP TABLE example_table
   ```
   


<span id="af66303c"></span>
# Snapshot Search

```SQL
-- Specify snapshotId=123456789
select * from tbl$version$123456789;

-- Specify branch name=branch_1
select * from tbl$version$branch_1;

-- Specify tag name=tag_1
select * from tbl$version$branch_1;
```


<span id="13917d0d"></span>
# Query the meta information of the table

Below are the meta information of all current Paimon tables supported for searching:


* manifests: contains information about the data file manifests, used to track the actual physical location of stored data.

* snapshots: provides snapshot\-level information, allowing users to view the state of data at different time points.

* options: contains configuration options or parameter settings used during table creation.

* schemas: describes the structure of the dataset, including column names, data types, and other information.

* Partitions: If the data is partitioned, this table provides information about the partitions.

* Audit Log: Records actions performed on the data, useful for auditing purposes.

* Files: Contains information about the actual stored data files.

* Tags: Marks specific significant data states for quick location and rollback to specific versions.

* Branches: Provides branch information to support parallel development or experimenting with different data set versions.

* Consumers: May involve information about data subscribers or users, especially in a streaming data processing environment.

* RO: Optimizes read performance.

* Aggregation Fields: Information related to aggregate fields, helpful for understanding or managing summary data.

* Statistics: Provides various statistics about the data set, such as size and distribution, which are very useful for optimizing query performance.


```SQL
select * from tbl$metadata$manifests;
select * from tbl$metadata$snapshots;
select * from tbl$metadata$options;
select * from tbl$metadata$schemas;
select * from tbl$metadata$partitions;
select * from tbl$metadata$audit_log;
select * from tbl$metadata$files;
select * from tbl$metadata$tags;
select * from tbl$metadata$branches;
select * from tbl$metadata$consumers;
select * from tbl$metadata$ro;
select * from tbl$metadata$aggregation_fields;
select * from tbl$metadata$statistics;
```


<span id="82995c4c"></span>
# Reference: Data type mapping

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can control the process when the data type of the mapped data is not supported by using the <code>enable_schema_covert_fault_tolerance</code> parameter. When the type in Paimon cannot find a compatible type in Bytehouse: value <code>1</code> means ignore; <code>0</code> means report error; the default is <code>1</code>.</div>



|Paimon Type |ByteHouse Type |
|---|---|
|Boolean |UInt8 |
|TinyInt |Int8 |
|SmallInt |Int16 |
|Int |Int32 |
|BigInt |Int64 |
|Float |Float32 |
|Double |Float64 |
|Date |Date32 |
|Time |Not supported |
|Timestamp Wihtout TZ |DateTime64(UTC) |
|Timestamp With Local TZ |DateTime64(local time zone) |
|Char |FixedString |
|Varchar |String |
|Binary |FixedString |
|VarBinary |String |
|Decimal |Deciaml |
|Array |Array |
|Map |Map |
|Row |Tuple |
