---
title: "StarRocks cluster resource planning"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/StarRocks_cluster_resource_planning"
---

Cluster resource planning refers to the process within an enterprise or organization of improving system reliability, availability, and efficiency, and meeting business requirements by reasonably allocating and managing resources such as computing, storage, and networking. When performing cluster resource planning, consider the following aspects:


1. Business requirements: Determine the scale and configuration of cluster resources based on the characteristics and needs of the business.

2. Availability: Cluster resources must have high availability to ensure business continuity and stability.

3. Performance: Cluster resources must deliver high performance to meet business needs.

4. Cost: The cost of cluster resources must be within the budget of the enterprise or organization.

5. Scalability: Cluster resources must be scalable to meet the evolving needs of the business.

6. Document the number of resources, FE, and BE to configure based on data volume and query requirements.


<span id="_1-架构组件说明"></span>
## 1 **Architecture component description**

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_03f50b7c86ec14f790ea1ec52d139926.png) </span>


* FE: The frontend access node of StarRocks. Cluster metadata is stored in the Catalog within the FE. The FE is responsible for receiving SQL, parsing SQL, optimizing, generating the corresponding execution plan, and submitting the execution plan to the BE, which is responsible for executing the tasks.

* BE: The backend execution node of StarRocks, responsible for executing specific SQL tasks. BE nodes store data locally and can also access remote storage, such as HDFS/S3, to retrieve table data and perform computations.


<span id="_2-节点数量"></span>
## 2 Number of nodes

StarRocks consists mainly of two types of components: FE nodes and BE nodes. Each node must be deployed separately on a physical or virtual machine.

<span id="_2-1-fe-节点数量"></span>
### 2.1 Number of FE nodes

FE nodes are primarily responsible for metadata management, client connection management, query planning, and query scheduling.

For a StarRocks production cluster, it is recommended to deploy at least **three** Follower FE nodes to prevent single points of failure.

StarRocks manages metadata across FE nodes using the BDB JE protocol. StarRocks selects one Leader FE node from all Follower FE nodes. Only the Leader FE node can write metadata; other Follower FE nodes can only update metadata based on the logs of the Leader FE node. If the Leader FE node goes offline, as long as more than half of the Follower FE nodes remain active, StarRocks will re\-elect a new Leader FE node.

To handle high\-concurrency query requests from your application, you can add Observer FE nodes to the cluster. Observer FE nodes are only responsible for processing query requests and do not participate in the election of the Leader FE node.

<span id="_2-2-be-节点数量"></span>
### 2.2 Number of BE nodes

BE nodes are responsible for data storage and SQL execution.

For a StarRocks production cluster, it is recommended to deploy at least three BE nodes. These nodes will automatically form a highly available BE cluster to prevent single points of failure from affecting data reliability and service availability.

You can achieve high\-concurrency queries by increasing the number of BE nodes.

<span id="_2-3-cn-节点数量"></span>
### 2.3 Number of CN nodes

CN nodes are optional components in StarRocks and are only responsible for SQL execution.

You can elastically scale compute resources by increasing the number of CN nodes, without changing the data distribution in the cluster.

<span id="_3-cpu-和内存"></span>
## 3 CPU and memory

Typically, FE services do not consume large amounts of CPU or memory resources. It is recommended to allocate 8 CPU cores and 16 GB RAM for each FE node.

Unlike FE services, if your application needs to process highly concurrent or complex queries on large datasets, BE services may consume significant CPU and memory resources. Therefore, it is recommended to allocate 16 CPU cores and 64 GB RAM for each BE node. It is recommended that BE nodes have at least 16 cores and 64 GB RAM.

<span id="_3-1-基于数据量的资源评估基准"></span>
### 3.1 Resource evaluation benchmarks based on data volume

According to community practices, under normal circumstances and with low QPS for 1 TB of data, the minimum reference configuration is 8C\-16G 200G*3 for FE nodes and 16C\-64G 800G*3 for BE nodes. However, it is still necessary to estimate based on actual business scenarios after testing.


|Data volume |FE node CPU\-Memory |BE node CPU\-Memory |
|---|---|---|
|1TB |8C \- 16GB \* 3 |16C \-64GB \* 3 |


<span id="_3-2-fe节点资源配置原则"></span>
### 3.2 FE node resource configuration principles

FE resources are calculated per node. If high availability is configured, this is equivalent to three nodes, and each node will occupy the same amount of memory. The document only provides a reference value. Typically, for ten million Tablets, FE memory usage is around 20 GB. In addition to metadata, you also need to consider the memory usage from SQL Session connections and the memory consumption during SQL processing.

When the data volume doubles, or when QPS increases due to other factors, dynamic adjustments can be made based on monitoring.

<span id="_3-3-be-节点资源配置原则"></span>
### 3.3 Principles for BE node resource configuration


1. Total memory of BE nodes:

   1. The upper limit of available memory for BE nodes should be determined based on the server's total physical memory.

   2. Reserve sufficient memory for the operating system and other processes; it is generally recommended to allocate at least 20%\-30% of system memory to the operating system.

2. BE node configuration:

   1. The relevant memory configurations for BE nodes are set in `be.conf` (the BE configuration file).

   2. Key configuration items include `mem_limit` and `storage_page_cache_limit`.

   3. `mem_limit` is the maximum memory that the BE process can use.

   4. `storage_page_cache_limit` is responsible for the page cache of table data.

3. Data volume estimation:

   1. It is necessary to assess your data volume and expected growth in order to allocate sufficient memory to accommodate the data.

   2. For very large datasets, more memory or additional BE nodes may be required.

4. Query characteristics:

   1. If queries are very complex, such as involving a large amount of intermediate result computation or requiring high\-concurrency queries, memory requirements will be higher.

   2. For scenarios that require handling a large number of write operations concurrently, more memory is also needed to ensure query performance.

5. Monitoring and tuning:

   1. Use the monitoring tools provided by StarRocks to analyze the performance of BE nodes.

   2. Adjust memory configurations based on monitoring results and system logs.


<span id="_3-4-动态评估资源用量并规划"></span>
### 3.4 Dynamically assess and plan resource usage

You can analyze BE memory usage using the following methods.


* **Access the Metrics interface via a browser or curl command to analyze memory usage.** 


Metrics statistics are updated every 10 seconds.

```bash
curl -XGET -s http://be_ip:8040/metrics | grep "^starrocks_be_.*_mem_bytes\|^starrocks_be_tcmalloc_bytes_in_use"
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace the above <code>be_ip</code> with the actual IP address of the BE node.</div>


* <div data-tips="true" data-tips-type="tip">BE <code>be_http_port</code> defaults to <code>8040</code>.</div>


* **Access the mem_tracker interface via a browser or curl command to analyze BE memory usage.** 


```bash
http://be_ip:8040/mem_tracker
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace the above <code>be_ip</code> with the actual IP address of the BE node.</div>


* <div data-tips="true" data-tips-type="tip">BE <code>be_http_port</code> defaults to <code>8040</code>.</div>



<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_53f2d86813075dc13621ef8899f6aa81.png) </span>

Indicator descriptions:


* `level`: MemTracker uses a tree structure. The first level represents the total memory used by BE, and the second level represents categorized memory usage.

* `Label`: Identifies the memory category.

* `Parent`: Parent node label.

* `Limit`: Memory usage limits; `-1` indicates no limit.

* `Current Consumption`: Current memory usage.

* `Peak Consumption`: Peak memory usage.

* **Access the TCmalloc interface via a browser or curl command to analyze BE memory usage.** 


```bash
http://be_ip:8040/memz
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace the above <code>be_ip</code> with the actual IP address of the BE node.</div>


* <div data-tips="true" data-tips-type="tip">BE <code>be_http_port</code> defaults to <code>8040</code>.</div>



Indicator descriptions:


* `Bytes in use by application`: Actual memory used by BE.

* `Bytes in page heap freelist`: Memory that is no longer used by BE but has not yet been returned to the operating system.

* `Actual memory used`: The actual memory usage of BE as detected by the operating system (BE reserves some free memory, which is either not returned to the operating system or is returned slowly).

* `Bytes released to OS`: Memory that BE has marked as reclaimable but has not yet been reclaimed by the operating system.


<span id="_3-4-1-详细内存分类"></span>
#### 3.4.1 Detailed memory classification

The memory in StarRocks BE is divided into the following categories.


|Identifier |Metric name |Note |BE\-related configuration |
|---|---|---|---|
|process |starrocks_be_process_mem_bytes |Actual memory used by the BE process (excluding reserved free memory). |mem_limit |
|query_pool |starrocks_be_query_mem_bytes |Total memory used by the BE query layer. | |
|load |starrocks_be_load_mem_bytes |Total memory used by import tasks. |load_process_max_memory_limit_bytes, load_process_max_memory_limit_percent |
|table_meta |starrocks_be_tablet_meta_mem_bytes |Total memory used for metadata. | |
|compaction |starrocks_be_compaction_mem_bytes |Total memory used for version compaction. |compaction_max_memory_limit, compaction_max_memory_limit_percent |
|column_pool |starrocks_be_column_pool_mem_bytes |Column pool memory pool, used to accelerate column cache for reading data from the storage layer. | |
|page_cache |starrocks_be_storage_page_cache_mem_bytes |BE storage layer page cache. |disable_storage_page_cache, storage_page_cache_limit |
|chunk_allocator |starrocks_be_chunk_allocator_mem_bytes |CPU per\-core cache, used to accelerate small memory allocations. |chunk_reserved_bytes_limit |
|consistency |starrocks_be_consistency_mem_bytes |Memory used for periodic consistency checks. |consistency_max_memory_limit_percent, consistency_max_memory_limit |
|schema_change |starrocks_be_schema_change_mem_bytes |Total memory used by Schema Change tasks. |memory_limitation_per_thread_for_schema_change |
|clone |starrocks_be_clone_mem_bytes |Total memory used by Tablet Clone tasks. | |
|update |starrocks_be_update_mem_bytes |Total memory used by primary key tables. | |


<span id="_3-4-2-建议资源配置内存相关配置项"></span>
#### 3.4.2 Recommended memory\-related configuration items for resource allocation


|Name |Default value |Note |
|---|---|---|
|mem_limit |90% |BE process memory limit. Can be set as a percentage limit (such as "80%") or a physical limit (such as "100G"). The default hard limit is 90% of the memory on the machine where the BE is located, and the soft limit is 80% of the memory on the machine where the BE is located. If BE is deployed independently, no configuration is required. If BE is deployed together with other memory\-intensive services, reasonable configuration is needed. |
|load_process_max_memory_limit_bytes |107374182400 |The maximum memory usage for all import threads on a single node is determined by taking the smaller value between mem_limit \* load_process_max_memory_limit_percent / 100 and load_process_max_memory_limit_bytes. If the import memory reaches the limit, it will trigger flush and backpressure logic. |
|load_process_max_memory_limit_percent |30 |The upper limit ratio for memory occupied by all import threads on a single node. The smaller value between mem_limit \* load_process_max_memory_limit_percent / 100 and load_process_max_memory_limit_bytes is used. When import memory reaches the limit, flush and backpressure logic will be triggered. |
|compaction_max_memory_limit |\-1 |The maximum memory usage for all Compaction threads. The smaller value between mem_limit \* compaction_max_memory_limit_percent / 100 and compaction_max_memory_limit is used. \-1 means no limit. It is currently not recommended to modify the default configuration. If Compaction memory reaches the limit, the Compaction task will fail. |
|compaction_max_memory_limit_percent |100 |The maximum memory usage percentage for all Compaction threads. The smaller value between mem_limit \* compaction_max_memory_limit_percent / 100 and compaction_max_memory_limit is used. \-1 means no limit. It is currently not recommended to modify the default configuration. If Compaction memory reaches the limit, the Compaction task will fail. |
|disable_storage_page_cache |FALSE |Whether to enable PageCache. After PageCache is enabled, StarRocks caches recently scanned data. For scenarios with high query repetition, this significantly improves query efficiency. true means disabled. This configuration item is used together with storage_page_cache_limit. Enabling it in scenarios with sufficient memory resources and large data volume scans can accelerate query performance. Since version 2.4, the default value of this parameter has changed from TRUE to FALSE. Since version 3.1, this parameter has changed from static to dynamic. |
|storage_page_cache_limit |20% |The upper limit for memory that can be used by the BE storage layer page cache. |
|chunk_reserved_bytes_limit |2147483648 |Cache used to accelerate small memory block allocation. The default upper limit is 2GB. You can enable this when memory resources are sufficient. |
|consistency_max_memory_limit_percent |20 |The upper limit for memory usage of a consistency check task. The smaller value between mem_limit \* consistency_max_memory_limit_percent / 100 and consistency_max_memory_limit is used. If memory usage exceeds the limit, the consistency check task will fail. |
|consistency_max_memory_limit |10G |The upper limit for memory usage of a consistency check task. The smaller value between mem_limit \* consistency_max_memory_limit_percent / 100 and consistency_max_memory_limit is used. If memory usage exceeds the limit, the consistency check task will fail. |
|memory_limitation_per_thread_for_schema_change |2 |The upper limit for memory usage of a single Schema Change task. If memory usage exceeds the limit, the Schema Change task will fail. |
|max_compaction_concurrency |\-1 |The upper limit for the number of Compaction threads (that is, the maximum concurrency of BaseCompaction + CumulativeCompaction). This parameter prevents Compaction from consuming excessive memory. \-1 means no limit. 0 means compaction is not allowed. |


**Session variables**


|Name |Default value |Note |
|---|---|---|
|query_mem_limit |0 |The memory limit for a single query on each BE node. Unit: Byte. It is recommended to set this to 17179869184 (16GB) or higher. |
|load_mem_limit |0 |The memory limit for a single import task on each BE node. Unit: Byte. If set to 0, StarRocks uses exec_mem_limit as the memory limit. |


<span id="_4存储空间"></span>
## 4 Storage space

<span id="_4-1-fe-存储"></span>
### 4.1 FE storage

Since FE nodes only maintain StarRocks metadata in their storage, in most scenarios, each FE node only requires 128 GB of HDD/SSD storage.

<span id="_4-2-be-存储"></span>
### 4.2 BE storage

<span id="_4-2-1-预估-be-初始存储空间"></span>
#### 4.2.1 Estimating initial BE storage space

The total storage space required by a StarRocks cluster is affected by the size of the raw data, the number of data replicas, and the compression ratio of the data compression algorithm used.

You can estimate the total storage space required for all BE nodes using the following formula:

```plain
BE 节点所需的总存储空间 = 原始数据大小 * 数据副本数/数据压缩算法压缩比

原始数据大小 = 单行数据大小 * 总数据行数
```


In StarRocks, the data in a table is first divided into multiple partitions, and then further divided into multiple tablets. A tablet is the basic data management unit in StarRocks. To ensure high data reliability, you can maintain multiple replicas for each tablet, stored on different BE nodes. StarRocks maintains three replicas by default.

Currently, StarRocks supports four data compression algorithms: zlib, Zstandard (or zstd), LZ4, and Snappy (listed in order from highest to lowest compression ratio). These data compression algorithms can provide a compression ratio of 3:1 to 5:1.

After calculating the total storage space, you can simply divide it by the number of BE nodes in the cluster to estimate the average storage space required for each BE node.

<span id="_4-2-2-随时添加额外存储空间"></span>
#### 4.2.2 Add additional storage space at any time

If BE storage space is exhausted as raw data grows, you can supplement storage space by vertically or horizontally scaling the cluster or expanding cloud storage. For example, we can check the actual storage size while the cluster is running to make an estimate.


1. Estimate the size of the table and analyze whether the number of buckets is reasonable. The typical size of a bucket ranges from 100 MB to 1 GB (after data compression).

2. Log in to the ECS node of the BE instance and check the growth rate of Segment files in the data storage directory (the default is `/data01/ju/output/be/storage/data`):


```shell
find /data01/starrocks/be/storage/data -name *.dat |wc -l
shell
```


Example: After data import begins, the number of imported files can reach as high as 200,000 within two hours. If the import frequency is high, you can increase the size of the imported data.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea780d1a1d3068810656564d716d177d.png) </span>

By analyzing the memory consumption of BE during task execution, you can also determine whether memory expansion is needed.

You can add new BE nodes to the StarRocks cluster to redistribute the data across more nodes. After adding new BE nodes, StarRocks automatically rebalances the distribution of data among all BE nodes. All table types support this automatic balancing. Add additional storage volumes to BE nodes. After adding additional storage volumes, StarRocks automatically rebalances the data in all tables.

<span id="_4-2-3-基于存算分离的弹性be存储空间"></span>
#### 4.2.3 Elastic BE storage space based on storage\-compute separation

The StarRocks storage\-compute separation cluster adopts a storage\-compute separation architecture, designed specifically for cloud storage. In the storage\-compute separation mode, StarRocks stores data in TOS object storage compatible with the S3 protocol, while the local disk serves as a hot data cache to accelerate queries. Through the storage\-compute separation architecture, you can reduce storage costs and optimize resource isolation. In addition, the cluster's elastic scalability is also enhanced. When queries hit the cache, the query performance of the storage\-compute separation cluster is consistent with that of the integrated storage\-compute cluster.

Compared to the integrated storage\-compute architecture, StarRocks's storage\-compute separation architecture offers the following advantages:


* Low\-cost and seamlessly scalable storage.

* Elastic and scalable computing capacity. Because data is not stored on CN nodes, the cluster can be scaled in or out without cross\-node data migration or shuffle.

* Local disk caching of hot data to improve query performance.

* Optional asynchronous data import to object storage to improve import efficiency.
