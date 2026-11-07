---
title: "How to solve the problem of high memory usage"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/How_to_solve_the_problem_of_high_memory_usage"
---

When using RDS for MySQL, a high memory usage rate can lead to a risk of memory exhaustion. This article describes several common causes and their solutions.

<span id="问题确认"></span>
## Confirming the problem

You can confirm the current memory usage rate of the instance by viewing the monitoring item for instance memory usage rate.


1. On the Instances page, click the instance name of the target instance to enter the Instances page.

2. Click the Monitoring and alarm tab at the top of the page.

3. Under the **Resource monitoring** category, view the **Memory usage rate**.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6d314f1f8c47d22d7921df321f9bc930.png) </span>

&nbsp;

<span id="快速止损"></span>
## Quick mitigation

If the memory usage rate exceeds 90% for a long time and shows no downward trend, you can quickly restore instance performance through the following two methods.


* Restart instance

* Switch to the primary node


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">MySQL has a dynamic memory balancing mechanism, so memory usage below 90% can be ignored. We also recommend setting the memory usage alert threshold to at least 90%.</div>


* <div data-tips="true" data-tips-type="warning">RDS for MySQL provides a <code>memory usage</code> monitoring metric. You can configure an alert policy for your instance and set a threshold for this metric. When memory usage exceeds the threshold, you will receive an alert. For more information about creating alert policies, refer to <a href="https://www.volcengine.com/docs/6313/140424">Creating alert policies</a>.</div>



<span id="原因定位及解决"></span>
## Cause analysis

The InnoDB Buffer Pool typically uses the most memory. While the Buffer Pool's maximum memory usage is limited by its configuration parameters, a significant amount of memory is also dynamically allocated and adjusted during request execution. This includes memory for temporary in\-memory tables, the table cache, hash indexes, and row lock objects. For detailed information on memory usage and related parameter limits, refer to the [official MySQL documentation](https://dev.mysql.com/doc/refman/8.0/en/memory-use.html).

<span id="开启实例的内存监控功能（可选）"></span>
### Enable memory monitoring for the instance (Optional)

You can enable the memory monitoring feature of performance_schema to troubleshoot memory issues more easily. After you enable performance_schema, query tables with names starting with memory_summary in the performance_schema database to view memory usage. For example, the global memory usage analysis table is memory_summary_global_by_event_name.

Common queries:

```sql
SELECT EVENT_NAME, CURRENT_NUMBER_OF_BYTES_USED FROM performance_schema.memory_summary_global_by_event_name
    WHERE COUNT_ALLOC != 0 
       OR COUNT_FREE != 0
       OR SUM_NUMBER_OF_BYTES_ALLOC != 0 
       OR SUM_NUMBER_OF_BYTES_FREE != 0 
       OR LOW_COUNT_USED != 0 
       OR CURRENT_COUNT_USED != 0 
       OR HIGH_COUNT_USED != 0 
       OR LOW_NUMBER_OF_BYTES_USED != 0 
       OR CURRENT_NUMBER_OF_BYTES_USED != 0 
       OR HIGH_NUMBER_OF_BYTES_USED != 0 
    ORDER BY CURRENT_NUMBER_OF_BYTES_USED DESC
    LIMIT 10;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are not sensitive to query latency or the amount of hot data access is small, you can adjust the buffer pool size to reduce its usage and reserve more memory for dynamic SQL operations.</div>


<span id="qps-上升"></span>
### QPS increase

**Cause analysis**

First, confirm whether the traffic has changed and whether new SQL has been launched. A sudden increase in business traffic may lead to higher memory usage.

Path: log on to [Database Workshop](https://console.byteplus.com/dbw)\>**Observation diagnosis**\>**Performance monitoring**\>**Total queries**. For more information, refer to [View performance monitoring metrics](https://www.volcengine.com/docs/6956/1288461).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c8ea23cb7903596ab7fbb26c3fd85635.png) </span>

**Solutions**

Determine which SQL statements have excessive writes using the full SQL insight feature of the Database Workshop, and limit their execution frequency with [SQL throttling](https://www.volcengine.com/docs/6956/1110640).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Full SQL insight and SQL throttling are currently invitation\-only features of the Database Workshop. To use them, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000736">submit a ticket</a> to apply.</div>



1. Locate SQL: Determine which SQL statements have excessive writes. Path for SQL insight: Log on to [Database Workshop](https://console.byteplus.com/dbw)\>**Observation diagnosis**\>**Full SQL insight**. For more information, refer to [Full SQL insight](https://www.volcengine.com/docs/6956/1277446).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d2febb2c9d78ec5eda42cc9472361fba.jpg) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_da9cbd9c4a6444f1a9c2d7d4241f5da4.jpg) </span>


2. Process SQL. After locating the SQL, it can be processed by [SQL throttling](https://www.volcengine.com/docs/6313/1411540#sql-%E9%99%90%E6%B5%81) or [killing the session](https://www.volcengine.com/docs/6313/1411540#kill-%E4%BC%9A%E8%AF%9D).


<span id="连接数上升"></span>
### Increased connection count

**Cause analysis**

MySQL allocates memory for each connection, so an increased connection count also increases MySQL memory usage.

Path: log on to [Database Workshop](https://console.byteplus.com/dbw)\>**Observation diagnosis**\>**Performance monitoring**\>**Current open connections**. For more information, refer to [View performance monitoring metrics](https://www.volcengine.com/docs/6956/1288461).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_56390ed49796d4397f88c84ab49e8793.png) </span>

**Solution**

Release idle connections.

<span id="sql-导致内存上升"></span>
### SQL causes an increase in memory

<span id="_1-复杂-sql"></span>
#### 1. Complex SQL

**Cause analysis**

The caches that consume more memory at the Server layer include thread caches like Thread Cache, BinLog Cache, Sort Buffer, Read Buffer, and Join Buffer. These caches are non\-resident and are typically released when a connection is closed. A large number of complex SQL statements, such as those with join or order by clauses, may cause an increase in memory.

**Solution**


1. Decrease sort_buffer_size, join_buffer_size, or binlog_cache_size (this may reduce query efficiency).

2. Locate SQL: Run `show processlist` or use [Slow log analysis](https://www.volcengine.com/docs/6956/155352) in the Database Workshop. Then, use the `explain` statement to check for operations such as `JOIN` and `AGG`. The procedure is the same as above. The operation path for slow log analysis is: Log on to [Database Workshop](https://console.byteplus.com/dbw)\>**Observation diagnosis**\>\> **Slow log analysis**. For more details, refer to [Slow log analysis](https://www.volcengine.com/docs/6956/155352).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d2786d31f2ac5060775d6f826ee15a0.png) </span>


3. Process SQL: After locating the SQL, it can be processed by [SQL throttling](https://www.volcengine.com/docs/6313/1411540#sql-%E9%99%90%E6%B5%81) or [killing the session](https://www.volcengine.com/docs/6313/1411540#kill-%E4%BC%9A%E8%AF%9D).


<span id="_2-临时表"></span>
#### 2. Temporary tables

**Cause analysis**

MySQL may use temporary tables when processing SQL. The size of in\-memory temporary tables is limited by the tmp_table_size and max_heap_table_size parameters. When the limit is exceeded, they are converted to on\-disk temporary tables. If a large number of connections create many temporary tables at once, it may cause a sudden increase in memory usage. MySQL 8.0 implements a new temptable engine. The total size of in\-memory temporary tables allocated by all threads must be less than the `temptable_max_ram` parameter, which defaults to 1 GB. If this limit is exceeded, the tables are converted to on\-disk temporary tables.

**Solution**


1. Reduce `tmp_table_size` and `max_heap_table_size` (MySQL 5.7) or `temptable_max_ram` (MySQL 8.0).

2. Locate SQL: execute `show processlist` or use [Slow log analysis](https://www.volcengine.com/docs/6956/155352) in Database Workshop, and then use `explain` to check whether temporary tables are used.

3. Process SQL: after locating the SQL, it can be processed by [SQL throttling](https://www.volcengine.com/docs/6313/1411540#sql-%E9%99%90%E6%B5%81) or [killing the session](https://www.volcengine.com/docs/6313/1411540#kill-%E4%BC%9A%E8%AF%9D).


<span id="_3-多语句-multiple-statements"></span>
#### 3. Multiple statements

**Cause analysis**

MySQL allows multiple SQL statements, separated by semicolons (;), to be sent in a single request. MySQL processes these statements sequentially, but some memory is not freed until all statements have been executed.

When sending multiple statements this way, if a very large batch of SQL is sent at once (e.g., hundreds of megabytes), the cumulative memory consumed by various object allocations during execution can be substantial, potentially causing the MySQL process to run out of memory. In addition to multiple statements, bulk inserts (a single insert statement for batch\-inserting multiple records) and extremely long SQL statements generated by framework tools also allocate significant memory during the network protocol and SQL parser phases, and thus require close attention.

In typical scenarios, a large number of multiple statements or bulk inserts can cause a sudden surge in network traffic. You can determine if this is happening by monitoring network traffic.

Path: Log on to [Database Workshop](https://console.byteplus.com/dbw)\>**Observation diagnosis**\>**Performance monitoring**\>**The average number of bytes received from all clients per second**. For more details, refer to [View performance monitoring metrics](https://www.volcengine.com/docs/6956/1288461).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9023c041d6cffef6bfdeed7de945307d.png) </span>

**Solution**


1. Locate SQL: Run `show processlist` or use [Slow log analysis](https://www.volcengine.com/docs/6956/155352) in Database Workshop to check for suspicious SQL statements. The method is the same as described above.

2. Avoid sending SQL as multiple statements in your business implementation. Split statements to reduce the data volume of a single execution.

3. Reduce concurrency to avoid executing too many of the above statements concurrently.


<span id="_4-blob-text-字段"></span>
#### 4. **Blob/text fields**

**Cause analysis**

Querying or writing very large blob fields causes dynamic memory allocation. Some of this memory is not released until the table is closed, leading to increased memory usage.

**Solution**


1. Locate SQL: Execute `show processlist` or use [Slow log analysis](https://www.volcengine.com/docs/6956/155352) in the Database Workshop to find suspicious SQL. The method is the same as above.

2. Reduce concurrency to avoid executing too many of the above statements concurrently;

3. Execute `flush table table_name` during off\-peak hours to release the cache for the corresponding table.


<span id="_5-全文索引"></span>
#### 5. Full\-text index

**Cause analysis**

Full\-text indexing uses a large amount of memory to process index data, so it needs special attention.

**Solution**


1. Locate SQL: Check for suspicious SQL by executing `show processlist` or by using [Slow log analysis](https://www.volcengine.com/docs/6956/155352) in the Database Workshop. The method is the same as described above.

2. Execute `flush table table_name` during off\-peak hours to release the corresponding table's cache.


<span id="库表较多"></span>
### Large number of databases and tables

**Cause analysis**

In MySQL, each table has memory overhead. Besides the memory consumed by table objects in the InnoDB layer, the table cache in the server layer also consumes memory. A high number of tables in an instance or a high QPS can also increase memory usage.

**Solution**


1. Check if the table_open_cache parameter was recently increased.

   1. On the Instances page, click the instance name of the target instance to enter the Instances page.

   2. Click the **Parameter configuration** tab.

   3. View **MySQL parameter modification history**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3d0926875452461169193a0c925b7ed7.png) </span>

2. Confirm whether the number of databases and tables is continuously increasing. If so, upgrade the instance specification.


<span id="存储过程"></span>
### Stored procedure

**Cause analysis**

Calls to stored procedures, functions, triggers, or events consume additional memory and require special attention.

Use Database Workshop to view stored procedures and other objects created by the service. Log on to [Database Workshop](https://console.byteplus.com/dbw) to view the instance's usage of stored procedures.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fdaab3e230e5bc20afe5877c0ad9e56f.png) </span>


1. If performance_schema is enabled, use the following SQL statement to view the memory usage of stored procedures


```sql
select * from memory_summary_global_by_event_name where  EVENT_NAME like "%memory/sql/sp_head%"\G;
```


**Solution**

Log on to [Database Workshop](https://console.byteplus.com/dbw), check the number of triggers, stored procedures, functions, and events that the instance uses, and reduce their use.

<span id="performance-schema-导致的内存上升"></span>
### Increased memory usage caused by performance_schema

**Cause analysis**

Although performance_schema can monitor MySQL memory usage, its maintenance also incurs additional memory overhead. Therefore, enabling performance_schema or [loose_rds_performance_schema](https://www.volcengine.com/docs/6313/986036#%E5%90%8E%E7%BB%AD%E6%AD%A5%E9%AA%A4) may increase memory usage. Using this feature may put significant pressure on the instance, especially for instances with low specifications. Therefore, continuously monitor the instance's memory usage after enabling this feature.

Execute `SHOW ENGINE PERFORMANCE_SCHEMA STATUS` to obtain the memory consumed by performance_schema, and focus on performance_schema.memory in the output.

**Solution**


1. Close performance_schema or [loose_rds_performance_schema](https://www.volcengine.com/docs/6313/986036#%E5%90%8E%E7%BB%AD%E6%AD%A5%E9%AA%A4).

2. RDS for MySQL provides the modifiable parameter `performance_schema_max_thread_instances`, which sets the maximum number of observation threads (the maximum number of rows in the `performance_schema.threads` table) to control memory consumption by the `performance_schema` feature. The default value of this parameter is `1024` and can be adjusted based on the instance specification and business needs. For more information about modifying parameters, see [Modifying parameters](https://www.volcengine.com/docs/6313/75395).


<span id="提升实例规格"></span>
### Upgrade instance specification

If memory usage continues to increase after troubleshooting, it may be a normal result of business pressure. Consider upgrading the instance specification through regular modification of specification or temporary upgrade to increase memory.

For more information about modifying the instance specification, refer to [Modify configuration](https://www.volcengine.com/docs/6313/775063).

<span id="常用操作"></span>
## Common actions

<span id="sql-限流"></span>
### SQL throttling

After locating the problem SQL, you can limit its execution frequency by using SQL throttling.

**Procedure**


1. Log on to [Database Workshop](https://console.byteplus.com/dbw)\>**Observation diagnosis**\>**Session management**\>**SQL throttling**\>**Enable the SQL throttling feature**\>**Create a task**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b8f49aa63f890804c101340998585099.png) </span>

2. In the Create SQL throttling task window, enter the problem SQL and adjust the maximum concurrency (a value of 0 will completely block the SQL). Click **Generate and validate keywords** to split the keywords. The keywords are separated by a tilde (~).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb8b88675ee840d9ea89a9e1d1ed03e6.png) </span>


3. Click **OK** to submit the task.

> **Note**: For more information, refer to [SQL throttling management](https://www.volcengine.com/docs/6956/1110640).


<span id="kill-会话"></span>
### Kill session

**Procedure**


1. Log on to [Database Workshop](https://console.byteplus.com/dbw)\>**Observation diagnosis**\>**Session management**.

2. In the **Real\-time sessions** area, check the **Time** and **State** of the sessions.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0aa08ce82071aa488ca1fb16179ab269.png) </span>
