---
title: "Locate large queries"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Locate_large_queries"
---

<span id="853e927f"></span>
## Overview

In MPP analytical databases such as StarRocks and Apache Doris, **large queries / large jobs** may consume significant CPU, memory, disk, and IO resources in a short period, thereby affecting the stability and latency of other queries in the cluster.

This article introduces a practical troubleshooting method:


* How to **identify completed** top large queries (based on audit logs)

* How to **identify running** top large queries (based on runtime views)

* How to quickly **terminate queries** and provide a basis for subsequent optimization


<span id="dcdf2b02"></span>
## Use cases


* **Troubleshooting:**  When the cluster experiences abnormal CPU, memory, or disk resource usage, or widespread query timeouts, it is necessary to quickly identify the "recent culprit" and take action to reduce the overall impact.

* **Routine inspection:**  Periodically collect statistics on historical large queries and large jobs, conduct comprehensive evaluation based on business requirements and resource consumption, and drive optimization and governance.


<span id="51f90336"></span>
## Determination and key metrics (common audit log fields)

In audit logs, it is recommended to focus on the following metrics (field names may vary slightly by version; refer to the actual table structure):


* \*\*`cpuCost` / `cpu_time_ms` / `cpuCostNs`: \*\*CPU consumption (usually the accumulated CPU time across multiple threads)

* \*\*`scanBytes` / `scan_bytes`: \*\*Amount of data scanned (measures IO pressure and whether effective partition pruning is possible)

* \*\*`memCostBytes` / `peak_memory_bytes`: \*\*Memory consumption (indicates whether there are large aggregations, large sorts, large joins, and so on)

* \*\*`queryTime` / `query_time`: \*\*Query duration (directly related to user experience and SLA)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>How to interpret cpuCost:</strong></div>



* <div data-tips="true" data-tips-type="tip"><code>cpuCost</code> can be understood as "the total sum of CPU time slices occupied."</div>


* <div data-tips="true" data-tips-type="tip">For example, if the cluster is <code>8 * 48core</code> (total 384 cores), and a query has <code>cpuCost = 3840 seconds</code>, it means that all CPUs may need to run at 100% utilization for about <code>10 seconds</code> to complete execution (for intuitive understanding only).</div>



<span id="8019f7a9"></span>
## Procedure overview


1. **First, check monitoring**: Make a preliminary judgment on the type of resource bottleneck (CPU, memory, disk, IO).

2. **Next, check audit logs**: Identify historical top tasks (by hour, by SQL, by Digest fingerprint).

3. **Check runtime views**: Identify currently running top tasks (terminate quickly if necessary).

4. **Remediation and optimization**: Terminate queries and retain evidence (QueryId, ConnectionId, SQL, Digest) to drive subsequent governance.


<span id="aa759305"></span>
## Step 1: Use monitoring to preliminarily identify resource bottlenecks

It is recommended to first confirm the following on the monitoring side:


* Whether CPU usage is persistently high or has spikes

* Whether memory is near the limit or frequently triggers GC/Spill

* Whether disk IO is high or there is prolonged read/write congestion


Then, use the audit logs to identify the top queries by CPU, memory, scan volume, and other metrics.

<span id="0b93e5d9"></span>
## Step 2: Identify completed large queries/jobs (audit logs)

<span id="ef14343d"></span>
### StarRocks: Audit analysis example

<span id="55fcb1d4"></span>
#### 1) Report resource consumption of Insert and non\-Insert operations by hour

```SQL
-- Collect hourly metrics for Insert / non-Insert query types
SELECT 
    DATE_FORMAT(timestamp, '%Y-%m-%d %H:00:00') AS dt,
    CASE 
        WHEN (stmt LIKE '%INSERT%' OR stmt LIKE '%insert%') THEN 'isInsert'
        ELSE 'isQuery'
    END AS `type`,
    ROUND(SUM(scanBytes/1024/1024), 0) AS sum_scan_mb,
    ROUND(AVG(scanBytes/1024/1024), 0) AS avg_scan_mb,
    ROUND(SUM(cpuCostNs/1000/1000/1000), 0) AS sum_cpu_time_sec,
    ROUND(AVG(cpuCostNs/1000/1000/1000), 0) AS avg_cpu_time_sec,
    ROUND(SUM(queryTime/1000), 0) AS sum_query_time_sec,
    ROUND(AVG(queryTime/1000), 0) AS avg_query_time_sec,
    COUNT(*) AS total_query_count
FROM starrocks_audit_db__.starrocks_audit_tbl__
WHERE timestamp BETWEEN '2025-06-19 00:00:00' AND '2025-06-25 23:59:00'
  AND stmt != 'SELECT 1'
  AND stmt NOT LIKE '%@@%'
  AND user != 'root'
GROUP BY 1, 2
ORDER BY 2, 1;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Tips：</strong></div>



* <div data-tips="true" data-tips-type="tip">The time granularity can be adjusted as needed (by hour, day, or week).</div>


* <div data-tips="true" data-tips-type="tip">It is recommended to filter out health check SQL (such as <code>SELECT 1</code>) and system variable queries (such as those containing <code>@@</code>).</div>



<span id="4bf612c3"></span>
#### 2) Identify top SQL statements by CPU consumption (example)

```SQL
-- Example: Retrieve Top 50 by CPU consumption in descending order
-- Please use actual audit table field names (this example uses cpuCostNs)
SELECT
    timestamp,
    user,
    db,
    ROUND(cpuCostNs/1000/1000/1000, 0) AS cpuCostSec,
    ROUND(scanBytes/1024/1024/1024, 2) AS scanGB,
    ROUND(queryTime/1000, 0) AS queryTimeSec,
    stmt
FROM starrocks_audit_db__.starrocks_audit_tbl__
WHERE timestamp BETWEEN '2025-06-19 00:00:00' AND '2025-06-25 23:59:00'
  AND stmt != 'SELECT 1'
  AND stmt NOT LIKE '%@@%'
  AND user != 'root'
ORDER BY cpuCostNs DESC
LIMIT 50;
```


<span id="4d39f439"></span>
#### 3) Aggregate by Digest fingerprint (identify a class of SQL statements)

`digest` typically represents a class of SQL statements (SQL fingerprint), which helps determine whether they originate from the same business interface or query pattern.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Note:</strong> StarRocks requires the digest feature to be enabled in order to use related fields.</div>


<div data-tips="true" data-tips-type="tip">You can refer to the official documentation:</div>



* <div data-tips="true" data-tips-type="tip">https://docs.starrocks.io/zh/docs/administration/sql_digest/</div>



```SQL
-- Enable digest (example only, requires administrator privileges)
ADMIN SET FRONTEND CONFIG ("enable_sql_digest" = "true");
```


```SQL
WITH top_sql AS (
    SELECT digest, SUM(queryTime) AS sum_query_time
    FROM starrocks_audit_db__.starrocks_audit_tbl__
    GROUP BY digest
    ORDER BY SUM(queryTime) DESC
    LIMIT 10
)
SELECT *
FROM starrocks_audit_db__.starrocks_audit_tbl__
WHERE digest IN (SELECT digest FROM top_sql);
```


<span id="19f9c566"></span>
### Doris: Audit analysis example

<span id="5836f08b"></span>
#### 1) Report resource consumption of Insert and non\-Insert operations by hour

```SQL
-- Collect hourly metrics for Insert / non-Insert query types
SELECT 
    DATE_FORMAT(time, '%Y-%m-%d %H:00:00') AS dt,
    CASE 
        WHEN (stmt LIKE '%INSERT%' OR stmt LIKE '%insert%') THEN 'isInsert'
        ELSE 'isQuery'
    END AS `type`,
    ROUND(SUM(scan_bytes/1024/1024), 0) AS sum_scan_mb,
    ROUND(AVG(scan_bytes/1024/1024), 0) AS avg_scan_mb,
    ROUND(SUM(cpu_time_ms/1000), 0) AS sum_cpu_time_sec,
    ROUND(AVG(cpu_time_ms/1000), 0) AS avg_cpu_time_sec,
    ROUND(SUM(query_time/1000), 0) AS sum_query_time_sec,
    ROUND(AVG(query_time/1000), 0) AS avg_query_time_sec,
    COUNT(*) AS total_query_count
FROM __internal_schema.audit_log
WHERE time BETWEEN '2025-06-19 00:00:00' AND '2025-06-25 23:59:00'
  AND stmt != 'SELECT 1'
  AND stmt NOT LIKE '%@@%'
  AND user != 'root'
GROUP BY 1, 2
ORDER BY 2, 1;
```


<span id="baab9a0c"></span>
#### 2) Identify top SQL statements by CPU consumption

```SQL
SELECT 
    time,
    user,
    db,
    state,
    error_code,
    error_message,
    query_time/1000 AS queryTimeSec,
    ROUND(scan_bytes/1024/1024/1024, 2) AS scanGB,
    scan_rows,
    ROUND(cpu_time_ms/1000, 0) AS cpuCostSec,
    ROUND(peak_memory_bytes/1024/1024/1024, 2) AS memCostGB,
    stmt
FROM __internal_schema.audit_log
WHERE time BETWEEN '2025-06-21 10:00:00' AND '2025-06-21 11:00:00'
ORDER BY cpu_time_ms DESC
LIMIT 50;
```


<span id="867eae02"></span>
#### 3) Aggregate by Digest (identify a class of SQL statements)

Doris usually enables digest\-related capabilities by default. Example:

```SQL
SELECT 
    sql_digest,
    AVG(query_time)/1000 AS avgQueryTimeSec,
    ROUND(AVG(scan_bytes)/1024/1024/1024, 2) AS avgScanGB,
    AVG(scan_rows) AS avgScanRows,
    ROUND(AVG(cpu_time_ms)/1000, 0) AS avgCpuCostSec,
    ROUND(MAX(peak_memory_bytes)/1024/1024/1024, 2) AS maxMemCostGB
FROM __internal_schema.audit_log
WHERE time BETWEEN '2025-06-21 10:00:00' AND '2025-06-21 11:00:00'
GROUP BY sql_digest
ORDER BY avgCpuCostSec DESC
LIMIT 50;
```


<span id="b1a4f575"></span>
## Step 3: Identify running large queries/jobs (runtime view)

<span id="99adb5c0"></span>
### StarRocks: Runtime analysis

> Note: The following commands typically only take effect for **a single FE**, so they need to be executed separately on each FE.


```SQL
SHOW PROC '/current_queries';  -- View currently running queries
KILL <ConnectionId>;           -- Terminate running queries
```


Description of common fields in query results (may vary by version):


* `QueryId`

* `ConnectionId`

* `Database`

* `User`

* `ScanBytes`: Amount of data scanned so far

* `ProcessRow`: Number of rows scanned so far

* `CPUTime`: CPU time used by the current query (seconds, accumulated across threads)

* `MemoryUsage`: Current memory usage (if multiple BEs are involved, usually the sum across all BEs)

* `ExecTime`: Execution duration from initiation to current


<span id="c018c7bb"></span>
### Doris: Runtime analysis

<span id="fcfb80ae"></span>
#### 1) TopN SQL statements by CPU usage

```SQL
SELECT 
        t1.query_id AS be_query_id,
        t1.query_type,
        t2.query_id,
        t2.workload_group_id,
        t2.`database`,
        t1.cpu_time,
        t2.`sql`
FROM
    (
        SELECT query_id, query_type, SUM(task_cpu_time_ms) AS cpu_time
        FROM information_schema.backend_active_tasks
        GROUP BY query_id, query_type
    ) t1
    LEFT JOIN active_queries t2
    ON t1.query_id = t2.query_id
WHERE query_type != 'LOAD'
ORDER BY cpu_time DESC
LIMIT 10;
```


<span id="e9a8d255"></span>
#### 2) TopN SQL statements by memory usage

```SQL
SELECT 
        t1.query_id AS be_query_id,
        t1.query_type,
        t2.query_id,
        t2.workload_group_id,
        t1.mem_used
FROM
    (
        SELECT query_id, query_type, SUM(current_used_memory_bytes) AS mem_used
        FROM information_schema.backend_active_tasks
        GROUP BY query_id, query_type
    ) t1
    LEFT JOIN active_queries t2
    ON t1.query_id = t2.query_id
WHERE query_type != 'LOAD'
ORDER BY mem_used DESC
LIMIT 10;
```


<span id="3fe564e1"></span>
#### 3) TopN SQL statements by scan volume

```SQL
SELECT 
        t1.query_id AS be_query_id,
        t1.query_type,
        t2.query_id,
        t2.workload_group_id,
        t1.scan_rows,
        t1.scan_bytes
FROM
    (
        SELECT query_id, query_type,
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


Common meanings of runtime result fields:


* `be_query_id`: Query ID on the BE side

* `query_type`: `SELECT` / `LOAD` and so on

* `workload_group_id`: Workload isolation group information

* `database`: Database name

* `cpu_time`: CPU usage time (accumulated across threads)

* `mem_used`: Memory usage (if multiple BEs are involved, usually the sum across all BEs)


<span id="c536bfc4"></span>
## Step 4: Handling (terminate queries) and recording traces

<span id="ed1a7c26"></span>
### 1) Prioritize terminating queries: terminate large queries


* Doris：


```SQL
KILL QUERY "<query_id>";
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Note: Compatibility handling for lower versions</strong></div>


<div data-tips="true" data-tips-type="tip">If only <code>kill connection</code> is supported in lower versions, follow these steps:</div>



1. <div data-tips="true" data-tips-type="tip">First, enable display of all FE connections and view the connection list</div>


2. <div data-tips="true" data-tips-type="tip">Then, use <code>QueryId</code> to find the corresponding connection <code>Id</code> (Connection Id)</div>


3. <div data-tips="true" data-tips-type="tip">Finally, execute <code>kill <Id></code></div>



```SQL
SET SHOW_ALL_FE_CONNECTION = TRUE;
SHOW FULL PROCESSLIST;
-- After finding the corresponding Connection Id
KILL <connection_id>;
```



* StarRocks: Usually terminated using `KILL <ConnectionId>`.


<span id="4c6c2923"></span>
### 2) Retain key information (for review and optimization)

It is recommended to record at least the following after termination or identification:


* Time window (start/end time)

* `QueryId` / `ConnectionId`

* SQL text (or Digest fingerprint)

* Resource consumption (CPU/Scan/Memory/Time)

* Source (user/database/business party/interface)


<span id="1143a419"></span>
## Common troubleshooting and optimization recommendations

The following are common governance approaches, which can be advanced step by step based on audit and runtime evidence:


* **Reduce scan volume**: Partition pruning, adding filter conditions, avoiding full table scans, and using pre\-aggregation/materialized views appropriately.

* **Reduce memory pressure**: Avoid excessively large `GROUP BY` / `ORDER BY`, split queries appropriately, and pay attention to join order and data skew.

* **Reduce CPU pressure**: Minimize complex expressions, avoid redundant calculations, control concurrency, and use workload groups for isolation when necessary.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Governance recommendation:</strong> After terminating queries, strive to upgrade from "single SQL optimization" to "digest\-based governance" to more reliably cover similar problematic queries.</div>
