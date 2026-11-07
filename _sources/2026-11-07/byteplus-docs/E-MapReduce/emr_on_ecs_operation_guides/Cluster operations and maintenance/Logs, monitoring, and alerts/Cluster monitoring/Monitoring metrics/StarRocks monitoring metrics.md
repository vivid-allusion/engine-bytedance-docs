---
title: "StarRocks monitoring metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_StarRocks_monitoring_metrics"
---

This article provides detailed information about StarRocks metrics.

StarRocks metrics include the following sections:


* [StarRocks overview](https://docs.byteplus.com/docs/E-MapReduce/105469#starrocks-%E6%A6%82%E8%A7%88)

* [StarRocks-FE](https://docs.byteplus.com/docs/E-MapReduce/105469#starrocks-fe)

* [StarRocks-BE](https://docs.byteplus.com/docs/E-MapReduce/105469#starrocks-be)

* [StarRocks-CN](https://docs.byteplus.com/docs/E-MapReduce/105469#starrocks-cn)


<span id="starrocks-概览"></span>
## **StarRocks overview**


|Category |**Metric description** |**Unit** |
|---|---|---|
|Health status |Number of FE nodes |Unit |
||Number of live FE nodes |count |
||Number of failed FE nodes |count |
||Number of BE nodes |count |
||Number of live BE nodes |count |
||Number of failed BE nodes |count |
||Number of CN nodes |count |
||Number of live CN nodes |count |
||Number of failed CN nodes |count |
||Number of brokers |count |
|Capacity information |BE storage capacity |GiB |
||Average maximum heap memory of FE nodes |GiB |
|Request load |QPS |count/s |
||RPS |count/s |
|Query status |Total number of queries |count |
||Number of slow queries |count |
||Query response time |s |
|FE connection status |Average number of connections |count |
||Maximum number of connections |count |
||Total number of connections |count |
|FE heap memory usage |Average utilization of FE JVM heap memory |% |
||Maximum utilization of FE JVM heap memory |% |
|FE EditLog |FE Edit Log average read rate |count/s |
||FE Edit Log maximum read rate |times/s |
||FE Edit Log average write rate |count/s |
||FE Edit Log maximum write rate |count/s |
|Number of FE job submissions |Number of Insert jobs submitted by FE |count |
||Number of Broker jobs submitted by FE |count |
||Number of StreamLoad jobs submitted by FE |count |
||Number of SchemaChange jobs submitted by FE |count |
|Tablet |Total number of BE tablets |count |
||Total number of scheduled tablets |count |
||BE tablet creation failure rate |count/s |
||BE tablet creation request rate |count/s |
|Number of tables and databases |Number of tables |count |
||Number of databases |count |
|Disk read/write |BE average disk read rate |B/s |
||BE maximum disk read rate |B/s |
||BE average disk write rate |B/s |
||BE maximum disk write rate |B/s |
|Merge requests |Baseline merge failure rate of BE |count/s |
||Incremental merge failure rate of BE |count/s |
||Baseline merge request rate of BE |count/s |
||Incremental merge request rate of BE |count/s |
|Clone status |BE clone failure rate |count/s |
||BE clone request rate |count/s |
|Version publishing |BE version publishing failure rate |count/s |
||BE version publishing request rate |count/s |
|Table structure modification |Request rate for BE table structure modification |count/s |
||Failure rate for BE table structure modification |count/s |
|Fragment requests |Average response time of BE fragment requests |ms |
||Maximum response time of BE fragment requests |ms |
||Average fragment RPS of BE |count/s |
||Maximum fragment RPS of BE |count/s |
|Plan tasks |Current average number of BE plan tasks |count |
||Current maximum number of BE plan tasks |count |
|HTTP requests |Average HTTP RPS of BE |count/s |
||Maximum HTTP RPS of BE |count/s |
|StreamLoad |StreamLoad import byte rate of BE |B/s |
||StreamLoad row import rate of BE |count/s |
|File handles |Maximum number of file handles used by BE process |count |
||Average number of used file handles for BE process |count |
|Disk IO |Average disk IO latency for BE |ms |
||Maximum disk IO latency for BE |ms |
|Network transmission |Average network send rate for BE |KiB/s |
||Maximum network send rate for BE |KiB/s |
||Average network receive rate for BE |KiB/s |
||Maximum network receive rate for BE |KiB/s |


<span id="starrocks-fe"></span>
## **StarRocks\-FE**


|**Metric description** |**Unit** |
|---|---|
|FE Edit Log read rate |count/s |
|FE Edit Log write rate |count/s |
|FE Edit Log size |Bytes |
|Number of BE Tablets |count |
|Number of scheduled Tablets |count |
|FE JVM Heap memory utilization |% |


<span id="starrocks-be"></span>
## **StarRocks\-BE**


|**Metric description** |**Unit** |
|---|---|
|BE baseline merge rate |B/s |
|BE incremental merge rate |B/s |
|BE primary key table incremental merge rate |B/s |
|BE baseline merge rowsets merge rate |count/s |
|BE incremental merge rowsets merge rate |count/s |
|BE primary key table incremental merge rowsets merge rate |count/s |
|BE Fragment request response time |ms |
|Current number of Plan tasks for BE |count |
|BE Fragment RPS |count/s |
|BE HTTP RPS |count/s |
|BE node CCPU utilization |% |
|BE process disk utilization |% |
|BE process disk read/write speed |KiB/s |
|BE process disk I/O latency |ms |
|BE process network read/write speed |KiB/s |
|Total number of used file handles for BE |count |


<span id="starrocks-cn"></span>
## **StarRocks\-CN**


|Category |Metric name |Unit |
|---|---|---|
|Process metrics |CN process CPU utilization |% |
||Total number of used file handles for CN |count |
||CN process network read/write speed |KB/s |
|File system read/write metrics |StarRocks CN Fslib average read request latency |ms |
||StarRocks CN Fslib total bytes read |KB |
||StarRocks CN Fslib average data per read request |KB |
||StarRocks CN Fslib read throughput |KB/s |
||StarRocks CN Fslib read frequency |count/s |
||StarRocks CN Fslib average write request latency |ms |
||StarRocks CN Fslib total bytes written |KB |
||StarRocks CN Fslib average data per write request |KB |
||StarRocks CN Fslib write throughput |KB/s |
||StarRocks CN Fslib write frequency |count/s |
||StarRocks CN Fslib S3 single upload frequency |count/s |
||StarRocks CN Fslib S3 multi upload frequency |count/s |
||StarRocks CN Fslib cache eviction count |count |
||StarRocks CN Fslib cache hit frequency |count/s |
||StarRocks CN Fslib cache miss frequency |count/s |
||StarRocks CN Fslib cache miss count |count |
||StarRocks CN Fslib cache hit rate |% |
||StarRocks CN Fslib number of active FS instances |count |
||StarRocks CN Fslib number of open files |count |
||StarRocks CN Fslib List operation frequency |count/s |
||StarRocks CN Fslib Exist operation frequency |count/s |
||StarRocks CN Fslib Stat operation frequency |count/s |
||StarRocks CN Fslib number of async caches |count |
||StarRocks CN Fslib number of created files |count |
|Metrics for storage\-compute separation tables |StarRocks CN Lake transaction log deletion latency |ms |
||StarRocks CN Lake transaction log deletion QPS |count/s |
||StarRocks CN Lake delVector cache hits in the past minute |count |
||StarRocks CN Lake number of TabletMeta retrievals |count |
||StarRocks CN Lake TabletMeta retrieval latency |ms |
||StarRocks CN Lake TabletMeta retrieval QPS |count/s |
||StarRocks CN Lake number of transaction log retrievals |count |
||StarRocks CN Lake transaction log retrieval latency |ms |
||StarRocks CN Lake transaction log retrieval QPS |count/s |
||StarRocks CN Lake Load primary key index count |count |
||StarRocks CN Lake Load primary key index latency |ms |
||StarRocks CN Lake Load primary key index QPS |count/s |
||StarRocks CN Lake Publish Tablet Version count |count |
||StarRocks CN Lake Publish Tablet Version latency |ms |
||StarRocks CN Lake Publish Tablet Version Qps |count/s |
||StarRocks CN Lake Put Tablet Metadata count |count |
||StarRocks CN Lake Put Tablet Metadata latency |ms |
||StarRocks CN Lake Put Tablet Metadata Qps |count/s |
||StarRocks CN Lake Put Txn Log count |count |
||StarRocks CN Lake Put Txn Log latency |ms |
||StarRocks CN Lake Put Txn Log Qps |count/s |
||StarRocks CN Lake Vacuum Delete Txn Log count |count |
||StarRocks CN Lake Vacuum Delete Txn Log latency |ms |
||StarRocks CN Lake Vacuum Delete Txn Log Qps |count/s |
||StarRocks CN Lake Vacuum number of active tasks |count |
||StarRocks CN Lake Vacuum number of deleted files |count |
||StarRocks CN Lake Vacuum Delete File failure count |count |
||StarRocks CN Lake Vacuum Delete File latency |ms |
||StarRocks CN Lake Vacuum Delete File queued task count |count |
||StarRocks CN Lake Publish Version active task count |count |
||StarRocks CN Lake Publish Version failed task count |count |
||StarRocks CN Lake Publish Version queued task count |count |
