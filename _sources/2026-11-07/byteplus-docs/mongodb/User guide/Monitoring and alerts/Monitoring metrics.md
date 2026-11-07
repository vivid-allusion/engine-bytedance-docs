---
title: "Monitoring metrics"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/monitoring-metric"
---

Document Database for MongoDB supports two instance architectures: replica set and sharding cluster. Different instance architectures support different monitoring metrics. You can learn the running status and usage of instances based on monitoring metrics.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Cloud Service Monitor acquires data once every 30s by default, and aggregates the acquired data in different intervals and modes based on the time range for querying monitoring data. For more information, refer to [Viewing data in Cloud Service Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor#.5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u).

* You can view monitoring data for up to the last 15 days. For more information about how to view monitoring data, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/mongodb/view-monitoring-data).

* The units adopted in the monitoring metrics table are all base units. You can find details of the exact units used for each monitoring item on the console. The units displayed on the console will be adjusted based on the monitoring values and applying certain conversion criteria.

   
   |Unit type |Specific units included |Conversion standards |
   |---|---|---|
   |Capacity\-related units |* B<br><br>* B/s |According to the SI standard, 1,000 is used as the prefix for unit conversion. During conversion, prefixes such as K (Kilo, which means 1,000), M (Mega, which means 1,000,000), G (Giga, which means 1,000,000,000), will be added before the base unit.<br><br>For example, the base unit of **Total used disk space** is B (Byte). If the monitoring value of **Total used disk space** is large, the unit on the console may be adjusted to KB, MB, GB, and so on. |
   |Quantity\-related units |* Count<br><br>* Count/s |According to the SI standard, 1,000 is used as the prefix for unit conversion. During conversion, prefixes such as K (Kilo, which means 1,000), M (Mega, which means 1,000,000), G (Giga, which means 1,000,000,000) and so on, will be added before the base unit.<br><br>For example, the base unit of **Processed requests** is Count/s. If the monitoring value of **Processed requests** is large, the unit on the console may be adjusted to KCount/s, MCount/s, GCount/s, etc. |
   |Time\-related units |s |Conversion is carried out according to the international system of units, such as microseconds (µs), milliseconds (ms), seconds (s), minutes (min), hours (h), etc. |
   |Other units |% |Unit conversion is not involved. |
   

* Some monitoring indicators can only be viewed after upgrading to the specified instance version. For details, please refer to the following table.

   
   |Metric Name |Requirements that the instance must meet to view the current metrics |
   |---|---|
   |* Current active connections<br><br>* Total number of new connections per second<br><br>* Number of connections currently available<br><br>* The average execution time of all requests<br><br>* Number of requests with execution time less than or equal to 8 milliseconds<br><br>* Number of requests with execution time greater than 8 milliseconds and less than or equal to 24 milliseconds<br><br>* Number of requests that took longer than 24 milliseconds to execute |* Instances created after June 10, 2025, support viewing left\-side metrics by default.<br><br>* For instances created before June 10, 2025, if you need to view the left\-side metrics, [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/) to contact technical support to upgrade the instance version.<br><br><br> |
   |Number of write conflicts<br><br> |* Instances created after December 04, 2025, support viewing the left\-side metrics by default.<br><br>* For instances created before December 04, 2025, if you need to view the left\-side metrics, [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/) to contact technical support to upgrade the instance version. |
   


<span id=".55uR5o6n5oyH5qCH6KGo"></span>
## Monitoring metrics table

Document Database for MongoDB supports two instance architectures: replica set and sharding cluster. Different instance architectures support different monitoring metrics.

<span id=".5YiG54mH6ZuG576k5a6e5L6L"></span>
### Sharding cluster instance

In the monitoring metrics of a Document Database for MongoDB sharding cluster instance, in addition to displaying the relevant monitoring metrics of the nodes of each component (including Mongos, ConfigServers, Shards), the relevant metrics at the overall instance (Instance) level will also be displayed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call <a href="https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData">GetMetricData</a> interface to query the data of various monitoring metrics of the MongoDB sharding cluster instance. When calling this interface for querying, you need to obtain the relevant information of the following monitoring metrics:</div>



* <div data-tips="true" data-tips-type="tip"><code>Namespace</code>: The product space to which the monitoring metric to be queried belongs.</div>


   <div data-tips="true" data-tips-type="tip">The name of the product space of the MongoDB sharding cluster instance is <code>VCM_MongoDB_Sharded_Cluster</code>.   </div>
   

* <div data-tips="true" data-tips-type="tip"><code>SubNamespace</code>: The dimension to which the metric to be queried belongs.</div>


   <div data-tips="true" data-tips-type="tip">MongoDB sharding cluster instance supports viewing monitoring metrics in 4 dimensions: <code>mongos</code>, <code>config</code>, <code>shard</code>, and <code>instance</code>.   </div>
   

* <div data-tips="true" data-tips-type="tip"><code>MetricName</code>: The name of the monitoring metric to be queried.</div>


   <div data-tips="true" data-tips-type="tip">For details of the <code>MetricName</code> corresponding to each monitoring metric of MongoDB sharding cluster instance, refer to <a href="https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_MongoDB_Sharded_Cluster">Query of monitoring metrics of Document Database for MongoDB sharding cluster instance</a>.   </div>
   



<Tabs>
<Tab zoneid="JN5JnUMnII" title="Mongos">
<TabTitle>Mongos</TabTitle>


|Metric Name |MetricName (for API use) |Unit |Description |
|---|---|---|---|
|Network input rate |NetworkReceiveThroughput |B/s |Average traffic input from all network adapters on a node per second. |
|Network output rate |NetworkTransmitThroughput |B/s |Average traffic output from all network adapters on a node per second. |
|CPU usage |CpuUtil |% |CPU utilization of a node. |
|Memory usage |MemUtil |% |Memory usage of a node. |
|Processed requests |NetworkRequestPerSec |Count/s |Average number of operations processed per second by all network adapters on a node. |
|Current connections |CurrConn |Count |Number of connections from the client to the current node. |
|COMMAND operations per second |CommandOperationPerSec |Count/s |Average number of times the COMMAND statement is executed per second on a node. |
|DELETE operations per second |DeleteOperationPerSec |Count/s |Average number of times the DELETE statement is executed per second on a node. |
|GETMORE operations per second |GetmoreOperationPerSec |Count/s |Average number of times the GETMORE statement is executed per second on a node. |
|INSERT operations per second |InsertOperationPerSec |Count/s |Average number of times the INSERT statement is executed per second on a node. |
|QUERY operations per second |QueryOperationPerSec |Count/s |Average number of times the QUERY statement is executed per second on a node. |
|UPDATE operations per second |UpdateOperationPerSec |Count/s |Average number of times the UPDATE statement is executed per second on a node. |
|Current connection usage |CurrConnRate |% |The ratio of the current number of connections to the total number of connections supported by the current node (i.e., the value of the `net.maxIncomingConnections` parameter). |
|Current active connections |ActiveConnections |Count |The number of active client connections on the current node. |
|Total number of new connections per second |CreateConnectionPerSec |Count/s |The total number of new connections created per second on the current node. |
|Number of connections currently available |AvailConnections |Count |The number of available connections remaining on the current node. |





</Tab>
<Tab zoneid="LqKIukf7dt" title="Config Servers">
<TabTitle>Config Servers</TabTitle>


|Metric Name |MetricName (for API use) |Unit |Description |
|---|---|---|---|
|Network input rate |NetworkReceiveThroughput |B/s |Average traffic input from all network adapters on a node per second. |
|Network output rate |NetworkTransmitThroughput |B/s |Average traffic output from all network adapters on a node per second. |
|CPU usage |CpuUtil |% |CPU utilization of a node. |
|Memory usage |MemUtil |% |Memory usage of a node. |
|Processed requests |NetworkRequestPerSec |Count/s |Average number of operations processed per second by all network adapters on a node. |
|Current connections |CurrConn |Count |Number of connections from the client to the current node. |
|COMMAND operations per second |CommandOperationPerSec |Count/s |Average number of times the COMMAND statement is executed per second on a node. |
|DELETE operations per second |DeleteOperationPerSec |Count/s |Average number of times the DELETE statement is executed per second on a node. |
|GETMORE operations per second |GetmoreOperationPerSec |Count/s |Average number of times the GETMORE statement is executed per second on a node. |
|INSERT operations per second |InsertOperationPerSec |Count/s |Average number of times the INSERT statement is executed per second on a node. |
|QUERY operations per second |QueryOperationPerSec |Count/s |Average number of times the QUERY statement is executed per second on a node. |
|UPDATE operations per second |UpdateOperationPerSec |Count/s |Average number of times the UPDATE statement is executed per second on a node. |
|Total disk usage |TotalDiskUtil |% |Ratio of the total used space of an instance to the maximum available space. |
|Total used disk space |TotalDiskUsage |B |Overall usage space of the log disk and data disk on a node. |
|Total used log disk space |LogDiskUsage |B |Usage space of the log disk on a node. |
|Total used data disk space |DataDiskUsage |B |Usage space of the data disk on a node. |
|Remaining concurrent write requests that can be handled |AvailConcurrentWriteRequest |Count |Number of remaining available concurrent write transaction requests on a node. |
|Current concurrent write requests |RunningConcurrentWriteRequest |Count |Number of ongoing concurrent write transaction requests on a node. |
|Remaining concurrent read requests that can be handled |AvailConcurrentReadRequest |Count |Number of remaining available concurrent read transaction requests on a node. |
|Current concurrent read requests |RunningConcurrentReadRequest |Count |Number of ongoing concurrent read transaction requests on a node. |
|Data read by the cache per second |ReadIntoCachePerSec |B/s |Average amount of data read into the cache per second on a node. |
|Data written to the disk from the cache per second |WrittenFromCachePerSec |B/s |Average amount of data flushed from the cache to the disk per second on a node. |
|Maximum available disk space |MaxDiskConfigured |B |Storage space specification purchased on the current node. |
|Operations queued waiting for global locks |GlobalWaitTotalLockQueue |Count |Length of the waiting queue for all global locks on a node (that is, number of operations waiting for all global locks). |
|Operations queued waiting for global read locks |GlobalWaitReadLockQueue |Count |Length of the waiting queue for global read locks on a node (that is, number of operations waiting for global read locks). |
|Operations queued waiting for global write locks |GlobalWaitWriteLockQueue |Count |Length of the waiting queue for global write locks on a node (that is, number of operations waiting for global write locks). |
|Timed out cursors |TimeOutCursor |Count |Number of cursors with service timeout on a node. |
|Open cursors |TotalOpenCursor |Count |Number of open cursors on a node. |
|Primary\-secondary delay |ReplicationDelay |s |Data synchronization delay duration between the primary and secondary nodes for an instance. |
|Slow queries |SlowOpCount |Count/s |Number of slow queries within the selected query duration on a node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">All queries recorded in slow logs are counted in <strong>Slow queries</strong>. For more information about how to query slow logs, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/query-slow-log">Querying slow logs</a>.</div><br> |
|Oplog available time |OplogAvailTime |s |The available time of the Oplog of the node. |
|Current connection usage |CurrConnRate |% |The ratio of the current number of connections to the total number of connections supported by the current node (i.e., the value of the `net.maxIncomingConnections` parameter). |
|Percentage of dirty data in cache |CacheDirty |% |The ratio of the storage space occupied by dirty data in the cache to the maximum available storage space configured for the current node. |
|Cache usage percentage |CacheUsed |% |The ratio of the storage space occupied by the cache to the maximum available storage space configured for the current node. |
|Cache hit rate |CacheHitRatio |% |The ratio of the amount of data requested and hit from the cache by the current node to the total amount of data requested from the cache. |
|Current active connections |ActiveConnections |Count |The number of active client connections on the current node. |
|Total number of new connections per second |CreateConnectionPerSec |Count/s |The total number of new connections created per second on the current node. |
|Number of connections currently available |AvailConnections |Count |The number of available connections remaining on the current node. |
|The average execution time of all requests |AvgRequestDelay |µs |The average delay in the execution of all requests on the current node. |
|Number of requests with execution time less than or equal to 8 milliseconds |ExecutionTime0msTo8ms |Count |Number of requests with execution time not exceeding 8 milliseconds on the current node. |
|Number of requests with execution time greater than 8 milliseconds and less than or equal to 24 milliseconds |ExecutionTime8msTo24ms |Count |Number of requests with execution time exceeding 8 milliseconds but not exceeding 24 milliseconds on the current node. |
|Number of requests that took longer than 24 milliseconds to execute |ExecutionTimeBeyond24ms |Count |Number of requests with execution time exceeding 24 milliseconds on the current node. |
|Average transaction response time |TransactionAvgRequestDelay |µs |The average response time of transactions on the current node. |
|Average command response time |CommandAvgRequestDelay |µs |The average response time of commands on the current node. |
|Number of write conflicts |WriteConflictsCount |Count |The number of conflicts encountered by the current node during the write operation. |
|Maximum cache size |MaxCacheConfigured |B |Maximum available disk size configured for a node. |





</Tab>
<Tab zoneid="YlQBEJOtl1" title="Shards">
<TabTitle>Shards</TabTitle>


|Metric Name |MetricName (for API use) |Unit |Description |
|---|---|---|---|
|Network input rate |NetworkReceiveThroughput |B/s |Average traffic input from all network adapters on a node per second. |
|Network output rate |NetworkTransmitThroughput |B/s |Average traffic output from all network adapters on a node per second. |
|CPU usage |CpuUtil |% |CPU utilization of a node. |
|Memory usage |MemUtil |% |Memory usage of a node. |
|Processed requests |NetworkRequestPerSec |Count/s |Average number of operations processed per second by all network adapters on a node. |
|Current connections |CurrConn |Count |Number of connections from the client to the current node. |
|COMMAND operations per second |CommandOperationPerSec |Count/s |Average number of times the COMMAND statement is executed per second on a node. |
|DELETE operations per second |DeleteOperationPerSec |Count/s |Average number of times the DELETE statement is executed per second on a node. |
|GETMORE operations per second |GetmoreOperationPerSec |Count/s |Average number of times the GETMORE statement is executed per second on a node. |
|INSERT operations per second |InsertOperationPerSec |Count/s |Average number of times the INSERT statement is executed per second on a node. |
|QUERY operations per second |QueryOperationPerSec |Count/s |Average number of times the QUERY statement is executed per second on a node. |
|UPDATE operations per second |UpdateOperationPerSec |Count/s |Average number of times the UPDATE statement is executed per second on a node. |
|Total disk usage |TotalDiskUtil |% |Ratio of the total used space of an instance to the maximum available space. |
|Total used disk space |TotalDiskUsage |B |Overall usage space of the log disk and data disk on a node. |
|Total used log disk space |LogDiskUsage |B |Usage space of the log disk on a node. |
|Total used data disk space |DataDiskUsage |B |Usage space of the data disk on a node. |
|Remaining concurrent write requests that can be handled |AvailConcurrentWriteRequest |Count |Number of remaining available concurrent write transaction requests on a node.。 |
|Current concurrent write requests |RunningConcurrentWriteRequest |Count |Number of ongoing concurrent write transaction requests on a node. |
|Remaining concurrent read requests that can be handled |AvailConcurrentReadRequest |Count |Number of remaining available concurrent read transaction requests on a node. |
|Current concurrent read requests |RunningConcurrentReadRequest |Count |Number of ongoing concurrent read transaction requests on a node. |
|Data read by the cache per second |ReadIntoCachePerSec |B/s |Average amount of data read into the cache per second on a node. |
|Data written to the disk from the cache per second |WrittenFromCachePerSec |B/s |Average amount of data flushed from the cache to the disk per second on a node. |
|Maximum available disk space |MaxDiskConfigured |B |Storage space specification purchased on the current node. |
|Operations queued waiting for global locks |GlobalWaitTotalLockQueue |Count |Length of the waiting queue for all global locks on a node (that is, number of operations waiting for all global locks). |
|Operations queued waiting for global read locks |GlobalWaitReadLockQueue |Count |Length of the waiting queue for global read locks on a node (that is, number of operations waiting for global read locks). |
|Operations queued waiting for global write locks |GlobalWaitWriteLockQueue |Count |Length of the waiting queue for global write locks on a node (that is, number of operations waiting for global write locks). |
|Timed out cursors |TimeOutCursor |Count |Number of cursors with service timeout on a node. |
|Open cursors |TotalOpenCursor |Count |Number of open cursors on a node. |
|Primary\-secondary delay |ReplicationDelay |µs |Data synchronization delay duration between the primary and secondary nodes for an instance. |
|Slow queries |SlowOpCount |Count/s |Number of slow queries within the selected query duration on a node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">All queries recorded in slow logs are counted in <strong>Slow queries</strong>. For more information about how to query slow logs, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/query-slow-log">Querying slow logs</a>.</div><br> |
|Oplog available time |OplogAvailTime |s |The available time of the Oplog of the node. |
|Current connection usage |CurrConnRate |% |The ratio of the current number of connections to the total number of connections supported by the current node (i.e., the value of the `net.maxIncomingConnections` parameter). |
|Percentage of dirty data in cache |CacheDirty |% |The ratio of the storage space occupied by dirty data in the cache to the maximum available storage space configured for the current node. |
|Cache usage percentage |CacheUsed |% |The ratio of the storage space occupied by the cache to the maximum available storage space configured for the current node. |
|Cache hit rate |CacheHitRatio |% |The ratio of the amount of data requested and hit from the cache by the current node to the total amount of data requested from the cache. |
|Current active connections |ActiveConnections |Count |The number of active client connections on the current node. |
|Total number of new connections per second |CreateConnectionPerSec |Count/s |The total number of new connections created per second on the current node. |
|Number of connections currently available |AvailConnections |Count |The number of available connections remaining on the current node. |
|The average execution time of all requests |AvgRequestDelay |µs |The average delay in the execution of all requests on the current node. |
|Number of requests with execution time less than or equal to 8 milliseconds |ExecutionTime0msTo8ms |Count |Number of requests with execution time not exceeding 8 milliseconds on the current node. |
|Number of requests with execution time greater than 8 milliseconds and less than or equal to 24 milliseconds |ExecutionTime8msTo24ms |Count |Number of requests with execution time exceeding 8 milliseconds but not exceeding 24 milliseconds on the current node. |
|Number of requests that took longer than 24 milliseconds to execute |ExecutionTimeBeyond24ms |Count |Number of requests with execution time exceeding 24 milliseconds on the current node. |
|Average transaction response time |TransactionAvgRequestDelay |µs |The average response time of transactions on the current node. |
|Average command response time |CommandAvgRequestDelay |µs |The average response time of commands on the current node. |
|Number of write conflicts |WriteConflictsCount |Count |The number of conflicts encountered by the current node during the write operation. |
|Maximum cache size |MaxCacheConfigured |B |Maximum available disk size configured for a node. |





</Tab>
<Tab zoneid="yAc0q6QSmY" title="Instance">
<TabTitle>Instance</TabTitle>


|Metric Name |MetricName (for API use) |Unit |Description |
|---|---|---|---|
|CPU usage |AggregatedCpuUtil |% |CPU utilization of the instance. |
|Memory usage |AggregatedMemUtil |% |Memory usage of the instance. |
|Total disk usage |AggregatedTotalDiskUtil |% |The ratio of the total used space of the instance to the maximum available space of the specification. |
|Chunks per shard |ChunkNumber |Count |The number of chunks in each shard of the instance. |





</Tab>
</Tabs>


<span id=".5Ymv5pys6ZuG5a6e5L6L"></span>
### Replica set instance

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call <a href="https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData">GetMetricData</a> interface to query the data of various monitoring metrics of the MongoDB replica set instances. When calling this interface for querying, you need to obtain the relevant information of the following monitoring metrics:</div>



* <div data-tips="true" data-tips-type="tip"><code>Namespace</code>: The product space to which the monitoring metric to be queried belongs.</div>


   <div data-tips="true" data-tips-type="tip">The name of the product space of the MongoDB replica set instance is <code>VCM_MongoDB_Replica</code>.   </div>
   

* <div data-tips="true" data-tips-type="tip"><code>SubNamespace</code>: The dimension to which the metric to be queried belongs.</div>


   <div data-tips="true" data-tips-type="tip">MongoDB replica set instance supports viewing monitoring metrics in 2 dimensions: <code>instance</code> and <code>replica</code>.   </div>
   

* <div data-tips="true" data-tips-type="tip"><code>MetricName</code>: The name of the monitoring metric to be queried.</div>


   <div data-tips="true" data-tips-type="tip">For details of the <code>MetricName</code> corresponding to each monitoring metric of MongoDB replica set instance, refer to <a href="https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_MongoDB_Replica">Query of monitoring metrics of Document Database for MongoDB replica set instance</a>.   </div>
   



|Metric Name |MetricName (for API use) |Unit |Description |
|---|---|---|---|
|Network input rate |NetworkReceiveThroughput |B/s |Average traffic input from all network adapters on a node per second. |
|Network output rate |NetworkTransmitThroughput |B/s |Average traffic output from all network adapters on a node per second. |
|CPU usage |CpuUtil |% |CPU utilization of a node. |
|Memory usage |MemUtil |% |Memory usage of a node. |
|Processed requests |NetworkRequestPerSec |Count/s |Average number of operations processed per second by all network adapters on a node. |
|Current connections |CurrConn |Count |Number of connections from the client to the current node. |
|COMMAND operations per second |CommandOperationPerSec |Count/s |Average number of times the COMMAND statement is executed per second on a node. |
|DELETE operations per second |DeleteOperationPerSec |Count/s |Average number of times the DELETE statement is executed per second on a node. |
|GETMORE operations per second |GetmoreOperationPerSec |Count/s |Average number of times the GETMORE statement is executed per second on a node. |
|INSERT operations per second |InsertOperationPerSec |Count/s |Average number of times the INSERT statement is executed per second on a node. |
|QUERY operations per second |QueryOperationPerSec |Count/s |Average number of times the QUERY statement is executed per second on a node. |
|UPDATE operations per second |UpdateOperationPerSec |Count/s |Average number of times the UPDATE statement is executed per second on a node. |
|Total disk usage |TotalDiskUtil |% |Ratio of the total used space of an instance to the maximum available space. |
|Total used disk space |TotalDiskUsage |B |Overall usage space of the log disk and data disk on a node. |
|Total used log disk space |LogDiskUsage |B |Usage space of the log disk on a node. |
|Total used data disk space |DataDiskUsage |B |Usage space of the data disk on a node. |
|Remaining concurrent write requests that can be handled |AvailConcurrentWriteRequest |Count |Number of remaining available concurrent write transaction requests on a node.。 |
|Current concurrent write requests |RunningConcurrentWriteRequest |Count |Number of ongoing concurrent write transaction requests on a node. |
|Remaining concurrent read requests that can be handled |AvailConcurrentReadRequest |Count |Number of remaining available concurrent read transaction requests on a node. |
|Current concurrent read requests |RunningConcurrentReadRequest |Count |Number of ongoing concurrent read transaction requests on a node. |
|Data read by the cache per second |ReadIntoCachePerSec |B/s |Average amount of data read into the cache per second on a node. |
|Data written to the disk from the cache per second |WrittenFromCachePerSec |B/s |Average amount of data flushed from the cache to the disk per second on a node. |
|Maximum available disk space |MaxDiskConfigured |B |Storage space specification purchased on the current node. |
|Operations queued waiting for global locks |GlobalWaitTotalLockQueue |Count |Length of the waiting queue for all global locks on a node (that is, number of operations waiting for all global locks). |
|Operations queued waiting for global read locks |GlobalWaitReadLockQueue |Count |Length of the waiting queue for global read locks on a node (that is, number of operations waiting for global read locks). |
|Operations queued waiting for global write locks |GlobalWaitWriteLockQueue |Count |Length of the waiting queue for global write locks on a node (that is, number of operations waiting for global write locks). |
|Timed out cursors |TimeOutCursor |Count |Number of cursors with service timeout on a node. |
|Open cursors |TotalOpenCursor |Count |Number of open cursors on a node. |
|Primary\-secondary delay |ReplicationDelay |µs |Data synchronization delay duration between the primary and secondary nodes for an instance. |
|Slow queries |SlowOpCount |Count/s |Number of slow queries within the selected query duration on a node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">All queries recorded in slow logs are counted in <strong>Slow queries</strong>. For more information about how to query slow logs, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/query-slow-log">Querying slow logs</a>.</div><br> |
|Oplog available time |OplogAvailTime |s |The available time of the Oplog of the node. |
|Current connection usage |CurrConnRate |% |The ratio of the current number of connections to the total number of connections supported by the current node (that is, the value of the `net.maxIncomingConnections` parameter). |
|Percentage of dirty data in cache |CacheDirty |% |The ratio of the storage space occupied by dirty data in the cache to the maximum available storage space configured for the current node. |
|Cache usage percentage |CacheUsed |% |The ratio of the storage space occupied by the cache to the maximum available storage space configured for the current node. |
|Cache hit rate |CacheHitRatio |% |The ratio of the amount of data requested and hit from the cache by the current node to the total amount of data requested from the cache. |
|Current active connections |ActiveConnections |Count |The number of active client connections on the current node. |
|Total number of new connections per second |CreateConnectionPerSec |Count/s |The total number of new connections created per second on the current node. |
|Number of connections currently available |AvailConnections |Count |The number of available connections remaining on the current node. |
|The average execution time of all requests |AvgRequestDelay |µs |The average delay in the execution of all requests on the current node. |
|Number of requests with execution time less than or equal to 8 milliseconds |ExecutionTime0msTo8ms |Count |Number of requests with execution time not exceeding 8 milliseconds on the current node. |
|Number of requests with execution time greater than 8 milliseconds and less than or equal to 24 milliseconds |ExecutionTime8msTo24ms |Count |Number of requests with execution time exceeding 8 milliseconds but not exceeding 24 milliseconds on the current node. |
|Number of requests that took longer than 24 milliseconds to execute |ExecutionTimeBeyond24ms |Count |Number of requests with execution time exceeding 24 milliseconds on the current node. |
|Average transaction response time |TransactionAvgRequestDelay |µs |The average response time of transactions on the current node. |
|Average command response time |CommandAvgRequestDelay |µs |The average response time of commands on the current node. |
|Number of write conflicts |WriteConflictsCount |Count |The number of conflicts encountered by the current node during the write operation. |
|Maximum cache size |MaxCacheConfigured |B |Maximum available disk size configured for a node. |
