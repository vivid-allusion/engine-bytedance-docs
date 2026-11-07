---
title: "HBase memory tuning"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/HBase_memory_tuning"
---

As the cluster's data volume and workload increase, the default configuration may not meet the performance requirements of the business. Adjusting HBase's memory configuration appropriately based on specific business scenarios helps improve HBase's performance. This article introduces common methods for HBase memory tuning.

<span id="c96ec57d"></span>
## JVM parameters

Note: JVM\-related configuration parameters.


|Configuration parameters |Parameter purpose |
|---|---|
|HBASE_OPTS |This parameter applies to all HBase roles. |
|HBASE_MASTER_OPTS |This parameter applies to HBase Master. |
|HBASE_REGIONSERVER_OPTS |This parameter applies to HBase RegionServer. |


HBase's performance mainly depends on RegionServer, so this article focuses on memory configuration in `HBASE_REGIONSERVER_OPTS`:


|JVM parameters |Parameter meaning |
|---|---|
|\-Xmx |Maximum heap size |
|\-Xms |Initial heap size |
|\-XX:MaxDirectMemorySize |Maximum off\-heap memory size |


To improve performance, you can increase the above memory configurations as appropriate based on business usage, or allocate more heap memory to off\-heap memory, and configure off\-heap memory implementations for BlockCache, MemStore, and many other.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When tuning HBase memory, also consider node memory specifications and the memory usage of other services. If the total memory configured for the service exceeds the node memory, the operating system's oom\-killer may be triggered, causing the service to crash.</div>


* <div data-tips="true" data-tips-type="warning">HBase provides several features that use off\-heap memory. Ensure that the MaxDirectMemorySize configuration is greater than the sum of all off\-heap memory configurations; otherwise, there is a risk of service failure.</div>



<span id="019a5d29"></span>
## HBase parameters

HBase relies on memory to achieve low\-latency read and write access. However, this brings JVM GC pressure, which can slow down requests or even cause service outages, affecting business stability. To alleviate GC pressure and reduce P99/P999 tail latency for RPC, HBase 2.x supports using off\-heap memory in both read and write paths.

<span id="45daca36"></span>
### Configure BlockCache

In the read path, HBase uses BlockCache to cache data read from HDFS, reducing read latency.

By default, BlockCache only uses heap memory to cache all data, which can cause significant GC pressure when cluster load is high. It is recommended to use CombinedBlockCache, which has two layers of cache: L1 is an on\-heap cache implemented by LruBlockCache for caching metadata blocks (INDEX and BLOOM); L2 is BucketCache for caching data blocks (DATA), which can be implemented using off\-heap memory or files.


|Parameter |Note |Default value |
|---|---|---|
|`hfile.block.cache.size` |The maximum percentage of heap memory (\-Xmx) allocated to LruBlockCache.<br><br>If CombinedBlockCache is not enabled, this is the total BlockCache capacity; if CombinedBlockCache is enabled, this is the L1 cache capacity. |0.4 |
|`hbase.bucketcache.ioengine` |BucketCache provides three modes:<br><br><br>* offheap: Uses off\-heap memory as the L2 cache.<br><br>* file: Uses files as the L2 cache. For a single file, for example `file:PATH_TO_FILE`; for multiple files, for example `files:PATH_TO_FILE1,PATH_TO_FILE2,PATH_TO_FILE3`<br><br>* mmap: Uses mmapped files as the L2 cache. Configuration method: `mmap:PATH_TO_FILE` |The default is empty, and BucketCache is not enabled. |
|`hbase.bucketcache.size` |Indicates the capacity of BucketCache.<br><br>When both `hbase.bucketcache.ioengine` and `hbase.bucketcache.size` are configured, the CombinedBlockCache implementation is enabled.<br><br>Unit: MB. |0 |


<span id="6fa79aed"></span>
### Configure MemStore

By default, MemStore in HBase uses MSLAB to create fixed\-size chunks for storing written Cells and pools these chunks to avoid memory fragmentation and reduce GC pressure. Starting from HBase 2.x, the MSLAB pool is enabled by default, and using off\-heap memory for MemStore is also supported.


|**Parameter** |**Note** |Default value |
|---|---|---|
|`hbase.regionserver.global.memstore.size` |When using heap memory for MemStore, the maximum percentage of heap memory (\-Xmx) used by MemStore. |0.4 |
|`hbase.regionserver.offheap.global.memstore.size` |This configuration defaults to 0. When set to a value greater than 0, off\-heap memory is used for MemStore.<br><br>This value indicates the off\-heap memory capacity used by MemStore.<br><br>Unit: MB |0 |
|`hbase.hregion.memstore.mslab.enabled` |Whether to enable MSLAB. |true |
|`hbase.hregion.memstore.mslab.chunksize` |The chunk size for MSLAB. The default is 2 MB.<br><br>Unit: B |20997152 |
|`hbase.hregion.memstore.chunkpool.initialsize` |The proportion of memory prepared for MemStore at startup. When write pressure is low, it is not recommended to set this value, as it may lead to low memory utilization and frequent Full GC. |0 |
