---
title: "Hive metastore cache"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/hive-metastore-cache"
---

To accelerate access to external Hive tables, ByteHouse has developed Hive metastore cache, storing metastore in server memory to reduce the overhead of accessing the Hive Metastore. This significantly improves query performance when the same tables or partitions are frequently accessed by business processes. This article introduces the source data cache feature of Hive and how to use it.

<span id="2b4c2187"></span>
# Function overview

<span id="a1eacb47"></span>
## Hive metastore cache procedure

ByteHouse supports separately caching Hive external table metastore at four levels—table schema, partition name, partition information, and remote files—in the memory of a private server.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ff8e903c2384e83bd0363031d2ed941~tplv-goo7wpa0wc-image.image) </span>

<span id="28278ef2"></span>
## Hive metastore cache level

Hive metastore cache consists of four levels: Schema Cache, Partition Name Cache, Partition Cache, and Remote File Cache. The details are as follows:


|Cache level |Cache key |Cache Value |Cached content |
|---|---|---|---|
|**Schema Cache** |Hive database names and table names, such as `db.table_name`. |`StorageInMemoryMetadata` |Cache table schema, column name, column type, partition key. |
|**Partition Name Cache** |Hive table name. |Collection of partition name strings (`List<String>`) |All partition names of the current table, such as `dt=2025-05-20/region=us`. |
|**Partition Cache** |Hive partition name. For example, `db.table/dt=2025-05-20/region=us`. |`DataLakeCache::Partition` |The physical path information for the partitions contained in the storage table, as well as other meta attributes. |
|**Remote File Cache** |The remote path for partition storage includes the Hive table name and partition name. |`List<DataLakeCache::RemoteFile>` |All file names, file sizes, modification times, and other information under this partition to avoid retrieving directory contents from remote storage (such as HDFS or S3) during each scan. |


<span id="43437af3"></span>
## Cache strategy

The metastore cache strategy adopts a combination of "LRU Cache (least recently used cache) + TTL (time to live)". The specific logic is as follows:


* It binds an independent TTL value to the cache key of each metastore record. Within the TTL validity period, the system does not repeatedly initiate data retrieval requests to the remote endpoint, but instead reads data directly from the local cache to improve access efficiency.

* When the TTL value of a cache key expires, the system automatically deletes the corresponding cached content. It then requests the latest data from the Hive metastore (metadata storage) and synchronously updates the TTL value for that key to ensure the cache remains up to date.

* TTL time for different cache levels is as follows:

   
   |Cache level |Ttl |
   |---|---|
   |**Schema Cache** |900 s |
   |**Partition Name Cache** |900 s |
   |**Partition Cache** |21600 s |
   |**Remote File Cache** |21600 s |
   


<span id="2ebf9b36"></span>
# Prerequisites

The Hive metastore cache feature depends on a private server. You must purchase a private server before use. Enabling Hive metastore cache will occupy the private server's memory. For an introduction and activation instructions for the private server, see [Private server](https://docs.byteplus.com/docs/bytehouse/private-server).

<span id="82592d5d"></span>
# Use Hive metastore cache

ByteHouse supports enabling Hive metastore cache by configuring user\-level SQL parameters. Once enabled, you can monitor the usage of the Hive metastore cache through the tenant's `bh_system.query_log` system table. Caution: Relevant parameters must be added to each query; otherwise, ByteHouse will not enable Hive metastore cache.

<span id="18d9a740"></span>
## Enable Hive metastore cache

By adding settings parameters at the user SQL level when executing each SQL statement, you can control the enabled state of the Hive metastore cache and set the expiration time for each cache level at the query level. Currently, enabling during table creation is not supported.

ByteHouse supports two methods to enable this feature: configure it through SQL parameter groups, or add the settings parameter directly in the query.

<span id="33c23001"></span>
### Enable via SQL parameter groups

When executing SQL statements in the ByteHouse Cloud Data Warehouse Console, you can add Hive metastore\-related parameters as an SQL parameter group. Before running SQL statements, select the parameter group, and ByteHouse will, by default, add the parameter group when executing SQL statements. For instructions on how to configure this, refer to [Use SQL parameter groups](https://docs.byteplus.com/docs/bytehouse/docs-query-editor-and-worksheet#b8e3c040). For the parameters that can currently be set, see [Parameter description](https://docs.byteplus.com/docs/bytehouse/74140#412a69dd). Examples of settings are as follows:

```XML
<sql_parameters>
       <enable_hive_schema_cache>false</enable_hive_schema_cache>
       <hive_schema_cache_ttl>1000</hive_schema_cache_ttl>
</sql_parameters>
```


<span id="dff17ff2"></span>
### Enable via the settings parameters

You can add the settings parameter each time you execute an SQL statement to enable Hive metastore cache. For the parameters that can currently be set, see [Parameter description](https://docs.byteplus.com/docs/bytehouse/74140#412a69dd). Examples are as follows:

```SQL
-- Enable during query
SELECT * FROM ext.las 
SETTINGS 
    enable_hive_schema_cache = 'true', -- Enable Hive table schema cache
    hive_schema_cache_ttl = '1000'; -- Set the Hive table schema cache expiration time to 1000 seconds
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">See <a href="https://docs.byteplus.com/docs/bytehouse/hive-external-table">Hive external table</a> for creating and using Hive external tables.</div>


<span id="412a69dd"></span>
### Parameter description


|Parameter |Description |
|---|---|
|`enable_hive_schema_cache` |Whether to use table schema cache. You can set this option to false or true, or to 0 (equivalent to false) or 1 (equivalent to true). The system will convert the values accordingly.<br><br>The default value is true, and the data type is Bool. |
|`hive_schema_cache_ttl` |Set the lifetime of the table structure cache. The unit is seconds.<br><br>The default value is 900, and the data type is UInt64. |
|`enable_hive_partition_name_cache` |Whether to use partition name cache. You can set this option to false or true, or to 0 (equivalent to false) or 1 (equivalent to true); the system will convert the value accordingly.<br><br>The default value is true, and the data type is Bool. |
|`hive_partition_name_cache_ttl` |Set the lifetime of the partition name cache. The unit is seconds.<br><br>The default value is 900, and the data type is UInt64. |
|`enable_hive_partition_cache` |Whether to use Hive partition metastore cache. You can set this option to false or true, or to 0 (equivalent to false) or 1 (equivalent to true); the system will convert the values accordingly.<br><br>The default value is true, and the data type is Bool. |
|`hive_partition_cache_ttl` |Set the lifetime of the Hive partition cache. The unit is second.<br><br>The default value is 21600, and the data type is UInt64. |
|`enable_hive_remote_file_cache` |Whether to use remote file cache. You can set it to false or true, or to 0 (corresponding to false) or 1 (corresponding to true); the system will convert the values accordingly.<br><br>The default value is true, and the data type is Bool. |
|`hive_remote_file_cache_ttl` |Set the lifetime of the remote file cache, in seconds.<br><br>The default value is 21600, and the data type is UInt64. |


<span id="4199269f"></span>
## Monitor cache metrics

You can query the tenant's `bh_system.query_log` system table to view cache metrics, including whether SQL hit the Hive metastore cache and the number of times expired caches were detected.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><code>bh_system.query_log</code> system table is a non\-public feature and requires allowlist access. Before use, please submit a ticket or contact the ByteHouse team to obtain allowlist permission. For details on feature usage, please refer to <a href="https://docs.byteplus.com/docs/bytehouse/sql-audit#60829051">Detailed log (query_log)</a>.</div>


Using the `bh_system.query_log` system table, you can query and obtain the value of the corresponding cache metric based on the specific Key in the event source `ProfileEvents`. The correspondence between cache metrics and event source Key is as follows:


|Cache metrics |Key of event source (`query_log.ProfileEvents`) |
|---|---|
|Cache deliveries |The metric is presented in the form `DataLake{Schema\|PartitionName\|Partition\|RemoteFiles}CacheHits`, with the meaning explained as follows:<br><br><br>* `DataLakeSchemaCacheHits`: Table schema cache hit count.<br><br>* `DataLakePartitionNameCacheHits`: Partition name cache hit count.<br><br>* `DataLakePartitionCacheHits`: Partition cache hit count.<br><br>* `DataLakeRemoteFilesCacheHits`: Remote file cache hit count. |
|Cache miss count |The metric is presented in the form of `DataLake{Schema\|PartitionName\|Partition\|RemoteFiles}CacheMisses`. The explanation is as follows:<br><br><br>* `DataLakeSchemaCacheMisses`: Number of cache misses for table schemas.<br><br>* `DataLakePartitionNameCacheMisses`: Number of partition name cache misses.<br><br>* `DataLakePartitionCacheMisses`: Number of partition cache misses.<br><br>* `DataLakeRemoteFilesCacheMisses`: Number of cache misses for the remote file cache. |
|Number of times an expired cache is detected (retrieved again from the remote source) |The metric is presented in the form of `DataLake{Schema\|PartitionName\|Partition\|RemoteFiles}CacheExpired`. The meaning is explained as follows:<br><br><br>* `DataLakeSchemaCacheExpired`: Lifetime of the table schema cache.<br><br>* `DataLakePartitionNameCacheExpired`: Lifetime of the partition name cache.<br><br>* `DataLakePartitionCacheExpired`: Lifetime of the partition cache.<br><br>* `DataLakeRemoteFilesCacheExpired`: Lifetime of the remote file cache. |


Examples of query methods are as follows:

```SQL
SELECT
    k,
    v
FROM bh_system.query_log
ARRAY JOIN
    mapKeys(ProfileEvents) AS k,
    mapValues(ProfileEvents) AS v
WHERE (query_id = '4e9xxxxx-xxxx-xxxx-xxxx-0bxxxxxxxxxx') AND (k LIKE '%DataLake%')
```


**Parameter description**


|Parameter |Description |
|---|---|
|`k` |Set it to k. This means querying the metric name of currently enabled cache events. |
|`v` |Set it to v. This indicates the statistical value of the metrics, that is, the number of occurrences of various cache events. |
|`ARRAY JOIN...AS...` |Pair the extracted keys and values to form multiple rows of data; here, this is used to parse the key\-value pair data in the `ProfileEvents` field and expand it into multiple records.<br><br><br>* `mapKeys(ProfileEvents) AS k`: Parse all cache metric names stored in the `ProfileEvents` field.<br><br>* `mapValues(ProfileEvents) AS v`: Parse the statistical values for each metric in the `ProfileEvents` field. |
|`WHERE...AND...` |Use WHERE to filter data, retaining only records that meet the condition.<br><br><br>* `AND`: Indicates that both conditions must be satisfied.<br><br>* `query_id`: Specifies the ID of the target SQL statement to query.<br><br>* `k LIKE '%DataLake%'`: Filter criteria, indicating that only measures related to the Hive metastore cache are retained. |


Sample output results are as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c38942e3dc14b968bfca184e743ddc0~tplv-goo7wpa0wc-image.image) </span>
