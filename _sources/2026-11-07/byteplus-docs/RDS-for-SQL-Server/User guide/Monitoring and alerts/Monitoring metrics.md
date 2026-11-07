---
title: "Monitoring metrics"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/monitoring-metrics"
---

This article introduces the metrics and related instructions for monitoring and alerting support for RDS for SQL Server.

<span id="monitoring-indicator-description"></span>
## Monitoring indicator description

You can call the [GetMetricData ](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData)interface to query the monitoring metric data of the RDS for SQL Server instance. When calling this interface to query, you need to obtain relevant information about the following monitoring metrics:


* **Namespace** : The product space to which the monitoring indicator to be queried belongs. The product space name for RDS for SQL Server is `VCM_RDS_SQLServer`.

* **SubNamespace** : The dimension to which the metric to be queried belongs. RDS for SQL Server instances support monitoring metrics for the `engine` dimension (base dimension).

* **MetricName** : The name of the monitoring indicator to be queried. The MetricName corresponding to each monitoring indicator of the RDS for SQL Server instance is shown in the following table. For more details, please refer to the [cloud monitoring indicator query](https://console.volcengine.com/cloud_monitor/docs?namespace=VCM_RDS_SQLServer).


<span id="monitoring-indicator-table"></span>
## **Monitoring indicator table**

A detailed description of the various monitoring metrics in a SQL Server instance can be found in the following table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cloud monitoring acquires data every 30 seconds by default, and displays the collected data after obtaining the average or maximum value according to the display granularity of the query results. For example, when querying QPS data from proxy nodes in the past 3 hours, the cloud monitoring query results are displayed with a granularity of 2 minutes, that is, the data displayed each time is actually the average of the past 4 query results. To view monitoring data, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-monitoring-information">View monitoring data</a>.</div>


<span id="resource-monitoring"></span>
## **resource monitoring**


|**indicator name** |**MetricName** |**unit** |**indicator description** |
|---|---|---|---|
|CPU usage |CpuUtil |% |CPU usage. |
|memory usage |MemUtil |% |Memory usage. |
|disk usage |DiskUtil |% |Disk usage space/instance purchase space. |
|total disk size |DiskTotalSize |GiB |This metric is used to count the total disk size of the measurement object. |
|disk usage |DiskUsedSize |GiB |This metric is used to measure the disk usage size of the measurement object. |
|disk average queue length |AvgDiskQueueLength |Count/s |This metric is used to count the number of processes waiting to write to the measured object. |
|IOPS |IOPS |Count/s |The number of I/O requests processed per second. |
|network input traffic |NetworkReceiveThroughput |B/s |The number of bytes received per second. |
|network output traffic |NetworkTransmitThroughput |B/s |The number of bytes sent per second. |


<span id="engine-monitoring"></span>
## **Engine monitoring**


|indicator name |MetricName |<div style="text-align: center"><br>unit</div><br> |indicator description |
|---|---|---|---|
|Number of database connections in use |ConnectionsInUse |<div style="text-align: center"><br>Count</div><br> |The number of connections a user has to the database. |
|average transactions per second |TPS |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the number of transactions initiated per second by the database. |
|Average batches per second |QPS |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the number of Transact\-SQL command batches received per second. |
|logins per second |Logins |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the total number of logins launched per second. |
|cache hit rate |CacheHitRatio |<div style="text-align: center"><br>%</div><br> |This metric is used to count the percentage of pages found in the buffer cache that do not need to be read from disk. |
|full table scans per second |FullScans |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the number of unrestricted full scans per second. |
|user errors per second |Errors |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the number of user errors per second. |
|latch waits per second |LatchWaits |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the number of latch requests per second that were not granted immediately. |
|lock waits per second |LockWaits |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the number of lock requests per second that the caller is required to wait for. |
|lock requests per second |LockRequests |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the number of new locks and lock conversions requested by the lock manager per second. |
|lock timeouts per second |LockTimeouts |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the number of lock requests that time out per second. |
|deadlocks per second |DeadLocks |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the number of lock requests per second that cause deadlocks. |
|Pages Written Per Second |CheckpointPages |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the number of pages flushed to disk per second by a checkpoint or other operation that flushes all dirty pages. |
|Average SQL compilations per second |SqlCompilations |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the number of SQL compilations per second. |
|Average SQL recompilations per second |SqlRecompilations |<div style="text-align: center"><br>Count/s</div><br> |This metric is used to count the number of statements recompiled per second. |
|Difference number of primary and secondary node objects |InstanceObjectDifference |<div style="text-align: center"><br>Count</div><br> |The number of object differences between primary and secondary nodes. |
