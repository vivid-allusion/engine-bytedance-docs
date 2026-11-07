---
title: "EMR Serverless Doris cluster resource planning"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_Doris_cluster_resource_planning"
---

<span id="77a5a1e1"></span>
## Overview

This article aims to introduce how to evaluate and plan the resource configuration of an EMR Serverless Doris cluster. EMR Serverless Doris cluster resource planning is the management process by which enterprises or organizations **reasonably configure and dynamically manage core resources such as compute, storage, and network** to enhance system reliability, availability, and operational efficiency, ultimately achieving precise alignment with and support for business requirements. This process applies to scenarios such as creating a cluster for the first time or expanding an existing cluster.

<span id="d30f8b91"></span>
## Key considerations


1. **Business requirements**: Determine the basic scale and configuration standards of cluster resources based on business characteristics (such as peak traffic, data processing volume, and service type), ensuring that resources are directly aligned with business objectives.

2. **Availability**: Ensure continuous availability of cluster resources through redundancy design, automatic failover, and other measures to avoid single points of failure and support uninterrupted business operations.

3. **Performance**: Configure resource performance parameters (such as CPU computing power, storage IOPS, and network bandwidth) according to requirements for business response time and concurrent processing capability, meeting the needs for efficient business operation.

4. **Cost control**: While meeting business requirements, balance costs such as hardware procurement, cloud resource leasing, and operations management to ensure resource investment remains within the enterprise budget and achieves optimal cost\-effectiveness.

5. **Scalability**: Reserve resource expansion interfaces or adopt an elastic architecture to support rapid resource expansion (such as adding nodes or expanding storage) as the business grows, preventing business development from being limited by resource bottlenecks.


<span id="1f06d0cd"></span>
## **Solution architecture**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83390d52481a433e846a1ed00656db43~tplv-goo7wpa0wc-image.image) </span>


* **FE**: The front\-end access node of Doris. Cluster metadata is stored in the Catalog within FE. FE is responsible for receiving SQL, parsing SQL, performing optimization, generating the corresponding execution plan, and submitting the execution plan to BE, which is responsible for executing the specific tasks.

* **BE**: The back\-end execution node of Doris, responsible for executing specific SQL tasks. BE nodes store data locally.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Doris mainly consists of two types of components: FE nodes and BE nodes. Each node must be deployed separately on a physical or virtual machine.</div>


<span id="cdc3081e"></span>
## **Integrated compute and storage version**

In the integrated compute and storage version, the instance contains only front\-end (FE) and back\-end (BE) nodes. Recommendations for the specifications of both will be provided separately below.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The formula\-based estimation may not be sufficiently accurate, as differences in SQL complexity can lead to variations. In actual production environments, it is also necessary to combine the results of stress testing based on real business scenarios to assess the final required resources.</div>


<span id="5905e7b6"></span>
### **BE node specification evaluation**

In the unified storage and compute version, BE nodes are responsible for actual data storage and compute tasks.

**Estimation formula**

```Plain
CU总数 = 扫描数据总行数 / CPU处理能力 / 预期响应时间*QPS（每秒查询次数）
所需的总存储空间 = 原始数据大小 * 数据副本数/数据压缩算法压缩比
```


**Parameter note**:


* **Total number of scanned data rows**: The total number of data rows expected to be scanned by each SQL query. Note: this amount does not refer to the total data volume of a single table, but only to the data that actually needs to be scanned.

* **CPU processing capability**: This value dynamically changes based on the complexity of different SQL queries, typically ranging from 10 million rows/second to 100 million rows/second. The higher the SQL complexity, the fewer rows can be processed.

* **Expected response time**: The expected execution time for SQL queries, for example, expecting the SQL to return results within 1 second.

* **QPS (Queries Per Second)** : The number of SQL queries submitted concurrently per second, for example, 30 queries per second.


**Reference resource configuration for BE nodes**:


|**Total number of scanned data rows** |**SQL complexity** |**Estimated CPU processing capability (rows/second)**  |**Expected response time (seconds)**  |**QPS (queries per second)**  |**Estimated total required CU** |**Estimated BE specification** |
|---|---|---|---|---|---|---|
|50 million rows |High |20 million rows |2 |50 |63 |16CU\*4 units |
|50 million rows |Medium |50 million rows |1.5 |100 |67 |16CU\*5 units |
|50 million rows |Low |100 million rows |1 |200 |100 |32CU\*3 units |
|1 billion rows |High |20 million rows |5 |20 |200 |32CU\*7 units |
|1 billion rows |Medium |50 million rows |3 |50 |333 |64CU\*6 units |
|1 billion rows |Low |100 million rows |1 |80 |800 |64CU\*13 units |
|30 billion rows |High |20 million rows |30 |10 |500 |64CU\*8 units |
|30 billion rows |Medium |50 million rows |15 |20 |800 |64CU\*13 units |
|30 billion rows |Low |100 million rows |15 |20 |400 |64CU\*6 units |
|300 billion rows |High |20 million rows |60 |5 |1250 |64CU\*20 units |
|300 billion rows |Medium |50 million rows |45 |10 |1333 |64CU\*21 units |
|300 billion rows |Low |100 million rows |45 |10 |667 |64CU\*11 units |


<span id="fa2575f5"></span>
### **FE node specification evaluation**

FE nodes are mainly responsible for metadata management, client connection management, query planning, and query scheduling.

The FE specification can be roughly estimated based on the number of CUs of BE nodes. Specific recommendations are shown in the table below. The data disk of an FE node usually only requires 100 GB. If subsequent storage space is insufficient, it can be expanded separately.

Reference resource configuration for FE nodes:


|**Total BE CU quantity** |**Scenario type** |**Recommended FE specification** |
|---|---|---|
|< 120CU |General scenario |8CU \* 3 |
|120CU ~ 1000CU |General scenario |16CU \* 3 |
|1000CU ~ 3000CU |General scenario |32CU \* 3 |
|> =3000CU |General scenario |64CU \* 3 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The above table provides only recommended values. Actual production environments require evaluation of final resource requirements based on the results of business stress testing.</div>


* <div data-tips="true" data-tips-type="tip">For high\-concurrency point query scenarios, it is recommended to appropriately increase the number of FE nodes, for example, increase to 5 nodes.</div>



<span id="b14af001"></span>
## Resource scaling evaluation criteria

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Note: This is intended to help customers better assess the health status of the current cluster and avoid business unavailability caused by resource shortages due to sudden imports or large queries.</div>


<span id="c76a518b"></span>
### FE resource metric


|**Resource type** |**Health level** |**Correlation description** |
|---|---|---|
|CPU |60% |Usually positively correlated with cluster QPS/RPS |
|Memory |80% |Usually positively correlated with cluster replica metadata and cache |
|Disk capacity |80% |Usually positively correlated with metadata |


<span id="6216a5cc"></span>
### BE resource metric


|**Resource type** |**Health level** |**Correlation description** |
|---|---|---|
|CPU |60% |Usually positively correlated with cluster write data volume, query data volume, query complexity, and QPS |
|Memory |70% |Usually positively correlated with cluster write data volume, cache, query complexity, and QPS |
|Disk bandwidth |300MB/s |Usually positively correlated with cluster write data volume, query data volume, and replica cloning |
|Disk capacity |80% |Usually positively correlated with cluster data volume |


<span id="1d58e9f8"></span>
### Scaling reference


* If either the CPU or memory metric of the FE exceeds the healthy threshold, consider upgrading the FE configuration.

* If either the CPU or memory metric of the BE exceeds the healthy threshold, consider upgrading the BE configuration or horizontal scaling.

* If either the disk bandwidth or capacity metric of the BE exceeds the healthy threshold, consider upgrading the disk or horizontally scaling the BE.
