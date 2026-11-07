---
title: "Overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/starrocks_overview"
---

StarRocks is a new\-generation, ultra\-fast, all\-scenario MPP (Massively Parallel Processing) database. Its vision is to make users' data analytics simpler and more agile. With StarRocks, you can connect to and operate the StarRocks cluster via the MySQL protocol without any complex data preprocessing, enabling ultra\-fast analytics across multiple scenarios. Typical analytics scenarios include real\-time online business reporting and analysis, user profiling and behavior analysis, data lake query analytics, and log management and analysis, among many others.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Some content and images in this chapter are cited from the StarRocks official website.</div>


<span id="_1-产品特性"></span>
## **Product features**

<span id="_1-1-mpp-分布式执行框架"></span>
### MPP distributed execution framework

StarRocks adopts an MPP (Massively Parallel Processing) distributed execution framework. In the MPP execution framework, a query request is split into multiple physical computation units that are executed in parallel across multiple machines. Each execution node has dedicated resources (CPU, memory). The MPP execution framework enables a single query request to fully utilize the resources of all execution nodes, so the performance of a single query can continuously improve as the cluster scales horizontally.

<span id="_1-2-全面向量化执行引擎"></span>
### Fully vectorized execution engine

StarRocks fully leverages the processing power of the CPU by implementing a fully vectorized engine. The fully vectorized engine organizes and processes data in a columnar manner. StarRocks's data storage, in\-memory data organization, and SQL operator computation methods are all implemented in a columnar fashion. Column\-based data organization also makes better use of the CPU's cache characteristics. Columnar computation results in fewer virtual function calls and fewer branch judgments, thereby achieving more efficient CPU instruction pipelines.

On the other hand, StarRocks's fully vectorized engine makes full use of the CPU's SIMD (Single Instruction Multiple Data) instructions through vectorized algorithms. This allows StarRocks to perform more data operations with fewer instructions. Validated by standard test suites, StarRocks's fully vectorized engine can improve the performance of execution operators by 3 to 10 times overall.

<span id="_1-3-存储计算分离"></span>
### Separation of storage and compute

StarRocks' compute\-storage separation technology, based on the existing integrated compute\-storage architecture, decouples compute and storage. In the new compute\-storage separation architecture, data is persistently stored on more reliable and cost\-effective remote object storage (such as S3) or HDFS, while the local disks of compute nodes are used only to cache hot data to accelerate queries. When the local cache is hit, compute\-storage separation can achieve the same query performance as the integrated compute\-storage architecture. With the compute\-storage separation architecture, users can dynamically add or remove compute nodes to achieve scaling within seconds. Compute\-storage separation significantly reduces data storage costs and scaling costs, and helps achieve resource isolation and elastic scaling of compute resources.

<span id="_1-4-cbo-优化器"></span>
### CBO optimizer

StarRocks has designed and implemented from scratch a brand\-new, Cascades\-like, cost\-based optimizer (CBO). During its design, this optimizer was deeply customized for StarRocks' fully vectorized execution engine, with multiple optimizations and innovations. Internally, the optimizer implements several important features and optimizations, including common expression reuse, correlated subquery rewriting, lateral join, join reordering, selection of distributed join execution strategies, and low\-cardinality dictionary optimization. Currently, this optimizer can fully support all 99 SQL statements of TPC\-DS.

<span id="_1-5-可实时更新的列式存储引擎"></span>
### Columnar storage engine with real\-time updates

StarRocks implements a columnar storage engine, where data is stored by column, allowing data of the same type to be stored consecutively. On one hand, data can use more efficient encoding methods to achieve higher compression ratios and reduce storage costs. On the other hand, this also reduces the total I/O required for the system to read data, improving query performance. In addition, in most OLAP scenarios, queries involve only a subset of columns. Compared to row\-based storage, columnar storage only needs to read data from some columns, which can greatly reduce disk I/O throughput.

<span id="_1-6-智能的物化视图"></span>
### Intelligent materialized views

StarRocks supports users in using materialized views to accelerate queries and implement data warehouse layering. Unlike some similar products where materialized views require manual data synchronization with the original table, StarRocks materialized views can automatically update data based on the source table. As long as the source table data changes, the materialized view is updated synchronously, ensuring consistency with the base table without any additional maintenance operations. Moreover, the selection of materialized views is also performed automatically. When StarRocks performs query planning, if there is a suitable materialized view that can accelerate the query, StarRocks automatically rewrites the query (Query Rewrite), directing the query to the most appropriate materialized view for acceleration.

<span id="_1-7-数据湖分析"></span>
### Data lake analytics

StarRocks can efficiently analyze not only locally stored data but also directly analyze data in data lakes as a compute engine. Users can easily query data stored in data lakes such as Hive, Iceberg, Hudi, and Delta Lake through the External Catalog provided by StarRocks, without the need for data migration.

<span id="_2-系统架构"></span>
## System architecture

StarRocks supports two deployment modes: integrated storage and compute (shared\-nothing) and separated storage and compute (shared\-data).

<span id="_2-1-存算一体"></span>
### Integrated storage and compute

In integrated storage and compute mode, a StarRocks cluster consists of FE and BE node types. The overall architecture is shown in the following diagram:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64e43b6bb3be871884992bba671f74b1.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>FE</strong>: Frontend, which is the access node for StarRocks, responsible for metadata management, client connection management, query planning, and query scheduling. Each FE node retains a complete copy of metadata in memory, thereby providing identical services.</div>


* <div data-tips="true" data-tips-type="tip"><strong>BE</strong>: Backend, which is the data storage and compute node for StarRocks, responsible for data storage and SQL computation. Functionally, BE nodes are equal and support horizontal scaling to flexibly adjust the cluster's storage and compute capacity.</div>



<span id="_2-2-存算分离"></span>
### Separated storage and compute

In separated storage and compute mode, a StarRocks cluster consists of FE and CN node types. The overall architecture is shown in the following diagram:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c541502dd5b6919633078ff1d464874b.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>FE</strong>: Frontend, which is the access node for StarRocks. Functionally, it is consistent with the integrated compute\-storage architecture and is also responsible for metadata management, client connection management, query planning, and query scheduling.</div>


* <div data-tips="true" data-tips-type="tip"><strong>CN</strong>: Compute Node, which is the compute node for StarRocks. In the compute\-storage separation mode, data storage is upgraded from local storage to shared storage. As a result, the storage function of BE nodes is decoupled, and they are transformed into stateless CN nodes, responsible for executing data import, query computation, and cache data management tasks.</div>



<span id="_3-更多信息"></span>
## User guide documentation


* If you are using the fully managed EMR mode, refer to the EMR Serverless instance best practices documentation for advanced usage of StarRocks. For details, see: [EMR Serverless 实例-Starrocks 最佳实践文档](https://www.volcengine.com/docs/6491/1927104).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to use EMR Serverless instances for StarRocks, which require no maintenance and are hassle\-free.   </div>
   

* If you are using the semi\-managed EMR mode, refer to the documents in this directory to further explore the following StarRocks\-related sections:

   * [quickstart](https://docs.byteplus.com/docs/E-MapReduce/109494): Learn about the creation and basic usage of StarRocks clusters, such as database and table management, data queries, and so on.

   * [运维管理](https://docs.byteplus.com/docs/E-MapReduce/109496): Learn about the daily management of StarRocks clusters and components, such as parameter configuration, scaling, monitoring, and alerting.

   * [数据湖分析](https://docs.byteplus.com/docs/undefined/69a9666710be4d05382fbfe0): Learn how to access data stored in data lakes through the External Catalog.

   * [Advanced usage](https://docs.byteplus.com/docs/undefined/69a9666710be4d05382fbfc8): Learn how to use advanced features, including partitioned table design, data import and export, compute\-storage separation, and how to analyze slow SQL queries.

   * [Best practices](https://docs.byteplus.com/docs/undefined/69a9666710be4d05382fbfe4): Learn how to use StarRocks in the optimal way.

   * [FAQs](https://docs.byteplus.com/docs/undefined/69aa387a1f8f6105696f7c75): Learn about some frequently encountered issues and how to resolve them.

* To learn more details about StarRocks, refer to the [StarRocks official documentation](https://docs.starrocks.io/zh/docs/introduction/StarRocks_intro/).
