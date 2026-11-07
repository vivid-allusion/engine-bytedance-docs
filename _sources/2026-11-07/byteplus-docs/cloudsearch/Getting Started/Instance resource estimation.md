---
title: "Instance resource estimation"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Estimating_instance_resources"
---

This article introduces resource estimation methods for Cloud Search service instance specifications from two dimensions: general scenarios (such as text retrieval and log analysis) and vector scenarios (vector storage and vector search). The core resources of Cloud Search service are computing and storage. This article focuses on estimating these two types of resources, including node type, node specification, node disk space, and the number of nodes.

<span id="FrOFHlku"></span>
## Background and principles

The resource estimation for instances follows these principles:


* If you are migrating from other vendors or self\-built environments, since the original instance specifications have been validated under actual data scales and business scenarios, it is recommended to prioritize reusing the original Elasticsearch or OpenSearch instance specifications and capacity configurations to reduce migration costs and improve deployment efficiency.

* The read and write performance of indexes is affected by multiple factors, including index Mapping and Settings metadata, data characteristics, query complexity, and read/write QPS. Therefore, there is no uniform standard answer for estimating Elasticsearch resource specifications. It is recommended to test according to the actual data scale and business scenarios to determine the instance specification and capacity that meet real needs.

* If you cannot fully test with real business scenarios, strongly configure alarm rules for key metrics such as instances, indexes, and nodes immediately after purchasing and activating an instance to continuously monitor its running status. When resource shortage alarms occur, promptly identify the issue and quickly upgrade the instance to an appropriate specification to avoid resource bottlenecks impacting the business. Refer to the [Recommended alarm rules](https://docs.byteplus.com/docs/6465/1219834) for specific alarm metrics.

* Vector search scenarios consume more memory resources than general search scenarios. Insufficient memory estimation can easily cause OOM issues. It is strongly recommended to use data node specifications with a CPU to memory ratio of 1:8 (e.g., 4 cores and 32 GiB) as the initial configuration, and it is also advised to use FlexPL type storage.

* Estimating computing resources is generally more difficult than estimating storage space. However, based on actual alarm conditions from Volcengine Cloud Search service, disk space tends to trigger capacity shortage alarms more frequently, so storage space should be prioritized in resource planning.

* There is a certain linear relationship between node disk capacity and node memory specifications. When a large disk storage demand exists, it is recommended to choose nodes with high memory specifications to ensure instance stability and overall performance. Avoid configurations that use many low\-spec nodes combined with large\-capacity disks.

* When the instance is generally normal but triggers an alarm due to insufficient node resources and requires expansion, prioritize vertical specification expansion. For example, upgrade nodes to 8\-core 32 GiB or 16\-core 64 GiB specifications (this operation will trigger an instance rolling restart; perform it during off\-peak hours). Then consider horizontal expansion to increase the number of nodes if needed (this operation will not trigger an instance rolling restart).


The Cloud Search service also offers a resource calculator feature. You can use the experimental data provided to understand resource scale estimation methods and make adjustments based on the test results during actual deployment. For details, see the [Resource calculator](https://docs.byteplus.com/en/docs/cloudsearch/Resource_calculator).

<span id="af72fdab"></span>
## General scenarios

<span id="4a997f83"></span>
### Scenario description

General scenarios refer to common uses of Cloud Search service such as text retrieval and log analysis. It leverages near real\-time search and analysis of massive datasets, combined with open\-source components like Logstash/Kibana/Dashboards and Cloud Search’s own core enhancements, to quickly build practical applications for log analysis, information retrieval, and more.

<span id="48b38e81"></span>
### Estimate computing resources

The computing resources of the Cloud Search service are mainly used for data writing and query processes. Since many factors affect computing resource consumption, resource estimation often has some uncertainty. This article provides two methods for estimating computing resources for your reference


<Tabs>
<Tab zoneid="RbBU4OGrFo" title="Estimated based on business data">
<TabTitle>Estimated based on business data</TabTitle>

* Log scenarios typically involve write\-intensive and read\-light operations, with computing resources mainly consumed during the writing phase. According to BytePlus's test results, a 2\-core 8 GB node can support a maximum write throughput of approximately 5,000 to 10,000 log entries per second in log writing scenarios. With the increase in node specifications, write capacity generally grows linearly. For example, an 8\-core 32 GB node can support approximately 20,000 to 40,000 log entries per second for writing. We recommend estimating based on the lower limit of the range during initial planning and adjusting elastically according to the actual load during instance operation.

* In log scenarios, to achieve long\-term data storage (e.g., more than 1 month), configure warm data nodes and cold data nodes, combined with data lifecycle management policies for tiered storage. Proper lifecycle configuration significantly reduces storage costs while improving overall instance processing performance. Refer to [Managing time-series data with Data Streams and ISM](https://docs.byteplus.com/docs/cloudsearch/Manage_time-series_data_using_Data_Streams_and_ISM) for detailed configuration methods.

* Text search scenarios (such as website search and online search) differ from log scenarios and usually involve read\-heavy and write\-light workloads, with computing resources mainly used for query processing. Based on BytePlus's experience, resource consumption varies greatly depending on data structure, query syntax, data volume, and write and query QPS, so there is no unified recommended specification. We suggest testing based on your actual data volume and business scenario to determine the instance specification and capacity that best suit your needs.


</Tab>
<Tab zoneid="KbMkAwl2Oo" title="BytePlus's recommended configuration values">
<TabTitle>BytePlus's recommended configuration values</TabTitle>

* Single\-node instances are prohibited in production environments. Single\-node instances are only suitable for testing scenarios. If you use a single\-node instance for testing and want to switch to production, upgrade to 3 nodes or more is recommended. For detailed steps, see Upgrade an instance.

* The recommended calculation for the maximum number of nodes per instance is: maximum nodes = number of CPU cores per single node × 5. For example, if the data node specification is 16 cores 128 GiB, the recommended maximum number of data nodes is 80.

* In log analysis scenarios, the recommended calculation for the maximum storage per single node is: maximum storage = single\-node memory size (GiB) × 50. For example, if the data node specification is 8 cores 32 GiB, the recommended disk space is 1600 GiB.

* In search scenarios, the recommended calculation for the maximum storage per single node is: maximum storage = single\-node memory size (GiB) × 10. For example, when the data node specification is 16 cores 32 GiB, the recommended disk space is 320 GiB.

* When the number of data nodes in the instance reaches a certain scale, it is recommended to enable dedicated master nodes with the following recommended configurations:

   * When the number of data nodes exceeds 10, the recommended specification for dedicated master nodes is 4 cores 16 GiB.

   * When the number of data nodes exceeds 30, the recommended specification for dedicated master nodes is 8 cores 32 GiB

   * When the number of data nodes exceeds 50, the recommended specification for dedicated master nodes is 16 cores 64 GiB

* When query or write pressure is high, it is recommended to enable coordinating nodes to decouple read and write requests and reduce pressure on data nodes, with the following recommended configurations:

   * The number of coordinating nodes is recommended to start from 2, with CPU to memory ratio of 1:4 or 1:8.

   * The ratio of coordinating nodes to data nodes is recommended to be around 1:5. The specification of coordinating nodes should not be lower than that of data nodes but can be adjusted according to test results.

   For example, when the instance contains 10 data nodes with 8 cores 32 GiB each, it is recommended to configure 2 coordinating nodes with 8 cores 32 GiB each

* If enabling warm data nodes, it is recommended that their specifications match those of data nodes or be reduced to half of the data node specifications. At the same time, reducing the number of replicas can also decrease storage space usage, saving storage costs. For example, when the data node is configured as (8 cores 32 GiB + 1000 GiB) × 20, the warm data node is recommended to be configured as (4 cores 16 GiB + 1000 GiB) × 20

* To enable cold data nodes, it is recommended to set the cold data node disk space to 10%–20% of TOS’s total storage capacity. When TOS storage space continuously grows, expanding the number or storage specifications of cold nodes accordingly ensures search performance and availability.

   * The number of cold nodes is recommended to start from 2.

   * Cold nodes consume relatively high memory resources and only support selecting CPU\-to\-memory specifications of 1:8.

   * In general log scenarios, the memory\-to\-disk space ratio for cold nodes is recommended to be 1:50.

   For example, when the amount of cold data stored in TOS reaches 100 TB, the recommended total disk capacity for cold nodes is 20 TB, with a corresponding memory requirement of about 400 GiB. At this point, cold nodes can be configured as (8 cores 64 GiB + 3200 GiB disk) × 7.


</Tab>
</Tabs>


<span id="511d9a75"></span>
### Shard quantity estimation and recommendation

In Cloud Search service instances, each index is divided into multiple shards. The number of shards directly affects the index’s read/write performance and recovery speed. Since modifying shard quantity after creating the index is costly, it should be planned in advance. BytePlus offers the following shard quantity estimation and configuration recommendations:


* Oversized shards extend recovery time, while too many small shards consume excess CPU and memory, causing read/write performance drops and memory shortages.

* During planning or testing, shard quantity should be reasonably planned and adjusted based on business needs, index data size, and expected data growth to avoid frequent changes in production.

* BytePlus recommends each shard’s size be controlled between 10 and 50 GiB, preferably 30 GiB or less. You can calculate the required shard quantity based on the total index data volume. It is also recommended to keep no more than five shards of the same index on a single data node.

* When the total number of shards in an instance exceeds the number of data nodes, it is recommended to set the number of shards as an integer multiple of the number of data nodes. This allows shards to distribute evenly across the data nodes, improving overall resource utilization.

   For example, the instance contains 6 data nodes, the current index size is 200 GiB, and data volume is expected to double within half a year. If planning based on 30 GiB per shard, the required number of shards is approximately: 200 GiB × (1 + 100%) ÷ 30 ≈ 14 shards. With this number of shards, the distribution is uneven among the nodes. To improve load balancing, it is recommended to adjust the number of shards to 18.

* Estimated shard count per node recommendation:

   * For small specification instances, the recommended number of shards on a single data node across all indexes is: shard count per node = node memory size (GiB) × 30. For example, if the node specification is 4 cores and 16 GiB memory, the recommended shard count on a single node should not exceed 480.

   * For large specification instances, the recommended number of shards on a single data node across all indexes is: shard count per node = node memory size (GiB) × 50. For example, if the node specification is 24 cores and 48 GiB memory, the recommended shard count on a single node should not exceed 2400.

* Shard and replica configuration recommendations:

   * When the data volume is large and write pressure is high, configure multiple shards to reduce write pressure on a single shard and improve concurrency.

   * When the data volume is small and write pressure is low, use a configuration with one primary and multiple replicas or one primary and one replica to enhance data reliability and query performance.

   * For other write and shard optimization measures, refer to [Bulk directed routing](https://docs.byteplus.com/docs/cloudsearch/Bulk_directional_routing) and [Adaptive write optimization](https://docs.byteplus.com/docs/cloudsearch/Adaptive_write_optimization).


<span id="75c0a308"></span>
### Storage resource estimation

The main factors affecting the disk storage size of nodes in Cloud Search are:


* The size of original data: the amount of data to be stored in Cloud Search.

* The number of index replicas: each index requires at least one replica by default (adding replicas improves reliability but increases storage cost).

* Index overhead or expansion: usually about 10% of the original data.

* Instance internal overhead: internal operations such as segment merging, Translog, logs, etc., requiring a 20% reserve.

* Operating system reservation: by default, 5% of space is reserved for system recovery, critical process handling, and preventing disk fragmentation.

* Storage security threshold: Cloud Search generally recommends reserving at least 15% as a security threshold.


Recommended instance storage space based on the above factors:

```Plain Text
实际空间 = 原始数据 × (1 + 副本数) × (1 + 索引开销或膨胀) / (1 - 实例内部开销) / (1 - 操作系统预留) / (1 - 存储安全阈值） 
        ≈ 原始数据 × (1 + 副本数) × 1.7
```


Cloud Search uses a native distributed architecture, with storage space as the sum of all nodes. Each node’s storage capacity is:

```Plain Text
每个节点的存储容量 ≈ 原始数据 × (1 + 副本数) × 1.7 / 节点数量
```


<span id="896b3cb8"></span>
## Vector scenarios

<span id="7d3a99b7"></span>
### Applicable scenario analysis

Vector scenarios refer to the OpenSearch 2.9 version provided by Cloud Search, supporting vector and text hybrid search, multiple algorithms including DiskANN, Hybrid DiskANN, or HNSW, enabling stable and fast retrieval at the billion\-scale level. Together with models like Doubao and DeepSeek, it quickly builds  applications such as RAG, semantic analysis, image\-to\-image search, and multimodal search.

Vector storage and retrieval are highly sensitive to memory and disk capacity and performance. Without proper resource planning, cluster crashes can easily occur. This document introduces resource planning methods for vector storage.

<span id="fa661415"></span>
### Memory resource estimation

Since vectors reside in memory, different algorithms have varying memory requirements. The DiskANN algorithm consumes less memory and is more economical for ultra\-large scale scenarios, such as over one billion vectors. Below is the memory calculation for various algorithms supported by Cloud Search.

**Vamana memory estimation**

Vamana is the vector index algorithm of the DiskANN engine. Its graph construction speed is slightly slower than HNSW, but it offers better query performance and cost than HNSW at the same recall rate.

```Plain Text
vector_size：单个向量大小，fp32=4，fp16=2，int8=1，单位为 Byte。
dimension：向量的维度
m：向量间指针的数量，默认 32
num_vectors：索引的数量
1.1：预留 10% 作为图索引的临时空间
storage_request = 1.1 * (vector_size * dimension + 8 * m) * num_vectors
```


**HNSW memory estimation**

HNSW is a widely used vector index algorithm known for its fast speed and high accuracy.

```Plain Text
vector_size：单个向量大小，fp32=4，fp16=2，int8=1，单位为 Byte。
dimension：向量的维度
m：向量间指针的数量，默认 32
num_vectors：索引的数量
1.1：预留 10% 作为图索引的临时空间
storage_request = 1.1 * (vector_size * dimension + 8 * m) * num_vectors
```


**IVF memory estimation**

IVF is a low\-cost vector index algorithm that generally has a lower recall rate.

```Plain Text
'''
vector_size：单个向量大小，fp32=4，fp16=2，int8=1，单位为 Byte。
dimension：向量的维度
num_vectors：索引的数量
nlist：bucket（中心点）数量
1.1：预留 10% 作为图索引的临时空间
'''
storage_request = 1.1 * ((vector_size * dimension * num_vectors) + (4 * nlist * dimension))
```


<span id="b2a81213"></span>
### Memory usage estimation

Since Cloud Search service nodes’ memory is also needed for JVM or other purposes, the following shows the required node memory calculations for each supported algorithm category in Cloud Search.

**Memory allocation configuration**

```HTTP
# 向量内存占比默认50%，剩余的内存分配给 JVM 以及其他用途，可以根据实际需求进行配置

PUT _cluster/_settings
{
    "persistent": {
        "knn.memory.circuit_breaker.limit": "70%" 
    }
}
```


<span id="e9ea1a9c"></span>
### Vector memory usage estimation

```Plain Text
计算向量内存需求
replica_number：副本数量
storage_request：向量存储占用计算得到的结果，计算方法参考内存资源预估
vector_memory_request =  (1 + replica_number) * storage_request
```


<span id="f15e64d5"></span>
#### full memory mode

```Plain Text
计算内存需求
vector_memory_request：向量的内存空间需求
heap_memory：堆内存，32 GiB(含)以下占比 50%，32 GiB(不含）以上固定 31 GiB
1.5：预留一些内存来存放cache、程序以及其他内存开销保证稳定性，可以按需调整
memory_request = (vector_memory_request +  heap_memory) * 1.5
```


<span id="e9a824cf"></span>
#### DiskANN disk or hybrid DiskANN mode

```Plain Text
计算内存需求
vector_memory_request：向量的内存空间需求
heap_memory：堆内存，32 GiB(含)以下占比 50%，32 GiB（不含）以上固定 31 GiB
1.5：预留一些内存来存放 cache、程序以及其他内存开销保证稳定性，可以按需调整
磁盘内存混合：memory_request = (vector_memory_request / 2 + heap_memory) * 1.5
纯磁盘+默认配置：memory_request = （vector_memory_request / 3 + heap_memory) * 1.5 （保守估计）
纯磁盘+参数优化：memory_request = （vector_memory_request / 6 + heap_memory) * 1.5
```


Cloud Search has a native distributed architecture. The total memory space equals the sum of all nodes, with each node's memory capacity as follows:

```Plain Text
每个节点的内存容量 ≈ 内存空间/ 节点数量
```


<span id="e1d39fca"></span>
### storage resource estimation

Using a calculation method 1.7 times that of general scenarios and considering vector scenarios' higher disk capacity requirements, such as DiskANN storing part of the graph structure's nodes and edges on disk, storage space needs to reserve twice the capacity.

```Plain Text
vector_size：单个向量大小，fp32=4，fp16=2，int8=1，单位为 Byte。
dimension：向量的维度
m：向量间指针的数量，默认 32
num_vectors：索引的数量
存储空间 = 2.0 * (vector_size * dimension + 8 * m) * num_vectors * (1 + 副本数)
```


Cloud Search has a native distributed architecture. The total storage space equals the sum of all nodes, with each node's storage capacity as follows.

```Plain Text
每个节点的存储容量 ≈ 存储空间/ 节点数量
```
