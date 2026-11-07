---
title: "Broker Load"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Broker_Load"
---

EMR StarRocks provides a Broker Load import method based on the MySQL protocol, enabling you to import large volumes of data from HDFS or external cloud storage systems (such as TOS).

This document introduces usage examples and FAQs for Broker Load import. The images and content in this document are sourced from the open\-source StarRocks community [Importing data from HDFS or external cloud storage systems](https://docs.starrocks.io/zh/docs/loading/BrokerLoad#%E4%BB%8E-hdfs-%E6%88%96%E5%A4%96%E9%83%A8%E4%BA%91%E5%AD%98%E5%82%A8%E7%B3%BB%E7%BB%9F%E5%AF%BC%E5%85%A5%E6%95%B0%E6%8D%AE) section.

<span id="_1-基本原理"></span>
## 1 Basic principles

Broker Load is an asynchronous import method. After you submit an import job, FE generates the corresponding query plan and, based on the number of available BEs and the size of the source data files, distributes the query plan to multiple BEs for execution. Each BE is responsible for executing part of the import task. During execution, BE pulls data from HDFS or cloud storage systems, and after preprocessing the data, imports it into StarRocks. Once all BEs have completed the import, FE determines whether the import job was successful.

You need to use the [SHOW LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/SHOW_LOAD) statement or the curl command to check the result of the import job.

CSV, ORCFile, and Parquet file formats are supported. It is recommended that each import operation handles data volumes ranging from tens of GB to hundreds of GB.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_35085a029abad40143311481947b5eb7.png) </span>

<span id="_2-基本操作"></span>
## 2 Basic operations

<span id="_2-1-查看broker"></span>
### 2.1 View Broker

The Broker service is automatically deployed and started on each Core node when the EMR StarRocks cluster is created. You can use the following SQL command to view the Broker.

```sql
SHOW PROC "/brokers"\G
```


<span id="_2-2-创建导入任务"></span>
### 2.2 Create import tasks

<span id="_2-2-1-语法"></span>
#### 2.2.1 Syntax

```properties
LOAD LABEL [<database_name>.]<label_name>
(
    data_desc[, data_desc ...]
)
WITH BROKER
(StorageCredentialParams)
[PROPERTIES (opt_properties)]
```


Parameter descriptions are as follows. Also refer to the StarRocks community [BROKER LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/BROKER_LOAD).


|Parameter |Description |
|---|---|
|database_name |Optional. Specifies the database where the target table resides. |
|label_name |Specifies the label for the import job. Each import job corresponds to a unique label. The label allows you to view the execution status of the import job. When the import job status is FINISHED, its label cannot be reused for other import jobs. When the import job status is CANCELLED, its label can be reused for other import jobs. For label naming conventions, see [system limitations](https://docs.starrocks.io/zh/docs/reference/System_limit). |
|data_desc |Used to describe a batch of data to be imported. The format is as follows:<br><br>```sql```<br>```DATA INFILE ("<file_path>"[, "<file_path>" ...])```<br>```[NEGATIVE]```<br>```INTO TABLE <table_name>```<br>```[PARTITION (<partition1_name>[, <partition2_name> ...])]```<br>```[TEMPORARY PARTITION (<temporary_partition1_name>[, <temporary_partition2_name> ...])]```<br>```[COLUMNS TERMINATED BY "<column_separator>"]```<br>```[ROWS TERMINATED BY "<row_separator>"]```<br>```[FORMAT AS "CSV```<br>```[(column_list)]```<br>```[COLUMNS FROM PATH AS (<partition_field_name>[, <partition_field_name> ...])]```<br>```[SET <k1=f1(v1)>[, <k2=f2(v2)> ...]]```<br>```[WHERE predicate]```<br><br><br>For parameter details, refer to the StarRocks community website [data_desc introduction](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/BROKER_LOAD#data_desc). |
|StorageCredentialParams |Authentication configuration for StarRocks to access storage systems. Please refer to the StarRocks community[storagecredentialparams](https://docs.byteplus.com/docs/E-MapReduce/109121#storagecredentialparams). |


<span id="_2-2-2-查看导入作业"></span>
#### 2.2.2 View import jobs

Broker Load supports viewing the execution status of import jobs using either the SHOW LOAD statement or the curl command.


* **Using the SHOW LOAD statement**


Execute [SHOW LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/SHOW_LOAD) to view information about specified import jobs in the database. The syntax is as follows:

```sql
SHOW LOAD [ FROM db_name ]
[
   WHERE [ LABEL { = "label_name" | LIKE "label_matcher" } ]
         [ [AND] STATE = { "PENDING" | "ETL" | "LOADING" | "FINISHED" | "CANCELLED" } ]
]
[ ORDER BY field_name [ ASC | DESC ] ]
[ LIMIT { [offset, ] limit | limit OFFSET offset } ]
```


Example: View the status of import tasks in the `test_db` database:

```sql
MySQL [test_db]> SHOW LOAD \G;
*********************** 1. row ***************************
         JobId: 10244
         Label: label1
         State: FINISHED
      Progress: ETL:100%; LOAD:100%
          Type: BROKER
      Priority: NORMAL
       EtlInfo: unselected.rows=0; dpp.abnorm.ALL=0; dpp.norm.ALL=5
      TaskInfo: resource:N/A; timeout(s):3600; max_filter_ratio:0.0
      ErrorMsg: NULL
    CreateTime: 2023-09-23 12:44:38
  EtlStartTime: 2023-09-23 12:44:43
 EtlFinishTime: 2023-09-23 12:44:43
 LoadStartTime: 2023-09-23 12:44:43
LoadFinishTime: 2023-09-23 12:44:45
           URL: NULL
    JobDetails: {"All backends":{"467eaa1a-03c0-4012-a320-bd310bc32d8a":[10002],"5f6e6eae-ebc8-4577-afd2-8e5a742434d0":[10004]},"FileNumber":2,"FileSize":55,"InternalTableLoadBytes":181,"InternalTableLoadRows":5,"ScanBytes":55,"ScanRows":5,"TaskNumber":2,"Unfinished backends":{"467eaa1a-03c0-4012-a320-bd310bc32d8a":[],"5f6e6eae-ebc8-4577-afd2-8e5a742434d0":[]}}
1 row in set (0.004 sec)
```


For descriptions of the response parameters, refer to the StarRocks community official website [SHOW LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/SHOW_LOAD). Here, `Type: BROKER` indicates that the Load belongs to BROKER Load.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">Import job\-related information is time\-sensitive, with a default validity of 3 days after job completion. You can modify the default validity period (unit: seconds) via the FE parameter <code>label_keep_max_second</code>.</div>


2. <div data-tips="true" data-tips-type="tip">If the <code>LoadStartTime</code> of the import job remains <code>N/A</code> for a long time, it indicates a severe backlog of import jobs. You can reduce the frequency of job creation.</div>


3. <div data-tips="true" data-tips-type="tip">Total duration consumed by the import job = <code>LoadFinishTime</code> \- <code>CreateTime</code>.</div>


4. <div data-tips="true" data-tips-type="tip">Duration consumed in the <code>LOAD</code> phase = <code>LoadFinishTime</code> \- <code>LoadStartTime</code>.</div>


* **Using the curl command**


```sql
curl --location-trusted -u <username>:<password> \
    'http://<fe_host>:<fe_http_port>/api/<database_name>/_load_info?label=<label_name>'
```


<span id="_2-2-3-取消导入任务"></span>
#### 2.2.3 Cancel import tasks

When the Broker Load job status is not CANCELLED or FINISHED, you can manually cancel it by executing the [CANCEL LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/CANCEL_LOAD) command. When canceling, you need to specify the Label of the import task to be canceled.

Syntax:

```sql
CANCEL LOAD
[FROM db_name]
WHERE LABEL = "label_name"
```


<span id="_2-3-相关配置项"></span>
### 2.3 Related configuration items

A Broker Load job is split into one or more subtasks for parallel processing. All subtasks of a job succeed or fail as a single transaction. The splitting of a job is specified by the `LOAD LABEL` statement's `data_desc` parameter:


* If multiple `data_desc` parameters are declared to import data into different tables, the import of each table's data is split into a subtask.

* If multiple `data_desc` parameters are declared to import data into different partitions of the same table, the import of each partition's data is split into a subtask.


Each subtask is further split into one or more instances, which are then evenly distributed across the BEs for parallel execution. The splitting of instances is determined by the following FE configurations:


|Parameter |Description |
|---|---|
|min_bytes_per_broker_scanner |The minimum amount of data processed by a single instance. The default is 64 MB. |
|load_parallel_instance_num |The number of concurrent instances allowed per job on a single BE. The default is 1.<br><br>Total number of instances for a single subtask = min (total size of data to be imported for a single subtask / `min_bytes_per_broker_scanner`, `load_parallel_instance_num` times the total number of BEs). |
|max_broker_load_job_concurrency |Specifies the maximum number of Broker Load jobs that can be executed concurrently in the StarRocks cluster. The default value is 5. |


Typically, a job has only one DataDescription and is split into a single task. The task is split into instances equal to the number of BEs, then distributed to all BEs for parallel execution.

<span id="_3-导入示例"></span>
## 3 Import examples

<span id="_3-1-从-hdfs-导入"></span>
### 3.1 Import from HDFS

This example demonstrates how to create a Multi\-Table Load job using CSV data format and explains how to import multiple data files into multiple target tables. For information on importing other data formats, as well as detailed syntax and parameter descriptions for Broker Load, see [BROKER LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/BROKER_LOAD).


1. Run in the HDFS cluster

   1. Create a data file named `file1.csv` with the following test data:

      ```plain
      1,Lily,23
      2,Rose,23
      3,Alice,24
      4,Julia,25
      ```
      

   2. Create a data file named `file2.csv` with the following test data

      ```sql
      200,'北京'
      ```
      

   3. Upload the above CSV data to HDFS in the HDFS cluster

      ```shell
      hdfs dfs -mkdir -p /user/hive/data/
      hdfs dfs -put file1.csv /user/hive/data/
      hdfs dfs -put file2.csv /user/hive/data/
      ```
      

2. Create the StarRocks target database and tables in the EMR StarRocks cluster

   1. Create a primary key model table named `table1`. The table contains three columns: `id`, `name`, and `score`.

   ```sql
   CREATE DATABASE IF NOT EXISTS test_db;
   USE test_db;
   CREATE TABLE `table1`
   (
       `id` int(11) NOT NULL COMMENT "用户 ID",
       `name` varchar(65533) NULL DEFAULT "" COMMENT "用户姓名",
       `score` int(11) NOT NULL DEFAULT "0" COMMENT "用户得分"
   )
       ENGINE=OLAP
       PRIMARY KEY(`id`)
       DISTRIBUTED BY HASH(`id`);
   ```
   

   3. Create a primary key model table named `table2`. The table contains two columns: `id` and `city`.

   ```sql
   CREATE TABLE `table2`
   (
       `id` int(11) NOT NULL COMMENT "城市 ID",
       `city` varchar(65533) NULL DEFAULT "" COMMENT "城市名称"
   )
       ENGINE=OLAP
       PRIMARY KEY(`id`)
       DISTRIBUTED BY HASH(`id`);
   ```
   

3. Execute the import job SQL operation in the StarRocks cluster

   ```sql
   LOAD LABEL test_db.label1
   (
       DATA INFILE("hdfs://<hdfs_host>:<hdfs_port>/user/hive/data/file1.csv")
       INTO TABLE table1
       COLUMNS TERMINATED BY ","
       (id, name, score)
       ,
       DATA INFILE("hdfs://<hdfs_host>:<hdfs_port>/user/hive/data/file2.csv")
       INTO TABLE table2
       COLUMNS TERMINATED BY ","
      (id, city)
   )
   WITH BROKER
   (
       StorageCredentialParams
   )
   PROPERTIES
   (
       "timeout" = "3600"
   );
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>StorageCredentialParams</code> represents a set of authentication parameters. The content must be determined according to the authentication method you use. For details, see <a href="https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/BROKER_LOAD">BROKER LOAD</a>.</div>



4. View the import tasks

   ```sql
   SHOW LOAD \G;
   ```
   


Or use the Curl command:

```sql
curl --location-trusted -u <username>:<password> \
    'http://<fe_host>:8030/api/test_db/_load_info?label=label1'
```


The returned information is as follows:

```json
{"jobInfo":{"dbName":"test_db","tblNames":["table2","table1"],"label":"label1","state":"FINISHED","failMsg":"","trackingUrl":"\\N"},"status":"OK","msg":"Success"}
```



5. View the data in the tables

   ```sql
   SELECT * FROM table1;
   SELECT * FROM table2;
   ```
   


<span id="_3-2-从-火山云tos中-导入"></span>
### 3.2 Import from Volcano Engine TOS

You can also specify to import a single data file or all data files under a path into a target table. Assume that your TOS storage space `bucket_s3` contains multiple data files in the `input` folder, and one of the data files is named `file1.csv`. These data files have the same number of columns as the target table `table1`, and the columns correspond one\-to\-one in order to those in the target table `table1`.


1. Upload `file1.csv` mentioned above to TOS.

2. Import the TOS file `file1.csv` into table1.


```SQL
TRUNCATE TABLE test_db.table1;
LOAD LABEL tos.table1
(
    DATA INFILE("s3a://emr-autotest/doris/s3_load.csv")
    INTO TABLE table1
    COLUMNS TERMINATED BY ","
    (id, name, score)
)
WITH BROKER
(
    "aws.s3.enable_ssl" = "false",
    "aws.s3.endpoint" = "{S3 Endpoint}.ivolces.com"
    "aws.s3.secret_key" = "{secret key}"
    "aws.s3.access_key" = "{access key}"
)
PROPERTIES
(
    "timeout" = "36000"
);
```



3. View the import job status.


```sql
curl --location-trusted -u <username>:<password> \
    'http://<fe_host>:8030/api/test_db/_load_info?label=lable_3'
```
