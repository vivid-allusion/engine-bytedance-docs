---
title: "Instructions"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Instructions"
---

[Apache Iceberg](https://iceberg.apache.org/) is an open\-source table format for data lakes that enables fast queries on large tables, atomic commits, concurrent writes, and schema evolution.

<span id="_1-核心能力"></span>
## 1 Core capabilities

Currently, Iceberg provides the following core capabilities:


|Core capabilities |Note |
|---|---|
|Support for multiple open\-source compute engines |Mainstream open\-source compute engines such as Apache Hive, Apache Spark, Apache Flink, and Trino are all well integrated with Apache Iceberg for both reading and writing. |
|Near real\-time data change capability |Apache Iceberg provides Copy On Write data change capabilities in format v1 and row\-level Merge On Read data change capabilities in format v2.<br><br>This flexible data change capability effectively addresses the challenge that traditional offline data warehouses cannot update data at a fine granularity. |
|Support for ACID semantics |Apache Iceberg provides complete transaction semantics based on an optimistic locking mechanism, ensuring the atomicity of DDL and DML operations and addressing the issue of dirty writes that can occur in traditional Hive offline data warehouses, which may affect online analytical tasks. |
|Hidden partitioning |In Apache Iceberg, partition information can be hidden, and Iceberg's partition fields can be computed from a field (partition strategies can be referenced in [Partiton Transforms](https://docs.byteplus.com/docs/E-MapReduce/109271#partition-transforms)), so after creating a table or modifying the partition strategy, new data will automatically be assigned to the appropriate partition. When querying, there is no need to be concerned with which field is used for partitioning; users only need to focus on business logic, and Iceberg will automatically filter out unnecessary partition data. Hive also supports partitioning, but requires specifying partition filter conditions in SQL queries to accelerate query performance.<br><br>Additionally, Iceberg's partition information is independent from the table data storage directory, which allows Iceberg table partitions to be modified without involving data migration. |
|Schema evolution |Apache Iceberg supports adding columns, deleting columns, renaming columns, updating column properties, and adjusting column order, all by modifying metadata without changing data files, which greatly reduces the high cost of rewriting data. This also resolves the issue in Hive where renaming columns can lead to data accuracy problems. |
|Time travel and rollback |Apache Iceberg uses snapshots to record every operation on the table, allowing historical data to be queried based on snapshots. It also provides version rollback functionality, making it convenient to track and restore data. |
|Data compaction |Apache Iceberg provides multiple rewrite strategies, such as sorting, to achieve data redistribution and improve data query performance. |


<span id="_2-使用场景"></span>
## 2 Use cases

[Apache Iceberg](https://iceberg.apache.org/), as an open\-source table format for data lakes, is mainly applicable to the following use cases:

<span id="_2-1-传统离线数仓搬迁上云"></span>
### 2.1 Migrating traditional offline data warehouses to the cloud

When deploying offline data warehouses on\-premises, Hive is an ideal choice. However, to migrate Hive data warehouses to cloud object storage, users encounter a series of technical challenges:


* Rename operations on files take too long

* The atomicity semantics of rename operations cannot be guaranteed

* Listing files via list RPC is time\-consuming, and more.


In recent years, Apache Iceberg has effectively addressed these issues faced by Hive tables. Additionally, it offers richer table\-level semantics than Hive, making it highly suitable for building offline data warehouses on cloud object storage.

<span id="_2-2-近实时数据导入和分析"></span>
### 2.2 Near real\-time data ingestion and analysis

Data flows into the Iceberg data lake in real time from upstream, and the query side can immediately access this data.

For example, in log scenarios, Flink or Spark streaming jobs can be launched to ingest log data into Iceberg tables in real time, and then Hive, Spark, Flink, or Presto can be used for real\-time queries. At the same time, since Iceberg supports ACID, it ensures isolation between data ingestion and queries, preventing dirty data.

<span id="_2-3-高效地分析rdbms的cdc数据"></span>
### 2.3 Efficient analysis of CDC data from RDBMS

Efficient, near real\-time analysis of CDC data is a longstanding challenge in big data systems.

Apache Kudu is one of the few open\-source big data system candidates, but using and maintaining Kudu is relatively complex and it is not well integrated with the Apache Hadoop ecosystem. For many users, near real\-time analysis of CDC data is sufficient, and the pure real\-time solution provided by Apache Kudu is overly complex. Apache Iceberg provides a near real\-time solution for analyzing CDC data through both Copy on Write and Merge On Read implementations.

<span id="_2-4-实时机器学习"></span>
### 2.4 Real\-time machine learning

In typical machine learning scenarios, a significant amount of time is spent processing data, such as data cleaning, transformation, and feature extraction, as well as handling both historical and real\-time data. However, Iceberg streamlines the workflow, turning the entire data processing procedure into a complete and reliable real\-time stream, where operations such as data cleaning, transformation, and feature engineering are performed as node actions on the stream, eliminating the need to separately process historical and real\-time data. In addition, Iceberg supports a native Python SDK, making it very user\-friendly for machine learning algorithm developers.
