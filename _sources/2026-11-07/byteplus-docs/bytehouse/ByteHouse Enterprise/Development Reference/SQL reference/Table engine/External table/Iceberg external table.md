---
title: "Iceberg external table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-iceberg-external-table"
---

Bytehouse Enterprise supports federated queries through Iceberg external tables. Users can directly query the data in Iceberg without importing the data. This provides flexibility and convenience in data processing.

<span id="52c20faf"></span>
# Background information

<span id="9fff06b4"></span>
## Cost description

The function of external tables is designed to handle data other than the internal tables in ByteHouse. By a simple DDL statement, an external table can be created on ByteHouse, linking ByteHouse tables with external data sources.


* External tables only incur computation costs on the ByteHouse side, following the ByteHouse compute resources billing rules.

* When using the external table function, the data of the external table **will not** be copied to ByteHouse and incur storage costs. For storage costs, please follow the billing rules on the storage side of external data sources.

* When using ByteHouse's external tables to access the external data source, the external data source may incur costs such as computation, access, and data transmission. The charge is based on the billing method of the external data source; please follow the relevant product's description.


<span id="4dfae6bd"></span>
## Iceberg data mapping method

For Iceberg tables, ByteHouse currently supports two methods for mapping data with Iceberg: **creating an external Iceberg table** and **creating an Iceberg database**.


|Data Mapping Method |Data Mapping Description |
|---|---|
|Create an Iceberg External Table |Establish a mapping from ByteHouse Table to Iceberg Table on the dimension of Table. Schema changes in the source table will not synchronize directly; if there are changes, delete the external table in ByteHouse and recreate one. |
|Create an Iceberg Database |On the Database dimension, establish a mapping from Bytehouse Database to Iceberg Database. After establishing the database mapping, there is no need to manually create a table mapping. It can automatically synchronize the table mapping under the database, and schema changes in the source table can be directly synchronized to ByteHouse. |


<span id="07a14ee6"></span>
# Usage restrictions


|Subitems |Limitations Description |
|---|---|
|Schema Evolution |Bytehouse supports querying tables that have Schema Evolution, but there are restrictions on the operation types on the source table’s schema:<br><br><br>* Supported source table actions: Add column, delete column, change column type, ByteHouse can query normally<br><br>* Unsupported actions: changing column names, ByteHouse query will result in an error |
|Time Travel |The current implementation hides the version information in the table name, which is `tbl$version$`. The current version does not support other types of version descriptors natively supported by iceberg, such as:<br><br><br>* Timestamp (String, for example: Dec 01 2024)<br><br>* snapshotId (Integer)<br><br>* Branch or tag name, which can be any string Content<br><br><br>**Using the current version descriptor supported by ByteHouse, can only be:** <br><br><br>* snapshotId (Integer)<br><br>* A string that meets the identifier naming rules |
|Automatically detect table structure changes |* Database method: can automatically detect table structure changes, as well as add and delete tables<br><br>* Table method: cannot automatically detect table structure changes and needs to delete and recreate the corresponding Table |


<span id="3d11706c"></span>
# Create external Iceberg table

When creating an external table, you need to specify the associated external table's database information. Currently, you can specify the column information of the external table, or obtain the corresponding column information automatically without specification.


* Specifying column information: All specified column names must exist in the corresponding Iceberg table and must be equivalent or compatible in type; otherwise, an error will be reported.

* Without specifying column information, automatically deducing the column information: The handling of types not found can be controlled by the `enable_schema_covert_fault_tolerance` parameter. When Iceberg's type cannot be found as a compatible type in Bytehouse, Value `1` means to ignore; `0` means an error will be reported; the default value is `1`.


Iceberg's data can be stored on different file systems, such as HDFS and S3. Here is a detailed introduction to the table creation statements on different file systems:

<span id="5b1a332e"></span>
## Iceberg on HDFS

<span id="1fba319a"></span>
### Manually specify column information

```SQL
CREATE TABLE `{tableName}` ON Cluster '{clusterName}' (
    `col_boolean` BOOLEAN,
    `col_integer` Int32,
    `col_long` Int64,
    `col_float` Float32,
    `col_double` Float64,
    `col_decimal` DECIMAL(10, 2),
    `col_date` DATE32,
    `col_timestamp` DateTime64(3),
    `col_uuid` UUID,
    `col_string` String,
    `col_fixed` FixedString(50),
    `col_binary` String,
    `col_list_integer` Array(Int32),
    `col_map` Map(String, Int32),
    `col_struct` Tuple(`field_integer` Int32, `field_string` String, `field_timestamp` DateTime64(3), `field_decimal` DECIMAL(28, 6), `field_binary` String)
) 
ENGINE = IcebergCluster('{clusterName}', 'hadoop', '{warehouse}', '{icebergDatabaseName}', '{icebergTableName}');
```



|Param |Configuration Description |
|---|---|
|Create Table Description |* Column names and types for Iceberg tables, see the **Column Type Mapping** section below for mapping rules.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Specify column names and types, as well as partition keys and other descriptions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Column names need to correspond one\-to\-one with the Iceberg table; the order of the columns does not need to match exactly.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When creating an external table, you can select only part of the columns from the Iceberg table, but all partition columns must be included.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The partitions of the external columns must be specified through the "partition by" statement and must be defined in the description list just like the normal columns.</div><br><br><br>* ClusterName: The cluster name of ByteHouse. |
|Engine Parameters |* ClusterName: The cluster name of ByteHouse.<br><br>* Hadoop: Fixed configuration as Hadoop.<br><br>* Warehouse: Configured as the address connected to Iceberg's data warehouse, for example: `hdfs://haruna/home/byte_flink_test/table_store/bytehouse_test`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This is where you enter the top\-level directory of Iceberg.</div><br><br><br><br>* IcebergDatabaseName: Specifies the database in Iceberg.<br><br>* IcebergTableName: Specifies the table in Iceberg. |


<span id="462588e1"></span>
### Automatically deduce column information

```SQL
CREATE TABLE `{tableName}` ON Cluster '{clusterName}'
ENGINE = IcebergCluster('{clusterName}', 'hadoop', '{warehouse}', '{icebergDatabaseName}', '{icebergTableName}')
SETTINGS enable_schema_covert_fault_tolerance = 1;
```



|Parameters |Configuration Description |
|---|---|
|Table Creation Description |* The column names and types in the Iceberg table, see the **column type mapping** section below for column type mapping rules.<br><br>* clusterName: The cluster name of ByteHouse. |
|Engine Parameters |* clusterName: The cluster name of ByteHouse.<br><br>* hadoop: Fixed configuration to hadoop.<br><br>* warehouse: Configured as the connection address of the Iceberg data warehouse, for example: `hdfs://haruna/home/byte_flink_test/table_store/bytehouse_test`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This is where you enter the top\-level directory of Iceberg.</div><br><br><br><br>* IcebergDatabaseName: Specifies the database in Iceberg.<br><br>* IcebergTableName: Specifies the table in Iceberg. |
|Settings (SETTINGS) |enable_schema_covert_fault_tolerance: Controls the handling method when automatic deduction of non\-existent types occurs.<br><br>When a type in Iceberg cannot find a compatible type in Bytehouse: `Value 1` means ignore; `Value 0` means report an error;<br><br><br>* The default value is `1`.<br><br>* When set to `0`, tables with type compatibility issues will not be displayed. |


<span id="7ea81c11"></span>
## Iceberg on S3（TOS）

<span id="88160a85"></span>
### Manually specify column information

```SQL
CREATE TABLE `{tableName}` ON Cluster '{clusterName}' (
    `col_boolean` BOOLEAN,
    `col_integer` Int32,
    `col_long` Int64,
    `col_float` Float32,
    `col_double` Float64,
    `col_decimal` DECIMAL(10, 2),
    `col_date` DATE32,
    `col_timestamp` DateTime64(3),
    `col_uuid` UUID,
    `col_string` String,
    `col_fixed` FixedString(50),
    `col_binary` String,
    `col_list_integer` Array(Int32),
    `col_map` Map(String, Int32),
    `col_struct` Tuple(`field_integer` Int32, `field_string` String, `field_timestamp` DateTime64(3), `field_decimal` DECIMAL(28, 6), `field_binary` String)
) 
ENGINE = IcebergCluster('{clusterName}', 'hadoop', '{warehouse}', '{icebergDatabaseName}', '{icebergTableName}')
SETTINGS region='{region}', 
endpoint='{endpoint}', 
ak_id='{accessKey}', 
ak_secret='{accessSecretKey}'; 
```



|Parameter |Configuration Description |
|---|---|
|Create Table Description |* Iceberg table column names and types, see the **column type mapping** section below for column type mapping rules.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When specifying column names and types, as well as partition keys and other descriptions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Column names need to correspond one\-to\-one with the Iceberg table; however, the order of the columns does not need to correspond.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When creating the external table, you can select only part of the columns from the Iceberg table, but all partition columns must be included.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The partitions of the external columns must be specified through the "partition by" statement and must be defined in the description list just like the normal columns.</div><br><br><br>* clusterName: The cluster name for ByteHouse. |
|Engine Parameters |* clusterName: The cluster name for ByteHouse.<br><br>* hadoop: Configured fixedly as hadoop.<br><br>* warehouse: Configured as the address connected to the Iceberg data warehouse, for example: `tos://test-dev-hcf/iceberg`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This is where you enter the top\-level directory of Iceberg.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the data storage filesystem for Iceberg is the BytePlus TOS, this can be configured to begin with <code>tos://</code> or <code>s3://</code> as the domain name.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, after copying, the storage path of the external data source is: <code>bhlasinfo/Iceberg</code>.</div><br><br><br><div data-tips="true" data-tips-type="warning">Then, the address to be configured after concatenation can be: <code>tos://bhlasinfo/Iceberg</code>, <code>s3://bhlasinfo/Iceberg</code>.</div><br><br><br><br>* IcebergDatabaseName: Specifies the database in Iceberg.<br><br>* IcebergTableName: Specifies the table in Iceberg. |
|Create MVT versions using Visual Editor |* Region: External data source service region, for example, `ap-southeast-1`.<br><br>* Endpoint: Connection address of the external data source, for example, `tos-s3-ap-southeast-1.bytepluses.com`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can go to the TOS console to view the corresponding S3 endpoint.</div><br><br><br><br>* ak_id/ak_secret, keys with S3 access permissions. |


<span id="9f5a2c04"></span>
### Automatically deduce column information

```SQL
CREATE TABLE `{tableName}` ON Cluster '{clusterName}'
ENGINE = IcebergCluster('{clusterName}', 'hadoop', '{warehouse}', '{icebergDatabaseName}', '{icebergTableName}')
SETTINGS enable_schema_covert_fault_tolerance = 1,
region='{region}', 
endpoint='{endpoint}', 
ak_id='{accessKey}', 
ak_secret='{accessSecretKey}'; 
```



|Param |Configuration description |
|---|---|
|Database description |* Customize external database name. ByteHouse will automatically infer and establish during table creation. See the **column type mapping** section below for column type mapping rules.<br><br>* Cluster Name: ByteHouse Cluster Name |
|Engine Parameters (Engine) |* Cluster Name: ByteHouse Cluster Name<br><br>* Hadoop: Fixed configuration as Hadoop<br><br>* Warehouse: The Connection address configured for the Iceberg data warehouse, such as `tos://test-dev-hcf/iceberg`<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This is filled with the top\-level directory of Iceberg.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If Iceberg's data storage file system is BytePlus TOS, this can be configured to start with <code>tos://</code> or <code>s3://</code> Domain Name.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, after copying the storage path of the external datasource will be: <code>bhlasinfo/Iceberg</code>.</div><br><br><br><div data-tips="true" data-tips-type="warning">Then, the address to be configured after concatenation can be: <code>tos://bhlasinfo/Iceberg</code>, <code>s3://bhlasinfo/Iceberg</code>.</div><br><br><br><br>* IcebergDatabaseName: Specifies the database within Iceberg |
|Set Parameters (SETTINGS) |* enable_schema_covert_fault_tolerance: Controls the handling method when automatic type derivation does not exist<br><br><br>When a compatible type for a type in Iceberg cannot be found in Bytehouse: select `1` to ignore; `0` to throw an error;<br><br><br>* The default value is `1`.<br><br>* When set to `0`, tables with type compatibility issues cannot be displayed.<br><br>* Region: External data source service area, for example, `ap-southeast-1`.<br><br>* Endpoint: Connection address of the external data source, for example, `tos-s3-ap-southeast-1.bytepluses.com`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can go to the TOS console to view the corresponding S3 endpoint.</div><br><br><br><br>* ak_id/ak_secret, the key with S3 access permission. |


<span id="0072484a"></span>
# Create an external Iceberg database

Create an external ByteHouse database and establish a mapping from Bytehouse Database to Iceberg Database at the Database dimension. After the database mapping is established, there is no need to manually create the table mapping, and the table mapping under the database can be synchronized automatically.

Iceberg data can be stored on various file systems, such as HDFS, S3. Below is a detailed description of the table creation statements on different file systems:

<span id="8daed85f"></span>
## Iceberg on HDFS

```SQL
CREATE DATABASE {databaseName} ON Cluster '{clusterName}'
engine = Iceberg('{clusterName}', 'hadoop', '{warehouse}', '{icebergDatabaseName}')
SETTINGS enable_schema_covert_fault_tolerance = 1;
```



|Parameter |Configuration description |
|---|---|
|Database description |* Customize the external database name.<br><br>* Cluster name: ByteHouse Cluster name. |
|Engine Parameters (Engine) |* Cluster name: ByteHouse Cluster name.<br><br>* Hadoop: Fixed Configuration as hadoop.<br><br>* Warehouse: Configuration for Iceberg Data Warehouse connection address, for example: `hdfs://haruna/home/byte_flink_test/table_store/bytehouse_test`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This is filled with the top\-level directory of Iceberg</div><br><br><br><br>* IcebergDatabaseName: Specifies the database in Iceberg. |
|Create MVT versions using Visual Editor |enable_schema_covert_fault_tolerance: Controls the handling method when automatic inference type does not exist.<br><br>When the type in Iceberg cannot be found in Bytehouse for compatible type: Value `1` means ignore; `0` means throw an error;<br><br><br>* The default value is `1`.<br><br>* When set to `0`, tables with type compatibility issues will not be displayed. |


<span id="ab63a098"></span>
## Iceberg on S3

```SQL
CREATE DATABASE {databaseName} ON Cluster '{clusterName}'
engine = Iceberg('{clusterName}', 'hadoop', '{warehouse}', '{icebergDatabaseName}')
SETTINGS enable_schema_covert_fault_tolerance = 1,
region='{region}', 
endpoint='{endpoint}', 
ak_id='{accessKey}', 
ak_secret='{accessSecretKey}'; 
```



|Parameter |Configuration Description |
|---|---|
|Database Description |* Customize external database name.<br><br>* clusterName: Cluster name for ByteHouse. |
|Engine Parameter |* clusterName: Cluster name for ByteHouse.<br><br>* Hadoop: Fixed configuration for Hadoop.<br><br>* Warehouse: Connection address for a data warehouse configured as Iceberg, for example: `tos://test-dev-hcf/iceberg`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This is filled with the top\-level directory of Iceberg.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If Iceberg's data storage file system is BytePlus TOS, this can be configured to start with <code>tos://</code> or <code>s3://</code> Domain Name.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, after copying, the storage path of the external data source becomes: <code>bhlasinfo/Iceberg</code>.</div><br><br><br><div data-tips="true" data-tips-type="warning">Then, the address to be configured after concatenation can be: <code>tos://bhlasinfo/Iceberg</code> or <code>s3://bhlasinfo/Iceberg</code>.</div><br><br><br><br>* IcebergDatabaseName: Specifies the database in Iceberg. |
|Create MVT Versions Using Visual Editor |* Enable_schema_convert_fault_tolerance: Controls how to handle types that do not exist when automatically inferring types.<br><br><br>When a type in Iceberg cannot be found as a compatible type in Bytehouse: `Value 1` means ignore; `Value 0` means report an error;<br><br><br>* Default value is `1`.<br><br>* When set to `0`, tables with type compatibility issues will not be displayed.<br><br>* Region: External data source service region, for example, `ap-southeast-1`.<br><br>* Endpoint: Connection address for external data sources, for instance, `tos-s3-ap-southeast-1.bytepluses.com`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can go to the TOS console to view the corresponding S3 endpoint.</div><br><br><br><br>* ak_id/ak_secrent, keys with S3 access permission. |


<span id="e18ee3f0"></span>
# Search external tables

The query operations for external tables are consistent with those for normal tables.


* General Method


```SQL
select * from  t where xxx;
   
```


<span id="655eadca"></span>
# Delete external database tables

The delete operations for external database tables are consistent with those for normal tables.


* Delete external database.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deleting an external database, all the external tables under the database will be deleted too, please proceed with caution.</div>


```SQL
DROP DATABASE example_db ON Cluster '{clusterName}';
   
```



* Delete external tables.


```SQL
DROP TABLE example_table ON Cluster '{clusterName}';
```


<span id="baa3fc91"></span>
# Snapshot search

```SQL
-- Specify snapshotId as 123456789
select * from tbl$version$123456789;

-- Specify branch name as branch_1
select * from tbl$version$branch_1;

-- Specify tag name as tag_1
select * from tbl$version$branch_1;
```


<span id="6d93e9a8"></span>
# Search the metadata of the table

Here is the metadata for all currently supported Iceberg tables:


* snapshots: Records all snapshot information of the dataset for tracking and restoring historical versions.

* refs: Contains references to snapshots (branches and tags), supporting parallel development and marking important versions.

* history: Records the change history of the dataset to help with auditing and data change backtracking.

* files: Provides information related to the data files in the actual physical storage of the dataset, facilitating data management and performance optimization.

* properties: Schema\-related configuration properties.


```SQL
select * from tbl$metadata$snapshots;
select * from tbl$metadata$refs;
select * from tbl$metadata$history;
select * from tbl$metadata$files;
select * from tbl$metadata$properties;
```


<span id="9efb9922"></span>
# Reference: Data type mapping


|Type: Iceberg |Type: Bytehouse |
|---|---|
|Boolean |UInt8 |
|Integer |Int32 |
|Long |Int64 |
|Float |Float32 |
|Double |Float64 |
|Date |Date32 |
|Time |Not supported |
|Timestamp |DateTime64 |
|String |String |
|UUID |UUID |
|Fixed |FixedString |
|Binary |String |
|Decimal |Deciaml |
|Struct |Tuple |
|List |Array |
|Map |Map |
