---
title: "ELT Support"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-elt-support"
---

As a cloud\-native data warehouse, ByteHouse Cloud Data Warehouse is gradually introducing support for ELT (Extract\-Load\-Transform), to avoid maintaining multiple heterogeneous data systems.

<span id="e170aa9e"></span>
## Overview

Before data is loaded into the database, it often needs to go through complex data cleansing and transformation processes, which is commonly known as ETL. In previous engineering practices, this part of the work was completed by some external data warehouse tools, such as typical tools like Hive and Spark SQL. ByteHouse continuously strives to expand its boundaries and reduce the operational burden caused by the coupling of multiple systems between data processing and data analysis. By moving the data processing (T) process into ByteHouse, it enables one\-stop data ingestion, processing, and analysis, providing comprehensive data warehouse capabilities.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99ed46e3a700461fbc27aae1614547b3~tplv-goo7wpa0wc-image.image) </span>

<span id="20bf117b"></span>
## Background

ClickHouse was designed from the outset for **OLAP** (**online analytical processing**) **scenarios**, and whether it is columnar storage, indexing, or vectorized execution optimizations, they all effectively address aggregation computations on large wide tables.

However, when it comes to complex queries, especially typical ETL tasks in data warehouses, ClickHouse is not adept. **Complex structure**, **time\-consuming data processing jobs**, and **complex tuning processes are usually required**. Typical issues are as follows:


* **High retry cost**: For ETL jobs that run for minutes or even hours, if a failure occurs during execution, ClickHouse can only retry at the query level. Retrying from the beginning not only causes significant resource waste but also poses challenges to the SLA of processing tasks.

* **Massive resource consumption**: Due to the lack of iterative computation and effective task splitting, when querying large volumes of data with complex computations, nodes are typically required to have sufficient memory for processing.

* **Concurrency control**: When multiple queries run simultaneously, ClickHouse does not schedule based on resource usage. Tasks squeezing each other can lead to failures (usually Memory limit errors). The lack of a retry mechanism often results in a cascading failure effect.


To address the above issues, the ByteHouse team has added support for the BSP (Bulk Synchronous Parallel) mode on top of the high\-performance computing framework: this enables task\-level fault tolerance and finer\-grained scheduling, and will support resource\-aware scheduling in the future. The following benefits are provided to users:


* When an error occurs during query execution, the current task can be automatically retried instead of restarting from the beginning. This greatly reduces retry costs.

* When a query requires a large amount of memory, even more than the memory of a single machine, increasing the parallelism can reduce memory usage per unit time. Simply increase the parallelism parameter; in theory, this can be scaled infinitely.

* Concurrent ETL tasks can be scheduled in an orderly manner based on cluster resource usage, thereby reducing resource contention and avoiding frequent failures.


<span id="c0e90b63"></span>
## Using ByteHouse ELT

ByteHouse currently supports ELT capabilities by setting the compute group type or by configuring parameters. For instructions on setting the compute group type, refer to [Create⧸Edit virtual warehouse](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse).

You can also enable ELT capabilities by setting compute group\-level parameters or by adding the following parameters in query settings:


|Settings parameter name |Type |Default value |Description |
|---|---|---|---|
|**bsp_mode** |Bool |0 |Enable BSP mode; queries will be executed in stages. Task\-level retries will be performed in case of failure. |
|**distributed_max_parallel_size** |UInt64 |Equal to the number of workers |When a single query consumes a large amount of memory, increasing this parameter can raise the operator parallelism, reduce the amount of data processed by each parallel unit, and decrease memory usage per unit time. This can only exceed the number of workers when `bsp_mode` is enabled. It is recommended to set this as a multiple of the number of workers. |
|bsp_max_retry_num |UInt64 |3 |The maximum number of task retries. Counted at the task level, with a default of 3 times. |
|disk_shuffle_files_codec |LZ4/ZSTD/NONE |LZ4 |The encoding used for Shuffle files can effectively reduce disk usage. |
|use_bsp_in_insert_select |Bool |0 |The BSP mode is used by default for all insert statements. |


The above options can be set at the compute group level, session level, or SQL level.


* For details on setting compute group\-level parameters, see [Set virtual warehouse parameters](https://docs.byteplus.com/docs/bytehouse/manage-virtual-warehouse-parameters#9fd5d768).

* For session\-level parameter settings, refer to the following example:

   ```SQL
   set bsp_mode = 1; 
   insert into demo_db.demo_tb select * from tb1 join tb2 on tb1.id = tb2.id;
   ```
   

* For SQL\-level parameter settings, refer to the following example:

   ```SQL
   insert into demo_db.demo_tb select * from tb1 join tb2 on tb1.id = tb2.id settings bsp_mode =1; 
   ```
   

   You can add the relevant configuration items as needed after `bsp_mode`.
