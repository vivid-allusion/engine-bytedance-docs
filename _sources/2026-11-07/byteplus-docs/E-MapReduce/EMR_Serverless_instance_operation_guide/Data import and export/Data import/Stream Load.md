---
title: "Stream Load"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Stream_Load"
---

This document introduces the Stream Load transaction interface and explains how to use this interface to import data into StarRocks. The images and related content in this document are sourced from the open\-source StarRocks [StreamLoad](https://docs.starrocks.io/zh/docs/loading/StreamLoad) section.

<span id="_1-功能介绍"></span>
## 1 Feature overview

Stream Load is a synchronous import method based on the HTTP protocol, supporting the import of local files or data streams into StarRocks. After you submit an import job, StarRocks synchronously executes it and returns the result information. You can determine whether the import job was successful based on the returned result information.

CSV and JSON file formats are supported. The recommended data volume is less than 10 GB.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Stream Load currently does not support importing data from CSV files where a column is JSON.</div>


<span id="_2-基本原理"></span>
## 2 Basic principles

The user submits a Stream Load import job request via the HTTP protocol. After the FE receives the request, it forwards it to a BE node. This BE node becomes the Coordinator node, responsible for receiving the data and distributing it to other data nodes. After the import is complete, the result is returned to the user.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_defdb98f9befcbe88b64d35f088f7076.png) </span>

<span id="_2-1-使用介绍"></span>
### 2.1 Usage introduction

Stream Load submits and transfers data via the HTTP protocol. This example demonstrates how to submit an import task using the `curl` command. You can also perform this operation using other HTTP clients.

<span id="_2-2-语法"></span>
### 2.2 Syntax

```powershell
curl --location-trusted -u username:password [data_desc] -T file_path -XPUT \
http://fe_host:fe_http_port/api/database_name/table_name/_stream_load
```


The parameter descriptions are as follows:


|Parameter |Description |
|---|---|
|username:password |Used to specify the username and password for the StarRocks cluster account. Required parameter. |
|file_path |The save path of the source data file. |
|fe_host:fe_http_port |The IP and port of FE (the default port is 8030). |
|database_name |The name of the database where the target table is located. |
|table_name |The name of the target table. |
|data_desc |Optional. Used to describe the source data file. The syntax is:<br><br>```sql```<br>```-H "format: CSV```<br>```-H "column_separator: <column_separator>"```<br>```-H "row_delimiter: <row_delimiter>"```<br>```-H "columns: <column1_name>[, <column2_name>，... ]"```<br>```-H "partitions: <partition1_name>[, <partition2_name>, ...]"```<br>```-H "temporary_partitions: <temporary_partition1_name>[, <temporary_partition2_name>, ...]"```<br>```-H "jsonpaths: [ \"<json_path1>\"[, \"<json_path2>\", ...] ]"```<br>```-H "strip_outer_array:  true```<br>```-H "json_root: <json_path>"```<br><br><br>For parameter descriptions, refer to the StarRocks community [data_desc](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/STREAM_LOAD#data_desc) section. |


After the import task is completed, Stream Load returns the related content of the import task in JSON format. An example of the returned result is as follows:

```json
{
    "TxnId": 13,
    "Label": "123",
    "Status": "Success",
    "Message": "OK",
    "NumberTotalRows": 4,
    "NumberLoadedRows": 4,
    "NumberFilteredRows": 0,
    "NumberUnselectedRows": 0,
    "LoadBytes": 42,
    "LoadTimeMs": 45,
    "BeginTxnTimeMs": 8,
    "StreamLoadPlanTimeMs": 9,
    "ReadDataTimeMs": 0,
    "WriteDataTimeMs": 6,
    "CommitAndPublishTimeMs": 21
}
```


For a description of the return value parameters, refer to the [Return Value](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/STREAM_LOAD#%E8%BF%94%E5%9B%9E%E5%80%BC) section in the StarRocks community.

<span id="_3-导入示例"></span>
## 3 Import examples

<span id="_3-1-导入-csv-格式的数据"></span>
### 3.1 Importing data in CSV format


1. Prepare the data

   Create a CSV format data file named `example1.csv` in the local file system with the following content:


```sql
1,Lily,23
2,Rose,23
3,Alice,24
4,Julia,25
```



2. Create the target table `table1` in the database `test_db`

   ```sql
   CREATE DATABASE IF NOT EXISTS test_db;
   USE test_db;
   CREATE TABLE `table1`
   (
       `id` int(11) NOT NULL COMMENT "用户 ID",
       `name` varchar(65533) NULL COMMENT "用户姓名",
       `score` int(11) NOT NULL COMMENT "用户得分"
   )
   ENGINE=OLAP
   PRIMARY KEY(`id`)
   DISTRIBUTED BY HASH(`id`);
   ```
   

3. Create the import job

   ```sql
   curl --location-trusted -u <username>:<password> -H "label:123" \
       -H "Expect:100-continue" \
       -H "column_separator:," \
       -H "columns: id, name, score" \
       -T example1.csv -XPUT \
       http://<fe_host>:8030/api/test_db/table1/_stream_load
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">column_separator parameter: Defines the file delimiter. The <code>example1.csv</code> file contains three columns, which correspond one\-to\-one with the <code>table1</code> table's <code>id</code>, <code>name</code>, and <code>score</code> columns, and use a comma (,) as the column separator.</div>


4. After the import is complete, query the data in the `table1` table

   ```sql
   SELECT * FROM table1;
   ```
   


<span id="_3-2-导入-json-格式的数据"></span>
### 3.2 Importing data in JSON format


1. Prepare the data

   Create a JSON format data file named `example2.json` with the following content:

   ```sql
   {"name": "北京", "code": 2}
   ```
   

2. Create the target table `table2` in the database `test_db`

   ```sql
   CREATE TABLE `table2`
   (
       `id` int(11) NOT NULL COMMENT "城市 ID",
        `city` varchar(65533) NULL COMMENT "城市名称"
   )
   ENGINE=OLAP
   PRIMARY KEY(`id`)
   DISTRIBUTED BY HASH(`id`);
   ```
   

3. Create the import job to import the data from the `example2.json` file into the `table2` table

   ```sql
   curl -v --location-trusted -u <username>:<password> -H "strict_mode: true" \
       -H "Expect:100-continue" \
       -H "format: json" -H "jsonpaths: [\"$.name\", \"$.code\"]" \
       -H "columns: city,tmp_id, id = tmp_id * 100" \
       -T example2.json -XPUT \
       http://<fe_host>:8030/api/test_db/table2/_stream_load
   ```
   

   The `example2.json` file contains two keys, `name` and `code`, which correspond to the columns in the `table2` table as shown in the following figure.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff3286b6b1b31b2a1410b3bc3b31442a.png) </span>

   The mapping relationship shown above is described as follows:

   * Extract the `example2.json` file's `name` and `code` fields, and sequentially map them to the `jsonpaths` parameter's declared `name` and `code` fields.

   * Extract the `jsonpaths` parameter's declared `name` and `code` fields, and sequentially map them to the `columns` parameter's declared `city` and `tmp_id` columns.

   * Extract the `columns` parameter's declared `city` and `id` columns, and map them by name to the `table2` table's `city` and `id` columns.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">jsonpaths parameter: Specify the keys to be imported one by one according to the order of keys in the JSON file.</div>


2. <div data-tips="true" data-tips-type="tip">columns parameter: If the columns in the source data file do not correspond one\-to\-one in order with the columns in the target table, including differences in quantity or order, you must use the <code>COLUMNS</code> parameter to specify the column mapping and transformation relationships.</div>


3. <div data-tips="true" data-tips-type="tip">For information about the correspondence between imported JSON data fields, refer to the "<a href="https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/STREAM_LOAD#%E5%88%97%E6%98%A0%E5%B0%84">Column mapping</a>" section in the STREAM LOAD documentation.</div>


4. After the import is complete, query the data in the `table2` table.

   ```sql
   SELECT * FROM table2;
   ```
