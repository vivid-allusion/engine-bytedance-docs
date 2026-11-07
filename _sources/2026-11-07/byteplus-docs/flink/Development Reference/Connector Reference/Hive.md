---
title: "Hive"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Hive"
---

The Hive connector provides read and write capabilities for Hive data sources; by using the Hive Catalog, Flink can perform uniform batch and stream processing of Hive tables. This means that Flink can be a better performing choice as a Hive batch processing engine, or for streaming data into Hive tables to support real\-time data warehouse applications.

<span id="0b82e2b9"></span>
## Usage Restrictions


* The Hive connector is currently only supported in the **Flink 1.16\-volcano** engine version.

* Stream writing to Hive does not support `insert overwrite`.


<span id="bdc48a50"></span>
## Table Creation Methods

In Flink SQL syntax, data tables are expressed in a three\-part form: `Catalog`.`Database`.`Table`. In relation to Hive data sources, the Catalog is the Hive Catalog.

For stream writing Hive tables, table parameters need to be set, see [流写的表级别参数](https://docs.byteplus.com/docs/flink/Hive#70d03e08).

<span id="f13623ac"></span>
## Parameter

<span id="30a21cbf"></span>
### Parameters for batch read and write job level


|**Parameters** |**Mandatory** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|table.exec.hive.fallback\-mapred\-reader |No |true |Boolean |Set the parameter that enables vectorized reading.<br><br>When the following conditions are met, Flink will automatically vectorize reading from Hive tables:<br><br><br>* Format: ORC or Parquet.<br><br>* There are no columns with complex types, such as Hive column types: List, Map, Struct, Union.<br><br><br>This feature is enabled by default; to disable it, set it to false. |
|table.exec.hive.infer\-source\-parallelism |no |true |Boolean |Set whether to enable Source concurrent inference. By default, Flink determines the optimal parallelism for reading Hive based on the number of files and the number of blocks in each file.<br><br>Flink allows flexible configuration of concurrency inference strategies.<br><br>If this parameter is true, the concurrency of the source will be inferred based on the number of splits. If it is false, the concurrency of the source is determined by the configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter will affect all Hive sources in the current job.</div><br> |
|table.exec.hive.infer\-source\-parallelism.max |No |1000 |Integer |Set the maximum concurrency for inferring source operators.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter affects all Hive sources for the current job.</div><br> |
|table.exec.hive.split\-max\-size |No |128mb |MemorySize |Set the data shard size adjustment when reading Hive tables.<br><br>When reading Hive tables, data files will be split into several shards (splits), each shard representing a part of the data to be read. Slicing is the basic unit of task allocation and data parallel reading in Flink. Users can adjust the size of each slice through this parameter to optimize reading performance.<br><br>This parameter represents the maximum byte size each slice can contain when reading Hive tables (default is 128MB).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only applicable to Hive tables in ORC format.</div><br> |
|table.exec.hive.file\-open\-cost |No |4mb |MemorySize |This setting estimates the cost of opening a file when reading Hive tables, expressed in bytes, with a default of 4MB.<br><br>If this value is large, Flink will tend to divide the Hive tables into fewer slices, which is useful when the Hive tables contain many small files. Conversely, Flink will tend to split Hive tables into more shards, which helps to increase the parallelism of data reading.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only applicable to Hive tables in ORC format.</div><br> |
|table.exec.hive.calculate\-partition\-size.thread\-num |No |3 |Integer |Set the number of threads to calculate the size of all files under all partitions.<br><br>To adjust the size of data shards, Flink first calculates the size of all files under all partitions, but this can be time\-consuming when there are many partitions. By adjusting this parameter to a larger value, use more threads to speed up the process. |
|table.exec.hive.load\-partition\-splits.thread\-num |No |3 |Integer |Set the number of threads for splitting splits.<br><br>Flink uses multiple threads to concurrently split Hive partitions into multiple splits for reading. Configure the number of threads through this parameter to accelerate the split splitting process. |
|table.exec.hive.sink.statistic\-auto\-gather.enable |No |true |Boolean |Set whether to enable automatic collection of statistical information.<br><br>When using Flink to write to Hive tables, Flink automatically collects statistics on the written data and submits them to the Hive metastore by default. However, in some cases, you may not want to automatically collect statistics, as gathering these statistics can take some time. To prevent Flink from automatically collecting statistics, you can set this parameter to false.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Automatic collection of statistics is only supported in batch write mode; stream write mode does not currently support automatic collection of statistics.</div><br> |
|table.exec.hive.sink.statistic\-auto\-gather.thread\-num |No |3 |Integer |Set the number of threads for collecting statistical information.<br><br>For tables in Parquet or ORC format, to quickly collect statistics such as numRows/rawDataSize, Flink only reads the file's footer. However, when there are many files, this can also be time\-consuming. You can speed up the collection of statistics by setting this parameter to a larger value.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Automatic collection of statistics is only supported in batch write mode; stream write mode does not currently support automatic collection of statistics.</div><br> |


<span id="70d03e08"></span>
### Parameters for stream write at table level

The parameters for stream writing are at the table level; they need to be added to the table parameters when creating a table in Hive. These parameters are primarily table parameters of Filesystem, please see [Filesystem](https://docs.byteplus.com/docs/flink/Filesystem).

In addition, there are some parameters unique for streaming writes to Hive, as follows:


|**Parameter** |**Required** |**Default value** |**Data type** |**Description** |
|---|---|---|---|---|
|sink.partition\-commit.policy.kind |Yes |metastore,success\-file |String |Partition submission strategy: specifically, it notifies downstream that a certain partition has been completely written and is ready for reading, recommended settings are metastore, success\-file.<br><br><br>* **metastore**: Add partitions to the metadata. Only Hive supports the metastore strategy; the file system manages partitions through directory structure.<br><br>* **Success\-file**: Add a '_success' file in the directory; The two strategies above can be specified simultaneously: 'metastore,success\-file'.<br><br>* **Custom**: Create a submission strategy by specifying the class. Supports specifying multiple commit policies simultaneously: 'metastore, success\-file'. |


<span id="fe97201a"></span>
## **Example code**

The Hive Catalog in the example SQL is default_hive.

<span id="d96f36c4"></span>
### Batch read

```SQL
SELECT * FROM default_hive.db.table WHERE `date`='${date}'
```


<span id="5b4e0f76"></span>
### Batch write

```SQL
--Insert new data into a non-partitioned table
INSERT INTO default_hive.db.mytable SELECT 'Tom', 25; 
--Overwrite data in a non-partitioned table
INSERT OVERWRITE default_hive.db.mytable SELECT 'Tom', 25; 
--Insert new data into a partitioned table
INSERT INTO default_hive.db.myparttable PARTITION (`date`='${date}') SELECT 'Tom', 25; 
-- Overwrite data in a partitioned table
INSERT OVERWRITE default_hive.db.myparttable PARTITION (`date`='${date}') SELECT 'Tom', 25;
```


<span id="5be810b0"></span>
### Streaming Writing

Create a Hive table and add the streaming writing Hive\-related parameters to the table properties:

```SQL
CREATE TABLE db.hive_table (
  user_id STRING,
  order_amount DOUBLE
) PARTITIONED BY (dt STRING, hr STRING) STORED AS parquet TBLPROPERTIES (
  'partition.time-extractor.timestamp-pattern'='$dt $hr:00:00',
  'sink.partition-commit.trigger'='partition-time',
  'sink.partition-commit.delay'='1 h',
  'sink.partition-commit.policy.kind'='metastore,success-file'
);
```


Streaming writing Hive's Flink SQL:

```SQL
CREATE TABLE kafka_table (
  user_id STRING,
  order_amount DOUBLE,
  log_ts TIMESTAMP(3),
  WATERMARK FOR log_ts AS log_ts - INTERVAL '5' SECOND -- 在 TIMESTAMP 列声明 watermark。
) WITH (...);

INSERT INTO TABLE default_hive.db.hive_table 
SELECT user_id, order_amount, DATE_FORMAT(log_ts, 'yyyy-MM-dd'), DATE_FORMAT(log_ts, 'HH')
FROM kafka_table;
```
