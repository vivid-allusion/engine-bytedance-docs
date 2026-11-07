---
title: "Paimon overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Paimon_overview"
---

<span id="_1-paimon基本概念"></span>
## 1 Paimon basic concepts

Apache Paimon (incubating) is a streaming data lake platform that supports high\-speed data ingestion, change data tracking, and efficient real\-time analytics.

<span id="_2-架构"></span>
## 2 Architecture

**Read/write**: Paimon supports multiple methods for reading and writing data, as well as executing OLAP queries.


* For read operations, three methods are supported for consuming data:

   * From historical snapshots (batch mode)

   * From the latest offset (streaming mode)

   * Read incremental snapshots in a hybrid mode

* For write operations, Paimon supports streaming synchronization from database change logs (CDC), or batch insert/overwrite from offline data.


**Ecosystem**: In addition to Apache Flink, Paimon also supports reading with other compute engines such as Apache Hive, Apache Spark, and Trino.

**Internal**: Internally, Paimon stores column files on file systems or object storage and uses an LSM tree structure to support large\-scale data updates and high\-performance queries.

<span id="_3-统一存储"></span>
## 3 Unified storage

For streaming engines like Apache Flink, there are typically three types of connectors:


* Message queues, such as Apache Kafka, which are used at both the source and intermediate stages of the pipeline to ensure latency within seconds.

* OLAP systems, such as ClickHouse, which receive processed data in streaming mode and serve users' ad hoc queries.

* Batch storage, such as Apache Hive, which supports various traditional batch processing operations, including `INSERT OVERWRITE`.


Paimon provides a table abstraction. It is used in the same way as traditional databases:


* In `batch` execution mode, it acts like a Hive table and supports various batch SQL operations. Query it to view the latest snapshot.

* In `streaming` execution mode, it acts like a message queue. Querying it is like querying a streaming change log from a message queue, where historical data never expires.


<span id="_4-表类型"></span>
## 4 Table types

**Primary Key table (主键表)** 

When creating a table, the default table type is a changelog table (Primary Key table). Users can insert, update, or delete records in the table.

The primary key consists of a set of columns, and each record contains a unique value. Paimon enforces data ordering by sorting primary keys within each bucket, allowing users to achieve high performance by filtering by primary key.

**Append\-Only table (non\-primary key table)** 

If a table does not have a defined primary key, it is by default an Append\-Only table. Based on the bucket definition, there are two different append\-only modes: "append for scalable tables" and "append for queues".

You can only insert complete records into the table. Delete and update operations are not supported, and a primary key cannot be defined. This type of table is suitable for use cases that do not require updates, such as log data synchronization.

To create an Append\-Only table, specify 'bucket'='\-1' and do not specify a primary key when creating the table, as shown below:

```sql
CREATE TABLE MyTable (
    product_id BIGINT,
    price DOUBLE,
    sales BIGINT
) 
WITH ('bucket' = '-1');
```
