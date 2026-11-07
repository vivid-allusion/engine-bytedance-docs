---
title: "Overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/hive_overview"
---

Hive is a data warehouse architecture based on Hadoop that enables extraction, transformation, and loading (ETL) operations on large datasets stored in distributed storage using HiveQL (a SQL\-like language), as well as metadata management.

For more information about Hive, refer to the [Apache Hive official website](https://hive.apache.org/?spm=a2c4g.11186623.0.0.47cbc9c99Tvws5).

<span id="_1-hive-组件说明"></span>
## **1 Hive component note**

The basic components are as follows:


|Name |Note |
|---|---|
|**Hive Client** |Hive Client is the Hive client. It provides the driver packages required for Beeline and JDBC applications, and allows submission of SQL jobs to HiveServer2 through this client. |
|**Hive MetaStore** |Hive MetaStore is the Hive metadata management module, which stores metadata information such as database, table, and column in a database.<br><br>This module is also relied upon by the Spark engine. Thrift interfaces are also provided, allowing MetaStore clients to directly operate metadata information. In a high availability environment, deployment of multiple MetaStores is supported. |
|**HiveServer2** |HiveServer2 is a HiveQL query server that receives SQL requests submitted from JDBC clients, compiles and parses SQL statements into corresponding MapReduce tasks or HDFS operations, thereby completing data extraction, transformation, and analysis. It also supports multi\-client concurrency and authentication. Multiple HiveServers can be deployed within a single cluster to provide load balancing capability. |


<span id="_2-hive-原理"></span>
## **2 Hive principles**

As a data warehouse in the Hadoop ecosystem, Hive's main capability is to compile and parse HiveQL, generate and execute corresponding jobs. For HiveQL operations, see: [HiveQL Language Manual](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).

The structure of Hive is shown in the diagram:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3a4454e61f4ead5913859e8b2790d6e6.png) </span>


* **Meta Store:**  Performs read, write, and update operations on metadata.

* **JDBC:**  Client connection method.

* **Hive Server:**  Provides a Thrift interface, acts as the server side for JDBC connections, receives HiveQL requests, delegates execution to the Driver, and returns results to the client.

* **Driver:**  Manages the entire lifecycle of HiveQL execution. Through the Compiler, HiveQL is compiled and transformed into a series of interdependent Map/Reduce tasks, optimized by the Optimizer, and finally executed by the Executor.


<span id="_3-版本功能介绍"></span>
## **3 Version features overview**

Below is an introduction to the Hive component versions corresponding to each version of Volcano Engine E\-MapReduce (EMR), as well as the feature limitations of Hive in each version. For more information on component versions, see: [版本概述说明](https://docs.byteplus.com/docs/undefined/68da347242e561058e056938).


|EMR version |Hive component version |Feature overview |
|---|---|---|
|1.2.1 |3.1.2 |Supports Tez and MR computing engines. The default is Tez |
|1.3.0 |3.1.2 |Supports Tez and MR computing engines. The default is Tez |
|1.3.1 |3.1.2 |Supports Tez and MR computing engines. The default is Tez |
|EMR version |Hive component version |Feature overview |
|<br>---<br><br> |<br>---<br><br> |<br>---<br><br> |
|2.0.1 |2.3.9 |Supports Tez and MR computing engines. The default is Tez |
|2.1.0 |2.3.9 |Supports Tez and MR computing engines. The default is Tez |
|EMR version |Hive component version |Feature overview |
|<br>---<br><br> |<br>---<br><br> |<br>---<br><br> |
|3.0.1 |3.1.2 |Supports Tez and MR computing engines. The default is Tez |
|3.1.0 |3.1.2 |Supports Tez and MR computing engines. The default is Tez |
