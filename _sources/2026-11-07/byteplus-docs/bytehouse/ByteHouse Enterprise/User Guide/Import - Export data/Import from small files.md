---
title: "Import from small files"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/import-from-small-files"
---

This tutorial describes how to import small files into ByteHouse using data sources such as local files, object storage, HDFS, and other data sources.

<span id="0e6d0753"></span>
# Function overview

When you need to test file import, or when the files to be imported are small in size (such as a few KB to several tens of MB for small batches of data), it is recommended to use the `INSERT INTO` statement for import, as this method is more efficient. In terms of import efficiency, using batch import to process object storage data sources requires scheduling Spark resources, and even files as small as a few kilobytes can take several minutes to import. In contrast, the `INSERT INTO` method reads data directly from object storage and writes it to ByteHouse, without relying on Spark resource scheduling, allowing for fast import.

The ByteHouse small file import feature supports local files, object storage, and HDFS data sources:


* When importing local files into ByteHouse, you must ensure that both the tools and files you use are located locally. It is recommended to connect to ByteHouse using ClickHouse Client and use the `INSERT INTO` statement to complete the import, as this method is simpler and more convenient.

* To import from object storage and from HDFS, you can use connection tools that support executing SQL statements. You can use the query window in the ByteHouse Enterprise console, or use other connection tools to connect to ByteHouse, and complete the import using the `INSERT INTO` statement. For details on the procedures for connecting to ByteHouse, see [Query window](https://docs.byteplus.com/docs/bytehouse/query-window) and [connecting to a cluster](https://docs.byteplus.com/en/docs/bytehouse/connection).


<span id="fad77956"></span>
# Cautions


* Each time `INSERT INTO` is executed, it consumes CPU resources in the ByteHouse cluster, which may compete with ongoing query tasks for resources and result in delayed query responses or reduced performance. The batch import feature adopts bypass writing and uses the Spark cluster's CPU resources, so preemption does not occur.

* If you execute `INSERT INTO` directly on a Distributed table (as in the example scenario below), and the cluster has more than one shard, data must be routed and distributed among the shards. This results in additional network transmission and data processing overhead, leading to poor import performance. It is recommended that you split the source data according to the sharding rules and import each part separately into the local table of each node (that is, the Local table in the example). This can reduce resource consumption and improve import efficiency.

* Based on the above resource usage characteristics and performance limitations, the small file import method is suitable only for import testing and not for actual production. If you need to import large volumes of data, you may refer to [Batch import](https://docs.byteplus.com/docs/bytehouse/batch-import) or [Streaming import](https://docs.byteplus.com/docs/bytehouse/streaming-import).


<span id="733068d8"></span>
# Basic syntax

<span id="da5dffb4"></span>
## Import from local files

```Shell
clickhouse client \
  --host <host> \
  --user <user> \
  --password <password> \
  --query "INSERT INTO <database_name>.<table_name> FORMAT format SETTINGS key1=value1, key2=value2" \
  < File_Name.csv \ 
```


You can also use the Cat command:

```SQL
cat File_Name.csv | clickhouse-client \
    --host <host> \
    --user <user> \
    --password <password> \
    --query="INSERT INTO <database_name>.<table_name> FORMAT format SETTINGS key1=value1, key2=value2";
```


<span id="d0859f0c"></span>
### **Parameter description**


|Parameter |Configuration instructions |
|---|---|
|host |The network address of the ByteHouse cluster. You can log in to the ByteHouse Enterprise console. In **Cluster management** \> **Cluster list** \> **Cluster name** \> **Connect**, view and copy the host address in the ClickHouse Client card.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac970ce55489429ca5e5a7eaefaf68a7~tplv-goo7wpa0wc-image.image) </span> |
|user |The ByteHouse account name. Log in to the ByteHouse Enterprise console. Navigate to **Cluster management** \> **Cluster list** \> **cluster name** \> **Connect**, where you can view and copy the user information from the ClickHouse Client card. |
|password |The ByteHouse connection password. Log in to the ByteHouse Enterprise console, click ByteHouse **Personal Center** in the upper right corner, click **Account management**, and copy the cluster connection password.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a516fa958344dee857798b98b707f08~tplv-goo7wpa0wc-image.image) </span> |
|query |Set it as an `INSERT INTO` statement.<br><br><br>* `INSERT INTO <database_name>.<table_name>`: Specifies the database and table name to be imported.<br><br>* `FORMAT`: Specifies the format for the data source file. For currently supported formats, see [Input and output data formats](https://clickhouse.com/docs/interfaces/formats).<br><br>* `SETTINGS`: Configure the settings parameter to specify the actual format of CSV data and flexibly adapt to data read and write requirements. Please refer to [Configure settings](https://docs.byteplus.com/docs/bytehouse/import-from-small-files#75040f9d) for the settings parameters that can currently be configured. |
|File_Name |File path and file name to import. |


<span id="9a29a197"></span>
## Import from object storage

```SQL
INSERT INTO <database_name>.<table_name>
SELECT * FROM s3(
    path, 
    access_key_id,
    secret_access_key,
    format,
    structure,
    [compression]
)
[SETTINGS key1=value1, key2=value2];
```


<span id="617a856d"></span>
### **Parameter description**


|Parameter |Configuration instructions |
|---|---|
|database_name |Target database name. |
|table_name |The target data table name. |
|path |Specify the path of the source table in object storage. An example is shown below:<br><br>```Bash```<br>```https://{bucket_name}.endpoint/file_path/file```<br><br><br>If you are using TOS, you can view and copy the URL by navigating to **TOS Console** \> **Bucket** **list** \> **Bucket** **name** \> **File** **list** and then clicking the **Details** button next to the file name. Replace the domain name with the S3 Endpoint domain name; it is recommended to use the internal domain name. For more information, see [Region and Endpoint of TOS](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). Examples are as follows:<br><br>```SQL```<br>```https://{bucket_name}.tos-s3-{region}.ibytepluses.com/file_path/file```<br> |
|access_key_id |Set this to the Access Key ID of your object storage service. Refer to the official documentation of your object storage service to obtain the Access Key ID. If you are using BytePlus TOS, refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |
|secret_access_key |Set this value as the Secret Access Key for the object storage service you use. You can refer to the official documentation of the object storage service you use to obtain the Secret Access Key. If you are using BytePlus TOS, you can refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |
|format |Set to the source file format, such as CSV. For currently supported formats, see [Input and output data formats](https://clickhouse.com/docs/interfaces/formats). |
|structure |Set to match the source table structure, including column names and column types. Example: `'column1_name column1_type, column2_name column2_type, ...'`. |
|[compression] |Optional configuration that specifies the compression format for data; supports `none`, `gzip/gz`, `brotli/br`, `xz/LZMA`, and `zstd/zst`. |
|[SETTINGS] |Optional configuration. Set the settings parameter to configure the actual format of CSV data and flexibly accommodate data reading and writing needs. See [Configure settings](https://docs.byteplus.com/docs/bytehouse/import-from-small-files#75040f9d) for the settings parameters that are currently supported for configuration. |


<span id="1a4a30cf"></span>
## Import from HDFS

```SQL
INSERT INTO <database_name>.<table_name>
SELECT * 
FROM hdfs(
    'path', 
    'format',                    
    'structure'
)
[SETTINGS key1=value1, key2=value2];
```


<span id="07e205a3"></span>
### **Parameter description**


|Parameter |Configuration instructions |
|---|---|
|database_name |The target database name. |
|table_name |The target data table name. |
|path |Set to the full HDFS file path, in the format `hdfs://host:port/file_path/file_name`:<br><br><br>* host: The IP address or hostname of the HDFS cluster NameNode. For example: `192.168.1.100`.<br><br>* port: HDFS default port (typically 8020 for HA clusters, 9000 for non\-HA clusters);<br><br>* file_path/file_name: The file path. For example: `/user/data/user_202509.csv`. |
|format |Set to source file format, for example, CSV. |
|structure |Set to the source table structure, including column names and column types. Example: `'column1_name column1_type, column2_name column2_type, ...'`. |
|[SETTINGS] |Optional configuration: set the settings parameter to specify the actual format of CSV data, to flexibly meet data reading and writing needs. See [Configure settings](https://docs.byteplus.com/docs/bytehouse/import-from-small-files#75040f9d) for the settings parameters that are currently supported for configuration. |


<span id="75040f9d"></span>
## Configure settings

When executing SQL statements, you can add the following Settings configuration items as needed, based on the actual format of the CSV data, to flexibly adapt to data reading and writing requirements.


|Settings options |Default value |Description |
|---|---|---|
|format_csv_delimiter |`,` |It specifies the delimiter character for fields in CSV data. If set to a string, the string must be one character long. |
|format_csv_allow_single_quotes |`1`（true） |It specifies whether the single quotation marks (`'...'`) can be used to enclose field content. If set to true, strings enclosed in single quotes are allowed. |
|format_csv_allow_double_quotes |`1`（true） |It specifies whether the double quotation marks (`"..."`) can be used to enclose field content. If set to true, strings enclosed in double quotation marks are allowed. |
|format_csv_write_utf8_with_bom |`0`（false） |It specifies whether a UTF\-8 BOM (byte order mark) can be written at the beginning of the output CSV file. If set to true, a BOM will be written at the beginning of the output. |
|output_format_csv_crlf_end_of_line |`0`（false） |It specifies whether the line ending `\r\n` can be used when exporting CSV. Otherwise, use `\n`. |
|output_format_csv_null_representation |`\N` |The string used to represent the `NULL` value when output is specified. The default is `\N`. You can set it to other strings (such as `NULL`). |
|input_format_csv_unquoted_null_literal_as_null |`0`（false） |It specifies whether the unquoted text `NULL` can be treated as the value `\N`. If disabled, it is treated as a normal string. |
|input_format_csv_enum_as_number |`0`（false） |When importing a CSV file, whether enum values can be interpreted as their corresponding enum indices `\N`. |
|input_format_csv_arrays_as_nested_csv |`0`（false） |It sepecifies whether the array fields can be parsed as nested CSV format. For example, `"Hello", "world", "42 TV"` are parsed as array elements. It supports the use of double quotation marks and escape sequences. The outer square brackets of an array can be omitted. |


<span id="a87b3938"></span>
# Usage examples

<span id="668986cf"></span>
## Create ByteHouse target databases and tables

Create the target database and table in ByteHouse, and ensure that the structure of the target table matches that of the source table. For detailed instructions, please refer to [Create a new database/table](https://docs.byteplus.com/docs/bytehouse/create-a-new-database-table).

The example in this article uses a HaMergeTree table. The table creation statement is as follows:

```SQL
-- Create a database
CREATE DATABASE IF NOT EXISTS test_db

-- Create a local table
CREATE TABLE IF NOT EXISTS test_db.test_table_local ON CLUSTER default_cluster
(
    `id` String,
    `name` String,
    `date` Date
)
ENGINE = HaMergeTree('/clickhouse/tables/test_db/test_table_local/{shard}', '{replica}')
ORDER BY id;

-- Create a distributed table
CREATE TABLE IF NOT EXISTS test_db.test_table ON CLUSTER default_cluster
AS test_db.test_table_local
ENGINE = Distributed('default_cluster', 'test_db', 'test_table_local', rand());
```


<span id="c7f8e3fe"></span>
## Import from local files

<span id="9f31c8dc"></span>
### Preparation

Install the ClickHouse Client tool, [click here to download](https://clickhouse.com/docs/zh/interfaces/cli).

<span id="a8b49b27"></span>
### Steps


1. Prepare the local file `test.csv`, and write the following data into it. Ensure that the field order in the local CSV file matches the field order in the target table.

   ```powershell
   $ cat /test.csv
       A001,Amy,2023-01-01
       A002,Bob,2023-01-02
       A003,Charles,2023-01-03
   ```
   

2. Use ClickHouse Client to write data to the target table.

   ```haskell
   cat test.csv | clickhouse-client \
       --host 2xxxxxxxxxxxxxxxxx.bytehouse-ce.ibytepluses.com \
       --user demo_user \
       --password Mt**************  \
       --query="INSERT INTO test_db.test_table_local FORMAT CSV";
   ```
   

3. Check whether the write was successful.

   ```sql
   SELECT * FROM test_db.test_table;
   ```
   


<span id="b439c236"></span>
## Import from object storage

This example demonstrates how to use the ClickHouse `s3()` function to write data from a local file into the ByteHouse table created in the Preparation section.

<span id="99596800"></span>
### Preparation

Please ensure that you already have access permissions for the object storage bucket you are using before starting operations:


* Obtain Access Key ID (AK) and Secret Access Key (SK). If you are using BytePlus Torch Object Storage Service (TOS), for more details, refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).


<span id="9f7f4006"></span>
### Steps


1. Build a schema mapping. This step is used to obtain the field names and field types of the target table. This ensures that the source data matches the structure of the target table and prevents failures caused by structural mismatches during import.

   ```SQL
   SELECT arrayStringConcat(groupArray(concat(name, ' ', type)), ', ')  
   FROM system.columns 
   WHERE DATABASE = '<database_name>' AND TABLE = '<table_name>'
   ```
   

2. Import data from object storage into ByteHouse.

   ```sql
   INSERT INTO test_db.test_table_local
   SELECT *
   FROM s3(
       'https://bucket.endpoint/file_path/test_outfile.csv', 
       'AK***************',                                 
       'aBc********************',                
       'CSV',                                          
       '(id String, name String, date Date)',  
       'none',                                           
   );
   ```
   

3. Check whether the write operation was successful.

   ```sql
   SELECT * FROM test_db.test_table;
   ```
   


<span id="2b895433"></span>
## Import from HDFS

This example demonstrates how to use the ClickHouse `hdfs()` function to write data from a local file into the ByteHouse table created in the preparation section.

<span id="8e1bda40"></span>
### Preparation

Before you begin, make sure you have obtained the access path for the HDFS file and have permission to access that path.

<span id="188c11c8"></span>
### Steps


1. Import data from HDFS to ByteHouse.

   ```sql
   INSERT INTO test_db.test_table_local 
   SELECT * 
   FROM hdfs(
       'hdfs://192.168.x.xxx:8020/user/data/202509_user.csv',
       'CSV',
       '(id String, name String, date Date)'
   );
   ```
   

2. Check whether the write was successful.

   ```sql
   SELECT * FROM test_db.test_table;
   ```
   


<span id="6fb90583"></span>
# Frequently asked questions

<span id="ae7b5d4f"></span>
## Code: 27

If you encounter the following errors while using the product:

```Bash
Code: 27, e.displayText() = DB::ParsingException:Cannot parse input: expected '\\N' before: ... (version 21.8.7.1)
```



* **Cause of the problem**:

   This error typically occurs when a string in the CSV file is not enclosed in single or double quotation marks and contains a backslash `\`, such as `aaa,bbb,cc\c`. ByteHouse treats the backslash as a special character in this case.

* **Solutions**:

   * In the data source, enclose all strings in double or single quotation marks so that ByteHouse treats the backslash as part of the string.

   * When `input_format_null_as_default = 0` is set during insertion, ByteHouse will no longer recognize `\N` as `Null`. However, this approach will make it impossible to import Null values.
