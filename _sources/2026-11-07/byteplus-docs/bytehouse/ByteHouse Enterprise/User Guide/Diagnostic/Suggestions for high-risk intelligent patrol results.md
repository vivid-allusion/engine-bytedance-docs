---
title: "Suggestions for high-risk intelligent patrol results"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/suggestions-for-intelligent-patrol"
---

This tutorial focuses on scenarios where intelligent inspection items present high risks and provides specific recommendations for handling them. You may refer to the corresponding response plans based on the high\-risk inspection indicators triggered in practice.

<span id="32137310"></span>
## Service down count

When a node fails, the ByteHouse team will intervene with high priority, and in most cases, recovery is automatic. You can also use monitoring to further identify down nodes. To view monitoring information, go to **Cluster management** \> target cluster name \> **Alerts** \> **Operating system load** \> **Node downtime**.

If a node remains down for an extended period or if immediate action is required, please contact the ByteHouse after\-sales support team.

<span id="5740ccd7"></span>
## Shard down count

In the event of shard failure, the ByteHouse team will intervene promptly, and recovery is usually automatic. You can further identify down nodes through monitoring. To view, go to **Cluster management** \> target cluster name \> **Alerts** \> **Operating system load** \> **Shard failed count**.

If a shard outage is not resolved for an extended period, or requires immediate attention, please contact the ByteHouse after\-sales support team.

<span id="20d48232"></span>
## Disk error

Disk abnormalities are usually caused by the disk being full. To check whether the disk is full, go to **Cluster management** \> target cluster name \> **Alerts** \> **Operating system load** \> **Disk remaining capacity GiB** in monitoring.

To resolve a full disk, expand the disk or delete some historical data. Disk expansion operations can be performed by initiating vertical scaling and adjusting storage capacity. For details, see [Vertical scaling](https://docs.byteplus.com/docs/bytehouse/reconfigure-a-cluster#f53340e8).

If, after expanding capacity or deleting historical data, recovery is still not possible, please contact the ByteHouse after\-sales support team.

<span id="64e14ab6"></span>
## Average CPU usage rate

Excessive CPU usage is typically caused by two main reasons: an excessively high overall query load, or individual large queries consuming too many CPU resources. Troubleshoot using the following steps:


1. By monitoring metrics such as query concurrency and CPU usage, determine whether the overall query load has consistently remained relatively high or whether the query load has significantly increased during a specific time window. If so, it is recommended to perform vertical or horizontal scaling on the cluster. For specific operations, please refer to [Reconfigure a cluster](https://docs.byteplus.com/docs/bytehouse/reconfigure-a-cluster).

2. After ruling out high overall query load as the cause, you can further identify and optimize some large queries.

   You can use the SQL diagnosis feature to view the top 5 queries consuming CPU. SQL fingerprint analysis within SQL diagnostics can also be used to aggregate SQL queries with the same query pattern, calculate their total count, total CPU consumption, and more, and identify a category of queries that significantly impact CPU performance from a global perspective. For instructions on using the SQL diagnostic feature, please refer to [SQL diagnosis](https://docs.byteplus.com/docs/bytehouse/sql-diagnostic).

   After identifying SQL queries with the same query pattern, you can use [Query insight](https://docs.byteplus.com/docs/bytehouse/query-insight) to further retrieve information such as query plans to assist with troubleshooting.


<span id="1f273fb4"></span>
## IO usage rate

Monitor ByteHouse load and query load metrics, such as query concurrency, background merge task count, overall concurrency, and data import tasks, to check for any spikes and determine whether these tasks are affecting IO. Further optimize queries based on the observed metrics. You can view the above relevant metrics by going to **Cluster management** \> target cluster name \> **Alerts**.

If the relevant metrics are normal but the exception still persists, please contact the ByteHouse after\-sales support team to handle it.

<span id="6cf48aed"></span>
## Average memory usage rate

The causes of high memory usage can be investigated from three aspects: background merge (merge) tasks, running queries, and query cache. For detailed instructions and handling, please see [Performance analysis: Memory usage](https://docs.byteplus.com/docs/bytehouse/performance-analysis-memory-usage).

<span id="b6a342e8"></span>
## Average disk usage rate

You can find tables with high disk usage by executing the following command:

```SQL
SELECT 
    table,
    sum(rows),
    formatReadableSize(sum(data_compressed_bytes)) AS size
FROM system.parts
GROUP BY table
ORDER BY sum(data_compressed_bytes) DESC
LIMIT 10;
```


When disk usage rate is too high, it is recommended to use the following methods to optimize:


* Method 1: Disk expansion.

* Method 2: Delete some historical data.

* Method 3: Refer to [Viewing table disk space usage](https://docs.byteplus.com/docs/bytehouse/disk-space-analysis-in-performance-diagnosis#09b98503) and combine the following commands to locate the optimization target.


To address a significant difference between the table's storage size shown in query results and the actual disk usage, which may be caused by cluster logs or metadata occupying too much space, it is recommended to contact the ByteHouse after\-sales support team for further investigation.

<span id="c1336a4d"></span>
## Average iNode usage rate

High file count is usually due to too many small files. ByteHouse automatically merges small files in the background. If a high iNode usage ratio persists for an extended period, please contact the ByteHouse after\-sales support team.

<span id="975f945d"></span>
## System disk usage rate

To address this exception, please contact the ByteHouse after\-sales support team.

<span id="7d4f0e9d"></span>
## Cluster part count

You can execute the following commands to query the distribution of part counts in the cluster and identify tables with abnormal part counts as well as their causes. When using, replace the placeholders or example content in the sample with actual database and table information.


1. View system table Part quantity distribution:

   ```SQL
   SELECT  
       database || '.' || table AS db_tbl,
       active,
       count(),
       sum(rows)
   FROM system.parts
   GROUP BY db_tbl,
            active
   ORDER BY count() DESC
   LIMIT 10;
   ```
   

2. If you discover active parts accumulation, follow these steps to locate the problem table and the cause:

   * Reason 1: Background merge (merge) task exception

      1. Compare write and merge performance.

         ```SQL
         SELECT 
             toHour(event_time) AS h, 
             countIf(event_type = 1) AS insert, 
             countIf(event_type = 2) AS merge, 
             sumIf(length(merged_from), event_type = 2) AS merge_parts 
         FROM system.part_log 
         WHERE (table = 'xx_local')  -- Replace with the actual table name
           AND (event_date = today()) 
         GROUP BY h 
         ORDER BY h;
         ```
         

         Under normal circumstances, the number of inserts should be less than the number of merge_parts. If insert is much greater than merge_parts, it indicates that there may be an abnormality in the merging process.

      2. Troubleshoot merge task errors.

         ```SQL
         SELECT event_time, exception 
         FROM system.part_log 
         WHERE table = 'xx_local'  -- Replace with the actual table name
           AND event_type = 2 
           AND exception != '' 
         ORDER BY event_time DESC 
         LIMIT 10; 
         ```
         

      3. Check the execution status of merge tasks.

         ```SQL
         SELECT 
             event_time,
             event_type,
             current_parts,
             source_parts_in_new_tasks,
             duration_us
         FROM system.part_merge_log
         WHERE (table = 'xx_local')  -- Replace with the actual table name
           AND (event_date = today())
         ORDER BY event_time DESC
         LIMIT 20;
         ```
         

   * Reason 2: Too many small Parts (inefficient writing method)

      If writing data into too many partitions at once results in a large number of small parts, it is necessary to optimize the data writing strategy; you may refer to [Kafka message backlog](https://docs.byteplus.com/docs/bytehouse/suggestions-for-intelligent-patrol#a82bf2ed).


<span id="b496bcb6"></span>
## Query success rates

Use the SQL diagnosis feature to locate failed SQL queries within a specified time period, identify and analyze the causes of query failures, prioritize resolving queries that fail frequently, and improve the query success rate to an acceptable level. See [SQL diagnosis](https://docs.byteplus.com/docs/bytehouse/sql-diagnostic) for the SQL diagnostic feature.

Review the details of the failed Query and troubleshoot the issue based on the failure reason. The common causes of failure are as follows:


* Query, user, and service\-level memory overage;

* Database and table do not exist;

* SQL syntax error;

* Query timeout.


<span id="f536873b"></span>
## Write success rates

Run the following command to query the reason for write failures using the system table `query_log`. In actual use, replace the placeholders in the command examples with the actual time periods.

```SQL
SELECT query_id,
       query,
       event_time,
       exception,
       exception_code
FROM system.query_log
WHERE query_kind = 'Insert'
  AND event_time > 'xxx'
  AND event_time < 'xxx'
  AND exception != ''
LIMIT 100;
```


Check the `exception` field in the query results to obtain the reason for the failure, and then troubleshoot accordingly. Among them, the common reasons for failure are as follows:


* Query, user, and service\-level memory overage;

* Database and table do not exist;

* SQL syntax error;

* Query timeout.


<span id="96c566e6"></span>
## Concurrency

The system default concurrency limit is 200. Check for queries that have not completed for an extended period or are stuck. These may cause abnormal concurrency counts. Perform overall performance tuning for scenarios involving high\-concurrency point queries.


* Method 1: View queries and terminate abnormal queries

   1. Check the currently running queries and determine whether there are any queries that are taking a long time or are stuck.

      ```SQL
      SELECT * FROM system.processes
      ```
      

   2. To terminate an abnormal query, execute the following command.

      ```SQL
      KILL query where query_id=xxx
      ```
      

* Method 2: Performance tuning

   For high\-concurrency point query scenarios, query performance can be optimized. For more information, see [Best practices for high-concurrency point query optimization in ByteHouse](https://docs.byteplus.com/docs/bytehouse/high-concurrency-point-query-optimization).


<span id="6b79a543"></span>
## Long mutation execution time

To resolve the issue of excessive execution time for data mutations, follow these steps:


1. Query the system table `system.mutations` and confirm data mutations with long execution times:

   ```SQL
   SELECT *
   FROM system.mutations
   WHERE is_done = 0;
   ```
   

2. Check whether the tasks associated with the mutation, such as data deletion and table structure modification, have actually been completed, and verify the status of changes to relevant data or table structures:

   * Directly terminate the mutation if the change has already been completed;

   * Terminate the mutation and re\-initiate the data change if the change is not completed and the mutation has stopped executing.

      The following is a sample command for terminating a mutation. When using this command, replace the placeholder in the example with the actual mutation_id.

   ```SQL
   KILL MUTATION WHERE mutation_id = 'xxx';
   ```
   


<span id="f052c01f"></span>
## Broken table

Query the system table `system.broken_tables` to obtain the reason why the exception occurred.

```SQL
SELECT * FROM system.broken_tables;
```


Example: The data for the node does not exist on Zookeeper, causing the table to malfunction. To resolve this issue, recreate the table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28919af1ddd94abba6d5b5cebe78129a~tplv-goo7wpa0wc-image.image) </span>

<span id="70419872"></span>
## Query tables without a leader

Query the system tables `system.ha_replicas` and `system.ha_unique_replicas` to obtain the reason for this exception. The following are example query commands: When using these commands, replace the placeholder in the example with the actual name of your cluster.

```SQL
# Query system.ha_unique_replicas
SELECT *
FROM clusterAllReplicas('cluster_name', system.ha_unique_replicas)
WHERE is_leader = 0;

# Query system.ha_replicas
SELECT *
FROM clusterAllReplicas('cluster_name', system.ha_replicas)
WHERE is_leader = 0;
```


Example: The table data does not exist in ZooKeeper, resulting in the table having no leader. This issue can be resolved by recreating the table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/055f3c61eadd40f78173b559c9415be2~tplv-goo7wpa0wc-image.image) </span>

<span id="c3129cba"></span>
## View number of MergeTree tables

You can use the following command to query the number of MergeTree tables in the cluster. It is recommended that the number of MergeTree tables in a cluster does not exceed 2,000. To reduce the number of MergeTree tables, delete unnecessary tables.

```SQL
SELECT count()
FROM system.tables
WHERE engine LIKE '%MergeTree%';
```


<span id="a2c6a477"></span>
## Cluster slow query count

Query the system table `system.query_log` to locate slow queries, analyze the causes using relevant metrics, and optimize. The specific steps are as follows:


1. Filter slow queries To find queries that exceed the duration (in seconds) threshold, you can use `event_date` to specify the date when the slow query occurred.

   ```SQL
   SELECT *
   FROM system.query_log
   WHERE (type> 1)
   AND (query_duration_ms > consumed time of a slow query  * 1000)
   AND event_date = today ();
   ```
   

2. Analyze the load conditions associated with slow queries.

   View the number of SQL queries and the load level during the period when slow queries occurred. Replace `event_time` with the specific time period when the slow queries appeared.

   You can try `toStartOfHour` if the time granularity of `toStartOfFiveMinute` is not suitable.

   In addition to `query_duration_ms`, query complexity can also be comprehensively evaluated by combining columns such as `total_cpu_seconds`, `read_rows`, and `read_bytes`.

   ```SQL
   SELECT
   toStartOfFiveMinute (event_time) AS h,
   count (*),
   avg (query_duration_ms),
   min (query_duration_ms),
   max (query_duration_ms)
   FROM system.query_log
   WHERE event_time > '2023-12-22 14:30:00'
   AND event_time < '2023-12-31 14:30:00'
   GROUP BY h
   ORDER BY h DESC;
   ```
   

3. Reproduce slow queries. Retrieve slow query statements from the system table `query_log`, re\-execute them, and verify whether the slow query issue can be reproduced.

   Caution: Refer to the parameters in the `Settings` column of the original slow query record (such as whether `enable_optimizer` is enabled), and ensure that the parameters remain consistent when rerunning the query.


<span id="23c195a0"></span>
## Maximum number of primary\-replica synchronous delay tables

Query the system table `system.ha_queue`, check the queue backlog, and identify tables with slow synchronization.

```SQL
SELECT 
    database, table, type, count()  
FROM system.ha_queue  
GROUP BY database,table,type
ORDER BY count()
```


Meanwhile, by monitoring and checking metrics such as query concurrency, merge task count, and concurrency, it is possible to determine whether the write pressure on the current cluster is increasing. You can view monitoring information by navigating through **Cluster management** \> target cluster name \> **Alerts**.

Under normal circumstances, synchronization between the primary and replica can be completed within 5 minutes after the write task is finished. If stricter requirements for primary\-replica synchronization latency are required, you can reduce the cluster write rate or contact the ByteHouse support team for assistance.

<span id="44279f11"></span>
## Number of delayed files in distributed tables

You can troubleshoot and resolve the issue by following these steps:


1. View information related to delay files of distributed tables.


```SQL
SELECT * FROM system.distribution_queue 
```



2. Check the field `last_exception` for abnormal values:

   * If `last_exception` has a value, you can directly identify the cause of the problem using exception information and resolve it in a targeted manner.

   * If `last_exception` has no value, contact the ByteHouse after\-sales support team for further investigation.


<span id="6045bb96"></span>
## Number of failed data mutations

Query the system table `system.mutations` to locate mutation tasks with execution errors:

```SQL
SELECT * 
FROM system.mutations 
WHERE is_done = 0 
  AND latest_fail_reason != ''
```


The above query allows you to directly obtain details of failed mutations, including the specific error reason (the `latest_fail_reason` field), to facilitate targeted analysis and problem resolution.

<span id="a82bf2ed"></span>
## Kafka message backlog


1. Query Kafka\-related log information:

   ```SQL
   SELECT * FROM system.kafka_log ORDER BY event_time DESC LIMIT 10;
   ```
   

2. Check whether a new POLL event has been generated:

   * If there is a latest POLL event, this indicates that the message backlog is caused by a surge in message volume, causing the consumption speed to lag behind the production speed. If the surge is temporary, observe first; if the production speed remains high, it is recommended to consider scaling ByteHouse nodes to increase consumption capacity.

   * If the latest POLL event does not exist, it is recommended to contact the ByteHouse after\-sales support team for further investigation.


<span id="aaab3fd2"></span>
## Kafka consumption error count


1. Execute the following SQL query to obtain the reasons for Kafka\-related operation failures:

   ```SQL
   SELECT * 
   FROM system.kafka_log 
   WHERE exception != '' 
   ORDER BY event_time DESC 
   LIMIT 10;
   ```
   

2. Analyze the root cause of the problem and take targeted action based on the specific error information in the `exception` field of the query results.


<span id="ada4acdb"></span>
## Disk usage rate increased by xx% compared to yesterday

You can execute the following commands to identify the main source of disk usage growth. When using, please replace the placeholders or sample content in the example with actual database and table information.


1. View cloud monitoring and the details of the cluster growth curve via the **Cluster management** \> target cluster name \> **Alerts** path.

2. Query tables with high disk usage.

   ```SQL
   SELECT 
     database,
     table,
     formatReadableSize(sum(bytes_on_disk))
   FROM system.parts
   WHERE active
   GROUP BY database, table
   ORDER BY sum(bytes_on_disk) DESC
   LIMIT 20;
   ```
   

3. View the partition usage of a specific table.

   ```SQL
   SELECT 
     partition_id,
     formatReadableSize(sum(bytes_on_disk))
   FROM system.parts
   WHERE database = 'xxx' 
     AND table = 'xxx' 
     AND active
   GROUP BY partition_id
   ORDER BY partition_id DESC
   LIMIT 50;
   ```
   


By following the above steps, you can identify the main sources of disk usage growth, such as specific tables or partitions, providing a basis for subsequent cleanup or capacity expansion.

<span id="fc36dcea"></span>
## CPU usage increased xx% compared to yesterday

You can execute the following commands to identify SQL statements or query patterns with high CPU consumption. When using, replace the placeholders or sample content with actual cluster information, database name, table name, and time information.


1. Execute the following command to identify query patterns with high CPU consumption (normalized_query_hash).

   ```SQL
   SELECT
       normalized_query_hash,
       sum(cpu_s),
       sum(io),
       sum(mem),
       count() AS count,
       sum(sub_query_count),
       avg(query_duration_ms),
       any(query),
       groupArray(query_start_times)
   FROM 
   (
       SELECT
           any(if(is_initial_query, query, null)) AS query,
           groupArray(if(is_initial_query, query_start_time, null)) AS query_start_times,
           initial_query_id,
           max(if(is_initial_query, normalized_query_hash, 0)) AS normalized_query_hash,
           max(if(is_initial_query, query_duration_ms, 0)) AS query_duration_ms,
           count(1) AS sub_query_count,
           sum(total_cpu_seconds) AS cpu_s,
           sum(io_wait_seconds) AS io,
           sum(memory_usage) AS mem
       FROM cluster({cluster_name}, system.query_log, (1, 2))
       WHERE (event_date = '2024-12-23') AND (query_start_time > '2024-12-23 06:00:00') AND (query_start_time < '2024-12-23 06:05:00') AND (type != 1)
       GROUP BY initial_query_id
   )
   GROUP BY normalized_query_hash
   ORDER BY sum(cpu_s) DESC
   LIMIT 1
   ```
   

2. Query all SQL distributions corresponding to the `normalized_query_hash`, and identify the specific SQL statements with high CPU consumption.

   ```SQL
   SELECT user,
          query,
          query_start_time
   FROM cluster({cluster_name}, system.query_log, (1, 2))
   WHERE (event_date = '2025-01-09')
     AND (query_start_time > '2025-01-09 15:00:00')
     AND (query_start_time < '2025-01-09 16:06:00')
     AND (type != 1)
     AND normalized_query_hash = xxxxxxxxxxxxxxxxxxx;
   ```
   


<span id="d3147a75"></span>
## Memory usage increased xx% compared to yesterday

You can run the following command to check cache usage. When using, replace the placeholders or example content in the example with actual cluster information, database name, table name, and time information.


1. Query the current memory usage.

   ```SQL
   SELECT query, formatReadableSize(memory_usage) 
   FROM system.processes 
   ORDER BY memory_usage DESC;
   ```
   

2. View the memory usage of the Merge operation.

   ```SQL
   SELECT database, 
          table, 
          source_part_names, 
          formatReadableSize(memory_usage) 
   FROM system.merges;
   \G
   ```
   

3. Query cache\-related memory usage.

   ```SQL
   SELECT *, formatReadableSize(value)  
   FROM system.asynchronous_metrics 
   WHERE metric LIKE '%Cache%' 
   ORDER BY metric;
   ```
   

4. View the overall memory usage of ClickHouse.

   ```SQL
   SELECT metric, formatReadableSize(value) 
   FROM system.metrics 
   WHERE metric = 'MemoryTracking';
   ```
   

5. Temporarily clear the uncompressed cache (applicable when memory is low).

   ```SQL
   SYSTEM DROP UNCOMPRESSED CACHE;
   ```
   

6. View historical cache usage trends

   ```SQL
   -- Non-compressed cache history
   SELECT
       toStartOfFiveMinute(event_time) AS fm,
       formatReadableSize(max(value))
   FROM system.asynchronous_metric_log
   WHERE metric = 'UncompressedCacheBytes' 
     AND event_date = today()
   GROUP BY fm
   ORDER BY fm ASC;
   
   -- Cache history for unique key index blocks
   SELECT 
       toStartOfFiveMinute(event_time) AS fm, 
       formatReadableSize(max(value))  
   FROM system.asynchronous_metric_log 
   WHERE metric = 'UniqueKeyIndexBlockCacheBytes' 
     AND event_date = today() 
   GROUP BY fm 
   ORDER BY fm;
   
   -- Cache status for the specified time period
   SELECT 
       toStartOfFiveMinute(event_time) AS fm,
       lower(metric), 
       formatReadableSize(max(value))  
   FROM system.asynchronous_metric_log 
   WHERE lower(metric) LIKE '%cache%'  
     AND event_date = '' 
     AND event_time > '' 
     AND event_time < '' 
   GROUP BY fm, lower(metric) 
   ORDER BY fm;
   ```
   


<span id="c54748de"></span>
## P95 elapsed time increased by xx% compared to yesterday

You can execute the following commands to locate slow queries. When using, please replace the example content with actual time information.


1. Filter slow queries exceeding the threshold.

   ```SQL
   SELECT *
   FROM system.query_log
   WHERE (type > 1) 
     AND (query_duration_ms > time consumed by slow query * 1000) 
     AND event_date = today();
   ```
   

2. Analyze the load conditions during the slow query time period.

   ```SQL
   SELECT 
       toStartOfFiveMinute(event_time) AS h, 
       count(*),
       avg(query_duration_ms),
       min(query_duration_ms),
       max(query_duration_ms) 
   FROM system.query_log  
   WHERE event_time > '2023-12-22 14:30:00' 
     AND event_time < '2023-12-22 14:30:00'  
   GROUP BY h 
   ORDER BY h DESC;
   ```
   

   To avoid a granularity that is too fine, replace the 5\-minute granularity with `toStartOfHour`.

   In addition to `query_duration_ms`, metrics such as `total_cpu_seconds`, `read_rows`, and `read_bytes` can be combined to comprehensively assess query complexity.

3. Reproduce slow queries.

   Obtain slow query statements from `query_log`, re\-execute them, and verify whether the slow query phenomenon can be reproduced.

   Caution: Refer to the parameters in the `Settings` column of the original slow query record (such as whether the optimizer `enable_optimizer` is enabled), and ensure that the parameters remain consistent when rerunning.


<span id="d074b177"></span>
## Cluster QPS increased xx% compared to yesterday

You can view cloud monitoring by navigating through **Cluster management** \> target cluster name \> **Alerts**. Then, check the QPS trend of the cluster and observe whether it meets expectations.
