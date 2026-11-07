---
title: "Import data using S3/TOS external table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/import-data-using-s3-tos-external-table"
---

This article describes how to import data from S3 or TOS external tables into ByteHouse CDW using persistent external tables and one\-time queries.

<span id="25939967"></span>
# Feature overview

ByteHouse Cloud Data Warehouse Edition (CDW) provides three methods for importing data from S3/TOS external tables:


|Import methods |Persistent external table |CnchS3 function |`INSERT INFILE` clause |
|---|---|---|---|
|Import steps |1. Enable data ingestion by creating a standard external table structure (`CREATE TABLE ... ENGINE = CnchS3`).<br><br>2. Use `INSERT INTO ...` The `SELECT FROM` statement imports data. |This method uses `INSERT INTO ...` `SELECT ...` The `FROM CnchS3` function directly queries and imports external data. |This method uses`INSERT INTO ...` `INFILE` statement directly queries and imports external data. |
|Operational logic |Through the table distribution mechanism of the `SELECT` statement, data is automatically and evenly distributed across all worker nodes to achieve load balancing. ||It imports data by directly reading files and does not have a load balancing mechanism. |
|Usage scenarios |* This method supports repeated queries and is suitable for scenarios that require repeated access to external data.<br><br>* It is suitable for small\-batch and large\-batch data import. |* One\-time queries do not require tables to be created in advance and offer relatively flexible syntax. However, each query must specify all parameters in full, making this approach more suitable for one\-time data loading tasks.<br><br>* Suitable for small and large batch data imports. |* One\-time queries do not require pre\-creating tables, and the syntax is relatively flexible. However, each query must specify all parameters in full, which makes them more suitable for one\-time data loading tasks.<br><br>* It is only applicable to small\-batch data import scenarios. |


Supported file types and compression formats in ByteHouse CDW are as follows:


* Supported file types: `CSV`, `TSVWithNames`, `TSV`, `CSVWithNames`, `JSONEachRow`, `Parquet`, `ORC`, and other common data types

* Supported compression formats: `none`, `gzip`, `deflate`, `br`, `xz`, `zstd`, and `snappy`.


<span id="bca24f22"></span>
# Prerequisites

Before you start, ensure you have the necessary permissions and information:


* Access to ByteHouse Cloud Data Warehouse service:

   * It is recommended to have the AccountAdmin or SystemAdmin roles.

   * For granting the ByteHouseFullAccess IAM policy to new users, please refer to [Grant privileges](https://docs.byteplus.com/docs/bytehouse/docs-user-management#0d0076bb).

* Access permissions for the object storage bucket you use: Obtain Access Key ID (AK) and Secret Access Key (SK). If you are using BytePlus Object Storage Service (TOS), please refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).

* Create the target database and target table in ByteHouse. For more information, see [Working with databases, tables and views](https://docs.byteplus.com/docs/bytehouse/docs-databases-tables-and-views).


<span id="2316650b"></span>
# Cautions


1. **Security**: Ensure secure storage of Access Key ID and Secret Access Key; do not expose them to unauthorized persons.

2. **Performance**: When importing large amounts of data, monitor the database and network load. Import in batches to reduce the load.

3. **Cost**: Importing data from Object Storage Service to ByteHouse using public network access incurs associated charges. It is recommended to understand the billing rules for the services you use before proceeding.

4. **S3 URL correctness**: When importing data using TOS external tables, note that the endpoint provided by BytePlus TOS differs from the S3 endpoint. The TOS file URL link copied from the BytePlus TOS console, `https://tos-{REGION}.bytepluses.com/xxx`, cannot be used directly. You need to replace the domain name with the S3 Endpoint domain and modify it to `https://tos-s3-{REGION}.bytepluses.com/xxx` format. For details, see [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint).


<span id="e609750b"></span>
# Basic syntax

This section introduces the basic syntax used for importing data via S3 external tables, CncnS3 functions, and INSERT INFILE, helping you understand the functions of core statements and the usage of parameters therein. For specific usage examples, please refer to [Steps](https://docs.byteplus.com/docs/bytehouse/import-data-using-s3-tos-external-table#cd8d5dea).

<span id="49a57122"></span>
## Import data by creating an S3 external table

<span id="7c674094"></span>
### Create a table

```SQL
# Create the ByteHouse target table
CREATE TABLE [db_name.]table_name (
    column1 type1,
    column2 type2,
    column3 type3,
    ...
) 
ENGINE=CnchMergeTree;

# Create the S3 external table of the ByteHouse target table
CREATE TABLE [db_name.]table_name_s3 AS table_name
ENGINE=CnchS3(
  'http://....' or 'https://', 
  'FORMAT',
  'COMPRESSION', 
  'access_key_id', 
  'secret_access_key'
);
```


**Parameter descriptions**


|Parameter name |Required |Description |
|---|---|---|
|`db_name` |No |It specifies the database name where the table resides. If you execute USE db_name before creating the table, you don't need to fill in the database name.<br><br>Example: `demo_db.target_table_name`. |
|`table_name` |Yes |It specifies the name of the ByteHouse target table for data import. Example: `demo_db.target_table_name`. |
|`table_name_s3` |Yes |It specifies the name of the S3 external table corresponding to the ByteHouse target table. |
|`column1 type1` |Yes |It specifies the schema of the ByteHouse target table, including column names and column types. Example: `id UInt64, name String`. |
|`ENGINE` |Yes |The table engine.<br><br><br>* ByteHouse target table: CnchMergeTree<br><br>* S3 external table: CnchS3 |
|`'http://....' or 'https://'` |Yes |It specifies the path to the object storage bucket corresponding to the S3 external table, using an HTTP(S) URL.<br><br><br>* `'http://....' or 'https://'`: Specify the data source path for the S3 external table. For example:<br><br>   ```Bash```<br>```   https://bucket.endpoint/file_path/file```<br>```   ```<br>   <br><br>* If you are using TOS, you can navigate to **TOS Console** \> **Bucket List** \> **Bucket Name** \> **File List**, then click the **Details** button next to the file name to view and copy the URL. Replace the domain with the S3 Endpoint domain. For more information, see [Regions and access domains supported by BytePlus TOS](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). Examples are as follows:<br><br>   ```Bash```<br>```   https://{bucket_name}.tos-s3-{region}.bytepluses.com/file_path```<br>```   ```<br>    |
|`FORMAT` |Yes |It specifies the file format for the S3 external table. For supported formats, see the description in the [Feature overview](https://docs.byteplus.com/docs/bytehouse/import-data-using-s3-tos-external-table#25939967) section. |
|`COMPRESSION` |Yes |It specifies the compression format for the S3 external table. For supported formats, see the introduction in the [Feature overview](https://docs.byteplus.com/docs/bytehouse/import-data-using-s3-tos-external-table#25939967) section. |
|`access_key_id` |Yes |It specifies the Access Key ID of the object storage service used by the S3 external table. You can refer to the official documentation of your object storage service to obtain the Access Key ID. If you are using BytePlus TOS, refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |
|`secret_access_key` |Yes |It specifies the Secret Access Key for the object storage service used by the S3 external table. You can refer to the official documentation of your object storage service to obtain the Secret Access Key. If you are using BytePlus TOS, you can refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |


To import data sources from multiple files, use a wildcard to replace the corresponding "file_path/file" path. For example, if you want to import all files from the "/source/" directory, you can write:

```SQL
CREATE TABLE db.table_name_s3 (
    id String,
    name String,
    city String
) ENGINE=CnchS3(
    'https://bucket.endpoint/source/*', 
    'FORMAT', 
    'COMPRESSION'
    'access_key_id', 
    'secret_access_key'
) 
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about S3 external table, see <a href="https://docs.byteplus.com/docs/bytehouse/docs-s3-external-table">External Table \- S3</a>.</div>


<span id="16af2565"></span>
### Insert data

```SQL
INSERT INTO table_name
SELECT column1, column2, ...
FROM table_name_s3
[WHERE _path like '%{path}%']
[SETTINGS parameter1 = value1, parameter2 = value2, ...]
```


**Parameter description**


|Parameter |Required |Description |
|---|---|---|
|`db_name` |No |It specifies the database name where the table resides. If you execute USE db_name before creating the table, you don't need to fill in the database name.<br><br>Example: `demo_db.target_table_name`. |
|`table_name` |Yes |It specifies the name of the ByteHouse target table for data import. Example: `demo_db.target_table_name`. |
|`column1, column2` |Yes |It specifies the column names to import. The column name should be the same as the S3 external table. Example: `id UInt64, name String`. |
|`table_name_s3` |Yes |The S3 external table name or subquery. |
|`WHERE _path like '%{path}%'` |No |`where _path like '%{path}%'` is used to prune and filter unnecessary files for reading, such as when many days of data exist under a certain path:<br><br>```Bash```<br>```/source/20240601/xxx```<br>```/source/20240602/xxx```<br>```....```<br><br><br>For example, adding `where _path like '%20240602%'` in a query causes the engine to scan only files under the `20240602` path. |
|`settings` |No |Custom parameters. You can set the following timeout parameters as needed:<br><br><br>* `receive_timeout`: Sets the timeout for reading data from S3 in seconds.<br><br>* `max_execution_time`: Sets the maximum query execution time in seconds.<br><br>* `exchange_timeout`: Sets the data exchange timeout in seconds.<br><br>* `send_timeout`: Sets the data sending timeout in seconds. |


<span id="7beb8ebc"></span>
## Import data using the CnchS3 function

```SQL
INSERT INTO [db_name.]table_name
SELECT column1, column2, ...
FROM CnchS3(
    'http://....' or 'https://', 
    'column1 type1, column2 type2, ...',
    'format'，
    'compression',
    'access_key_id', 
    'secret_access_key'
)
[WHERE _path like '%{path}%']
[SETTINGS parameter1 = value1, parameter2 = value2, ...]
```


**Parameter description**


|Parameter |Required |Description |
|---|---|---|
|`db_name` |No |It specifies the database name where the table resides. If you execute USE db_name before creating the table, you don't need to fill in the database name.<br><br>Example: `demo_db.target_table_name`. |
|`table_name` |Yes |It specifies the name of the ByteHouse target table for data import. Example: `demo_db.target_table_name`. |
|`column1, column2` |Yes |It specifies the list of fields to import, which must match the source table. Example: `id UInt64, name String`. |
|`FROM CnchS3` |Yes |It indicates importing data using the CnchS3 function. |
|`'http://....' or 'https://'` |Yes |It specifies the path to the source table in object storage. The path can be an HTTP or HTTPS URL.<br><br><br>* `'http://....' or 'https://'`: It specifies the datasource path for the S3 external table. Examples are as follows:<br><br>   ```SQL```<br>```   https://bucket.endpoint/file_path/file```<br>```   ```<br>   <br><br>* If you use TOS, you can go to **TOS console** \> **Bucket list** \> **Bucket name** \> **File list** \> and then click the **Details** button after the file name to view and copy the URL. Replace the domain name with the S3 Endpoint domain name. For details, see [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). For example,<br><br>   ```SQL```<br>```   https://{bucket_name}.tos-s3-{region}.bytepluses.com/file_path/file```<br>```   ```<br>    |
|`column1 type1, column2 type2, ...` |Yes |It specifies which columns and column types from the source table to import into the target table. Example: `city String, name String`. |
|`format` |Yes |It specifies the file format of the data in S3. Supported formats are introduced in [Feature overview](https://docs.byteplus.com/docs/bytehouse/import-data-using-s3-tos-external-table#25939967). |
|`compression` |Yes |It specifies the compression format of the data. Supported formats are introduced in [Feature overview](https://docs.byteplus.com/docs/bytehouse/import-data-using-s3-tos-external-table#25939967). |
|`access_key_id` |Yes |The Access Key ID for the object storage service. You can refer to the official documentation of the object storage service you are using to obtain the Access Key ID. If you are using BytePlus TOS, see [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |
|`secret_access_key` |Yes |The Secret Access Key for the object storage service can be obtained by referring to the official documentation of the object storage service you are using. If you are using BytePlus TOS, see [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |
|`WHERE _path like '%{path}%'` |No |`where _path like '%{path}%'` is used for pruning to filter out files that do not need to be read, for example, when a path contains data for many days:<br><br>```Bash```<br>```/source/20240601/xxx```<br>```/source/20240602/xxx```<br>```....```<br><br><br>For example, add `where _path like '%20240602%'` in your query; the engine will only scan files under the `20240602` path. |
|`settings` |No |Custom parameters; set the following timeout parameters as needed:<br><br><br>* `receive_timeout`: sets the timeout duration in seconds for reading data from S3.<br><br>* `max_execution_time`: sets the maximum execution time for a query, in seconds.<br><br>* `exchange_timeout`: sets the data exchange timeout, in seconds.<br><br>* `send_timeout`: sets the data send timeout, in seconds. |


<span id="80ed3758"></span>
## Import data through the INSERT INFILE clause

```SQL
INSERT INTO [db_name.]table_name
FORMAT data_format INFILE 'object_storage_path' COMPRESSION 'compression_format' 
SETTINGS
s3_ak_id = 's3_ak',
s3_ak_secret = 's3_sk',
s3_region = 's3_region',
s3_endpoint= 's3_endpoint',
s3_use_virtual_hosted_style=1;
```


**Parameter descriptions**


|Parameter name |Required |Description |
|---|---|---|
|`[db_name.]` |No |It specifies the database name where the table resides. If you execute USE db_name before creating the table, you don't need to fill in the database name.<br><br>Example: `demo_db.target_table_name`. |
|`table_name` |Yes |It specifies the name of the ByteHouse target table for data import. |
|`FORMAT` |Yes |Set the file format. For supported formats, see the introduction in [Feature overview](https://docs.byteplus.com/docs/bytehouse/import-data-using-s3-tos-external-table#25939967). |
|`INFILE` |Yes |It specifies the source file in object storage. Example: `s3://bucket_name/test_outfile.csv`. |
|`COMPRESSION` |Yes |It sets the compression format. For information about the supported formats, see the introduction in [Feature overview](https://docs.byteplus.com/docs/bytehouse/import-data-using-s3-tos-external-table#25939967). |
|`settings` |Yes |It sets the connection information for the object storage service:<br><br><br>* `s3_ak_id`: The Access Key ID for the object storage service. You can refer to the official documentation of your object storage service to obtain the Access Key ID. If you are using BytePlus TOS, refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).<br><br>* `s3_ak_secret`: The Secret Access Key for the object storage service. You can refer to the official documentation of the object storage service you use to obtain the Secret Access Key. If you are using BytePlus TOS, refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).<br><br>* `s3_region`: The region ID to which the object storage service belongs. You can refer to the official documentation of your object storage service to obtain the region. Example formats include `oss-cn-beijing` and `cn-northwest-1`. If you are using BytePlus TOS, you can refer to [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). Example: `cn-beijing`.<br><br>* `s3_endpoint`: The access domain name of the object storage service. You can refer to the official documentation of your object storage service to obtain the access domain name. Format examples include: `http://s3.eu-west-1.amazonaws.com`, `https://oss-cn-beijing.aliyuncs.com`. If you are using BytePlus TOS, you can refer to the S3 endpoint column in [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). Example: `https://tos-s3-ap-southeast-1.bytepluses.com`.<br><br>* `s3_use_virtual_hosted_style`: Sets the access style for the bucket. The default value is 0 (false), which means the bucket is accessed using the path style. If you are using BytePlus TOS, you must set this parameter to 1, as BytePlus TOS does not support path style access. |


<span id="cd8d5dea"></span>
# Steps

<span id="93c16f1b"></span>
## Step 1: Connect to ByteHouse CDW

You can connect to ByteHouse CDW by logging into the ByteHouse CDW console, using the ByteHouse CLI tool, or a database client such as DBeaver, DataGrip. For detailed instructions, refer to the following explanations or documentation:


* **ByteHouse CDW console**

   Log in to the ByteHouse CDW console, click **SQL worksheet**, and enter commands in the SQL editor area.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf390cb393eb4715bbf20f2ea01dfb96~tplv-goo7wpa0wc-image.image) </span>

* **ByteHouse CLI**

   Refer to [ByteHouse CLI](https://docs.byteplus.com/docs/bytehouse/docs-gateway-client) for operation instructions.

* **Database client tool**

   You can refer to the [ByteHouse ecosystem tools](https://docs.byteplus.com/en/docs/bytehouse/docs-ecosystem) documentation and use ecosystem tools to connect to ByteHouse as needed.

   Alternatively, you can click **Tenant management** at the top of the ByteHouse console, view the supported ecosystem tools under the **Ecosystem tools** tab, and click **Supported Driver types** to access the operation instructions document.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e7f1319561b4abab468e1fdcd3ece0c~tplv-goo7wpa0wc-image.image) </span>


<span id="27c8c48f"></span>
## Step 2: Select the target database

Execute the following SQL statement to select the target database.

```SQL
USE demo_db;
```


<span id="76521a6e"></span>
## Step 3: Create the ByteHouse target table

Create the target table in ByteHouse with the same structure as the source table. For example,

```SQL
CREATE TABLE demo_db.demo_table (
    id String,
    name String,
    city String,
  ) ENGINE = CnchMergeTree
ORDER BY
  id
```


<span id="28d71555"></span>
## Step 4: Import data

<span id="7d1e5bf0"></span>
### Method 1: Create an S3 external table and write data


1. Create the S3 external table by executing the following SQL. Replace the placeholders in the command with actual parameter values when using it.

   ```SQL
   CREATE TABLE demo_db.demo_table_s3 AS demo_db.demo_table
   ENGINE=CnchS3(
     'https://bucket.endpoint/file_path/file', 
     'FORMAT',
     'COMPRESSION', 
     'access_key_id', 
     'secret_access_key'
   ) 
   ```
   

2. Refer to the following SQL to import data directly from an existing table into a ByteHouse table. See [Import data by creating an S3 external table](https://docs.byteplus.com/docs/bytehouse/import-data-using-s3-tos-external-table#16af2565) for parameter explanations.

   ```SQL
   INSERT INTO demo_db.demo_table
   SELECT col0, col1, ... 
   FROM demo_db.demo_table_s3
   WHERE _path like '%{path}%'
   SETTINGS 
       receive_timeout = 10800000, 
       max_execution_time = 10800000, 
       exchange_timeout = 10800000, 
       send_timeout = 10800000;
   ```
   


<span id="4b580b15"></span>
### Method 2: Import data using the S3 table function

Run the following SQL command to import data from S3 / TOS into a ByteHouse table using the CnchS3 table function. Replace the placeholders in the command with actual parameter values when using. See [Import data using the CnchS3 function](https://docs.byteplus.com/docs/bytehouse/import-data-using-s3-tos-external-table#7beb8ebc) for parameter explanations.

```SQL
INSERT INTO demo_db.demo_table
SELECT col0, col1... 
FROM CnchS3(
    'https://bucket.endpoint/file_path/test_outfile.csv', 
    'id String, name String, city String', 
    'FORMAT CSV', 
    'COMPRESSION none'
    '{your_access_key_id}', 
    '{your_secret_access_key}'
)
WHERE _path like '%{path}%'
SETTINGS 
    receive_timeout = 10800000, 
    max_execution_time = 10800000, 
    exchange_timeout = 10800000, 
    send_timeout = 10800000;
```


<span id="515b20e1"></span>
### Method 3: Write data using the INSERT INFILE clause

Execute the following SQL statement to import data from the object storage bucket into the ByteHouse table. When using the command, please replace the placeholders with actual parameter values. Please refer to [Import data through the INSERT INFILE clause](https://docs.byteplus.com/docs/bytehouse/import-data-using-s3-tos-external-table#80ed3758) for parameter descriptions.

```SQL
INSERT INTO demo_db.demo_table
FORMAT CSV INFILE 's3://s3_bucket/test_outfile.csv' COMPRESSION 'none' 
SETTINGS
s3_ak_id = '{your_access_key_id}',
s3_ak_secret = '{your_secret_access_key}',
s3_region = '{your_s3_region}',
s3_endpoint= '{your_s3_endpoint}'，
s3_use_virtual_hosted_style=1;
```


<span id="301cb609"></span>
## Step 5: Data validation

After performing the import, verify the data by querying the target table. Example as follows:

```SQL
SELECT * FROM demo_db.demo_table LIMIT 10;
```


Complete the above steps to import data from the S3/TOS bucket into the ByteHouse table. If you have any questions, contact the system administrator or database administrator for support.

<span id="14ac4260"></span>
# See also: Use wildcard matching when importing files in bulk

When importing data, ByteHouse supports performing string regular expression matching on the **last segment of the path**, allowing multiple files to be specified at once. The following usages are currently supported:

```C++
/* Parse a string that generates shards and replicas. Separator - one of two characters | or ,
 *  depending on whether shards or replicas are generated.
 * For example:
 * host1,host2,...      - generates set of shards from host1, host2, ...
 * host1|host2|...      - generates set of replicas from host1, host2, ...
 * abc{8..10}def        - generates set of shards abc8def, abc9def, abc10def.
 * abc{08..10}def       - generates set of shards abc08def, abc09def, abc10def.
 * abc{x,yy,z}def       - generates set of shards abcxdef, abcyydef, abczdef.
 * abc{x|yy|z} def      - generates set of replicas abcxdef, abcyydef, abczdef.
 * abc{1..9}de{f,g,h}   - is a direct product, 27 shards.
 * abc{1..9}de{0|1}     - is a direct product, 9 shards, in each 2 replicas.
 */
```


Usage examples:

```SQL
INSERT INTO numbers 
FORMAT CSV 
INFILE 's3://bucket/data_path/clickhouse_outfile_{1..100}.csv'
```


In addition to pure regular expression parsing, it now supports ListFile in Local and S3 file systems, with support for `*` and `?`. Wildcard matching and similar methods.

```SQL
INSERT INTO numbers 
FORMAT CSV 
INFILE 's3://bucket/data_path/clickhouse_outfile_*.csv'
```
