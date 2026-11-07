---
title: "Parameter list"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/parameter-list"
---

This article introduces the query parameters and table parameters that can be configured in ByteHouse.

<span id="ed37fb23"></span>
# Background information

The following table lists the terms used in this document.


|**Name** |**Introduction** |
|---|---|
|worker |Nodes of the virtual warehouse. |
|Dedup |Deduplication is a process used by the unique key engine to ensure data uniqueness and achieve the desired result by removing duplicate data. |
|Dedup task |After the dedup task is completed, the selected data parts will become visible. |
|Dedup worker |A deduplication computing node is used to select and execute running instances for dedup tasks, and by default, it selects the account\-level write virtual warehouse. |
|Staging area |The data staging area is located in the default cache or virtual warehouse local disk and is used to accumulate deduplicated data into batches for batch processing. |
|Staged part |Data blocks in the staging area are located in the default cache or virtual warehouse local disk; part data stored in the staging area is not visible to queries. |


<span id="d2e8dd92"></span>
# Query parameters

<span id="ead51ea9"></span>
## Data query (SELECT)


|**Parameter name** |**Parameter types** |**Optional values** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|enable_point_lookup_profile |Bool |true/false |false |It defines whether to use a lookup profile to optimize lookup efficiency. |
|max_threads |UInt64 |0 ≤ X ≤ number of CPU cores |0 |The single\-machine query parallelism. |
|max_plan_segment_num |UInt64 |0 ≤ X |500 |Maximum allowed number of plan segments; 0 means unlimited. |
|enable_intermediate_result_cache |Bool |true/false |false |It defines whether to enable intermediate result caching. |
|log_segment_profiles |Bool |true/false |false |It defines whether to enable ByteHouse SQL performance diagnostics functionality. |
|max_execution_time |UInt64 |1 ≤ X ≤ 8000 |Log in to the ByteHouse Cloud Data Warehouse console, and go to **Tenant management** \> **Parameter settings** \> **Virtual warehouse parameters**, search the parameter name and view the reference value. For details, refer to [Manage parameters](https://docs.byteplus.com/docs/bytehouse/manage-virtual-warehouse-parameters). |It defines the maximum execution time. The unit is second. |
|max_query_cpu_seconds |UInt64 |0 ≤ X ≤ 20000 ||It limits the maximum amount of CPU resources that a query segment can consume (unit: seconds). |
|distributed_max_parallel_size |UInt64 |0 ≤ X ≤ number of workers in the virtual warehouse |0 |It defines the concurrency for non\-Source PlanSegment: 0 indicates the total number of nodes in the virtual warehouse. If concurrency is high or the number of virtual warehouse workers exceeds 10, it is recommended to reduce this value. |
|join_algorithm |JoinAlgorithm |'grace_hash' 'auto', 'hash', 'partial_merge', 'prefer_partial_merge', 'parallel_hash', 'auto' |auto |It defines the Join algorithm. |
|max_memory_usage_ratio |Float |0.01 ≤ X ≤ 0.99 |None |It defines the maximum memory usage ratio for a single query. |


You can log in to the ByteHouse CDW console and, via the path **Tenant management** \> **Parameter settings** \> **Virtual warehouse parameters**, view the reference values in the virtual warehouse module.

<span id="2d931c8e"></span>
## Data insertion (INSERT)


|**Parameter name** |**Parameter types** |**Optional values** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|enable_unique_partial_update |Bool |true/false |true |It defines whether to use partial column update mode. This must be used together with the table\-level parameter of the same name. Partial column update mode takes effect if and only if **both this parameter and the table\-level parameter are enabled**. |
|partial_update_enable_row_level_defaults |Bool |true/false |true |When only part of the columns are updated, the columns that are not updated are filled with row\-level default values. |
|staging_area_wait_mode |StagingAreaWaitMode |no_wait/wait_txn_visible |no_wait |It defines the data write mode after **enabling the staging area**. `no_wait` indicates **asynchronous write mode**, `wait_txn_visible` indicates **synchronous write mode**. |
|enable_staging_area_for_write |Bool |true/false |false |**Whether to enable the staging area**, which supports scenarios for optimizing asynchronous or concurrent writes. |
|optimize_unique_table_write |Bool |true/false |false |Import optimization switch for `INSERT SELECT` on unique key tables. It is recommended to enable this only in scenarios where the staging area is not enabled and `dedup_impl_version` is set to 'dedup_in_txn_commit'. |
|max_insert_threads |UInt64 |Positive integer |0 |Configures the thread pool size for write operations when a Worker node executes an `INSERT SELECT` request. |
|min_insert_block_size_bytes |UInt64 |Positive integer |1073710080 |It controls the minimum size, in bytes, of a data batch block in the `INSERT SELECT` operation. |
|min_insert_block_size_rows |UInt64 |Positive integer |1048545 |It controls the minimum number of rows in a data batch block during `INSERT SELECT` operations. |


<span id="f9cfd85b"></span>
# Table parameters


|**Parameter name** |**Parameter types** |**Optional values** |**No default configuration value** |**Parameter description** |
|---|---|---|---|---|
|**Deduplication related to unique key tables** |||||
|unique_table_dedup_threads |MaxThreads |An integer value not exceeding the number of cores |8 |Each dedup task is split into subtasks with **different deduplication granularities** during execution. This parameter allows you to configure the thread pool size for executing these subtasks. |
|cloud_enable_staging_area |Bool |true/false |false |It defines whether to **enable the staging area** to support scenarios such as asynchronous writes or concurrent write optimization. |
|cloud_staging_area_wait_mode |StagingAreaWaitMode |no_wait/wait_txn_visible |no_wait |It defines the data write mode after **enabling the staging area**. `no_wait` represents **asynchronous write mode**, `wait_txn_visible` represents **synchronous write mode**. |
|min_check_txn_staging_area_visible_interval |UInt64 |Integer |50 |**When the staging area is enabled** and **write mode is set to wait_txn_visible**: the minimum interval for polling whether the data is already visible, in milliseconds (ms). |
|max_check_txn_staging_area_visible_interval |UInt64 |Integer |1000 |When **the staging area is enabled** and **the write mode is wait_txn_visible**, this parameter specifies the maximum interval for polling whether the data has become visible, in milliseconds (ms). |
|max_dedup_worker_number |UInt64 |Integer |1 |It is recommended to set the number of dedup workers to match the number of virtual warehouse pods configured for cnch_vw_write. |
|pick_dedup_worker_by_mod |Bool |true/false |false |For the distribution mode of Dedup worker, when the configuration is set to true, distribution is performed using the modulo of the total number of nodes in the virtual warehouse, which ensures even distribution. By default, when set to false, distribution is based on hash values and may not be even. |
|max_staged_part_number_per_task |UInt64 |Integer |100 |It defines the maximum number of staged parts per selected dedup task. |
|max_staged_part_rows_per_task |UInt64 |Integer |15000000 |It defines the total number of rows in the largest staged part for each selected dedup task. |
|dedup_impl_version |DedupImplVersion |dedup_in_write_suffix/<br><br>dedup_in_txn_commit |dedup_in_write_suffix |Deduplication implementation: `dedup_in_write_suffix` executes deduplication logic at the end of the write phase, while `dedup_in_txn_commit` executes deduplication logic during the transaction pre\-commit phase and is the optimized version. |
|allow_nullable_key |UInt8 |0/1 |0 |After enabling, nullable keys are supported as unique keys. |
|**Related to background tasks** |||||
|enable_addition_bg_task |Bool |true/false |false |It defines whether to allow more merge tasks to run concurrently. |
|max_partition_for_multi_select |UInt64 |Integer |10 |A merge task first selects partitions and then selects a range within each partition. If there are many partitions, it is usually necessary to increase this value. |
|max_addition_bg_task_num |UInt64 |Integer |32 |It is used to limit the maximum number of concurrent background tasks. |
|cnch_merge_enable_batch_select |Bool |true/false |true |batch_select selects a large batch of ranges in each round. In subsequent rounds, these ranges are directly submitted, which shortens the trigger cycle for the merge operation and allows the total workload to reach the concurrency limit. |
|cnch_merge_max_total_rows_to_merge |UInt64 |Integer |50000000 |It defines the maximum number of rows for a single merged part. |
|**Features related to some column updates** |||||
|enable_unique_partial_update |Bool |true/false |false |It defines whether partial column update capability is enabled for the table. |
|partial_update_max_process_parts |UInt64 |Integer |100 |When performing a partial column update task, subtasks are split according to this parameter. |
|partial_update_query_parts_thread_size |MaxThreads |An integer value not exceeding the core count |8 |It defines the thread pool size for reading historical data during execution of partial column update tasks. |
|partial_update_replace_columns_thread_size |MaxThreads |Integer value not exceeding the number of cores |8 |It defines the thread pool size for the column replacement stage in partial column update mode. |
|partial_update_replace_if_not_null |Bool |true/false |false |In partial column update mode, update operations are performed only when the value is not null. |


This article introduces the query parameters and table parameters that can be configured in ByteHouse.

<span id="70bf2011"></span>
# Background information

The following table lists the terms used in this document.


|**Name** |**Introduction** |
|---|---|
|worker |Nodes of the virtual warehouse. |
|Dedup |Deduplication is a process used by the unique key engine to ensure data uniqueness and achieve the desired result by removing duplicate data. |
|Dedup task |After the dedup task is completed, the selected data parts will become visible. |
|Dedup worker |A deduplication computing node is used to select and execute running instances for dedup tasks, and by default, it selects the account\-level write virtual warehouse. |
|Staging area |The data staging area is located in the default cache or intelligent cache and is used to accumulate deduplicated data into batches for batch processing. |
|Staged part |Data blocks in the staging area are located in the default cache or intelligent cache; part data stored in the staging area is not visible to queries. |


<span id="13b90929"></span>
# Query parameters

<span id="a997dbd2"></span>
## Data query (SELECT)


|**Parameter name** |**Parameter types** |**Optional values** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|enable_point_lookup_profile |Bool |true/false |false |It defines whether to use a lookup profile to optimize lookup efficiency. |
|max_threads |UInt64 |0 ≤ X ≤ number of CPU cores |0 |The single\-machine query parallelism. |
|max_plan_segment_num |UInt64 |0 ≤ X |500 |Maximum allowed number of plan segments; 0 means unlimited. |
|enable_intermediate_result_cache |Bool |true/false |false |It defines whether to enable intermediate result caching. |
|log_segment_profiles |Bool |true/false |false |It defines whether to enable ByteHouse SQL performance diagnostics functionality. |
|max_execution_time |UInt64 |1 ≤ X ≤ 50000 |Log in to the ByteHouse cloud data warehouse console, and navigate through the **Tenant management** \> **Parameter settings** \> ***Virtual warehouse parameters*** path. In the virtual warehouse module, view the reference values. |It defines the maximum execution time. The unit is second. |
|max_query_cpu_seconds |UInt64 |0 ≤ X ≤ 3000 ||It limits the maximum amount of CPU resources that a query segment can consume (unit: seconds). |
|max_memory_usage |UInt64 |1000 ≤ X ≤ the maximum memory of the Pod ||It defines the maximum memory usage per query, in bytes. |
|distributed_max_parallel_size |UInt64 |0 ≤ X ≤ number of workers in the virtual warehouse |0 |It defines the concurrency for non\-Source PlanSegment: 0 indicates the total number of nodes in the virtual warehouse. If concurrency is high or the number of virtual warehouse workers exceeds 10, it is recommended to reduce this value. |
|join_algorithm |JoinAlgorithm |'grace_hash' 'auto', 'hash', 'partial_merge', 'prefer_partial_merge', 'parallel_hash', 'auto' |auto |It defines the Join algorithm. |
|max_memory_usage_ratio |Float |0.01 ≤ X ≤ 0.99 |None |It defines the maximum memory usage ratio for a single query. |


You can log in to the ByteHouse CDW console and, via the path **Tenant management** \> **Parameter settings** \> **Virtual warehouse parameters**, view the reference values in the virtual warehouse module.

<span id="5e0801d9"></span>
## Data insertion (INSERT)


|**Parameter name** |**Parameter types** |**Optional values** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|enable_unique_partial_update |Bool |true/false |true |It defines whether to use partial column update mode. This must be used together with the table\-level parameter of the same name. Partial column update mode takes effect if and only if **both this parameter and the table\-level parameter are enabled**. |
|partial_update_enable_row_level_defaults |Bool |true/false |true |When only part of the columns are updated, the columns that are not updated are filled with row\-level default values. |
|staging_area_wait_mode |StagingAreaWaitMode |no_wait/wait_txn_visible |no_wait |It defines the data write mode after **enabling the staging area**. `no_wait` indicates **asynchronous write mode**, `wait_txn_visible` indicates **synchronous write mode**. |
|enable_staging_area_for_write |Bool |true/false |false |**Whether to enable the staging area**, which supports scenarios for optimizing asynchronous or concurrent writes. |
|optimize_unique_table_write |Bool |true/false |false |Import optimization switch for `INSERT SELECT` on unique key tables. It is recommended to enable this only in scenarios where the staging area is not enabled and `dedup_impl_version` is set to 'dedup_in_txn_commit'. |
|max_insert_threads |UInt64 |Positive integer |0 |Configures the thread pool size for write operations when a Worker node executes an `INSERT SELECT` request. |
|min_insert_block_size_bytes |UInt64 |Positive integer |1073710080 |It controls the minimum size, in bytes, of a data batch block in the `INSERT SELECT` operation. |
|min_insert_block_size_rows |UInt64 |Positive integer |1048545 |It controls the minimum number of rows in a data batch block during `INSERT SELECT` operations. |


<span id="7011c34a"></span>
# Table parameters


|**Parameter name** |**Parameter types** |**Optional values** |**No default configuration value** |**Parameter description** |
|---|---|---|---|---|
|**Deduplication related to unique key tables** |||||
|unique_table_dedup_threads |MaxThreads |An integer value not exceeding the number of cores |8 |Each dedup task is split into subtasks with **different deduplication granularities** during execution. This parameter allows you to configure the thread pool size for executing these subtasks. |
|cloud_enable_staging_area |Bool |true/false |false |It defines whether to **enable the staging area** to support scenarios such as asynchronous writes or concurrent write optimization. |
|cloud_staging_area_wait_mode |StagingAreaWaitMode |no_wait/wait_txn_visible |no_wait |It defines the data write mode after **enabling the staging area**. `no_wait` represents **asynchronous write mode**, `wait_txn_visible` represents **synchronous write mode**. |
|min_check_txn_staging_area_visible_interval |UInt64 |Integer |50 |**When the staging area is enabled** and **write mode is set to wait_txn_visible**: the minimum interval for polling whether the data is already visible, in milliseconds (ms). |
|max_check_txn_staging_area_visible_interval |UInt64 |Integer |1000 |When **the staging area is enabled** and **the write mode is wait_txn_visible**, this parameter specifies the maximum interval for polling whether the data has become visible, in milliseconds (ms). |
|max_dedup_worker_number |UInt64 |Integer |1 |It is recommended to set the number of dedup workers to match the number of virtual warehouse pods configured for cnch_vw_write. |
|pick_dedup_worker_by_mod |Bool |true/false |false |For the distribution mode of Dedup worker, when the configuration is set to true, distribution is performed using the modulo of the total number of nodes in the virtual warehouse, which ensures even distribution. By default, when set to false, distribution is based on hash values and may not be even. |
|max_staged_part_number_per_task |UInt64 |Integer |100 |It defines the maximum number of staged parts per selected dedup task. |
|max_staged_part_rows_per_task |UInt64 |Integer |15000000 |It defines the total number of rows in the largest staged part for each selected dedup task. |
|dedup_impl_version |DedupImplVersion |dedup_in_write_suffix/<br><br>dedup_in_txn_commit |dedup_in_write_suffix |Deduplication implementation: `dedup_in_write_suffix` executes deduplication logic at the end of the write phase, while `dedup_in_txn_commit` executes deduplication logic during the transaction pre\-commit phase and is the optimized version. |
|**Related to background tasks** |||||
|enable_addition_bg_task |Bool |true/false |false |It defines whether to allow more merge tasks to run concurrently. |
|max_partition_for_multi_select |UInt64 |Integer |10 |A merge task first selects partitions and then selects a range within each partition. If there are many partitions, it is usually necessary to increase this value. |
|max_addition_bg_task_num |UInt64 |Integer |32 |It is used to limit the maximum number of concurrent background tasks. |
|cnch_merge_enable_batch_select |Bool |true/false |true |batch_select selects a large batch of ranges in each round. In subsequent rounds, these ranges are directly submitted, which shortens the trigger cycle for the merge operation and allows the total workload to reach the concurrency limit. |
|cnch_merge_max_total_rows_to_merge |UInt64 |Integer |50000000 |It defines the maximum number of rows for a single merged part. |
|**Features related to some column updates** |||||
|enable_unique_partial_update |Bool |true/false |false |It defines whether partial column update capability is enabled for the table. |
|partial_update_max_process_parts |UInt64 |Integer |100 |When performing a partial column update task, subtasks are split according to this parameter. |
|partial_update_query_parts_thread_size |MaxThreads |An integer value not exceeding the core count |8 |It defines the thread pool size for reading historical data during execution of partial column update tasks. |
|partial_update_replace_columns_thread_size |MaxThreads |Integer value not exceeding the number of cores |8 |It defines the thread pool size for the column replacement stage in partial column update mode. |
|partial_update_replace_if_not_null |Bool |true/false |false |In partial column update mode, update operations are performed only when the value is not null. |
