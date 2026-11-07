---
title: "Performance diagnosis: Query log analysis"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/performance-diagnosis-query-log-analysis"
---

By analyzing query logs, you can monitor the execution of queries, identify slow queries, and enhance system performance and solve potential issues. This article explains how to view ByteHouse CE cluster query logs using SQL.

<span id="96f52b63"></span>
# **Prerequisites**

Ensure that query logs are activated.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Default query logs in ByteHouse are activated.</div>


* <div data-tips="true" data-tips-type="tip">You can <code>check the Parameter configuration 'log_queries'</code> by running SHOW settings like 'log_queries'; to confirm if query logs are activated. If this parameter configuration is set to 1, then query logs are activated; if it is set to 0, then query logs have not started. You can activate query logs using the following SQL statement.</div>



<div data-tips="true" data-tips-type="tip">```SQL
-- Execute in the mode of selecting all nodes
SET log_queries = 1;
```
</div>


<span id="b170d23e"></span>
# **Caution**


* Query logs may contain sensitive information; please manage them carefully.

* Regularly clean and archive query logs to prevent excessive file size.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In ByteHouse, a 30\-day TTL strategy has been set as default for the query_log table; query logs will be automatically deleted after 30 days.</div>



<span id="54b12039"></span>
# **Example Environment**

The following example is based on the nodes 192.168. *.* ; during actual use, please modify the corresponding parameters according to your scenario. If you do not know how to obtain the node name, you can do so by the following methods.


* Using the console: You can obtain the node name on the Manage Clusters page.

* Using SQL statements: You can run the following statement to obtain all node names in the cluster.


```SQL
SELECT * FROM system.clusters;
```


<span id="f62b628f"></span>
# View the recent error Query

Viewing error logs is important for enhancing the stability and security of the system. This is mainly reflected in the following aspects:


* Rapid problem identification: Error information can pinpoint the specific reason causing the problem, allowing for quick resolution.

* Trend analysis: By analyzing the error logs, identifying the time and pattern of errors can lead to defensive code optimization or configuration adjustments.

* Safety: By analyzing the error logs, potential security issues in the system, such as SQL injections and unauthorized access, have been identified.


**Query Template**

```SQL
SELECT
    written_rows,
    written_bytes,
    query_duration_ms,
    event_time,
    exception
FROM clusterAllReplicas('',system.query_log) ql
WHERE ((event_time >= '') 
       AND 
       (event_time <= '')) AND (lowerUTF8(query) LIKE '%insert into demo_local%') 
       AND (type != 'QueryStart')
       AND (exception_code != 0)
       [AND host() = '']
ORDER BY event_time DESC
[LIMIT <x>]
```


**Parameter Description**


|**Parameter** |Description |Example Value |
|---|---|---|
|cluster_name |Cluster name |default |
|startTime |Start time for querying data.<br><br>Format: yyyy\-mm\-dd hh:mm:ss |2025\-01\-21 22:00:00 |
|endTime |End time for querying data.<br><br>Format: yyyy\-mm\-dd hh:mm:ss |2025\-01\-23 23:00:00 |
|nodeIP |Cluster IP. For details on the method to obtain nodes, see **Example Environment** |`192.18.*.*` |
|x |Return the top x rows from the query results set. |30 |


**Example**

Query for error log information on the node at 192.18. *.*  between 2025\-01\-21 22:00:00 and 2025\-01\-23 23:00:00, returning the first 30 lines of results.

```SQL
SELECT
    written_rows,
    written_bytes,
    query_duration_ms,
    event_time,
    exception
FROM clusterAllReplicas('',system.query_log) ql
WHERE (lowerUTF8(query) LIKE '%insert into demo_local%') AND 
 ((event_time >= '2025-01-21 22:00:00') 
       AND 
       (event_time <= '2025-01-23 23:00:00')) 
       AND (type != 'QueryStart')
       AND (exception_code != 0)
AND host() = '192.18.*.*'
ORDER BY event_time DESC
LIMIT 30
```


<span id="551ca2ce"></span>
# View recent SQL

Query template

Write SQL

```SQL
--View the most recently written SQL, including the number of rows and byte size of each batch. 
SELECT
    written_rows,
    written_bytes,
    query_duration_ms,
    event_time
FROM clusterAllReplicas('',system.query_log) ql
WHERE ((event_time >= '') 
       AND (event_time <= ''))
       AND (upperUTF8(query) ILIKE '%INSERT INTO%') AND (type != 'QueryStart')
       [AND host() = '']
ORDER BY event_time DESC
[LIMIT x]
```


Not Write SQL

```SQL
SELECT   
    event_time,   
    user,   
    query_id AS query,   
    read_rows,   
    read_bytes,   
    result_rows,   
    result_bytes,   
    memory_usage,   
    exception  
FROM clusterAllReplicas('', system.query_log)  
WHERE (event_date = today()) AND (event_time >= (now() - <time>)) AND (is_initial_query = 1) AND (upperUTF8(query) NOT ILIKE 'INSERT INTO%'  [AND host() = ''])  
ORDER BY event_time DESC  
[LIMIT x]
```


**Parameter description**


|**Param** |**Description** |Example |
|---|---|---|
|cluster_name |Cluster name |default |
|time |Query the time moving backward from the current time.<br><br>Unit: Minute. |60 |
|nodeIP |Cluster node IP. Node acquisition method, see **Example Environment** for details. |192.168. *.*  |
|x |Return the top x rows in the query result set. |100 |


**Example**

Search for non\-write SQL activities on the node 192.168. *.*  within the last 60 minutes, and display the first 100 entries in the query results.

```SQL
SELECT   
    event_time,   
    user,   
    query_id AS query,   
    read_rows,   
    read_bytes,   
    result_rows,   
    result_bytes,   
    memory_usage,   
    exception  
FROM clusterAllReplicas('', system, query_log)  
WHERE (event_date = today()) AND (event_time >= (now() - 60)) AND (is_initial_query = 1) AND (query NOT LIKE 'INSERT INTO%')  
AND host() = '192.168.*.*'
ORDER BY event_time DESC  
LIMIT 100
```


<span id="4f9387c0"></span>
## **View non\-write statements executed more than 'n' times within a time frame**

**Search template**

```SQL
SELECT *
FROM
  (SELECT LEFT(query, 100) AS SQL,
          count() AS queryNum,
          sum(query_duration_ms) AS totalTime,
          totalTime/queryNum AS avgTime
   FROM clusterAllReplicas('', system.query_log) ql
   WHERE event_time > toDateTime('')
     AND event_time < toDateTime('')
     AND upperUTF8(query) not like '%INSERT INTO%'
     AND host() = ''
   GROUP BY SQL
   ORDER BY avgTime DESC)
WHERE queryNum > <queryNum> 
[LIMIT <x>]
```


**Parameter description**


|**Param** |Description |Value example |
|---|---|---|
|cluster_name |Cluster name |default |
|startTime |Start time for data query.<br><br>Format: yyyy\-mm\-dd hh:mi:ss |2022\-09\-23 12:00:00 |
|endTime |End time for data query.<br><br>Format: yyyy\-mm\-dd hh:mi:ss |2022\-09\-23 17:00:00 |
|queryNum |Exceeding number of queries required. |1000 |
|nodeIP |Cluster node IP. For node retrieval methods, see **Example Environment** |192.168. *.*  |
|x |Returns the top x rows of the query result set. |50 |


**Example**

Search for non\-write SQL statements with more than 1000 executions between 2024\-09\-23 12:00:00 to 2024\-09\-23 17:00:00 on node 192.168. *.* .

```SQL
SELECT *
FROM
  (SELECT LEFT(query, 100) AS SQL,
          count() AS queryNum,
          sum(query_duration_ms) AS totalTime,
          totalTime/queryNum AS avgTime
   FROM clusterAllReplicas('', system.query_log) ql
   WHERE event_time > toDateTime('2024-09-23 12:00:00')
     AND event_time < toDateTime('2024-09-23 17:00:00')
     AND upperUTF8(query) not like '%INSERT INTO%'
     AND host() = '192.168.*.*'
   GROUP BY SQL
   ORDER BY avgTime DESC)
WHERE queryNum > 1000
LIMIT 50
```


<span id="2d6cac80"></span>
## Statistics for queries per hour or per minute within a time frame

Search template

**Hourly aggregate**

Statistics on the number of queries and average time per hour during a period.

```SQL
--Aggregate by hour
SELECT toHour(event_time) AS t,
       count() AS queryNum,
       sum(query_duration_ms) AS totalTime,
       totalTime/queryNum AS avgTime
FROM clusterAllReplicas('', system.query_log) ql
WHERE event_time > toDateTime('')
  AND event_time < toDateTime('')
  AND upperUTF8(query) not like '%INSERT INTO%'
  AND read_rows != 0
  AND host() = ''
GROUP BY t
[LIMIT x]
```


**Minute\-by\-minute aggregate**

Statistics on the number of queries and average time per minute during a period.

```SQL
--Aggregate by minute
SELECT toMinute(event_time) AS t,
       count() AS queryNum,
       sum(query_duration_ms) AS totalTime,
       totalTime/queryNum AS avgTime
FROM clusterAllReplicas('', system.query_log) ql
WHERE event_time > toDateTime('')
  AND event_time < toDateTime('')
  AND upperUTF8(query) not like '%INSERT INTO%'
  AND host() = ''
  AND read_rows != 0
GROUP BY t
[LIMIT x]
```


**Parameter description**


|**Param** |Description |Value Example |
|---|---|---|
|cluster_name |Cluster Name |default |
|startTime |The start time for querying data.<br><br>Format: yyyy\-mm\-dd hh:mi:ss |2022\-09\-23 12:00:00 |
|endTime |The end time for querying data.<br><br>Format: yyyy\-mm\-dd hh:mi:ss |2022\-09\-23 17:00:00 |
|nodeIP |Cluster node IP. For details on node acquisition methods, see **Example Environment** |192.168. *.*  |
|x |Return the top x rows in the query result set. |50 |


**Search example**

Statistics and average execution time of hourly query counts on node 192.168. *.*  from 2024\-09\-23 08:00:00 to 2024\-09\-23 17:00:00.

```SQL
--Aggregate by hour
SELECT toHour(event_time) AS t,
       count() AS queryNum,
       sum(query_duration_ms) AS totalTime,
       totalTime/queryNum AS avgTime
FROM clusterAllReplicas('', system.query_log) ql
WHERE event_time > toDateTime('2024-09-23 08:00:00')
  AND event_time < toDateTime('2024-09-23 17:00:00')
  AND upperUTF8(query) not like '%INSERT INTO%'
  AND read_rows != 0
  AND host() = '192.168.*.*'
GROUP BY t
LIMIT 50
```


<span id="a71d18a4"></span>
## View the number of LEFT JOIN queries

View the number of `LEFT JOIN` queries within a time frame.

**Search template**

```SQL
SELECT *
FROM
  (SELECT LEFT(query, 100) AS SQL,
          count() AS queryNum,
          sum(query_duration_ms) AS totalTime,
          totalTime/queryNum AS avgTime
   FROM clusterAllReplicas('', system.query_log) ql
   WHERE upperUTF8(query) like '%LEFT JOIN%'
     AND read_rows != 0
     AND event_time > toDateTime('')
     AND event_time < toDateTime('')
     AND upperUTF8(query) not like '%INSERT INTO%'
     AND host() = ''
   GROUP BY SQL
   ORDER BY queryNum DESC)
```


**Parameter description**


|**Param** |Description |Value Example |
|---|---|---|
|cluster_name |Cluster Name |default |
|startTime |Start time to query the data.<br><br>Format: yyyy\-mm\-dd hh:mm:ss |2022\-09\-23 12:00:00 |
|endTime |End time to query the data.<br><br>Format: yyyy\-mm\-dd hh:mm:ss |2022\-09\-23 21:00:00 |
|nodeIP |Cluster node IP. For details on how to obtain nodes, see **the example environment**. |192.168. *.*  |


**Search example**

View the number of LEFT JOIN statements executed on the node at 192.168. *.*  during the period from 2024\-06\-25 12:00:00 to 2024\-06\-25 15:00:00.

```SQL
SELECT *
FROM
  (SELECT LEFT(query, 100) AS SQL,
          count() AS queryNum,
          sum(query_duration_ms) AS totalTime,
          totalTime/queryNum AS avgTime
   FROM clusterAllReplicas('', system.query_log) ql
   WHERE upperUTF8(query) like '%LEFT JOIN%'
     AND read_rows != 0
     AND event_time > toDateTime('2024-06-25 12:00:00')
     AND event_time < toDateTime('2024-06-25 15:00:00')
     AND upperUTF8(query) not like '%INSERT INTO%'
     AND host() = '192.168.*.*'
   GROUP BY SQL
   ORDER BY queryNum DESC)
```


<span id="33a66bbf"></span>
## **Rank the number of non\-write SQL executions by user**

**Search template**

```SQL
SELECT   
    user,   
    count(1) AS query_times,   
    sum(read_bytes) AS query_bytes,   
    sum(read_rows) AS query_rows  
FROM clusterAllReplicas('', system, query_log)  
WHERE (event_date = yesterday()) AND (is_initial_query = 1) AND (upperUTF8(query) NOT LIKE 'INSERT INTO%' AND host() = '')  
GROUP BY user  
ORDER BY query_times DESC  
[LIMIT x]
```


**Parameter description**


|**Param** |Description |Value example |
|---|---|---|
|cluster_name |Cluster name |default |
|nodeIP |Cluster node IP. For details, see **Example Environment** for the node acquisition method. |192.168. *.*  |
|x |The total number of search ranks. |10 |


**Example**

Search the top ten users who ran non\-write query statements on node 192.168. *.* .

```SQL
SELECT   
    user,   
    count(1) AS query_times,   
    sum(read_bytes) AS query_bytes,   
    sum(read_rows) AS query_rows  
FROM clusterAllReplicas('', system, query_log)  
WHERE (event_date = yesterday()) AND (is_initial_query = 1) AND (upperUTF8(query) NOT LIKE 'INSERT INTO%' AND host() = '192.168.*.*')  
GROUP BY user  
ORDER BY query_times DESC  
LIMIT 10
```
