---
title: "Locating large queries"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/si_locating_large_queries"
---

In a production environment, some large queries may exhaust the entire cluster's resources. This can affect the performance and availability of other queries. It is necessary to quickly locate and handle recent large queries or jobs that consume significant resources to reduce the overall impact on business operations. This article will guide you on how to quickly locate and handle these large queries.

<span id="6d4af48a"></span>
# Applicable versions


|**Product form** |**Engine** |**Deployment method** |**Applicable version** |
|---|---|---|---|
|Serverless instance<br><br>(Fully managed) |StarRocks |Storage and compute separation |Version 3.2.x and above |
|||Integrated storage and compute |Version 3.2.x and above |


<span id="0a19aade"></span>
# Procedure

<span id="1aa72865"></span>
## Locating large queries: Completed large queries/jobs

You can diagnose completed jobs using StarRocks audit logs to locate them and determine whether they are large query jobs that require management. During diagnosis:


* You can primarily focus on the cpuCost, scanBytes, memCostBytes, and queryTime metrics.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">cpuCost can be understood as the amount of CPU time consumed. For example, if the cluster is 8 \* 48 cores and the query's cpuCost = 3840 seconds, it means the cluster CPU needs to be fully utilized at 100% for 10 seconds to complete the query.   </div>
   

* The following queries can be used to locate top tasks, and you can optimize them based on scheduling cycles or SQL statements. That is, use monitoring to preliminarily identify hardware resource bottlenecks (cpu/mem/disk), then use the audit log table to determine the top tasks with the highest cpu/mem/disk resource usage.

   The following is sample code for analyzing StarRocks audit logs.

   ```SQL
   -- Collect hourly metrics for Insert/no-Insert query types
   SELECT
       DATE_FORMAT(timestamp, '%Y-%m-%d %H:00:00') AS dt,
       CASE
           WHEN (stmt LIKE '%INSERT%' OR stmt LIKE '%insert%') THEN 'isInsert'
           ELSE 'isQuery'
       END AS `type`,
       ROUND(SUM(scanBytes / 1024 / 1024), 0) AS sum_scan_mb,
       ROUND(AVG(scanBytes / 1024 / 1024), 0) AS avg_scan_mb,
       ROUND(SUM(cpuCostNs / 1000 / 1000 / 1000), 0) AS sum_cpu_time_sec,
       ROUND(AVG(cpuCostNs / 1000 / 1000 / 1000), 0) AS avg_cpu_time_sec,
       ROUND(SUM(queryTime / 1000), 0) AS sum_query_time_sec,
       ROUND(AVG(queryTime / 1000), 0) AS avg_query_time_sec,
       COUNT(*) AS total_query_count
   FROM starrocks_audit_db__.starrocks_audit_tbl__
   WHERE timestamp BETWEEN '2025-06-19 00:00:00' AND '2025-06-25 23:59:00'
     AND stmt != 'SELECT 1'
     AND stmt NOT LIKE '%@@%'
     AND user != 'root'
   GROUP BY 1, 2
   ORDER BY 2, 1;
   
   -- Collect SQL statements with the highest cpuCost
   SELECTg BY cpuCostSec DESC LIMIT 50;
   
   -- Collect cpuCost by digest (digest: SQL fingerprint, usually represents a type of SQL and can be used to identify the user's interface)
   -- StarRocks requires the digest feature to be enabled
   -- ADMIN SET FRONTEND CONFIG ("enable_sql_digest" = "true");
   -- https://docs.starrocks.io/docs/administration/sql_digest/
   
   WITH top_sql AS (
       SELECT
           digest,
           SUM(queryTime)
       FROM starrocks_audit_db__.starrocks_audit_tbl__
       GROUP BY digest
       ORDER BY SUM(queryTime) DESC
       LIMIT 10
   )
   SELECT *
   FROM starrocks_audit_db__.starrocks_audit_tbl__
   WHERE digest IN (SELECT digest FROM top_sql);
   ```
   


<span id="1354c2a3"></span>
## Locating large queries: Running large queries/jobs


1. To view the resource consumption of current queries, pay special attention to the ExecTime (query runtime) or CPUTime (CPU usage time) columns in the results. Use the values in these columns to identify large queries with high resource consumption. For details, please refer to: [StarRocks 查看运行中的查询](https://docs.byteplus.com/docs/E-MapReduce/109152#global_current_queries).

   ```SQL
   -- View connections and query tasks on the current FE node
   SHOW PROCESSLIST;
   -- View connections and query tasks on all FE nodes
   SHOW FULL PROCESSLIST;
   
   -- For observation reference
   SHOW PROC '/current_queries'; -- View queries currently running on the current FE node
   SHOW PROC '/global_current_queries'; -- View queries currently running on all FE nodes
   ```
   

   The returned results usually include the following columns.

   * QueryId

   * ConnectionId

   * Database: The database of the current query

   * User: User

   * ScanBytes: The amount of data scanned by the current query

   * ProcessRow: The number of rows scanned by the current query

   * CPUTime: The CPU time used by the current query, Unit: seconds. This is the cumulative CPU time of multiple threads. For example, if two threads each use 1 second and 2 seconds of CPU time respectively, the total CPU time is 3 seconds.

   * MemoryUsage: Current memory usage. If the query involves multiple BE nodes, this value is the sum of memory used by the query across all BE nodes.

   * ExecTime: The duration from the start of the query to the present

2. Terminate queries with high CPU usage time (CPUTime). For details, please refer to: [Locating large queries](https://docs.byteplus.com/docs/E-MapReduce/109152).

   ```SQL
   -- Kill the corresponding processlist_id
   kill connection {processlist_id};
   ```
   


<span id="76e3fc8b"></span>
## To quickly stop losses when large queries cannot be located promptly


1. If it is not possible to quickly locate large queries that are running, it is recommended to restart BE to terminate all queries and restore overall business operations.

2. After restarting to mitigate losses, refer to [SQL diagnostics instructions](https://docs.byteplus.com/docs/E-MapReduce/109126) or the audit log table to perform statistics on historical queries. Combine business investigation to identify the source of large queries and optimize the queries. For detailed operations, see: [Locating large queries](https://docs.byteplus.com/docs/E-MapReduce/109152).

   ```SQL
   -- View the Top 10 queries with the highest CPU consumption in the past hour
   SELECT * FROM starrocks_audit_db__.starrocks_audit_tbl__
   WHERE timestamp >= DATE_SUB(NOW(), INTERVAL 1 HOUR)
   ORDER BY cpuCostSec desc limit 10;
   ```
