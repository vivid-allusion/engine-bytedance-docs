---
title: "Locating large queries"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/si_doris_locating_large_queries"
---

In a production environment, some large queries may exhaust the resources of the entire cluster. This can affect the performance and availability of other queries. It is necessary to quickly locate and handle recent large queries or jobs that consume significant resources to reduce the overall impact on business operations. This article will guide you on how to quickly locate and handle these large queries.

<span id="bdf76a63"></span>
# Applicable versions


|**Product form** |**Engine** |**Deployment method** |**Applicable version** |
|---|---|---|---|
|Serverless instance<br><br>(fully managed) |Doris |Integrated storage and compute |* Version 2.1.x and above<br><br>* Version 1.2.x and above |


<span id="aab98acc"></span>
# Procedure

<span id="1912a783"></span>
## Locating large queries: Completed large queries/jobs

You can use Doris's own audit logs for diagnosis to locate completed jobs and determine whether they are large query jobs that require management. During diagnosis:


* You can focus primarily on the cpuCost, scanBytes, memCostBytes, and queryTime metrics.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">cpuCost can be understood as the CPU time consumed. For example, if the cluster is 8 \* 48 cores and the query's cpuCost = 3840 seconds, it means the cluster CPU needs to run at 100% utilization for 10 seconds to complete the query.   </div>
   

* The following queries can be used to locate top tasks, and you can optimize them in conjunction with scheduling cycles or SQL. In other words, use monitoring to preliminarily identify hardware resource bottlenecks (CPU, memory, disk), and then use the audit log table to identify the top tasks with the highest CPU, memory, or disk resource usage.

   The following is sample code for Doris audit log analysis.

   ```SQL
   -- Collect hourly metrics for Insert/no-Insert query types
   SELECT
       DATE_FORMAT(time, '%Y-%m-%d %H:00:00') AS dt,
       CASE
           WHEN (stmt LIKE '%INSERT%' OR stmt LIKE '%insert%') THEN 'isInsert'
           ELSE 'isQuery'
       END AS `type`,
       ROUND(SUM(scan_bytes / 1024 / 1024), 0) AS sum_scan_mb,
       ROUND(AVG(scan_bytes / 1024 / 1024), 0) AS avg_scan_mb,
       ROUND(SUM(cpu_time_ms / 1000), 0) AS sum_cpu_time_sec,
       ROUND(AVG(cpu_time_ms / 1000), 0) AS avg_cpu_time_sec,
       ROUND(SUM(query_time / 1000), 0) AS sum_query_time_sec,
       ROUND(AVG(query_time / 1000), 0) AS avg_query_time_sec,
       COUNT(*) AS total_query_count
   FROM __internal_schema.audit_log
   WHERE time BETWEEN '2025-06-19 00:00:00' AND '2025-06-25 23:59:00'
     AND stmt != 'SELECT 1'
     AND stmt NOT LIKE '%@@%'
     AND user != 'root'
   GROUP BY 1, 2
   ORDER BY 2, 1;
   
   -- Collect SQL statements with the highest cpuCost
   SELECT
       time,
       user,
       db,
       state,
       error_code,
       error_message,
       query_time / 1000 AS queryTimeSec,
       ROUND(scan_bytes / 1024 / 1024 / 1024, 2) AS scanGB,
       scan_rows,
       ROUND(cpu_time_ms / 1000, 0) AS cpuCostSec,
       ROUND(peak_memory_bytes / 1024 / 1024 / 1024, 2) AS memCostGB,
       stmt
   FROM __internal_schema.audit_log
   WHERE time BETWEEN '2025-06-21 10:00:00' AND '2025-06-21 11:00:00'
   ORDER BY cpu_time_ms DESC
   LIMIT 50;
   
   -- Collect cpuCost by digest (digest: SQL fingerprint, which typically represents a class of SQL and can identify the user's interface)
   -- Doris is enabled by default
   SELECT
       sql_digest,
       AVG(query_time) / 1000 AS avgQueryTimeSec,
       ROUND(AVG(scan_bytes) / 1024 / 1024 / 1024, 2) AS avgScanGB,
       AVG(scan_rows) AS avgScanRows,
       ROUND(AVG(cpu_time_ms) / 1000, 0) AS avgCpuCostSec,
       ROUND(MAX(peak_memory_bytes) / 1024 / 1024 / 1024, 2) AS maxMemCostGB
   FROM __internal_schema.audit_log
   WHERE time BETWEEN '2025-06-21 10:00:00' AND '2025-06-21 11:00:00'
   GROUP BY sql_digest
   ORDER BY avgCpuCostSec DESC
   LIMIT 50;
   ```
   


<span id="04b579a4"></span>
## Locating large queries: Running large queries/jobs


1. View the current resource consumption of queries. For details, see [Doris View Running Queries](https://doris.apache.org/zh-CN/docs/2.1/sql-manual/sql-statements/system-info-and-help/SHOW-PROC?_highlight=current_query#%E6%8F%8F%E8%BF%B0). The following are query examples for several typical scenarios.

   * SQL for top N CPU usage

      ```SQL
      SELECT
          t1.query_id AS be_query_id,
          t1.query_type,
          t2.query_id,
          t2.workload_group_id,
          t2.`database`,
          t1.cpu_time,
          t2.`sql`
      FROM (
          SELECT
              query_id,
              query_type,
              SUM(task_cpu_time_ms) AS cpu_time
          FROM information_schema.backend_active_tasks
          GROUP BY query_id, query_type
      ) t1
      LEFT JOIN active_queries t2
          ON t1.query_id = t2.query_id
      WHERE query_type != 'LOAD'
      ORDER BY cpu_time DESC
      LIMIT 10;
      ```
      

   * SQL for top N memory usage

      ```SQL
      SELECT
          t1.query_id AS be_query_id,
          t1.query_type,
          t2.query_id,
          t2.workload_group_id,
          t1.mem_used
      FROM (
          SELECT
              query_id,
              query_type,
              SUM(current_used_memory_bytes) AS mem_used
          FROM information_schema.backend_active_tasks
          GROUP BY query_id, query_type
      ) t1
      LEFT JOIN active_queries t2
          ON t1.query_id = t2.query_id
      WHERE query_type != 'LOAD'
      ORDER BY mem_used DESC
      LIMIT 10;
      ```
      

   * SQL for top N scanned data volume

      ```SQL
      SELECT
          t1.query_id AS be_query_id,
          t1.query_type,
          t2.query_id,
          t2.workload_group_id,
          t1.scan_rows,
          t1.scan_bytes
      FROM (
          SELECT
              query_id,
              query_type,
              SUM(scan_rows) AS scan_rows,
              SUM(scan_bytes) AS scan_bytes
          FROM information_schema.backend_active_tasks
          GROUP BY query_id, query_type
      ) t1
      LEFT JOIN active_queries t2
          ON t1.query_id = t2.query_id
      WHERE query_type != 'LOAD'
      ORDER BY scan_rows DESC, scan_bytes DESC
      LIMIT 10;
      ```
      

   The returned results usually include the following columns.

   * be_query_id

   * query_type: SELECT, LOAD, indicating query, import, and so on

   * workload_group_id: workload group isolation information

   * database: database name

   * cpu_time: The CPU time used by the current query, Unit: seconds. This is the cumulative CPU time of multiple threads. For example, if two threads consume 1 second and 2 seconds of CPU time respectively, the total CPU time is 3 seconds.

   * mem_used: The current memory usage. If the query involves multiple BE nodes, this value is the sum of memory used by the query on all BE nodes.

2. Terminate queries with high CPU usage time (CPUTime). For details, see [Doris Kill](https://doris.apache.org/zh-CN/docs/admin-manual/workload-management/kill-query/).

   * Terminate large queries based on queryId.

      ```SQL
      -- Kill the corresponding queryId
      kill query {queryId};
      ```
      

   * If the version is lower, only direct connection termination may be supported. In this case, you need to first execute show processlist to obtain connection information, then locate the corresponding connection Id based on the query_id. For details about the commands, see [SHOW PROCESSLIST](https://doris.apache.org/docs/4.x/sql-manual/sql-statements/session/queries/SHOW-PROCESSLIST/?_highlight=show&_highlight=processli#%E8%AF%AD%E6%B3%95) and [Terminate query](https://doris.apache.org/docs/4.x/admin-manual/workload-management/kill-query?_highlight=kill). The following is a simple example.

      ```SQL
      -- For example, we have obtained query_id 1710f53deaed42b6-aa97fd39292eef56
      SET SHOW_ALL_FE_CONNECTION = TRUE;
      SHOW FULL PROCESSLIST;
      +------------------+------+--------------------------------------+---------------------+---------------------+----------+----------+---------+-------+-------+-----------------------------------+------+--------------+
      | CurrentConnected | Id   | User                                 | Host                | LoginTime           | Catalog  | Db       | Command | Time  | State | QueryId                           | FE   | CloudCluster |
      +------------------+------+--------------------------------------+---------------------+---------------------+----------+----------+---------+-------+-------+-----------------------------------+------+--------------+
      | No               | 4676 | doris_ad_high_dim_local_ssd_emr_lf_r | [fdbd:dc01:a:391:0:0:0:173]:37462 | 2026-01-27 18:07:54 | internal | information_schema | Sleep | 48 | ERR | errCode = 2, detailMessage = mismatched input '{' expecting {')', ',', ';', 'ORDER'}(line 1, pos 532) | 2605:340:cd51:4500:632a:3213:457f:88ef | NULL |
      | No               | 4358 | root                                 | 127.0.0.1:16210     | 2026-01-27 16:12:23 | internal | ad_high_dim_local | Sleep | 231 | EOF | 1710f53deaed42b6-aa97fd39292eef56 | 2605:340:cd51:4500:632a:3213:457f:88ef | NULL |
      +------------------+------+--------------------------------------+---------------------+---------------------+----------+----------+---------+-------+-------+-----------------------------------+------+--------------+
      
      -- As shown, 1710f53deaed42b6-aa97fd39292eef56 corresponds to the second record, with Connection Id 4358
      -- Directly kill the connection
      KILL 4358;
      ```
      


<span id="54920a87"></span>
## If you cannot quickly locate large queries and need to mitigate losses promptly


1. If you cannot quickly locate large running queries, it is recommended to restart BE to terminate all queries and restore overall business.

2. After restarting to mitigate losses, you can refer to [SQL diagnostics instructions](https://docs.byteplus.com/docs/E-MapReduce/109126) or the audit log table to analyze historical queries, investigate the source of large queries based on business context, and optimize queries. For detailed instructions, see: [Query optimization](https://doris.apache.org/zh-CN/docs/3.x/query-acceleration/performance-tuning-overview/tuning-overview).

   ```SQL
   -- View the top 10 queries with the highest CPU consumption in the past hour
   SELECT * FROM __internal_schema.audit_log
   where time >= DATE_SUB(NOW(), INTERVAL 1 HOUR)
   ORDER BY cpu_time_ms desc limit 10;
   ```
