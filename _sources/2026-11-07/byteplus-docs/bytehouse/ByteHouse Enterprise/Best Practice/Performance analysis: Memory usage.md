---
title: "Performance analysis: Memory usage"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/performance-analysis-memory-usage"
---

This article introduces how to analyze memory usage of ByteHouse enterprise edition queries through SQL.

<span id="dfe916ef"></span>
# **Example environment**

The following examples are based on the node 192.18. *.* , please change the parameters according to your scenario. If you do not know how to get the node name, you can obtain it by the following methods.


* Using SQL Statements: You can run the following statements to get the names of all cluster nodes.


```SQL
SELECT * FROM system.clusters;
```


<span id="2702fdd5"></span>
# Viewing and releasing system memory

Memory usage directly impacts system performance and stability. By viewing and analyzing the data in the `system.asynchronous_metrics` table, you can identify operations or data consuming significant memory, providing a basis for memory release.


* ## **View memory usage**   <span id="view-memory-usage"></span>


View memory usage for each node at 192.18. *.* .

```SQL
SELECT *,
       formatReadableSize(value)
FROM clusterAllReplicas('', system.asynchronous_metrics) 
WHERE (metric like '%Cach%'
  OR metric like '%Mem%')
  AND host() = '192.18.*.*'
ORDER BY metric;
```


```SQL
┌─metric───────────────────────┬───value─────┬─formatReadableSize(value)─┐
│ CGroupMemoryTotal            │ 34359738368 │ 32.00 GiB                 │
│ CGroupMemoryUsed             │  4641132544 │ 4.32 GiB                  │
│ CompiledExpressionCacheBytes │       16384 │ 16.00 KiB                 │
│ CompiledExpressionCacheCount │           2 │ 2.00 B                    │
│ FilesystemCacheBytes         │           0 │ 0.00 B                    │
│ FilesystemCacheFiles         │           0 │ 0.00 B                    │
│ HashTableStatsCacheEntries   │           8 │ 8.00 B                    │
│ HashTableStatsCacheHits      │      528011 │ 515.64 KiB                │
│ HashTableStatsCacheMisses    │          15 │ 15.00 B                   │
│ IndexMarkCacheBytes          │           0 │ 0.00 B                    │
│ IndexMarkCacheFiles          │           0 │ 0.00 B                    │
│ IndexUncompressedCacheBytes  │           0 │ 0.00 B                    │
│ IndexUncompressedCacheCells  │           0 │ 0.00 B                    │
│ MMapCacheCells               │           0 │ 0.00 B                    │
│ MarkCacheBytes               │        7968 │ 7.78 KiB                  │
│ MarkCacheFiles               │          24 │ 24.00 B                   │
│ MemoryCode                   │   390758400 │ 372.66 MiB                │
│ MemoryDataAndStack           │ 14373392384 │ 13.39 GiB                 │
│ MemoryResident               │   761221120 │ 725.96 MiB                │
│ MemoryShared                 │   377688064 │ 360.19 MiB                │
│ MemoryVirtual                │ 18072178688 │ 16.83 GiB                 │
│ OSMemoryAvailable            │ 32480075776 │ 30.25 GiB                 │
│ OSMemoryCached               │  4239949824 │ 3.95 GiB                  │
│ OSMemoryFreePlusCached       │ 32480169984 │ 30.25 GiB                 │
│ OSMemoryFreeWithoutCached    │ 28240220160 │ 26.30 GiB                 │
│ OSMemoryTotal                │ 32881352704 │ 30.62 GiB                 │
│ QueryCacheBytes              │           0 │ 0.00 B                    │
│ QueryCacheEntries            │           0 │ 0.00 B                    │
│ UncompressedCacheBytes       │      349487 │ 341.30 KiB                │
│ UncompressedCacheCells       │         114 │ 114.00 B                  │
└──────────────────────────────┴─────────────┴───────────────────────────┘
```


Analyze memory usage, focusing on the following parameters.


|**Parameter** |**Description** |
|---|---|
|cluster_name |Cluster name |
|MarkCacheBytes |Mark Cache.<br><br><br>* Record the number of bytes used by the current mark cache.<br><br>* ByteHouse uses mark cache to store index marks in the data file. |
|UncompressedCacheBytes |Uncompressed cache.<br><br><br>* Records the number of bytes used by the current uncompressed cache.<br><br>* ByteHouse data is usually compressed during storage to save space and improve I/O efficiency. The uncompressed cache is used to store data blocks read from the disk and decompressed, allowing direct retrieval from memory the next time the same data block is needed, without having to reread and decompress from disk, thereby further enhancing query performance. |


<span id="0150b6bb"></span>
## **Release cache**

After analyzing memory usage, you can release cache using the following SQL statement if needed.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">ByteHouse supports releasing the cache of a single node. You can select all nodes or a single node mode on the query page and execute the following command to release the cache of a single cluster node or all nodes. Releasing the cache will affect performance, possibly slowing down SQL execution. Please use it cautiously according to business scenarios.</div>


Release marked cache.

```SQL
SYSTEM DROP MARK CACHE;
```


Release uncompressed cache.

```SQL
SYSTEM DROP UNCOMPRESSED CACHE;
```


<span id="376ca03e"></span>
# View memory consumption during the Merge process

ByteHouse's Merge operation primarily serves to merge data parts to enhance query performance and reduce storage space. It is a regularly executed background process that may consume a considerable amount of memory.

Understanding the memory usage of Merge operations can help you identify whether it is the cause of high memory consumption in the system. You can view the specific memory usage of Merge operations by checking the `system.merges` table data.

<span id="4358cefb"></span>
## **View the total memory consumption before Merge**

View the total memory consumption of the current Merge on the 192.18. *.*  node.

```SQL
SELECT
  formatReadableSize (sum(memory_usage))
FROM
  clusterAllReplicas ('', system.merges)
WHERE
  host() = '192.18.*.*';
```


<span id="23e90a56"></span>
## **View details of Merge memory usage**

On the 192.18. *.*  node, view the detailed memory usage of the Merge from `2023-09-17 01:15:00` to `2023-09-17 01:30:00`.

```SQL
SELECT *
FROM   clusterAllReplicas ('', system.part_log)      -- Select records from the system.part_log table
WHERE (event_type = 'MergeParts')                           -- Find events where the event type is 'MergeParts'
  AND (event_time >= '2023-09-17 01:15:00')                 -- The event time is greater than or equal to September 17, 2023, 01:15:00
  AND (event_time <= '2023-09-17 01:30:00')                 -- And the event time is less than or equal to September 17, 2023, 01:30:00
  AND host() = '192.18.*.*'
ORDER BY peak_memory_usage DESC                             -- Sort the results in descending order based on the peak_memory_usage field
LIMIT 1    
```



* **Parameter description.** 



|**Parameter** |**Description** |
|---|---|
|cluster_name |Cluster Name |
|event_type |Event Type.<br><br>Obtain corresponding event information through different event types. You can get event types in ClickHouse using the following SQL statement.<br><br>```SQL```<br>```SELECT DISTINCT event_type FROM clusterAllReplicas ('', system.part_log) where host() = '192.18.*.*';```<br> |
|event_time |Event Time. |


<span id="4e17dc05"></span>
# View the memory consumption of InMemory datapart

In ByteHouse, `InMemory datapart` is commonly used to enhance query performance, and its memory consumption is a critical performance metric for ByteHouse. Understanding and monitoring the memory usage of `InMemory datapart` can help you better manage, allocate resources, and serve as a valid basis for system optimization.

The `system.parts` table provides information about partitions and data segments in the table, allowing you to view the memory usage details of `InMemory datapart`.

View the size of the `InMemory datapart` loaded into memory on the 192.18. *.*  node.

```SQL
SELECT
  sum(data_uncompressed_bytes)
FROM
  clusterAllReplicas ('', system.parts)
WHERE
  part_type = 'InMemory'
  AND host() = '192.18.*.*';
```


<span id="908cf98d"></span>
## View the total memory usage of the dictionary

In ByteHouse, the dictionary is an important data structure used to optimize query performance, especially when dealing with item mapping and foreign keys. By viewing the data in the `system.dictionaries` table, you can understand the loading state and memory usage of each dictionary.

Query the memory usage of the dictionary on the 192.18. *.*  node.

```SQL
SELECT 
  formatReadableSize(sum(bytes_allocated))
FROM clusterAllReplicas('', system.dictionaries)
WHERE host() = '192.18.*.*';
```


<span id="97dc09e0"></span>
## BitEngine dictionary memory usage

In ByteHouse, there is a special data type, BitMap64, which uses the BitEngine dictionary at the base to solve the problem of overly sparse elements in bitmap storage. Viewing the data in the system.bitengine table can help understand the memory usage.

```SQL
SELECT
    database,
    table,
    arraySum(encoded_columns_size) as dict_size,
    formatReadableSize(ceil(dict_size / 10000000.0) * 600 * 1024 * 1024) as memory_usage
FROM
    clusterAllReplicas('',system.bitengine）
WHERE host() = '192.18.*.*';
ORDER BY dict_size DES;
```


<span id="108f2a20"></span>
## View details of memory usage in the memory table

In ByteHouse, memory usage of engines like Memory, Set, and Join is limited; monitoring these metrics helps prevent errors or abnormal behavior due to memory overflow.

View the memory utilization of Memory, Set, and Join engine tables.

```SQL
SELECT
   `database`,
    name,
    formatReadableSize(total_bytes)
FROM clusterAllReplicas('',system.tables)
WHERE engine IN ('Memory','Set','Join');
```


<span id="7fec7b38"></span>
## View memory usage of queries

Targeted analysis of query memory usage during specific time frames can help identify potential memory bottlenecks or abnormal usage patterns during these periods.

In ByteHouse, the `system.query_log` table records detailed information about queries. This table can help you audit and analyze database usage, understand query performance, and thus solve potential problems.

<span id="ea71ef40"></span>
### **View the total memory consumption of currently running queries**

View the total memory consumption of queries currently running on nodes 192.18. *.* .

```SQL
SELECT formatReadableSize(sum(memory_usage)) -- The total memory occupied by currently running queries
FROM clusterAllReplicas('', system.processes)
WHERE host() = '192.18.*.*';
```


<span id="8f019fd8"></span>
### **View details of memory consumption of currently running queries**

View details of memory consumption of queries currently running on nodes 192.18. *.* .

```SQL
-- Memory occupancy of currently running queries
SELECT initial_query_id,
       elapsed,                               --Query execution time
       formatReadableSize(memory_usage),      --Memory consumption
       formatReadableSize(peak_memory_usage), --Peak memory allocation
       query                                  --Query details
FROM clusterAllReplicas('', system.processes)
WHERE host() = '192.18.*.*'
ORDER BY peak_memory_usage DESC
LIMIT 10;
```


<span id="96fecd5c"></span>
### **View details of memory consumption for historical Queries**

View the memory consumption details of the Queries run on node 192.18. *.*  between `2024-01-05 17:00:00` and `2024-01-05 17:40:00`.

```SQL
-- Memory occupancy of historical queries
SELECT type,
       event_time,
       initial_query_id,
       formatReadableSize(memory_usage),
       query
FROM clusterAllReplicas('', system.query_log)
WHERE (event_time >= '2024-01-05 17:00:00')
  AND (event_time <= '2024-01-05 17:40:00')
  AND host() = '192.18.*.*'
ORDER BY memory_usage DESC
LIMIT 10;
```
