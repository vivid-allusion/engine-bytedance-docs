---
title: "Iceberg external table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/iceberg-external-table"
---

Bytehouse Cloud Warehouse Edition supports federated queries using external tables, enabling users to query data directly in Iceberg without data import. This provides flexibility and convenience in data processing.

<span id="52c20faf"></span>
# Background

<span id="9fff06b4"></span>
## Billing

The function of external tables is designed to process other data besides the internal tables of ByteHouse. A simple DDL statement can create an external table on ByteHouse, establishing a connection between ByteHouse tables and external data sources.


* External tables on the ByteHouse side will only incur computation costs, following the ByteHouse compute resource billing rules.

* When using the external table feature, the data **will not** be duplicated on ByteHouse and incur storage costs. Please pay attention to the billing rules on the storage side of external data sources for storage costs.

* When using ByteHouse external tables to access external data sources, computational, access, and data transmission costs may occur, which are subject to the billing method of the external data sources. Please refer to the respective product descriptions.


<span id="4dfae6bd"></span>
## Iceberg data mapping method

For Iceberg data tables, ByteHouse currently supports two methods to implement data mapping with Iceberg: **creating Iceberg external tables** and **creating Iceberg databases**.


|Data Mapping Method |Data Mapping Description |
|---|---|
|Create an Iceberg External Table |Establish a mapping from ByteHouse table to Iceberg table at the table dimension. Source table schema changes will not sync directly; if changes occur, it's necessary to delete the external table in ByteHouse and recreate it. |
|Create Iceberg Database |Establish a mapping from Bytehouse Database to Iceberg Database at the Database dimension. After establishing the database mapping, there's no need to manually establish table mappings; it can automatically sync the table mappings under the database, and source table schema changes can directly sync to ByteHouse. |


<span id="07a14ee6"></span>
# Usage Restrictions


|Subitems |Limitation Explanation |
|---|---|
|Schema Evolution |Bytehouse supports querying tables with Schema Evolution, but there are restrictions on the type of schema operations on the source table:<br><br><br>* Supported source table operations include adding columns, deleting columns, and modifying column types, allowing ByteHouse to query normally<br><br>* Unsupported operations include modifying column names, as ByteHouse queries will result in errors |
|Time Travel |The current implementation hides the version information in the table name, i.e., `tbl$version$`. Currently, it does not support other types of version descriptors natively supported by Iceberg, such as:<br><br><br>* Timestamp (string, e.g., 2024\-12\-01)<br><br>* snapshotId (integer)<br><br>* Branch name or tag name, which can be any string content<br><br><br>**When adopting the version descriptor currently supported by ByteHouse, can only be:** <br><br><br>* snapshotId (integer)<br><br>* A string that conforms to the identifier naming rules |
|Autodetect table structure changes |* Database mode: Autodetects table structure changes and additions or deletions of tables<br><br>* Table mode: Autodetects table structure changes |


<span id="3d11706c"></span>
# Create Iceberg external table

When creating an external table, you need to specify the associated external table database information. Currently, it supports specifying the columns of the external table or obtaining corresponding column information through automatic inference if not specified.


* Specifying column information: All specified column names must exist in the corresponding Iceberg table and must be equivalent or compatible in type; otherwise, an error will occur.

* If column information is not specified, automatic inference of corresponding column information: You can control the handling method for non\-existing types through the `enable_schema_covert_fault_tolerance` parameter. When a type in Iceberg cannot find a compatible type in Bytehouse: a value of `1` means ignore; `0` means an error; the default value is `1`.


Iceberg data can be stored on different file systems, such as HDFS, S3. Detailed introduction of table creation statements on different file systems:

<span id="5b1a332e"></span>
## Iceberg on HDFS

<span id="1fba319a"></span>
### Manually specify column information

```SQL
CREATE TABLE `{tableName}` (
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
ENGINE = CnchIceberg('hadoop', '{warehouse}', '{icebergDatabaseName}', '{icebergTableName}');
```



|Parameters |Configuration description |
|---|---|
|Create table description |Column names and types for Iceberg tables; see the **column type mapping** section below for the mapping rules.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When specifying column names and types, as well as descriptions of partition keys:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Column names must correspond one\-to\-one with the Iceberg table; the order of the columns doesn't need to match exactly.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When creating an external table, you can select only part of the columns from the Iceberg table, but all partition columns must be included.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The partition of external table columns must be specified by the partition by statement, and like normal columns, defined in the description list.</div><br> |
|Engine Parameters (Engine) |* Hadoop: fixed configuration for Hadoop.<br><br>* Warehouse: Configured as the address connected to Iceberg's data warehouse, for example: `hdfs://haruna/home/byte_flink_test/table_store/bytehouse_test`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Here, fill in the top directory of Iceberg.</div><br><br><br><br>* IcebergDatabaseName: Specifies the database in Iceberg.<br><br>* IcebergTableName: Specifies the table in Iceberg. |


<span id="462588e1"></span>
### Automatically deduce column information

```SQL
CREATE TABLE `{tableName}`
ENGINE = CnchIceberg('hadoop', '{warehouse}', '{icebergDatabaseName}', '{icebergTableName}')
SETTINGS enable_schema_covert_fault_tolerance = 1;
```



|Parameters |Configuration Explanation |
|---|---|
|Table Creation Description |The column names and types in the Iceberg table, as well as the Partition By key, will be automatically deduced and established during table creation. See the section on **column type mapping** rules below. |
|Engine parameters (Engine) |* Hadoop: Configured as hadoop.<br><br>* Warehouse: Configured as the address connected to Iceberg's data warehouse, for example: `hdfs://haruna/home/byte_flink_test/table_store/bytehouse_test`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This space is for filling in the top\-level directory of Iceberg.</div><br><br><br><br>* IcebergDatabaseName: Specifies the database in Iceberg.<br><br>* IcebergTableName: Specifies the table in Iceberg. |
|Settings Parameters (SETTINGS) |enable_schema_convert_fault_tolerance: Controls the handling method when the automatically deduced type does not exist.<br><br>When a type in Iceberg cannot find a compatible type in Bytehouse, a value of `1` means to ignore; `0` means to report an error.<br><br><br>* The default value is `1`.<br><br>* When set to `0`, tables with type compatibility issues cannot be displayed. |


<span id="7ea81c11"></span>
## Iceberg on S3（TOS）

<span id="88160a85"></span>
### Manually specify column information

```SQL
CREATE TABLE `{tableName}` (
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
ENGINE = CnchIceberg('hadoop', '{warehouse}', '{icebergDatabaseName}', '{icebergTableName}')
SETTINGS region='{region}', 
endpoint='{endpoint}', 
ak_id='{accessKey}', 
ak_secret='{accessSecretKey}',
```



|Parameter |Configuration Description |
|---|---|
|Table Creation Description |Column names and types for Iceberg tables, see the 'Column Type Mapping' section below for type mapping rules.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Specify column names and types, as well as descriptions of partition keys and others:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Column names must correspond one\-to\-one with the Iceberg table; the order of columns does not need to correspond.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When creating an external table, you can select only part of the columns from the Iceberg table, but all partition columns must be included.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The partition of the external table columns must be specified through the partition by statement and must be defined in the description list just like the normal columns.</div><br> |
|Engine Parameters |* hadoop: Permanently configured as hadoop.<br><br>* Warehouse: The address for the warehouse connection configured for Iceberg, such as: `tos://test-dev-hcf/iceberg`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This space is for filling in the top\-level directory of Iceberg.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If BytePlus TOS is the data storage file system for Iceberg, here it can be configured to start with <code>tos://</code> or <code>s3://</code> domain name.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, after copying, the storage path of the external data source becomes: <code>bhlasinfo/Iceberg</code>.</div><br><br><br><div data-tips="true" data-tips-type="warning">Then, the address to be configured can be: <code>tos://bhlasinfo/Iceberg</code> or <code>s3://bhlasinfo/Iceberg</code>.</div><br><br><br><br>* IcebergDatabaseName: Specifies the database in Iceberg.<br><br>* IcebergTableName: Specifies the table in Iceberg. |
|Set Parameters (SETTINGS) |* Region: The region of the external data source service. You can fill it in according to your available zone. For example, if you are using BytePlus services, please refer to the [region list](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint) for filling examples.<br><br>* Endpoint: The connection address of the external data source. For example, if you are using BytePlus Object Storage Service (TOS), you can log in to the TOS console, go to **Buckets** \> **Bucket Name** \> **Overview** \> **Access Domain** path to view the required Endpoint.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d89d9b0888d847c29e08e08ff129faf6~tplv-goo7wpa0wc-image.image) </span><br><br>* Ak_id/ak_secret: Keys with S3 access rights. |


<span id="9f5a2c04"></span>
### Automatically deduce column information

```SQL
CREATE TABLE `{tableName}` 
ENGINE = CnchIceberg('hadoop', '{warehouse}', '{icebergDatabaseName}', '{icebergTableName}')
SETTINGS region='{region}', 
endpoint='{endpoint}', 
ak_id='{accessKey}', 
ak_secret='{accessSecretKey}',
enable_schema_covert_fault_tolerance = 1;
```



|Parameters |Configuration Instructions |
|---|---|
|Create Table Description |Custom External Table Name. Column names and types for Iceberg tables, as well as the Partition By key, will be automatically inferred and established during table creation. See the **Column Type Mapping** section below for the rules on column type mapping. |
|Engine Parameters (Engine) |* Hadoop: Configuration is set to hadoop.<br><br>* Warehouse: Configured as the address connected to Iceberg’s data warehouse, such as `tos://test-dev-hcf/iceberg`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This section specifies the top\-level directory for Iceberg.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If Iceberg's data storage file system is BytePlus TOS, this section can be configured with a domain name starting with <code>tos://</code> or <code>s3://</code>.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, after copying, the storage path of the external data source becomes: <code>bhlasinfo/Iceberg</code>.</div><br><br><br><div data-tips="true" data-tips-type="warning">Then, the address to be configured could be: <code>tos://bhlasinfo/Iceberg</code>, <code>s3://bhlasinfo/Iceberg</code>.</div><br><br><br><br>* IcebergDatabaseName: Specifies the database in Iceberg. |
|Setting Parameters (SETTINGS) |* enable_schema_covert_fault_tolerance: Controls the handling method when the automatic derivation type does not exist.<br><br><br>When a type in Iceberg cannot be found compatible in Bytehouse: the value `1` means ignore; `0` means report an error;<br><br><br>* The default value is `1`.<br><br>* When set to `0`, tables with compatibility issues will not be displayed.<br><br>* Region: The region of the external data source service. You can fill it in according to your available zone. For example, if you are using BytePlus services, please refer to the [region list](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint) for filling examples.<br><br>* Endpoint: The connection address of the external data source. For example, if you are using BytePlus Object Storage Service (TOS), you can log in to the TOS console, go to **Buckets** \> **Bucket Name** \> **Overview** \> **Access Domain** path to view the required Endpoint.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d89d9b0888d847c29e08e08ff129faf6~tplv-goo7wpa0wc-image.image) </span><br><br>* ak_id/ak_secret, keys with S3 access rights. |


<span id="0072484a"></span>
# Create an external Iceberg database

By creating an external ByteHouse database, establish a mapping from Bytehouse Database to Iceberg Database at the Database dimension. After establishing the library mapping, there is no need to manually create table mappings, as table mappings under the database can be synchronized automatically.

Iceberg data can be stored on different file systems such as HDFS, S3. Next, the table creation statements on different file systems are detailed:

<span id="8daed85f"></span>
## Iceberg on HDFS

```SQL
CREATE DATABASE test_iceberg_db_hdfs
engine = Iceberg('hadoop', '{warehouse}', '{icebergDatabaseName}')
SETTINGS enable_schema_covert_fault_tolerance = 1;
```



|Parameter |Configuration description |
|---|---|
|Database Description |Customize the external database name. |
|Engine Parameters |* Hadoop: Permanently configured as Hadoop.<br><br>* Warehouse: Configured to the address connecting the Iceberg data warehouse, for instance, `hdfs://haruna/home/byte_flink_test/table_store/bytehouse_test`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This section specifies the top\-level directory for Iceberg.</div><br><br><br><br>* Iceberg Database Name: Specifies the database in Iceberg. |
|Settings |enable_schema_covert_fault_tolerance: Controls the handling method when auto\-inferred types are not present.<br><br>When types in Iceberg cannot be found as compatible types in Bytehouse: Selecting `1` means ignore; `0` means report an error.<br><br><br>* The default value is `1`.<br><br>* When set to `0`, tables with type compatibility issues will not be displayed. |


<span id="ab63a098"></span>
## Iceberg on S3

```SQL
CREATE DATABASE {databaseName}
engine = Iceberg('hadoop', '{warehouse}', '{icebergDatabaseName}')
SETTINGS region='{region}', 
endpoint='{endpoint}', 
ak_id='{accessKey}', 
ak_secret='{accessSecretKey}',
SETTINGS enable_schema_covert_fault_tolerance = 1; 
```



|Parameter |Configuration Details |
|---|---|
|Database Description |Customize the external database name. |
|Engine Parameters |* hadoop: Permanently configured as hadoop.<br><br>* warehouse: Configure as the address for the Iceberg data warehouse connection, for example: `tos://test-dev-hcf/iceberg`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This section specifies the top\-level directory for Iceberg.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If Iceberg's data storage file system is BytePlus TOS, this section can be configured with a domain name starting with <code>tos://</code> or <code>s3://</code>.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, after copying, the storage path of the external data source becomes: <code>bhlasinfo/Iceberg</code>.</div><br><br><br><div data-tips="true" data-tips-type="warning">Then, the address to be configured could be: <code>tos://bhlasinfo/Iceberg</code>, <code>s3://bhlasinfo/Iceberg</code>.</div><br><br><br><br>* Iceberg Database Name: Designates the database in Iceberg. |
|Set Parameters (SETTINGS) |* enable_schema_covert_fault_tolerance: Controls the handling method when an auto\-derived type does not exist.<br><br><br>When a type in Iceberg cannot find a compatible type in Bytehouse: A value of `1` means to ignore; a value of `0` means to report an error;<br><br><br>* The default value is `1`.<br><br>* When set to `0`, tables with type compatibility issues will not be displayable.<br><br>* Region: The region of the external data source service. You can fill it in according to your available zone. For example, if you are using BytePlus services, please refer to the [region list](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint) for filling examples.<br><br>* Endpoint: The connection address of the external data source. For example, if you are using BytePlus Object Storage Service (TOS), you can log in to the TOS console, go to **Buckets** \> **Bucket Name** \> **Overview** \> **Access Domain** path to view the required Endpoint.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d89d9b0888d847c29e08e08ff129faf6~tplv-goo7wpa0wc-image.image) </span><br><br>* ak_id/ak_secret, the secret key with S3 access permission. |


<span id="e18ee3f0"></span>
# Query external tables

The query of external tables is consistent with that of regular tables.


* Generic approach


```SQL
select * from  t where xxx;
```


<span id="655eadca"></span>
# Delete external library tables

The deletion of external library tables is consistent with that of regular tables.


* Delete external databases.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Once the external database is deleted, all external tables under it will also be removed. Please proceed with caution.   </div>
   

   ```SQL
   DROP DATABASE example_db
   ```
   

* Delete external data table.

   ```SQL
   DROP TABLE example_table
   ```
   


<span id="baa3fc91"></span>
# Snapshot query

```SQL
-- Specify snapshotId=123456789
select * from tbl$version$123456789;

-- Specify branch name=branch_1
select * from tbl$version$branch_1;

-- Specify tag name=tag_1
select * from tbl$version$branch_1;
```


<span id="6d93e9a8"></span>
# Query table metadata

Below is the metadata for all currently supported Iceberg tables:


* snapshots: Records all snapshot information of the dataset, used for tracking and restoring historical versions.

* refs: Contains references to snapshots (branches and tags), supporting parallel development and marking important versions.

* history: Records the change history of the dataset, aiding in auditing and retracing data changes.

* files: Provides information related to the actual physical storage data files in the dataset, facilitating data management and performance optimization.

* properties: Configuration properties related to Schema.


```SQL
select * from tbl$metadata$snapshots;
select * from tbl$metadata$refs;
select * from tbl$metadata$history;
select * from tbl$metadata$files;
select * from tbl$metadata$properties;
```


<span id="9efb9922"></span>
# Reference: Data type mapping


|Iceberg type |Bytehouse type |
|---|---|
|Boolean |UInt8 |
|Integer |Int32 |
|Long |Int64 |
|Float |Float32 |
|Double |Float64 |
|Date |Date32 |
|Time |Not supported |
|Timestamp |DateTime64(UTC) |
|String |String |
|UUID |UUID |
|Fixed |FixedString |
|Binary |String |
|Decimal |Deciaml |
|Struct |Tuple |
|List |Array |
|Map |Map |
