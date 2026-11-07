---
title: "Doris overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Doris_overview"
---

Apache Doris is a modern MPP analytical database product. Query results can be obtained with sub\-second response times, enabling efficient real\-time data analysis. The distributed architecture of Apache Doris is highly streamlined, easy to operate and maintain, and can support ultra\-large datasets exceeding 10 PB.

Apache Doris meets a variety of data analysis needs, such as fixed historical reports, real\-time data analysis, interactive data analysis, and exploratory data analysis.

<span id="_1-doris-功能特点"></span>
## **Doris features**


|Features |Note |
|---|---|
|**MySQL protocol compatibility** |Doris is compatible with the MySQL connection protocol, allowing users to directly connect to and access the Doris cluster using MySQL\-related libraries or tools.<br><br>Compatible with higher\-level applications, reducing the user learning curve and making it easy for users to get started. |
|**Modern MPP architecture** |Doris uses an MPP distributed computing architecture for task processing, enabling efficient execution of aggregation, sorting, join, and other computational tasks. Doris supports complex joins and multi\-level nested subqueries. |
|**Data updates** |Doris supports deleting and updating data by primary key.<br><br>It is easy to synchronize real\-time updated data from relational databases such as MySQL. |
|**High availability and high reliability** |Both the metadata of FE and the data of BE in Doris have a replication mechanism.<br><br>FE nodes use a primary\-secondary approach, with metadata distributed to all FE instances.<br><br>Data in BE is replicated, and it is generally recommended to use three replicas. In the event of partial node failures, Doris can ensure high availability of services and high reliability of data. |
|**Simplified operations and maintenance, elastic scalability** |Both FE nodes and BE nodes can be horizontally scaled. After scaling BE nodes, Doris automatically balances data shards based on the load conditions between nodes, without manual intervention. |
|**Materialized views and pre\-aggregation engine** |Doris supports storing the results of pre\-aggregation computations through materialized views or Rollup tables, thereby accelerating query efficiency in certain aggregation scenarios.<br><br>At the same time, Doris ensures data consistency between materialized views and base tables, making the use of materialized views in queries and imports completely transparent. Doris automatically selects the appropriate materialized view for data ingestion based on the user's query statements. |
|**Federated query** |Doris can efficiently analyze locally stored data, and can also serve as a compute engine to directly perform federated queries on data in the data lake. It supports data organization structures including Apache Hive, Apache Iceberg, and Apache Hudi, supports file formats such as Parquet, ORC, and CSV, and also supports storage methods such as HDFS and TOS. Using Doris to query data lake data fully leverages the advantages of the vectorized engine, greatly improving data lake analytics performance. |


<span id="_2-架构组件说明"></span>
## Note on architecture components

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4113b0b57c8b2f736fe1a4ede25a8fa1.png) </span>


* FE: The frontend access node of Doris. Cluster metadata is stored in the Catalog within FE. BE is responsible for receiving SQL, parsing SQL, performing optimization, generating the corresponding execution plan, and submitting the execution plan to BE, which is responsible for the actual execution of the task.

* BE: The backend execution node of Doris, responsible for executing specific SQL tasks. BE nodes store data locally and can also access remote storage, such as HDFS/S3, to retrieve the corresponding table data for computation.


For more information, refer to the [Doris official website](https://doris.apache.org/zh-CN/docs/gettingStarted/what-is-apache-doris).
