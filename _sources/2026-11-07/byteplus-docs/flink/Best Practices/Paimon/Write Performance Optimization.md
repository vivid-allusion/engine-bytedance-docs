---
title: "Write Performance Optimization"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Write_Performance_Optimization"
---

This document aims to help users systematically understand Paimon's write performance tuning techniques and provide common optimization suggestions to enhance throughput and stability.

<span id="75adb7f2"></span>
## 1. Write Performance Optimization

Paimon's write performance is closely related to Flink's checkpoint mechanism. Here are some common optimization techniques:

<span id="b02ba352"></span>
### 1.1 Adjusting Flink Task Configuration Parameters


* **Checkpoint Interval**: Increase the checkpoint interval to reduce the frequency, thereby lowering write overhead.


<span id="a62f5ee1"></span>
### 1.2 Buffer Optimization


* **Increase Write Buffer**: Improve the data volume per write by increasing `write-buffer-size`.

* **Enable Spillable Write Buffer**: Enable `write-buffer-spillable` to allow the buffer to spill data to disk when memory is insufficient, preventing OOM.


<span id="514f0501"></span>
### Bucket Quantity Adjustment


* If the Fixed\-Bucket Mode is used, it is advised to adjust the number of buckets based on the data volume and cluster resources to avoid a shortage of buckets, which can lead to write hotspots. It is recommended to maintain the size of each bucket file at around 1GB.


<span id="c62045cd"></span>
### Changelog Producer Configuration


* **Changelog producer**: The option `changelog-producer` can be set to `lookup` or `full-compaction`, but both options can significantly impact write performance.

   * During **snapshot**/**full synchronization** phases, it is recommended to **disable** these options to improve write performance.

   * In the **incremental synchronization** phase, these options can be **re\-enabled** to support incremental data processing.


<span id="d7bd6eae"></span>
### Asynchronous Compaction


* If jagged fluctuations are observed in job input under backpressure, it may be due to uneven workload distribution among nodes. At this time, enabling **asynchronous compaction** and observing whether throughput improves can be beneficial.

   * Compaction operations are essentially asynchronous, but to achieve maximum write throughput without blocking write operations, the process can be made smoother. You can set the following configurations in the table WITH parameters:


```SQL
CREATE TABLE IF NOT EXISTS catalog_test.db_test.table_test (...)
WITH (
    -- Enable asynchronous compaction
    'num-sorted-run.stop-trigger' = '2147483647', 
    'sort-spill-threshold' = '10', 
    'changelog-producer.lookup-wait' = 'false', 
    ... 
);
```



* This fully asynchronous Compaction configuration generates more small files during peak write periods, gradually merging these files during low write periods to optimize read performance.


<span id="b5815816"></span>
## 2. Parallelism Configuration

The write parallelism of Paimon is closely related to the number of buckets, and it is recommended to follow these principles:


* **Sink Parallelism**: It is recommended to set the Sink parallelism equal to or less than the number of buckets, ideally equal.

* **Configuration Method**: Adjust the Sink's parallelism through the table property `sink.parallelism`. For example:


```SQL
CREATE TABLE IF NOT EXISTS catalog_test.db_test.table_test (...)
WITH ('sink.parallelism' = '16', ...);
```


<span id="263d2bbd"></span>
## 3. Local Merging

If the job has **Primary Key Data Skew** issues (for example, when an AGG table is used to count website page views, some popular pages may have significantly higher traffic), consider the following optimization methods:


* **Enable local merge**: Set `local-merge-buffer-size` to buffer and merge input records before data is partitioned into buckets.

* **Recommended value**: It is suggested to start tuning from 64 MB and optimize progressively.

> **Note**: Local merge does not currently support Change Data Capture data synchronization.


<span id="c0e21b32"></span>
## 4. File Format Selection

Paimon supports multiple file formats, each with trade\-offs between write performance and query performance.

<span id="565d4ce5"></span>
### 4.1 Row storage format (AVRO)


* **Advantages**: High writing throughput and excellent compression performance.

* **Disadvantages**: Poor query performance, especially when there are many columns in the table but only a few are queried, resulting in high IO overhead. In addition, the compression efficiency is low, resulting in higher storage costs.

* **Applicable scenarios**: Suitable for write\-intensive scenarios, not suitable for scenarios with frequent queries.

* **Configuration method**:


```SQL
CREATE TABLE IF NOT EXISTS catalog_test.db_test.table_test (...)
WITH ('file.format' = 'avro', 'metadata.stats-mode' = 'none', ...);
```


<span id="437d6c4f"></span>
### 4.2 Layered file format


* If you do not want to change all files to AVRO format, you can set only the top layers to AVRO format. For example:


```SQL
CREATE TABLE IF NOT EXISTS catalog_test.db_test.table_test (...)
WITH ('file.format.per.level' = '0:avro,1:avro', ...);
```


<span id="8085b9ee"></span>
## 5. File compression optimization

Paimon uses zstd compression algorithm by default (level 1), and compression performance can be optimized as follows:


* **Adjust the compression level**: Increase `file.compression.zstd-level` to improve the compression rate but reduce read and write speed. For example:


```SQL
CREATE TABLE IF NOT EXISTS catalog_test.db_test.table_test (...)
WITH ('file.compression.zstd-level' = '3', ...);
```


<span id="7dba2f78"></span>
## 6. Stability optimization

<span id="3b7d0076"></span>
### 6.1 Checkpoint timeout


* If the number of buckets or resources is insufficient, full compaction may cause checkpoint timeouts. Flink's default checkpoint timeout is 10 minutes; it is advisable to increase the timeout period appropriately based on business needs.


<span id="0189e35f"></span>
### 6.2 Initialization Acceleration for Writing


* During the initialization of writing, the bucket writers need to read all historical files. If the initialization time is too long, enabling `write-manifest-cache` to cache the read manifest data can speed up the initialization.


<span id="425ee477"></span>
## 7. Memory Optimization

Main memory occupancies during Paimon's writing process include:


1. **Write buffer**: Adjusted through `write-buffer-size`.

2. **Compression memory**: Adjust the number of sorted runs for merging through `num-sorted-run.compaction-trigger`.

3. **Large\-scale data reading**: Reduce the amount of data read at once through `read.batch-size`.

4. **ORC write to memory**: Adjust the batch size of ORC writes through `orc.write.batch-size`.


<span id="e1bbdbae"></span>
### 7.1 Dictionary encoding optimization


* **Parquet format**: Disable dictionary encoding to reduce memory consumption.


```SQL
CREATE TABLE IF NOT EXISTS catalog_test.db_test.table_test (...)
WITH ('parquet.enable.dictionary' = 'false', ...);
```



* **ORC format**: Disable dictionary encoding or specify certain columns to disable.


```SQL
CREATE TABLE IF NOT EXISTS catalog_test.db_test.table_test (...)
WITH ('orc.dictionary.key.threshold' = '0', 'orc.column.encoding.direct' = 'field1,field2');
```


<span id="b4967a94"></span>
### 7.2 Managed memory optimization


* If the Flink job does not depend on state, managed memory can be disabled to reduce memory overhead.

* Alternatively, use Flink managed memory to manage the write buffer.


```SQL
CREATE TABLE IF NOT EXISTS catalog_test.db_test.table_test (...)
WITH ('sink.use-managed-memory-allocator' = 'true', ...);
```


<span id="7ab186ff"></span>
## 8. Commit memory optimization

If a large amount of data is written, the Committer may consume a significant amount of memory. Optimization can be achieved through the following methods:


* **Fine\-grained resource management**: Enable Flink’s fine\-grained resource management feature and additionally increase the heap memory of the submitter. For example:


```SQL
CREATE TABLE IF NOT EXISTS catalog_test.db_test.table_test (...)
WITH ('sink.committer-memory' = '300m');
```


<span id="f81f8f40"></span>
## 9. Recommended Configuration Optimizations

By properly adjusting Flink’s configurations, parallelism, file formats, compression algorithms, and memory parameters, the write performance and stability of Paimon can be significantly enhanced. It is advised to gradually try the above\-mentioned optimization measures based on actual business scenarios and data characteristics to achieve optimal performance.

Finally, the following are commonly suggested configuration items for optimizing write performance in large\-scale scenarios:

```SQL
CREATE TABLE IF NOT EXISTS `${catalog_name}`.`${db_name}`.`${table_name}` (
    word varchar, -- Example field
    cnt bigint,
    PRIMARY KEY (word) NOT ENFORCED
) WITH (
    'bucket' = 'N',  -- It is recommended to use a fixed number of buckets. Increase the number of buckets as needed; ideally, each bucket stores around 1GB of data
    'sink.parallelism' = 'N', -- During backfill, it's recommended that the sink parallelism matches the number of buckets
    -- Enable asynchronous compaction
    'num-sorted-run.stop-trigger' = '2147483647', 
    'sort-spill-threshold' = '10', 
    'changelog-producer.lookup-wait' = 'false',  -- This parameter can be ignored when changelog-producer is set to 'none'
    -- Enable write buffer spill to disk to avoid OOM failures
    'write-buffer-spillable' = 'true',
    'changelog-producer' = 'none' -- Set to 'none' if downstream doesn't rely on changelog or during full sync phase
);
```
