---
title: "Monitoring panel management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/performance_monitoring_management"
---

The Database Workshop (DBW) supports the performance monitoring feature, which can provide a wide range of performance metrics. With these metrics, you can view the performance trends of your database instances and identify possible risks in your database instances in a timely manner. This topic describes performance monitoring metrics and procedures to view performance monitoring, helping you understand the operation of database instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance for RDS for MySQL has been created, and the instance status is **Running**. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/create_instance).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This feature is not supported when the instance status is creating, recovering, importing, error, deleted, terminated, waiting for payment, billing suspension in progress, billing restoring, billing reclaiming or reconstructing.   </div>
   

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* It takes approximately 10 to 20 seconds to view SQL index optimization suggestions.

* Index optimization suggestions are based on sampling analysis of partial data in the table. The generated optimization suggestions are for reference only and need to be further evaluated based on the actual situation.

* The monitoring granularity of performance monitoring indicators is related to the query time range. The larger the query time range, the larger the monitoring granularity of the indicators. For example, when the time range is within 6 hours, the monitoring granularity is 30s; when the time range is within 24 hours, the monitoring granularity is 1min; when the time range is 3 days, the monitoring granularity is 5min.

* While using the performance monitoring feature, avoid modifying instance configurations, as this may prevent normal display of performance monitoring.


<span id=".55uR5o6n5oyH5qCH"></span>
## Monitoring metrics


|**Metric item** |**English name** |**Unit** |**Description** |
|---|---|---|---|
|InnoDB row lock current waits |InnodbRowLockWaits |count/s |Times of Row Locks Waiting. |
|Number of rollbacks |OperationRollback |count/s |Number of `Rollback` requests performed per second. |
|OperationUpdate |OperationUpdate |count/s |Number of `Update` requests executed per second |
|OperationInsert |OperationInsert |count/s |Number of `INSERT` requests executed per second. |
|OperationDelete |OperationDelete |count/s |Number of `Delete` requests executed per second |
|Number of queries |OperationSelect |count/s |Number of `Select` requests executed per second. |
|Slow queries |SlowQueries |count/s |Number of queries that exceed `long_query_time` seconds. |
|Number of queries |QPS |count/s |Number of requests per second. |
|Number of transactions |TPS |count/s |Number of transactions per second. |
|Outgestion |NetworkTransmitThroughput |Bytes/s |The average amount of data the server sends to the client per second. |
|Ingestion |NetworkReceiveThroughput |Bytes/s |Average amount of data the server receives per second from all clients. |
|SelectScan |SelectScan |count/s |Number of queries performing full table scans. |
|Threads running |ThreadsRunning |count/s |Number of active (non\-sleeping) threads. |
|Number of open connections |ThreadsConnected |count |The number of currently open connections. |
|InnoDB read count |InnodbDataReadCounts |count/s |The number of bytes of data that the InnoDB engine has read per second. |
|InnoDB write count |InnodbDataWriteCounts |count/s |The number of bytes of data that the InnoDB engine has written per second. |
|Average number of InnoDB physical writes to the Redo Log File per second |InnodbLogWrites |count/s |Average number of InnoDB physical writes to the Redo Log File per second. |
|Number of Fsync operations performed by InnoDB per second on average |InnodbDataFsyncs |count/s |The average number of I/O operations performed by the RDS for MySQL database InnoDB storage engine on the disk per second. |
|Number of InnoDB rows deleted per second |InnodbRowsDeleted |count/s |Rows deleted by the InnoDB engine per second. |
|Number of InnoDB rows inserted per second |InnodbRowsInserted |count/s |Rows inserted into the InnoDB engine per second. |
|InnoDB number of rows updated per second |InnodbRowsUpdated |count/s |Rows updated by the InnoDB engine per second. |
|InnoDB number of rows read per second |InnodbDataReadBytes |count/s |The rows read by the InnoDB engine per second. |
|Disk usage |DiskUsageBytes |Bytes |The used amount of disk space. |
|CPU usage |CpuUtil |% |CPU usage of the database. |
|Memory usage |MemUtil |% |Memory usage of the database. |
|Disk usage |DiskUtil |% |Disk space utilization |
|InnoDB Buffer Pool Usage |InnodbCacheUtil |% |InnoDB Buffer pool usage. |
|InnoDB Buffer Pool Hit Rate |InnodbCacheHitRate |% |InnoDB Buffer pool hit rate. |
|InnoDB Buffer Pool dirty page ratio |InnodbBpDirtyPct |% |InnoDB Buffer Pool dirty page ratio. |
|Number of InnoDB Buffer Pool flush Page requests |InnodbBufferPoolPagesFlushed |count/s |Number of InnoDB Buffer Pool flush Page requests per second. |
|Average number of times InnoDB reads pages from Buffer Pool per second (logical read). |InnodbBufferPoolReadRequests |count/s |Number of pages read from the Buffer Pool by the InnoDB storage engine per second. |


<span id=".5p-l55yL5oCn6IO955uR5o6n5oyH5qCH"></span>
## View performance monitoring metrics

You can view the development trend of performance within the query time period.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the project and region.

4. On the **Observation and diagnosis** page, click **Performance monitoring**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also switch to the target instance by searching for the instance ID.   </div>
   

5. In the upper left corner of the **Performance monitoring** tab, switch to the target instance.

6. On the **Performance monitoring** tab, set the query time, node, and metric item as needed to view the metric information.

   For details on performance monitoring, refer to [Monitoring metrics](https://docs.byteplus.com/en/docs/DBW/performance_monitoring_management#.55uR5o6n5oyH5qCH).


<span id=".5p-l55yL5oCn6IO955uR5o6n5YiG5p6Q57uT5p6c"></span>
## View the performance monitoring analysis results

DBW supports diagnostic analysis of performance metrics such as the number of slow queries and the number of Row Locks Waiting.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the project and region.

4. On the **Observation and diagnosis** page, click **Performance monitoring**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also switch to the target instance by searching for the instance ID.   </div>
   

5. In the upper left corner of the **Performance monitoring** tab, switch to the target instance.

6. On the **Performance monitoring** tab, set the query time and node as needed to view the diagnostic analysis results on the number of slow queries and Row Locks Waiting.

   
   |**Metric item** |**Description** |
   |---|---|
   |**Slow queries** |On the **Slow queries (count/s) pane, hover over a time point in the area, click Diagnostic analysis in the pop\-up dialog box**, and view the following information in the **Diagnostic analysis** control panel:<br><br><br>* **Slow queries**: In this area, view the trend of slow queries at a certain diagnostic time point.<br><br>* **TOP 8 slow SQL**: In this area, select a node ID as needed, and perform the following operations:<br><br>   * View SQL template information, including **SQL template**, **Database**, **Execution user**, **IP source**, **Execution times**, **Total time**, **Maximum execution time(s)** , **Average execution time(s)** , **Maximum lock wait time(s)** , **Maximum rows returned**, **Average rows returned**, **Maximum rows scanned**, **Average rows scanned**, **First occurrence time**, and **Last occurrence time**.<br><br>   * View SQL index optimization suggestions:<br><br>      1. Click **SQL optimization** in the **Actions** column of the target SQL template. In the **Allow authorization** dialog box, click **Authorize**.<br><br>         * The index optimization suggestion function needs to sample and analyze the content of the database and table. Therefore, when you view the index optimization suggestion of SQL for the first time, you need to authorize DBW to read the database and table. If it is already enabled, you do not need to perform this operation again.<br><br>         * It takes about 10 to 20 seconds to view SQL index optimization suggestions.<br><br>      2. In the **SQL optimization suggestions** dialog box, view SQL optimization suggestions, including the executed SQL statement, **Execution plan**, and **Optimization suggestions**, including **Index optimization** and **SQL rewrite**. |
   |**InnoDB row lock current waits** |In the **Number of Current Row Locks Waiting for InnoDB Table** area, hover the mouse over a certain point in **Diagnosis analysis**. On the **Diagnosis analysis** control panel, view the following information:<br><br><br>* **InnoDB row lock current waits**: View the trend of the InnoDB row lock current waits at a certain diagnostic time point in this area.<br><br>* **Lock wait list**: In this area, select a node ID as needed to perform the following operations:<br><br>   * View transaction ID formation: Includes **Transaction ID**, **Transaction status**, **Row lock wait SQL**, **Transaction start time**, **Transaction wait since**, **Blocked waiting time(s)** , **Number of rows modified by the transaction**, **Transaction locked rows**, **Transaction operation status**, **Blocking transaction ID**, **Blocking transaction status**, **Transaction context information (Blocker SQL)** , **Blocking transaction start time**, **Blocking transaction wait start time**, **Blocking transaction modified row count**, and **Blocking transaction operation status**.<br><br>   * View lock wait details:<br><br>      1. On the **Lock wait list** pane, click **View details** in the **Actions** column of the target transaction ID.<br><br>      2. In the **Lock wait details** dialog box, view the **Session ID** and **Blocking transaction session ID**.<br><br>         * Session ID: Includes **Transaction ID**, **Transaction status**, **Waiting for query**, **Transaction start time**, **Transaction wait since**, **Blocked waiting time(s)** , **Number of rows modified by the transaction**, **Number of rows locked**, and **Transaction operation status**. <br><br>         * Blocking transaction session ID: Includes **Blocking transaction ID**, **Blocking transaction status**, **Transaction context information**, **Blocking transaction wait start time**, **Blocked waiting time(s)** , **Blocking transaction modified row count**, **Number of locked rows for blocking transactions ** , and **Blocking transaction operation status**. |
   


<span id="faq"></span>
## FAQ

<span id=".5Li65LuA5LmI5Zyo5oCn6IO955uR5o6n6aG16Z2i5p-l55yL5oWi5p-l6K-i5ZKMLWlubm9kYi3ooajlvZPliY3nrYnlvoUtcm93LWxvY2tzLeasoeaVsOmDveacieaVsOaNru-8jOS9huWcqOiviuaWreWIhuaekOaOp-WItumdouadv-WNtOayoeaVsOaNru-8nw=="></span>
### Why is there data for the number of slow queries and Row Locks Waiting on the performance monitoring page, but no data on the diagnostic analysis control panel?

Due to the inconsistent collection frequency of Cloud Monitor and the Collector, the data of these two performance metrics is inconsistent on the performance monitoring page and the diagnostic analysis control panel.

<span id=".5Li65LuA5LmI5LqL5Yqh5LiO6ZSB6aG16Z2i6YeH6ZuG55qE5q276ZSB5pe26Ze044CB5q276ZSB5qyh5pWw5ZKM5oCn6IO955uR5o6n6YeH6ZuG55qE5LiN5LiA6Ie077yf"></span>
### Why are the deadlock time and deadlock count collected on the transactions and locks page inconsistent with those collected by performance monitoring?

The reasons for the inconsistency between Row Locks Waiting, Holding Locks, and Deadlocks are as follows:


* **Row locks waiting**: When a transaction attempts to acquire a lock on row data that has been locked by another transaction, the transaction will enter a waiting state before acquiring the lock. This lock is called a waiting row lock. This is a concurrency control mechanism implemented by the database to ensure data consistency.

* **Holding Locks:**  After a transaction starts executing, it locks the data it needs to access, thereby protecting this part of the data from being changed by other transactions during the transaction execution process. This type of lock is called a holding lock. A transaction can hold multiple locks, which can be row locks (locking a single record) or table locks (locking an entire table).

* **Deadlocks**: A deadlock refers to a blocked state caused by two or more transactions holding each other's required resources during execution. For example, transaction A holds resource 1 and waits to acquire resource 2, while transaction B holds resource 2 and waits to acquire resource 1, which constitutes a deadlock. When a deadlock occurs, the database system typically resolves it by terminating and rolling back one of the transactions through a certain mechanism, such as deadlock detection and timeout mechanisms.
