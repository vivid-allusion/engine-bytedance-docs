---
title: "Paimon external table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-paimon-external-table"
---

The Enterprise version of ByteHouse supports federated queries using external tables, allowing users to query data in Paimon through Paimon's external tables without data import. This provides flexibility and convenience in data processing.

<span id="c52a412d"></span>
# Background information

<span id="86246c7c"></span>
## Cost explanation

The functionality of external tables is designed to handle data other than that inside ByteHouse's internal tables. By a simple DDL statement, an external table can be created on ByteHouse, linking ByteHouse tables with external data sources.


* External tables on ByteHouse will only incur computation costs, following the ByteHouse computing resource billing rules.

* When using the external table feature, the data of the external table **will not** be duplicated and stored on ByteHouse, therefore no storage costs will be incurred. Please pay attention to the billing rules for storage on the external data source side for storage costs.

* When accessing external data sources using ByteHouse external tables, costs may be incurred by the external data source for computing, access, and data transfer. Specific charges are based on the billing method of the external data source; please check the relevant product documentation.


<span id="b4f83514"></span>
## Paimon data mapping method

For Paimon data tables, ByteHouse currently supports two methods to map data between ByteHouse and Paimon: **creating Paimon external tables** and **creating Paimon databases**.


|Data Mapping Methods |Data Mapping Description |
|---|---|
|Create Paimon External Table |Establish the mapping of ByteHouse tables to Paimon tables at the table dimension. Changes to the source table schema will not sync directly; if changes occur, the external table in ByteHouse must be deleted and recreated. |
|Create Paimon External Database |Establish the mapping from Bytehouse Database to Paimon Database at the Database dimension. After establishing the database mapping, there's no need to manually create table mappings; it can automatically sync mappings of tables under the database, detecting additions and deletions of Paimon tables, and changes to the source table schema can be directly synchronized to ByteHouse. |


<span id="afcb213b"></span>
# Usage restrictions


|Sub\-items |Limitations Description |
|---|---|
|Alter Operations |Currently, it is not possible to perform alter operations on Bytehouse external tables and Bytehouse DB, such as adding, deleting, or renaming columns; external table databases do not support `RENAME DATABASE`. |
|Write/Import Operations |Write/import operations are currently not supported. |
|Time Travel |The current implementation hides the version information in the table name, namely `tbl$version$`. Currently, it does not support multiple types of version descriptors natively supported by Paimon, such as:<br><br><br>* Timestamps (strings, e.g., 2024\-12\-01)<br><br>* snapshotId (integer)<br><br>* Branch or tag names, which can be any string content<br><br><br>**In ByteHouse, can only be:** <br><br><br>* snapshotId (integer)<br><br>* a string that complies with identifier naming rules |
|Auto\-detect table structure changes |* Database mode: Can auto\-detect table structure changes, and add or remove tables<br><br>* Table mode: Cannot auto\-detect table structure changes, requires deletion and re\-creation of the corresponding Table |
|Complex data types |Currently does not support Nullable for complex data types. |


<span id="6f1f7c78"></span>
# Create external tables

By creating external tables in ByteHouse, establish a mapping from ByteHouse tables to Paimon tables at the table dimension. Paimon’s data can be stored on different distributed storage systems, such as HDFS and S3. The following details the table creation statements on different distributed storage systems:

<span id="3fc430ff"></span>
## Paimon on HDFS

When creating an external table, you need to specify the associated external table's information. Currently, it supports specifying column information for the external table, or retrieving the corresponding column information through automatic inference without specifying it.


* Specifying column information: All specified column names must exist in the corresponding Paimon table, and their types must be equivalent or compatible, otherwise an error will occur.

* Not specifying column information, automatically inferring corresponding column information: This can be controlled through the `enable_schema_covert_fault_tolerance` parameter. When a compatible type cannot be found in Bytehouse for a type in Paimon, setting `1` means to ignore; `0` means to report an error; the default value is `1`.


<span id="baa64d96"></span>
### Manually specify column information

```SQL
CREATE TABLE `{tableName}` ON Cluster '{clusterName}' (
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
ENGINE = PaimonCluster('{clusterName}', 'filesystem:HDFS', '{warehouse}', '{paimonDatabaseName}', '{paimonTableName}');
```



|Parameters |Configuration description |
|---|---|
|Create Table Description |* Column names and types in the Paimon table, see the **Column Type Mapping** section below for column type mapping rules.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When specifying column names and types, along with partition key descriptions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Column names must correspond one\-to\-one with the Paimon table; the order of the columns need not correspond exactly.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When creating an external table, you can select only a part of the columns from the Paimon table, but all partition columns must be included.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The partition of external table columns must be specified using a partition by statement, and must be defined in the description list like normal columns.</div><br><br><br>* clusterName: The cluster name of ByteHouse. |
|Engine Parameters |* clusterName: The cluster name of ByteHouse.<br><br>* `filesystem:HDFS`: Fixed parameter.<br><br>* warehouse: Configured as the address connected to Paimon's data warehouse, for example: `hdfs://haruna/home/byte_flink_test/table_store/bytehouse_test`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Here, the top\-level directory of Paimon is filled in.</div><br><br><br><br>* paimonDatabaseName: Specifies the database within Paimon.<br><br>* paimonTableName: Specifies the table in Paimon. |


<span id="8a3778d9"></span>
### Automatically deduce column information

```SQL
CREATE TABLE `{tableName}` ON Cluster '{clusterName}'
ENGINE = PaimonCluster('{clusterName}', 'filesystem:HDFS', '{warehouse}', '{paimonDatabaseName}', '{paimonTableName}')
SETTINGS enable_schema_covert_fault_tolerance = 0;
```



|Param |Description |
|---|---|
|Create table description |* tableName: Column names and types in the Paimon table, as well as the Partition By key, will be automatically deduced and established during table creation. See the **column type mapping** section below for column type mapping rules.<br><br>* clusterName: ByteHouse cluster name. |
|Engine parameters (Engine) |* clusterName: ByteHouse cluster name.<br><br>* `filesystem:HDFS`: Fixed parameter.<br><br>* warehouse: Configured as the address for the data warehouse connection in Paimon, for example: `hdfs://haruna/home/byte_flink_test/table_store/bytehouse_test`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Here, the top\-level directory of Paimon is filled in.</div><br><br><br><br>* paimonDatabaseName: Specifies the database in Paimon.<br><br>* paimonTableName: Specifies the table in Paimon. |
|Create MVT versions using Visual Editor |enable_schema_covert_fault_tolerance: Controls the handling method when an inferred type does not exist.<br><br>When there is no compatible type found in ByteHouse for a type in Paimon: a value of `1` means ignore; `0` means report an error; the default value is `1`. |


<span id="26f5c18b"></span>
## Paimon on S3

<span id="bc86e743"></span>
### Manually specify column information

```SQL
CREATE TABLE `{tableName}` ON Cluster '{clusterName}'(
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
ENGINE = PaimonCluster('{clusterName}', 'filesystem:S3', '${warehouse}', '{paimonDatabaseName}', '{paimonTableName}')
SETTINGS region='{region}', 
endpoint='{endpoint}', 
ak_id='{accessKey}', 
ak_secret='{accessSecretKey}',
s3_extra_options='fs.s3a.connection.maximum=1000'; 
```



|Parameter |Description |
|---|---|
|Create Table Description |* Paimon will automatically deduce and establish column names, types, and partition by key during table creation. See the **Column Type Mapping** section below for column type mapping rules.<br><br>* clusterName: The cluster name of ByteHouse. |
|Engine Parameters |* clusterName: The cluster name of ByteHouse.<br><br>* `filesystem:S3`: Fixed parameter.<br><br>* warehouse: Configured as the connection address to Paimon's data warehouse, such as: `s3://test-dev-hcf/paimon`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This is the top\-level directory of Paimon.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If Paimon's data storage system is BytePlus TOS, the domain name here must also be configured to start with <code>s3://</code>.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, after copying, the storage path of the external data source is: <code>bhlasinfo/paimon</code>.</div><br><br><br><div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7048edaac9724478a9d1df6d4e7bc384~tplv-goo7wpa0wc-image.image" /></div><br><br><br><div data-tips="true" data-tips-type="warning">Then, the address to be configured after concatenation is: <code>s3://bhlasinfo/paimon</code>.</div><br><br><br><br>* paimonDatabaseName: Specifies the database in Paimon.<br><br>* paimonTableName: Specifies the table in Paimon. |
|Create MVT versions using Visual Editor |* Region: External data source Service Region, for example, `ap-southeast-1`.<br><br>* Endpoint: External data source Connection address, for example, `tos-s3-ap-southeast-1.bytepluses.com`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can go to the TOS console to view the corresponding S3 endpoint.</div><br><br><br><br>* ak_id/ak_secrent, keys with S3 access permissions. |
|Parameter setting |* s3_extra_options: Optional parameters for setting S3 tuning parameters, you can refer to the following format to set tuning parameters:<br><br><br>```SQL```<br>```s3_extra_options='s3.xxx=value1,s3.yyy=value2,s3.zzz=value3'```<br><br><br>`fs.s3a.connection.maximum` is a common tuning parameter (default value is 500), used to set the maximum size of the connection pool when establishing a connection with the S3 storage service; please refer to [Help Documentation](https://hadoop.apache.org/docs/stable/hadoop-aws/tools/hadoop-aws/performance.html) for all parameters. |


<span id="681ea84f"></span>
### Automatically deduce column information

```SQL
CREATE TABLE `{tableName}` ON Cluster '{clusterName}'
ENGINE = PaimonCluster('{clusterName}', 'filesystem:S3', '${warehouse}', '{paimonDatabaseName}', '{paimonTableName}')
SETTINGS region='{region}', 
endpoint='{endpoint}', 
ak_id='{accessKey}', 
ak_secret='{accessSecretKey}',
s3_extra_options='fs.s3a.connection.maximum=1000'， 
enable_schema_covert_fault_tolerance = 0;
```



|Parameter |Configuration Description |
|---|---|
|Create Table Description |* Customize Paimon's appearance name. ByteHouse will automatically infer and establish during table creation. See the **column type mapping** section below for column type mapping rules.<br><br>* clusterName: The cluster name of ByteHouse. |
|Engine Parameters (Engine) |* clusterName: The cluster name of ByteHouse.<br><br>* `filesystem:S3`: Fixed parameter.<br><br>* warehouse: Configured as the connection address of Paimon's data warehouse, for example: `s3://test-dev-hcf/paimon`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This is the top\-level directory of Paimon.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If Paimon's data storage system is BytePlus TOS, the domain name here must also be configured to start with <code>s3://</code>.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, after copying, the storage path of the external data source is: <code>bhlasinfo/paimon</code>.</div><br><br><br><div data-tips="true" data-tips-type="warning">Then, the address to be configured after concatenation is: <code>s3://bhlasinfo/paimon</code>.</div><br><br><br><br>* paimonDatabaseName: Designates the database in Paimon.<br><br>* paimonTableName: Designates the table in Paimon. |
|Create MVT versions using Visual Editor |* enable_schema_covert_fault_tolerance: Controls the handling method when an automatically inferred type is absent.<br><br><br>When a type in Paimon cannot be found in ByteHouse as a compatible type: Value `1` means to ignore; `0` means to throw an error; the default value is `1`.<br><br><br>* Region: The region of the external data source service, for example, `ap-southeast-1`.<br><br>* Endpoint: The connection address of the external data source, for example, `tos-s3-ap-southeast-1.bytepluses.com`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can go to the TOS console to view the corresponding S3 endpoint.</div><br><br><br><br>* ak_id/ak_secrent, the key with S3 access permission. |
|Parameter setting for S3 |* s3_extra_options: Optional parameters for tuning S3 settings. You can refer to the following format to set tuning parameters:<br><br><br>```SQL```<br>```s3_extra_options='s3.xxx=value1,s3.yyy=value2,s3.zzz=value3'```<br><br><br>`fs.s3a.connection.maximum` is a common tuning parameter (default value is 500) for setting the maximum size of the connection pool when establishing connections with the S3 storage service; refer to [Hadoop Help Documentation](https://hadoop.apache.org/docs/stable/hadoop-aws/tools/hadoop-aws/performance.html) for all parameters. |


<span id="013922a0"></span>
# Create external Paimon database

Create a mapping from Bytehouse Database to Paimon Database at the Database dimension by creating an external database in ByteHouse. After establishing the database mapping, there's no need to manually create table mappings, as they can automatically sync with the database tables.

Paimon's data can be stored on different distributed storage systems, such as HDFS and S3. Below are the statements for creating tables on different distributed storage systems:

<span id="b5911451"></span>
## Paimon on HDFS

```SQL
CREATE DATABASE {databaseName} ON Cluster '{clusterName}'
engine = Paimon('{clusterName}', 'filesystem:HDFS', '{warehouse}', '{paimonDatabaseName}')
SETTINGS enable_schema_covert_fault_tolerance = 1;
```



|Parameter |Configuration Description |
|---|---|
|Database Description |* Customize External Database Name.<br><br>* clusterName: ByteHouse's Cluster Name. |
|Engine Parameters |* clusterName: ByteHouse's Cluster Name.<br><br>* `filesystem:HDFS`: Fixed parameter.<br><br>* Warehouse: Configured as the address of the warehouse connection in Paimon, such as: `hdfs://haruna/home/byte_flink_test/table_store/bytehouse_test`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This is the top\-level directory for Paimon.</div><br><br><br><br>* PaimonDatabaseName: Specifies the database in Paimon. |
|Parameter settings |* Enable_schema_covert_fault_tolerance: Controls the handling of missing type auto\-inference.<br><br><br>When the type in Paimon cannot be found in ByteHouse, value `1` means ignore; `0` means report an error.<br><br><br>* Default value is `1`.<br><br>* When set to `0`, tables with compatibility issues will not be displayed. |


<span id="b2cc4fff"></span>
## Paimon on S3

```SQL
CREATE DATABASE {databaseName} ON Cluster '{clusterName}'
ENGINE = Paimon('{clusterName}', 'filesystem:S3', '{warehouse}', '{paimonDatabaseName}')
SETTINGS enable_schema_covert_fault_tolerance = 1,
region='{region}', 
endpoint='{endpoint}', 
ak_id='{accessKey}', 
ak_secret='{accessSecretKey}',
s3_extra_options='fs.s3a.connection.maximum=1000'; 
```



|Parameter |Configuration Explanation |
|---|---|
|Database Description |* Customize the name of external databases.<br><br>* clusterName: Cluster name of ByteHouse. |
|Engine Parameters |* clusterName: Cluster name of ByteHouse.<br><br>* `filesystem:S3`: Fixed parameter.<br><br>* warehouse: Configuration address connected to Paimon's data warehouse, example: `s3://test-dev-hcf/paimon`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This is the top\-level directory for Paimon.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If Paimon's data distribution storage system is the BytePlus TOS, this should also be configured to start with <code>s3://</code>.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, after copying the storage path of the external data source becomes: <code>bhlasinfo/paimon</code>.</div><br><br><br><div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7048edaac9724478a9d1df6d4e7bc384~tplv-goo7wpa0wc-image.image" /></div><br><br><br><div data-tips="true" data-tips-type="warning">Then, the address to be configured after concatenation is: <code>s3://bhlasinfo/paimon</code>.</div><br><br><br><br>* paimonDatabaseName: Specifies the database in Paimon. |
|Create MVT versions using Visual Editor |* enable_schema_covert_fault_tolerance: Controls the handling method when the automatically deduced type does not exist.<br><br><br>When the type in Paimon cannot find a compatible type in ByteHouse: `Value 1` means ignore; `Value 0` means report an error;<br><br><br>* The default value is `1`.<br><br>* When set to `0`, tables with type compatibility issues will not be displayed.<br><br>* Region: The region of the external data source service, for example, `ap-southeast-1`.<br><br>* Endpoint: Connection address of the external data source, for example, `tos-s3-ap-southeast-1.bytepluses.com`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can go to the TOS console to view the corresponding S3 endpoint.</div><br><br><br><br>* ak_id/ak_secret, keys with S3 access permission. |
|S3 Parameter Settings |s3_extra_options: Optional parameters used for S3 tuning settings, you can refer to the following format to set tuning parameters:<br><br>```SQL```<br>```s3_extra_options='s3.xxx=value1,s3.yyy=value2,s3.zzz=value3'```<br>``````<br><br><br>`fs.s3a.connection.maximum` is a common tuning parameter (default value of 500), used to set the maximum pool size when establishing connections with S3 storage services; for all parameters, please refer to [Hadoop Help Documentation](https://hadoop.apache.org/docs/stable/hadoop-aws/tools/hadoop-aws/performance.html). |


<span id="b76e2934"></span>
# Query external tables

The queries for external tables are consistent with those for regular tables.


* General method.


```SQL
select * from  t where xxx;
```


<span id="21e7328f"></span>
# Delete external databases and tables

The deletion operation of external tables is consistent with that of regular tables.


* Delete the external database.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deleting an external database, all external tables under it will also be deleted. Please be cautious when operating.</div>


```SQL
DROP DATABASE example_db ON Cluster '{clusterName}';
   
```



* Delete the external data table.


```SQL
DROP TABLE example_table ON Cluster '{clusterName}';
```


<span id="72df55d7"></span>
# Snapshot query

```SQL
-- Specify snapshotId=123456789
select * from tbl$version$123456789;

-- Specify branch name as branch_1
select * from tbl$version$branch_1;

-- Specify tag name as tag_1
select * from tbl$version$branch_1;
```


<span id="06bded58"></span>
# Query table metadata

The following are the metadata of all the Paimon tables currently supported for query:


* Manifests: Contains information about the data file manifests used to track the actual physical storage locations of the data.

* Snapshots: Provide snapshot\-level information, allowing users to view the state of data at different points in time.

* Options: Contains configuration options or parameters set during table creation.

* Schemas: Describe the structure of the dataset, including column names, data types, and other information.

* Partitions: If the data is stored in partitions, this table provides information about the partitions.

* Audit log: Records logs of operations performed on the data, available for audit purposes.

* Files: Contains information related to the actual stored data files.

* Tags: Marks specific important data states, facilitating quick location and rollback to specific versions.

* Branches: Provides information about branches, supporting parallel development or experimentation with different data set versions.

* Consumers: May involve information about data subscribers or users, especially in a streaming data processing environment.

* RO: Optimizes read performance.

* Aggregation fields: Information related to aggregation fields, which helps in understanding or manipulating summarized data.

* Statistics: Provides various statistics about the dataset, such as size, distribution, etc., which are very useful for optimizing query performance.


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


<span id="84a564a4"></span>
# Reference: Data type mapping

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can control the handling method when mapping data types are unsupported via the <code>enable_schema_covert_fault_tolerance</code> parameter. When types in Paimon cannot find compatible types in Bytehouse: Value <code>1</code> means ignore; <code>0</code> means report error; the default value is <code>1</code>.</div>



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
