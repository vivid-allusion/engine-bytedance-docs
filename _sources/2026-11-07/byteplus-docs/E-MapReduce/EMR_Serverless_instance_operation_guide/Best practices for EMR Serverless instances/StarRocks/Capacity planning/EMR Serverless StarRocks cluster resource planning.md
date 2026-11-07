---
title: "EMR Serverless StarRocks cluster resource planning"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_StarRocks_cluster_resource_planning"
---

<span id="2ce371b6"></span>
## Overview

Cluster resource planning is the management process by which enterprises or organizations **reasonably configure and dynamically manage core resources such as compute, storage, and network** to enhance system reliability, availability, and operational efficiency, ultimately achieving precise alignment and support for business requirements.

<span id="76d28727"></span>
## Key considerations


1. **Business requirements**: Centered on business characteristics (such as peak traffic, data processing volume, and service types), determine the basic scale and configuration standards for cluster resources to ensure direct alignment between resources and business objectives.

2. **Availability**: Through redundancy design and automatic failover mechanisms, ensure continuous availability of cluster resources, avoid single points of failure, and support uninterrupted business operations.

3. **Performance**: Based on requirements for business response time and concurrent processing capability, configure resource performance parameters (such as CPU computing power, storage IOPS, and network bandwidth) to meet the needs of efficient business operation.

4. **Cost control**: While meeting business requirements, balance costs for hardware procurement, cloud resource leasing, and operations management to ensure resource investment stays within the enterprise budget and achieves optimal cost\-effectiveness.

5. **Scalability**: Reserve resource expansion interfaces or adopt elastic architectures to support rapid resource scaling (such as adding nodes or expanding storage) as the business grows, preventing resource bottlenecks from limiting business development.


<span id="c7bc9e13"></span>
## **Solution architecture**

<span id="50481524"></span>
### Integrated compute and storage

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88f41b79e66d455a91d4423645346f3a~tplv-goo7wpa0wc-image.image) </span>


* **FE**: The frontend access node of StarRocks. Cluster metadata is stored in the Catalog within FE. FE is responsible for receiving SQL, parsing SQL, optimizing, generating the corresponding execution plan, and submitting the execution plan to BE, which is responsible for executing the tasks.

* **BE**: The backend execution node of StarRocks, responsible for executing specific SQL tasks. BE nodes store data locally.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">StarRocks mainly consists of two types of components: FE nodes and BE nodes. Each node must be deployed separately on a physical or virtual machine.</div>


<span id="a9dc588f"></span>
### Compute and storage separation

For compute and storage separation, CN nodes are used to replace BE nodes. Refer to [Storage-compute separation best practices](https://docs.byteplus.com/docs/E-MapReduce/109144)creating an instance. The architecture for compute and storage separation is shown in the diagram.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad08f86795c14729b993a4b8da0d0635~tplv-goo7wpa0wc-image.image) </span>

<span id="e0eb9aa9"></span>
## **Integrated compute and storage**

In the integrated compute and storage version, the instance contains only frontend (FE) and backend (BE) nodes. Recommendations for the specifications of both will be provided separately.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The resource estimation results from formulas are for reference only. Due to varying SQL complexity across different business scenarios, the required resources may differ. In actual production environments, the final required resources should be evaluated based on the results of stress testing for the specific business.</div>


<span id="f33dbada"></span>
### **BE node specification evaluation**

In the integrated storage\-compute version, BE nodes are responsible for actual data storage and compute tasks.

**Estimation formula**

```Plain
CU总数 = 扫描数据总行数 / CPU处理能力 / 预期响应时间*QPS（每秒查询次数）
所需的总存储空间 = 原始数据大小 * 数据副本数/数据压缩算法压缩比
```


**Parameter note**:


* **Total number of scanned data rows**: The total number of data rows expected to be scanned by each SQL. Important: This amount does not refer to the total data volume of a single table, but only to the data that actually needs to be scanned.

* **CPU processing capability**: This value varies dynamically depending on the complexity of different SQL statements, typically ranging from 10 million rows per second to 100 million rows per second. The higher the SQL complexity, the fewer rows are processed.

* **Expected response time**: The expected execution time for SQL, for example, expecting SQL to return results within 1 second.

* **QPS (Queries Per Second)** : The number of SQL statements submitted concurrently per second, for example, 30 per second.


**Reference resource configuration for BE nodes**:


|**Total number of scanned data rows** |**SQL complexity** |**Estimated CPU processing capacity (rows/second)**  |**Expected response time (seconds)**  |**QPS (queries per second)**  |**Estimated total required CU** |**Estimated BE specification** |
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


<span id="18a5a72a"></span>
### **FE node specification evaluation**

FE nodes are mainly responsible for metadata management, client connection management, query planning, and query scheduling.

FE specifications can be roughly estimated based on the number of CUs of BE nodes. Specific recommendations are shown in the table below. The data disk of FE nodes usually requires only 100 GB. If subsequent storage space is insufficient, it can be expanded separately.

Reference resource configuration for FE nodes:


|**Total BE CU count** |**Scenario type** |**Recommended FE specification** |
|---|---|---|
|< 120CU |General scenario |8CU \* 3 |
|120CU ～ 1000CU |General scenario |16CU \* 3 |
|1000CU ～ 3000CU |General scenario |32CU \* 3 |
|> =3000CU |General scenario |64CU \* 3 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The values in the above table are only recommendations. In actual production environments, the final required resources should be evaluated based on the results of stress testing for the specific business.</div>


* <div data-tips="true" data-tips-type="tip">For high\-concurrency point query scenarios, it is recommended to appropriately increase the number of FE nodes, for example, increasing to 5 nodes.</div>



<span id="43f5464c"></span>
## **Storage\-compute separation**

In the storage\-compute separation version, the instance only includes frontend (FE) and backend (CN) nodes. Recommendations for the specifications of both will be provided separately.

<span id="2cf4adc0"></span>
### **CN node specification evaluation**

In the storage\-compute separation version, CN nodes are responsible for actual data compute tasks and remote data caching.

Refer to [BE node specification evaluation](https://docs.byteplus.com/docs/E-MapReduce/109147#f33dbada) and [StarRocks存算分离集群配置建议](https://docs.byteplus.com/docs/undefined/66581c67d9d1b4026c17b954) in the integrated storage\-compute version. The local storage of CN nodes only affects the cache size during query and write operations. Therefore, it is recommended to determine the storage size based on the volume of data to be queried. Typically, a 16\-core configuration uses 256 GB of storage space.

<span id="402ea652"></span>
### **FE node specification evaluation**

Refer to [FE node specification evaluation](https://docs.byteplus.com/docs/E-MapReduce/109147#18a5a72a) in the integrated storage\-compute version.

<span id="49d9eacc"></span>
## Resource expansion evaluation criteria

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Note: This is intended to help customers better assess the health status of the current cluster and avoid business unavailability caused by sudden imports or large queries resulting in resource shortages.</div>


<span id="6ed24f58"></span>
### FE resource usage


|**Resource type** |**Healthy threshold** |**Correlation description** |
|---|---|---|
|CPU |60% |Usually positively correlated with cluster QPS/RPS |
|Memory |80% |Usually positively correlated with cluster replica metadata and cache |
|Disk capacity |80% |Usually positively correlated with metadata |


<span id="81fd4f9c"></span>
### BE resource usage


|**Resource type** |**Healthy threshold** |**Correlation description** |
|---|---|---|
|CPU |60% |Usually positively correlated with cluster write volume, query volume, query complexity, and QPS |
|Memory |70% |Usually positively correlated with the amount of data written to the cluster, cache, query complexity, and QPS |
|Disk bandwidth |300MB/s |Usually positively correlated with the amount of data written to the cluster, the amount of data queried, and replica cloning |
|Disk capacity |80% |Usually positively correlated with the amount of data in the cluster |


<span id="1fd849e4"></span>
### Expansion reference


* When either the CPU or memory usage of FE exceeds the healthy level, consider upgrading the FE configuration.

* When any dimension of CPU or memory on a BE exceeds the healthy threshold, consider upgrading the BE configuration or scaling out horizontally.

* When any dimension of disk bandwidth or capacity on a BE exceeds the healthy threshold, consider upgrading the disk configuration or scaling out the BE horizontally.
