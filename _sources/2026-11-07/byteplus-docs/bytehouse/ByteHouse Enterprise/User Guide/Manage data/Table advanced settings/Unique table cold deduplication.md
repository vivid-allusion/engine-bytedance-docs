---
title: "Unique table cold deduplication"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/unique-table-cold-deduplication"
---

The unique table supports cold storage deduplication, allowing deletion of duplicate data in cold storage to improve storage space efficiency. This tutorial explains how to enable unique table cold storage deduplication and configure related memory parameters to reduce memory usage.

<span id="9fea1af8"></span>
# Background

In ByteHouse, cold storage data is stored on S3 while the local disk caches the remote `unique_key.idx` index file in the `/remote_unique_key_index_cache/` directory (shared by all unique tables) to avoid frequent S3 index file reads during deduplication, reducing additional performance overhead. Given sufficient local disk space, the default size of the `/remote_unique_key_index_cache/` directory is `min(50 GiB, available space * 0.25)`. When the storage directory reaches its limit, the system triggers an LRU (least recently used) eviction policy. When a remote part becomes inactive and is cleared, the corresponding unique index cached on the local disk is asynchronously deleted by the unique table’s background cleanup thread.

To achieve better cold storage write performance, newly created unique table parts are generated locally: the primary node supports write, merge, and mutate operations, while the replica node supports fetch part operations. Parts that meet the TTL (time to live) rule will be moved to S3/HDFS cold storage by the background move thread.

After enabling the unique table cold storage deduplication feature, memory usage will briefly increase because the system needs to deduplicate parts on S3 when writing cold data. Since parts on S3 may not have disk unique indexes, the data must first be loaded into memory to build memory unique indexes. ByteHouse supports managing memory usage through the memory unique index cache mechanism, which uses background threads to promptly evict memory indexes that exceed the memory threshold, improving global memory limit capabilities. If you need to limit the memory usage of memory unique indexes, you can refer to [memory_unique_index_max_bytes](https://docs.byteplus.com/docs/bytehouse/unique-table-cold-deduplication#92801eee)to set parameter thresholds. After enabling, it takes some time (minutes) to take effect, and memory usage may temporarily exceed the set threshold.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The memory index of Part uses a lazy loading mode and only loads when used for deduplication. Newly written parts' memory indexes are not immediately loaded into memory, so the total memory index usage may show as 0.</div>


<span id="3e935bf7"></span>
# Enable unique table cold storage deduplication

<span id="1c848e0f"></span>
## Syntax

Run the following command to enable deduplication for unique tables and parts on cold storage. After enabling, deduplication only applies to incremental parts (i.e., newly written parts).

```SQL
alter table {db}.{table} on cluster {xxx} modify setting enable_unique_dedup_with_remote_disk = true;
```


**Parameter description**


|Parameter |Default Value |Description |
|---|---|---|
|enable_unique_dedup_with_remote_disk |false |At the table level granularity, setting to true allows new writes and remote parts deduplication to ensure uniqueness. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you want it to take effect on all tables, refer to <a href="https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters">Modify configuration parameters</a> and add the parameter under <code>config.xml</code> within <code><merge_tree></merge_tree></code>. Restart the server for the changes to take effect after adjusting the parameters.</div>


<span id="6cfd851c"></span>
## Example

The following operations use a unique table on S3 as an example.


1. Enable the cold storage deduplication feature. Replace the variables in the following commands with the actual database, table, and cluster names.

   ```SQL
   alter table {db}.{table} on cluster {xxx} modify setting enable_unique_dedup_with_remote_disk = true;
   ```
   

2. Enable the cold storage merge switch; otherwise, when there are too many S3 parts, it will affect write deduplication performance.

   ```SQL
   ALTER TABLE {db}.{table} on cluster {xxx} modify setting skip_merge_for_unique_data_in_remote_disk = false; 
   ```
   

3. Check the memory usage of all unique tables on the node. For more memory query commands, see [memory_unique_index_max_bytes](https://docs.byteplus.com/docs/bytehouse/unique-table-cold-deduplication#92801eee).

   You can check memory usage based on the command output. If memory usage increases, follow the steps in step 4 to reduce memory consumption.

   ```SQL
   select formatReadableSize(sum(unique_index_bytes_in_memory))
   from system.parts
   where engine = 'HaUniqueMergeTree'; 
   ```
   

4. (Optional) If your memory usage increases significantly and you want to reduce it, you can lower memory consumption using the following two options:

   
   |Option |Instructions |
   |---|---|
   |Adjust the `memory_unique_index_max_bytes` parameter |The `memory_unique_index_max_bytes` parameter defines the maximum available memory for the in\-memory unique index of all unique tables. The default value is the maximum available memory \* 0.3\*\*,\*\* unit: bytes.<br><br>You can refer to [Modify configuration parameters](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters) and configure the `memory_unique_index_max_bytes` parameter in config.xml. The example below sets `memory_unique_index_max_bytes` to 30MiB (30 \* 1024 \* 1024 = 31457280). Restart the server for the changes to take effect after adjusting the parameters.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2768ab98dae4ff5b01e32d8f3b73dac~tplv-goo7wpa0wc-image.image) </span><br><br>For more information about this parameter, refer to the [memory_unique_index_max_bytes](https://docs.byteplus.com/docs/bytehouse/unique-table-cold-deduplication#92801eee) chapter. |
   |Materialized index |Execute the materialized index command to convert the memory unique index of a partition's unique table into a disk unique index. This mutation operation is heavy. It is recommended to materialize indexes at the partition level to avoid rewriting too many parts at once, which could fill up the local disk.<br><br>```SQL```<br>```ALTER TABLE {} on cluster {} MATERIALIZE UNIQUE INDEX IN PARTITION '{}';```<br><br><br>For more information about materialized indexes, refer to the [materialize unique index](https://docs.byteplus.com/docs/bytehouse/unique-table-cold-deduplication#be80d77c) chapter. |
   


<span id="a0bef9b3"></span>
# Related parameters

<span id="2477869d"></span>
## Query disk unique index cache

You can use the following commands to check the size and capacity of the disk index cache. This cache stores the `unique_key.idx` index files (managed by part granularity), supporting LRU eviction and global memory limits.

```SQL
SELECT
    metric,
    formatReadableSize(value)
FROM system.asynchronous_metrics
WHERE metric LIKE 'UniqueKeyIndex%Bytes'

Query id: 20528fa9-5d92-4961-90ae-1c221e8d8cb7

┌─metric────────────────┬─formatReadableSize(value)─┐
│ UniqueKeyIndexMetaCacheBytes     │ 0.00 B                      │
│ UniqueKeyIndexBlockCapacityBytes │ 20.00 GiB                   │
│ UniqueKeyIndexMetaCapacityBytes  │ 10.00 GiB                   │
│ UniqueKeyIndexBlockCacheBytes    │ 0.00 B                      │
└────────────────────┴──────────────────┘
```


<span id="92801eee"></span>
## memory_unique_index_max_bytes

The memory unique index is an in\-memory table used to store data for unique indexes. The `memory_unique_index_max_bytes` parameter limits the maximum available memory for the memory unique index to prevent out\-of\-memory (OOM) errors.


* Check the maximum capacity of the memory unique index:

   ```SQL
   -- Query the maximum capacity of Memory unique index:
   SELECT
       metric,
       formatReadableSize(value)
   FROM system.asynchronous_metrics
   WHERE metric LIKE 'MemoryUniqueKeyIndex%'
   ```
   

* Check the memory usage of the memory unique index:

   ```SQL
   -- Get the memory usage of memory indexes for all unique tables on the node
   select formatReadableSize(sum(unique_index_bytes_in_memory))
   from system.parts
   where engine = 'HaUniqueMergeTree';
   
   -- Get the top 10 unique tables by memory index memory usage on the node
   select database || '.' || table as db_tbl, 
   formatReadableSize(sum(unique_index_bytes_in_memory)) 
   from system.parts where engine = 'HaUniqueMergeTree' and active 
   group by db_tbl order by sum(unique_index_bytes_in_memory) desc limit 10;
   
   -- Query total memory of memory unique index for a table
   SELECT formatReadableSize(sum(unique_index_bytes_in_memory))
   FROM system.parts
   WHERE engine = 'HaUniqueMergeTree' and table = '';
   ```
   


<span id="be80d77c"></span>
## materialize unique index

Use the memory unique index to convert specified parts through mutation into parts using the local disk unique index, reducing memory usage. This command is also called materializing the index, meaning converting the in\-memory index to a disk\-based index. You can execute this command on both primary and standby nodes; the standby node will forward the command to the primary node after receiving it. Example:

```SQL
ALTER TABLE materialize_unique_index_{table.table_name} [on cluster {}] MATERIALIZE UNIQUE INDEX;
```


<span id="7d539eb0"></span>
### **Example 1: Table\-level setting**

```SQL
ALTER TABLE materialize_unique_index_tests.test_table1 [on cluster {}] MATERIALIZE UNIQUE INDEX;
```


<span id="742d6371"></span>
### **Example 2: Partition\-level setting**

```JavaScript
ALTER TABLE materialize_unique_index_tests.test_table1 on cluster {} MATERIALIZE UNIQUE INDEX IN PARTITION '2024-10-02';
```


&nbsp;
