---
title: "Impala overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Impala_overview"
---

The Apache Impala project provides high\-performance, low\-latency SQL queries for data stored in Apache Hadoop file formats. It delivers fast query responses and supports interactive data exploration and query tuning for analytical queries, rather than the traditional long\-running batch jobs typically associated with SQL\-on\-Hadoop technologies.

Impala integrates with the Apache Hive database, sharing databases and tables between the two components. With its deep integration with Hive and compatibility with HiveQL syntax, you can use either Impala or Hive to create tables, initiate queries, load data, and more.

<span id="_1-impala-优点"></span>
## **1. Impala advantages**

To avoid latency, Impala does not use MapReduce. Instead, it employs a distributed query engine based on MPP architecture to access data directly.

Compared to SQL queries on Hadoop, Impala offers the following advantages:


* Supports SQL queries and enables fast querying of large datasets.

* Allows querying of existing data, reducing the need for data loading and transformation.

* Multiple storage formats are available for selection (Parquet, Text, Avro, RCFile, SequenceFile).

* Can be used in conjunction with Hive.


For more details about Impala, see [Apache Impala](https://impala.apache.org/overview.html).

<span id="_2-架构"></span>
## **2. Architecture**

The architecture of Impala in Volcano Engine E\-MapReduce (EMR) is shown below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2157f803b577b8dbfd6cfff9ea883704.png) </span>

The Impala components are as follows:


|Component |Note |
|---|---|
|**Impalad** |Deployed on core nodes and task nodes, allowing for scaling up and down.<br><br>Impalad is responsible for reading and writing data files, receiving query statements sent from interfaces such as `impala-shell` commands, Hue, JDBC, or ODBC, executing queries in parallel and distributing work tasks to each Impala node in the cluster, and also sending locally computed query results back to the Coordinator Node. |
|**Statestored** |Deployed on the master\-1 machine of the primary node.<br><br>Statestored manages the health status of all Impalad processes in the cluster and forwards the status results to all Impalad processes. When an Impalad process becomes unavailable due to node failures, network issues, or software problems, Statestored ensures that the status results are communicated to other Impalad processes. When new query requests are made, Impalad processes will not send queries to the unavailable node. |
|**Catalogd** |Deployed on the master\-1 machine of the primary node.<br><br>Catalogd synchronizes metadata changes on each Impalad process to other Impalad processes within the cluster. Since all requests are routed through the Statestored process, it is recommended to run Statestored and Catalogd on the same node. |
|**HaProxy** |Deployed on the master\-1 machine of the primary node.<br><br>Responsible for proxying connections to each Impalad node in the cluster and forwarding query requests. |
