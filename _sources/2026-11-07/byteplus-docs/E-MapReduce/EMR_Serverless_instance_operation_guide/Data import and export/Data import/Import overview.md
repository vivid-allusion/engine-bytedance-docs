---
title: "Import overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Import_overview"
---

Data import refers to the process of cleaning, transforming, and loading raw data into Volcano Engine StarRocks according to business requirements.

This article introduces different data import methods. The images in this article are sourced from the open\-source StarRocks [Import Overview](https://docs.starrocks.io/zh/docs/loading/Loading_intro).

<span id="_1-背景信息"></span>
## 1. Context

StarRocks implements data import through import jobs. Each import job has a label (Label), and based on the uniqueness of the label, provides "At\-Most\-Once" semantics.

StarRocks offers multiple import methods. You can select the method that best meets your business requirements based on factors such as data volume or import frequency. The relationship diagram between StarRocks import methods and various data sources is as follows.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8c942551f9445ae3b11e6310267396cb.png) </span>

You can choose different import methods according to different data sources:


|**Scenario** |**Description** |
|---|---|
|Real\-time data import |After synchronizing log data and business database Binlog to Kafka, it is recommended to use [Routine Load](https://docs.starrocks.io/zh/docs/loading/RoutineLoad) to import. However, if there are complex multi\-table joins and ETL preprocessing during the import process, it is recommended to first process the data using Apache Flink, and then import it into StarRocks via [flink-connector-starrocks](https://docs.starrocks.io/zh/docs/loading/Flink-connector-starrocks). |
|Offline data import |If the data source is Hive or HDFS, it is recommended to use [Broker Load](https://docs.starrocks.io/zh/docs/loading/BrokerLoad). When importing a large number of tables, such as importing data from Hive, Iceberg, Hudi, or Delta Lake, it is recommended to create a [Hive catalog](https://docs.starrocks.io/zh/docs/data_source/catalog/hive_catalog), [Iceberg catalog](https://docs.starrocks.io/zh/docs/data_source/catalog/iceberg_catalog), [Hudi Catalog](https://docs.starrocks.io/zh/docs/data_source/catalog/hudi_catalog), [Delta Lake Catalog](https://docs.starrocks.io/zh/docs/data_source/catalog/deltalake_catalog), and then use [INSERT](https://docs.starrocks.io/zh/docs/loading/InsertInto) to import. |
|When importing data from another StarRocks cluster or from Elasticsearch |It is recommended to create a [StarRocks external table](https://docs.starrocks.io/zh/docs/data_source/External_table#starrocks-%E5%A4%96%E9%83%A8%E8%A1%A8) or [Elasticsearch external table](https://docs.starrocks.io/zh/docs/data_source/External_table#elasticsearch-%E5%A4%96%E9%83%A8%E8%A1%A8), and then use [INSERT](https://docs.starrocks.io/zh/docs/loading/InsertInto) to import.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">StarRocks external tables only support data writing, not data reading.</div><br> |
|MySQL data import |It is recommended to create a [MySQL external table](https://docs.starrocks.io/zh/docs/data_source/External_table#mysql-%E5%A4%96%E9%83%A8%E8%A1%A8), and then use [INSERT](https://docs.starrocks.io/zh/docs/loading/InsertInto) to import. To import real\-time data, refer to [real-time synchronization from MySQL](https://docs.starrocks.io/zh/docs/loading/Flink_cdc_load). |
|Internal import in StarRocks |It is recommended to use [INSERT](https://docs.starrocks.io/zh/docs/loading/InsertInto) to import. |
|Local files |It is recommended to use [Stream Load](https://docs.starrocks.io/zh/docs/loading/Stream_Load_transaction_interface). |


<span id="_2-导入方式"></span>
## 2. **Import methods**

StarRocks provides multiple import methods, including [Stream Load](https://docs.starrocks.io/zh/docs/loading/StreamLoad), [Broker Load](https://docs.starrocks.io/zh/docs/loading/BrokerLoad), [Routine Load](https://docs.starrocks.io/zh/docs/loading/RoutineLoad), [Spark Load](https://docs.starrocks.io/zh/docs/loading/SparkLoad), and [INSERT](https://docs.starrocks.io/zh/docs/loading/InsertInto), to meet your data import needs in various business scenarios.

The data import modes in StarRocks are divided into two models: synchronous import and asynchronous import. Different import methods use different import models.

<span id="_2-1-导入方式介绍"></span>
### 2.1 **Introduction to import methods**


|**Import method** |**Description** |**Supported data sources** |**Data volume**<br><br> **(single job)**  |**Data format** |**Synchronous mode** |**Protocol** |
|---|---|---|---|---|---|---|
|Stream Load |You can send requests via the HTTP protocol to import local files or data streams into StarRocks, and wait for the system to return the import result status to determine whether the import was successful. |* Local files<br><br>* Streaming data |Within 10 GB |* CSV<br><br>* JSON |Synchronous |HTTP |
|Broker Load |Access and read external data sources through the Broker process. |* HDFS<br><br>* External cloud storage system |Tens to hundreds of GB |* CSV<br><br>* Parquet<br><br>* ORC |Asynchronous |MySQL |
|Routine Load |Provides a feature for automatically importing data from specified data sources. Submit import jobs via the MySQL protocol, generate a resident thread, and continuously read data from the data source and import it into StarRocks. |Apache Kafka |Micro\-batch import from MB to GB scale |* CSV<br><br>* JSON |Asynchronous |MySQL |
|INSERT INTO SELECT |External table import. Data import between StarRocks tables. |StarRocks external table |Memory\-related |StarRocks table |Synchronous |MySQL |
|INSERT INTO VALUES |Single or batch insertion of small amounts of data. Import via JDBC and other interfaces. |Program ETL tool |For simple testing |SQL |Synchronous |MySQL |


<span id="_2-2-导入模型介绍"></span>
### 2.2 **Introduction to import models**

StarRocks supports two import modes: **synchronous import** and **asynchronous import.** 

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If an external program connects to the import functionality of StarRocks, it is necessary to first determine the type of import method used, and then decide on the integration logic.</div>



* **Synchronous import**

   Synchronous import means that after you create an import job, StarRocks executes the job synchronously and returns the import result after the job is completed. You can determine whether the import job was successful based on the returned import result. The import methods that support synchronous mode are Stream Load and INSERT.

   **Procedure:** 

   1. The user (external system) creates an import task.

   2. StarRocks returns the import result.

   3. The user (external system) determines the import result. If the import result is a failure, you can create the import task again.

* **Asynchronous import**

   Asynchronous import means that after you create an import job, StarRocks directly returns the job creation result.

   * If the import job is created successfully, StarRocks will execute the import job asynchronously. However, successful job creation does not mean that the data import has succeeded. You need to use statements or commands to check the status of the import job, and determine whether the data import was successful based on the status of the import job.

   * If the import job creation fails, you can determine whether a retry is needed based on the failure information.

      procedure:

   1. Create an import job.

   2. Determine whether the job was created successfully based on the job creation result returned by StarRocks.

      * If the job is created successfully, proceed to step 3 below.

      * If the job creation fails, return to step 1 above and retry the import job.

   3. Poll to check the status of the import job until the status changes to FINISHED or CANCELLED.


<span id="_2-3-支持的数据类型"></span>
### 2.3 Supported data types

StarRocks basically supports importing all data types:


|**Type** |**Description** |
|---|---|
|Integer type |TINYINT、SMALLINT、INT、BIGINT、LARGEINT |
|Floating\-point type |FLOAT、DOUBLE、DECIMAL |
|Date type |DATE、DATETIME |
|String type |CHAR、VARCHAR |


<span id="_3-使用说明"></span>
## 3 Usage note

<span id="_3-1-内存限制"></span>
### 3.1 **Memory limit**

You can set parameters to limit the memory usage of a single import job to prevent the import from consuming excessive memory and causing the system to run out of memory (OOM). Also avoid setting the memory limit too low, which can affect import efficiency, as reaching the memory limit may cause frequent flushing of in\-memory data to disk.

The methods for limiting memory differ slightly depending on the import method. For details, see [Stream Load](https://docs.starrocks.io/zh/docs/loading/StreamLoad), [Broker Load](https://docs.starrocks.io/zh/docs/loading/BrokerLoad), [Routine Load](https://docs.starrocks.io/zh/docs/loading/RoutineLoad), [Spark Load](https://docs.starrocks.io/zh/docs/loading/SparkLoad), and [INSERT](https://docs.starrocks.io/zh/docs/loading/InsertInto).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">An import job is usually executed across multiple BEs. These memory parameters limit the memory usage of an import job on a single BE, rather than the total memory usage across the entire cluster.</div>


<div data-tips="true" data-tips-type="warning">You can also set certain parameters to limit the total memory usage of all import jobs running on a single BE. Refer to the section below, "General system configuration."</div>


<span id="_3-2-通用系统配置"></span>
### 3.2 **General system configuration**

This section explains parameter configurations applicable to all import methods.


* **FE configuration**

   The following configurations are system configurations for FE and can be modified through the FE configuration file fe.conf.

   
   |Parameter |Description |
   |---|---|
   |max_load_timeout_second |The maximum and minimum values for import timeout. Unit: seconds. The default maximum timeout is 3 days, and the default minimum timeout is 1 second.<br><br>The custom import timeout cannot exceed the range defined by these maximum and minimum values. This parameter configuration applies to import jobs in all modes. |
   |min_load_timeout_second ||
   |desired_max_waiting_jobs |The maximum number of import jobs that the waiting queue can accommodate. The default value is 1024.<br><br>If the number of import jobs in PENDING status in FE reaches the maximum limit, FE will reject new import requests. This parameter configuration is only effective for asynchronously executed imports. |
   |max_running_txn_num_per_db |The maximum number of ongoing import transactions in each database, regardless of import type and counted uniformly, is 100 by default.<br><br>When the number of ongoing import transactions in the database reaches the maximum value, subsequent submitted import jobs will not be executed. If the import job is synchronous, the job will be rejected; if the import job is asynchronous, the job will wait in the queue. |
   |label_keep_max_second |The retention time for import task records.<br><br>The retention period for completed import job records in the FINISHED or CANCELLED state in the StarRocks system is 3 days by default. This parameter applies to all types of import tasks. |
   

* **BE configuration**

   The following configurations are system configurations for BE and can be modified through the BE configuration file be.conf.

   
   |Parameter |Description |
   |---|---|
   |push_write_mbytes_per_sec |The maximum write speed for a single Tablet on the BE is 10 MB/s by default.<br><br>Depending on the table schema, the maximum write speed for a single Tablet on the BE is typically between 10 MB/s and 30 MB/s. The value of this parameter can be adjusted as needed to control the import speed. |
   |write_buffer_size |Imported data is first written to a memory block on the BE. When the memory block size reaches the threshold, it is then written back to disk. The default threshold is 100 MB.<br><br><br>* If the threshold is too small, a large number of small files may exist on the BE, affecting query performance.<br><br>* If the threshold is too large, it may cause RPC timeout. This can be adjusted together with the `tablet_writer_rpc_timeout_sec` parameter below. |
   |tablet_writer_rpc_timeout_sec |The RPC timeout for sending a batch (1024 rows) during the import process is specified by this parameter. The default value is 600 seconds.<br><br>RPC may involve writing multiple shard memory blocks to disk, which can cause RPC timeout due to disk write operations. This timeout can be adjusted as needed. If the `write_buffer_size` parameter is increased, the `tablet_writer_rpc_timeout_sec` parameter should also be increased accordingly. |
   |streaming_load_rpc_max_alive_time_sec |During the import process, StarRocks starts a Writer process for each Tablet to receive and write data. This parameter specifies the waiting timeout for the Writer process, with a default value of 600 seconds.<br><br>If the Writer process does not receive any data within the time specified by the parameter, the StarRocks system will automatically destroy the Writer process. When the system processing speed is slow, the Writer process may not receive the next batch of data for an extended period, resulting in the "TabletWriter add batch with unknown id" error. The value of this parameter can be increased as needed. |
   |load_process_max_memory_limit_bytes |These are used for the maximum memory and maximum memory usage percentage for import, and are used to limit the total memory usage of all import jobs on a single BE. The system will use the smaller value of the two parameters as the final usage limit.<br><br><br>* load_process_max_memory_limit_bytes: The default is 100 GB.<br><br>* load_process_max_memory_limit_percent: Indicates the percentage of the total memory limit for BE, with a default of 30%. |
   |load_process_max_memory_limit_percent ||
   


<span id="_4-常见问题"></span>
## 4 FAQs

For exceptions and solutions that may be encountered during data import, see [Import FAQs](https://docs.starrocks.io/zh/docs/faq/loading/Loading_faq).
