---
title: "Best practice for vector search"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/best-practice-for-vector-search"
---

When using ByteHouse vector search features, ByteHouse provides a range of configuration parameters to help improve query accuracy and reduce response latency. You can choose to configure relevant parameters in the SQL table creation statement, config.xml file, or users.xml file as needed.

<span id="d170dd95"></span>
# SQL Table Creation Configuration

When creating tables with SQL statements, you can optimize vector search performance by configuring settings parameters. The recommended configuration is as follows:

```SQL
CREATE TABLE test_ann (
    id UInt64,
    embedding Array(Float32),
    INDEX vec_idx embedding TYPE HNSW('METRIC=COSINE, DIM=768')
)
ENGINE = MergeTree
ORDER BY id
SETTINGS 
    index_granularity = 128,         -- Reduce the Mark size
    index_granularity_bytes = 0,     -- Disable Adaptive Mark
    enable_vector_index_preload = 1, -- Enable index preloading
    merge_selector_config = '{"name": "dance", "max_parts_to_merge_base": 100, "min_parts_to_merge_base": 2, "min_parts_to_enable_multi_selection": 50, "max_total_rows_to_merge": 20000000, "max_parts_to_break": 10000, "enable_heuristic_to_align_parts": 0}'
;
```


**Parameter description**


|**Parameter** |**Function** |**Recommended value** |
|---|---|---|
|`index_granularity` |Control the number of rows included in each Mark; lowering this reduces read amplification and improves vector filtering accuracy. |`128` |
|`index_granularity_bytes` |Disable Adaptive Mark, fix Mark size, and reduce Mark positioning computation overhead. |`0` |
|`enable_vector_index_preload` |Load the vector index directly into memory after data is written to eliminate the initial query loading delay. |`1` |
|`merge_selector_config` |Optimize data merge strategy by controlling the number and scale of partitions merged to reduce the number of partitions scanned during queries. |See detailed explanation of merge_selector_config parameters below |


**Detailed Explanation of merge_selector_config Parameter**


|**Sub\-parameters** |**Function** |**Recommended value** |
|---|---|---|
|`name` |Select the merge algorithm; `dance` suits vector data distribution, balancing write and query performance. |`"dance"` |
|`max_parts_to_merge_base` |The maximum number of partitions merged in a single operation to prevent write blocking caused by excessive merging. |`100` |
|`min_parts_to_merge_base` |The minimum number of parts to trigger merging, preventing small parts from persisting long\-term and increasing scan overhead. |`2` |
|`max_total_rows_to_merge` |The maximum number of rows per merge to avoid building overly large indexes. |`20000000` |
|`max_parts_to_break` |When the number of parts exceeds this threshold, the built\-in strategy actively splits large parts to balance query performance and merge efficiency. |`10000` |
|`enable_heuristic_to_align_parts` |Disable heuristic alignment to simplify merge logic and reduce merge time. |`0` (disabled) |


<span id="1b299140"></span>
# User XML Configuration

Configure user\-level parameters through `users.xml` to optimize vector index construction efficiency and query performance. For details on modifying configuration parameters, please refer to [Modify configuration parameters](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters).

```Python
# Adjust based on actual import speed and number of CPU cores
<vector_index_build_threads>4</vector_index_build_threads>
<enable_new_ann>1</enable_new_ann>
<log_processors_profiles>0</log_processors_profiles>
<compile_expressions>0</compile_expressions>
<compile_sort_description>0</compile_sort_description> 
```



|**Parameter** |**Function** |**Recommended value** |
|---|---|---|
|`enable_new_ann` |Enable ByteHouse’s new generation vector approximate search engine, supporting efficient index algorithms like HNSW. |`1` (enabled) |
|`vector_index_build_threads` |Control the number of concurrent threads for vector index building to improve indexing speed with large datasets. |4\-8 (adjust based on CPU cores) |
|`log_processors_profiles` |Disable processor profile logs to reduce logging overhead and improve query performance. |`0` (disabled) |
|`compile_expressions` |Disable expression compilation optimization to avoid compile time overhead for complex vector calculations. |`0` (disabled) |
|`compile_sort_description` |Disable sort description compilation optimization to improve vector sorting performance. |`0` (disabled) |


<span id="01cea4ac"></span>
# Config xml configuration

For vector search scenarios with large data volumes, it is recommended to optimize the configuration through `config.xml`. For details on modifying configuration parameters, please refer to [Modify configuration parameters](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters).

```Python
<enable_use_local_lock>1</enable_use_local_lock>
## Adjust based on machine memory. Version 2.6 defaults to 2GB
<vector_index_cache_size>193273528320</vector_index_cache_size> ## 180 Gigabyte
<disk_unique_key_index_meta_cache_size>2147483648</disk_unique_key_index_meta_cache_size>
<disk_unique_key_index_data_cache_size>5368709120</disk_unique_key_index_data_cache_size>
<additional_services> # Can be added later, no restart required
  <VectorSearch>true</VectorSearch>
  <FullTextSearch>true</FullTextSearch>
</additional_services> 
```



|**Parameter** |**Function** |**Recommended value** |
|---|---|---|
|`enable_use_local_lock` |Enable local lock mechanism to reduce write conflicts and improve vector data write performance in high concurrency scenarios. |`1` (enabled) |
|`vector_index_cache_size` |Set the cache size of the vector index in memory, directly affecting the response speed of vector retrieval. |Adjust according to machine memory, recommended 100GB+ |
|`disk_unique_key_index_meta_cache_size` |Cache size for unique key index metadata, optimizing key\-value retrieval performance. |2147483648 bytes（2 GB） |
|`disk_unique_key_index_data_cache_size` |Cache size for unique key index data, improving data read speed. |5368709120 bytes（5 GB） |
|`additional_services` |Activate additional services dynamically without restarting the service. |Enable on demand |


&nbsp;
