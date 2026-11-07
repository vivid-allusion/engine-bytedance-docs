---
title: "Routine Load"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Routine_Load"
---

Routine Load is an asynchronous import method based on the MySQL protocol, supporting continuous consumption of Apache Kafka messages and importing them into StarRocks. This document introduces the basic principles of Routine Load and explains how to import data into StarRocks using Routine Load. The images and content in this document are sourced from open\-source StarRocks's [Continuous Import from Apache Kafka](https://docs.starrocks.io/zh/docs/loading/RoutineLoad).

<span id="_1-基本原理"></span>
## 1 Basic principles

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cd92a7518c547a8b414d7acd3840239d.png) </span>

The import process is as follows:


1. The client submits an SQL statement to the FE to create an import job. After parsing the SQL statement, the FE creates a persistent import job.

2. The FE splits the import job into several import tasks according to certain rules. Each import task acts as an independent transaction.

3. Each import task is assigned to a designated BE for execution.

4. After the BE completes the import task, it reports to the FE.

5. Based on the report results, the FE continues to generate new import tasks or retries failed import tasks, continuously importing data while ensuring that no data is lost or duplicated.


<span id="_2-导入流程"></span>
## 2 Import process

Routine Load supports accessing Kafka via no security authentication, SSL encryption and authentication, or SASL authentication mechanisms.

Routine Load supports consuming CSV and JSON format data from the Kafka cluster. For CSV format data: supports UTF\-8 encoded strings up to 50 bytes in length as column delimiters; null values are represented by `\N`.

<span id="_2-1-创建导入任务"></span>
### 2.1 Create import tasks

Create Routine Load import jobs using the [CREATE ROUTINE LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/CREATE_ROUTINE_LOAD) command.

Syntax:

```sql
CREATE ROUTINE LOAD [<database_name>.]<job_name> ON <table_name>
[load_properties]
[job_properties]
FROM data_source
[data_source_properties]
```


Parameter description:


|Parameter |Description |
|---|---|
|database_name |Optional. Name of the target database. |
|job_name |Required. Name of the import job. |
|table_name |Required. Name of the target table. |
|load_properties |Optional. Source data properties. For supported properties, see the StarRocks community [load_properties](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/CREATE_ROUTINE_LOAD#load_properties). |
|job_properties |Required. Import job properties. Syntax: `PROPERTIES ("<key1>" = "<value1>"[, "<key2>" = "<value2>" ...])`. See the StarRocks community [job_properties](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/CREATE_ROUTINE_LOAD#job_properties) introduction. |
|data_source |Required. Specify the data source. Currently, only `KAFKA` is supported. |
|data_source_properties |Required. Data source properties. See the StarRocks community [data_source_properties](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/CREATE_ROUTINE_LOAD#data_sourcedata_source_properties) introduction. |


<span id="_2-2-查看任务状态"></span>
### 2.2 View task status

View information about routine load tasks using the [SHOW ROUTINE LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/SHOW_ROUTINE_LOAD) command.


* Displays all Routine Load jobs (including stopped or canceled jobs), with results in one or more rows.


```sql
-- View all ROUTINE LOAD import jobs under a database
USE <db_name>;
SHOW ALL ROUTINE LOAD \G;

-- View a ROUTINE LOAD import job in a specific database
SHOW ROUTINE LOAD FOR <db_name>.<job_name>;
```


By executing the `SHOW ROUTINE LOAD` command, you can view all currently running Routine Load tasks, which returns information similar to the following.

```plain
*************************** 1. row ***************************
                  Id: 10160
                Name: example_tbl1_ordertest1
          CreateTime: 2023-09-23 10:43:47
           PauseTime: NULL
             EndTime: NULL
              DbName: example_db
           TableName: example_tbl1
               State: RUNNING
      DataSourceType: KAFKA
      CurrentTaskNum: 3
       JobProperties: {"partitions":"*","rowDelimiter":"\t","partial_update":"false","columnToColumnExpr":"order_id,pay_dt,customer_name,nationality,temp_gender,price","maxBatchIntervalS":"10","whereExpr":"*","timezone":"Asia/Shanghai","format":"csv","columnSeparator":"','","json_root":"","maxFilterRatio":"1.0","strict_mode":"false","jsonpaths":"","desireTaskConcurrentNum":"5","maxErrorNum":"0","strip_outer_array":"false","currentTaskConcurrentNum":"3","maxBatchRows":"200000"}
DataSourceProperties: {"topic":"ordertest1","currentKafkaPartitions":"0,1,2,3,4","brokerList":"192.168.10.17:9092"}
    CustomProperties: {"kafka_default_offsets":"OFFSET_BEGINNING","group.id":"example_tbl1_ordertest1_f205c7f5-bda9-4755-9e63-361eb8d774c2"}
           Statistic: {"receivedBytes":314,"errorRows":0,"committedTaskNum":2,"loadedRows":6,"loadRowsRate":0,"abortedTaskNum":2,"totalRows":6,"unselectedRows":0,"receivedBytesRate":0,"taskExecuteTimeMs":2068}
            Progress: {"0":"OFFSET_ZERO","1":"OFFSET_ZERO","2":"0","3":"0","4":"7"}
ReasonOfStateChanged: 
        ErrorLogUrls: 
            OtherMsg:
```


The relevant parameter descriptions are as follows:


* State: The status of the import task. RUNNING indicates that the import task is continuously running.

* Statistic: Progress information, recording import details since the task was created. Includes: size of received data, number of import error rows, number of imported rows, import data rate, total number of received rows, and other information.

* Progress: Consumption progress of each partition.


<span id="_2-3-暂停导入任务"></span>
### 2.3 Pause import tasks

After executing the [PAUSE ROUTINE LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/PAUSE_ROUTINE_LOAD) statement, the import job will be paused. The import job will enter the PAUSED state, but the import job is not finished. You can execute the [RESUME ROUTINE LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/RESUME_ROUTINE_LOAD) statement to restart the import job. You can also execute the [SHOW ROUTINE LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/SHOW_ROUTINE_LOAD) statement to view the status of the paused import job.

```sql
-- Pause the import job
PAUSE ROUTINE LOAD FOR <db_name>.<job_name>;
```


After pausing the import task, the task's `State` changes to `PAUSED`, and the import information in `Statistic` and `Progress` stops updating.

<span id="_2-4-恢复导入任务"></span>
### 2.4 Resume import task

Execute [RESUME ROUTINE LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/RESUME_ROUTINE_LOAD) to resume the import job. The import job will briefly enter the NEED_SCHEDULE state, indicating that the import job is being rescheduled. After a short period, it will return to the RUNNING state and continue consuming Kafka messages and importing data. You can execute the [SHOW ROUTINE LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/SHOW_ROUTINE_LOAD) statement to view the resumed import job.

```sql
-- Resume the import job
RESUME ROUTINE LOAD FOR  <db_name>.<job_name>;
```


<span id="_2-5-修改导入任务"></span>
### 2.5 Modify import task

Before making changes, you need to execute PAUSE ROUTINE LOAD to pause the import job. Then execute the [ALTER ROUTINE LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/ALTER_ROUTINE_LOAD/) statement to modify the parameter configuration of the import job. After the modification is successful, you need to execute [RESUME ROUTINE LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/RESUME_ROUTINE_LOAD) to resume the import job. Then execute the [SHOW ROUTINE LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/SHOW_ROUTINE_LOAD) statement to view the modified import job.

```sql
-- Modify the import job. For parameter descriptions, refer to the [ALTER ROUTINE LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/alter-routine-load) statement
ALTER ROUTINE LOAD FOR [db_name.]job_name
[load_properties]
[job_properties]
FROM data_source
[data_source_properties]
```


<span id="_2-6-停止导入任务"></span>
### 2.6 Stop import task

Execute [STOP ROUTINE LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/STOP_ROUTINE_LOAD) to stop the import job. The import job will enter the STOPPED state, indicating that the import job has ended and cannot be resumed. If you execute the SHOW ROUTINE LOAD statement again, you will not be able to see the stopped import job.

```sql
STOP ROUTINE LOAD FOR <job_name>;
```


<span id="_3-最佳实践案例"></span>
## 3 Best practice cases

<span id="_3-1-导入csv格式数据"></span>
### 3.1 Import CSV data


1. Perform the following operations in the Kafka cluster to prepare the source data

   1. Create topic

      ```shell
      /usr/lib/emr/current/kafka/bin/kafka-topics.sh --create --bootstrap-server `hostname -i`:9092 --topic ordertest1 --replication-factor 3 --partitions 10
      ```
      

   2. Execute Kafka data generation command

      ```shell
      /usr/lib/emr/current/kafka/bin/kafka-console-producer.sh --broker-list `hostname -i`:9092 --topic ordertest1
      ```
      

   3. In the console for the Kafka data generation command, enter the following test data.

      ```plain
      2020050802,2020-05-08,Johann Georg Faust,Deutschland,male,895
      2020050802,2020-05-08,Julien Sorel,France,male,893
      2020050803,2020-05-08,Dorian Grey,UK,male,1262
      2020050901,2020-05-09,Anna Karenina,Russia,female,175
      2020051001,2020-05-10,Tess Durbeyfield,US,female,986
      2020051101,2020-05-11,Edogawa Conan,japan,male,8924
      ```
      

2. Perform the action to import Kafka data in the StarRocks cluster.

   1. Create the target database and table

      Based on the columns in the CSV data that need to be imported (for example, import five columns except for the fifth column (gender) into StarRocks), create the target database and target table in the StarRocks cluster.

      ```sql
      CREATE DATABASE IF NOT EXISTS example_db;
      CREATE TABLE example_db.example_tbl1 ( 
          `order_id` bigint NOT NULL COMMENT "订单编号",
          `pay_dt` date NOT NULL COMMENT "支付日期", 
          `customer_name` varchar(26) NULL COMMENT "顾客姓名", 
          `nationality` varchar(26) NULL COMMENT "国籍", 
          `price`double NULL COMMENT "支付金额"
      ) 
      ENGINE=OLAP 
      DUPLICATE KEY (order_id,pay_dt) 
      DISTRIBUTED BY HASH(`order_id`) BUCKETS 5;
      ```
      

   2. Execute the import job

      Submit a Routine Load import job to start consuming data continuously from the earliest offset of the specified partition in the Kafka topic.

      ```sql
      CREATE ROUTINE LOAD example_db.example_tbl1_ordertest1 ON example_tbl1
      COLUMNS TERMINATED BY ",",
      COLUMNS (order_id, pay_dt, customer_name, nationality, temp_gender, price)
      PROPERTIES
      (
          "desired_concurrent_number" = "5"
      )
      FROM KAFKA
      (
          "kafka_broker_list" ="192.168.**.**:9092,192.168.**.**:9092,192.168.**.**:9092",
          "kafka_topic" = "ordertest1",
          "kafka_partitions" ="0,1,2,3,4",
          "property.kafka_default_offsets" = "OFFSET_BEGINNING"
      );
      ```
      


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">```Plain
  1. temp_gender字段属于占位，使得CSV中数据中列和目标表中的列名对应。
```
</div>



2. <div data-tips="true" data-tips-type="tip">The desired_concurrent_number parameter: Import concurrency, specifies the maximum number of sub\-tasks an import task can be divided into. This is an optional parameter, with a default value of 3. Supported job parameters can be found in the StarRocks community <a href="https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/CREATE_ROUTINE_LOAD#job_properties">job_properties</a>.</div>


3. <div data-tips="true" data-tips-type="tip">The kafka_partitions parameter: Partitions to be consumed. This is an optional parameter; by default, all partitions are consumed.</div>


4. <div data-tips="true" data-tips-type="tip">The kafka_offsets parameter: The starting offset for consuming the partition.</div>



c. View information about the import task

```sql
SHOW ROUTINE LOAD FOR example_db.example_tbl1_ordertest1;
```


d. Query the data in the target table to confirm that synchronization is complete

```sql
SELECT count(*) from example_db.example_tbl1;
```


e. You can also perform the following actions on the import task:


* Pause the import task.


```sql
PAUSE ROUTINE LOAD FOR example_db.example_tbl1_ordertest1;
```



* Modify the import task.


```sql
ALTER ROUTINE LOAD FOR example_db.example_tbl1_ordertest1
PROPERTIES
(
    "desired_concurrent_number" = "1"
);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">```Plain
  仅支持修改状态为PAUSED的任务。
```
</div>



* Resume import task


```sql
RESUME ROUTINE LOAD FOR example_db.example_tbl1_ordertest1;
```



* Stop import task


```sql
STOP ROUTINE LOAD FOR example_db.example_tbl1_ordertest1;
```


<span id="_3-2-导入json格式数据"></span>
### 3.2 Import JSON format data


1. Perform the following operations in the Kafka cluster to prepare the source data

   1. Create topic

      ```shell
      /usr/lib/emr/current/kafka/bin/kafka-topics.sh --create --bootstrap-server `hostname -i`:9092 --topic ordertest2 --replication-factor 3 --partitions 10
      ```
      

   2. Execute Kafka data generation command

      ```shell
      /usr/lib/emr/current/kafka/bin/kafka-console-producer.sh --broker-list `hostname -i`:9092 --topic ordertest2
      ```
      

   3. In the console for the Kafka data generation command, enter the following test data in JSON format

      Each line must contain one JSON object in a single Kafka message; otherwise, a "JSON parsing error" will occur

      ```plain
      {"commodity_id": "1", "customer_name": "Mark Twain", "country": "US","pay_time": 1589191487,"price": 875}
      {"commodity_id": "2", "customer_name": "Oscar Wilde", "country": "UK","pay_time": 1589191487,"price": 895}
      {"commodity_id": "3", "customer_name": "Antoine de Saint-Exupéry","country": "France","pay_time": 1589191487,"price": 895}
      ```
      

2. Perform the action to import Kafka data in the StarRocks cluster.

   1. Create the target database and table

      Based on the columns in the CSV data that need to be imported (for example, import five columns except for the fifth column (gender) into StarRocks), create the target database and target table in the StarRocks cluster.

   ```sql
   USE example_db;
   CREATE TABLE `example_tbl2` ( 
       `commodity_id` varchar(26) NULL COMMENT "品类ID", 
       `customer_name` varchar(26) NULL COMMENT "顾客姓名", 
       `country` varchar(26) NULL COMMENT "顾客国籍", 
       `pay_time` bigint(20) NULL COMMENT "支付时间", 
       `pay_dt` date NULL COMMENT "支付日期", 
       `price`double SUM NULL COMMENT "支付金额"
   )
   ENGINE=OLAP
   AGGREGATE KEY(`commodity_id`,`customer_name`,`country`,`pay_time`,`pay_dt`) 
   DISTRIBUTED BY HASH(`commodity_id`) BUCKETS 5;
   ```
   

   2. Execute the import job

      Submit a Routine Load import job to continuously consume data from the earliest offset of the specified partition in the Kafka topic


```sql
CREATE ROUTINE LOAD example_db.example_tbl2_ordertest2 ON example_tbl2
COLUMNS(commodity_id, customer_name, country, pay_time, price, pay_dt=from_unixtime(pay_time, '%Y%m%d'))
PROPERTIES
(
    "desired_concurrent_number"="5",
    "format" ="json",
    "jsonpaths" ="[\"$.commodity_id\",\"$.customer_name\",\"$.country\",\"$.pay_time\",\"$.price\"]"
 )
FROM KAFKA
(
    "kafka_broker_list" ="192.168.**.**:9092,192.168.**.**:9092,192.168.**.**:9092",
    "kafka_topic" = "ordertest2",
    "kafka_partitions" ="0,1,2,3,4",
    "property.kafka_default_offsets" = "OFFSET_BEGINNING"
);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">The pay_dt field: This field is imported after converting the <code>pay_time</code> key from the source data to the DATE type. For more notes on data conversion, see <a href="https://docs.starrocks.io/zh/docs/loading/Etl_in_loading">Data conversion during import</a>.</div>


2. <div data-tips="true" data-tips-type="tip">The jsonpaths parameter: Specifies the key of the JSON data to be imported.</div>


3. <div data-tips="true" data-tips-type="tip">If the outermost layer of the JSON data is an array structure, set <code>PROPERTIES</code> with <code>"strip_outer_array"="true"</code> to trim the outermost array structure. Important: When setting <code>jsonpaths</code>, the root node of the entire JSON data is the flattened JSON object after trimming the outermost array structure.</div>


4. <div data-tips="true" data-tips-type="tip">If you do not need to import the entire JSON data, use <code>json_root</code> to specify the actual root node of the JSON data to be imported.</div>



c. View information about the import task

```sql
USE example_db;
SHOW ROUTINE LOAD FOR example_tbl2_ordertest2 \G;
```


d. Query the data in the target table to confirm that synchronization is complete

```sql
SELECT count(*) from example_db.example_tbl2;
```
