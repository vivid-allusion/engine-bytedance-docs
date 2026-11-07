---
title: "View monitoring data"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/viewing-monitoring"
---

Cloud Search integrates with Cloud Monitor, allowing you to view monitoring metrics directly in the Cloud Search console or Cloud Monitor console. You can analyze the instance running state in real time, including instance resource usage, instance status, and node status information.

<span id="cec22043"></span>
## Procedure


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. In the left navigation of the instance details page, select **Observability \> Monitoring overview**.

5. View monitoring data.

   You can view monitoring data from different dimensions, currently including comprehensive metrics, business metrics, cluster metrics, resource metrics, index metrics, analytical service metrics, .


<span id="84a87345"></span>
## Monitoring metrics description

In the monitoring item chart, you can click the metric name to show or hide the current metric data, or click the icon after the metric<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_faff21b1eeec1295cd71678238c769c5.png) </span>to display only the current metric or show all metrics.

<span id="1a532597"></span>
### Comprehensive metrics


|**Monitoring item name.**  |**Monitoring Item ID** |**Unit** |**Description** |
|---|---|---|---|
|Instance health status |InstanceHealthState |None. |The instance health status has the following conditions:<br><br><br>* 0=Green, instance is healthy.<br><br>* 1=Yellow, data is complete, redundant replicas are offline, single point of failure risk exists.<br><br>* 2=Red, active replica is offline, data is missing, partial read/write failure.<br><br>* 3=Lost, unavailable status. |
|Total number of instance nodes |ClusterNodeCount |Count |Total number of instance nodes. |
|Instance node count by type |* InstanceMasterOnlyNodeNumber<br><br>* InstanceDataOnlyNodeNumber<br><br>* InstanceWarmNodeNumber<br><br>* InstanceColdNodeNumber<br><br>* InstanceCoordinatorOnlyNodeNumber |Count |Count nodes by purpose (such as Data node, Active master node, dedicated Coordinating node, etc.).<br><br>Corresponds to the following:<br><br><br>* Number of exclusive master nodes in instance<br><br>* Number of data nodes in instance<br><br>* Number of warm data nodes in instance<br><br>* Number of cold data nodes in instance<br><br>* Number of coordinating nodes in instance |
|Instance storage usage |InstanceStorageUsedBytes |Bytes(IEC) |Instance storage usage. |
|total index count |TotalIndexNumber |Count |Total number of instance indexes |
|Total number of shards |TotalShardNumber |Count |Total number of shards. |
|Total number of shards on the node |NodeShardCount |Count |Total number of shards per node. |
|Total number of documents. |TotalDocumentNumber |Count |Total number of documents. |
|Cluster maximum CPU usage |MaxCpuUsage |% |CPU usage\-related monitoring metrics of the instance:<br><br><br>* Average CPU usage per time period of the instance<br><br>* Peak CPU usage per time period of the instance |
|Cluster JVM average and maximum usage. |* AvgJvmUsage<br><br>* MaxJvmUsage |% |JVM usage\-related monitoring indicators of the instance:<br><br><br>* Average JVM usage of the instance in each period<br><br>* Peak JVM usage of the instance in each period |
|Cluster disk average usage & maximum usage. |* AvgDiskUsagePercent<br><br>* MaxDiskUsagePercent |% |Disk usage monitoring indicators for the instance:<br><br><br>* Average disk usage rate of the instance per time period.<br><br>* Peak disk usage rate of the instance per time period. |


<span id="f2ebd68e"></span>
### Business metrics


|**monitoring item name** |**Monitoring Item ID** |**Unit** |**Description** |
|---|---|---|---|
|Cluster search OPS |ClusterSearchOPS |None. |Cluster query count per second from a business perspective |
|Cluster search success/failure count |* ClusterSearchSuccessCount<br><br>* ClusterSearchFailedOPS |None. |Cluster business perspective, number of successful and exception queries per second. |
|search success rate |SearchSuccessRatio |% |Search request success rate. |
|Maximum cluster search latency |* ClusterSearchLatencyP99<br><br>* ClusterSearchLatencyP95 |Millisecond |Cluster query max P99 and P95 latency. |
|Cluster Bulk write OPS |ClusterBulkOPS |None. |Cluster bulk writes per second. |
|Bulk write success rate |BulkSuccessRatio |% |Bulk request success rate. |
|Maximum P99 latency of bulk write |ClusterBulkLatencyP99 |Millisecond |Cluster Bulk write P99 latency. |
|Query operations OPS. |QueryOps |None. |Instance dimension, number of shard queries per second. |
|Index operation OPS |IndexOps |None. |Number of document creation actions per second. |
|Merge operations OPS |MergeOps |None. |Number of small file merge operations per second. |
|Node Query operation OPS |NodeQueryOPS |None. |Query count of shards per second at the node level. |
|Node Index operation OPS. |NodeIndexOPS |None. |node dimension, number of document creation actions per second. |
|Node Merge operation OPS |NodeMergeOPS |None. |Node dimension, the number of small file merge actions per second. |
|Average search latency |SearchLatency |Second. |Average latency of query actions within one minute. |
|write latency |IndexLatency |Second. |Average Index operation latency within one minute. |
|Number of document deletions and updates per second |DeletedDocumentRate |None. |Number of documents deleted per second. |


<span id="597639e5"></span>
### Cluster metrics


|**Monitoring item name.**  |**Monitoring Item ID** |**Unit** |**Description** |
|---|---|---|---|
|Index status |* GreenIndexNumber<br><br>* YellowIndexNumber<br><br>* RedIndexNumber |Count |Number of indexes by status:<br><br><br>* Number of indexes in green status. Green indicates healthy; active and replica are both online.<br><br>* Number of indexes in yellow status. Yellow indicates data integrity; replica shards are offline, posing a single point of failure risk.<br><br>* Number of red indexes. Red indicates the active shard is offline, data is missing, and partial read/write failed |
|Node shard quantity |TotalShardNumber |Count |Total number of shards in the cluster. |
|Primary shard count & replica shard count. |* ActivePrimaryShardNumber<br><br>* ReplicaShardNumber |Count |Number of shards by type:<br><br><br>* Number of active shards<br><br>* Number of replica shards |
|Shard status |* ActiveShardNumber<br><br>* UnsignedShardNumber<br><br>* InitializingShardNumber<br><br>* RelocatingShardNumber |Count |Number of shards by different status:<br><br><br>* Active shard quantity<br><br>* Unassigned shard quantity<br><br>* Initializing shard quantity<br><br>* Relocating shard quantity |
|Maximum shard size |LargeShardStoredBytes |Bytes(IEC) |Large shard storage usage. |
|Number of Active Search Threads per Node |ThreadPoolActiveSearchThreads |Count |Number of active threads in the search thread pool. |
|Number of pending tasks |TotalPendingTasks |Count |Total number of pending tasks. |
|fielddata memory usage |FielddataMemorySize |Bytes(IEC) |Fielddata memory usage. |
|Cache hit rate |CacheHitRatio |% |Cache hit rate. |
|Number of search tasks in the node queue. |ThreadPoolSearchQueue |Count |Query task count in sub\-node queue |
|Number of search tasks rejected by node. |ThreadPoolSearchRejected |Count |Number of query tasks rejected by data nodes. |
|Number of SearchContexts per node |ClusterSearchContextCount |Count |Cluster query context quantity. |
|Number of active write threads per node |ThreadPoolActiveWriteThreads |Count |Number of active write threads per node. |
|Number of write tasks in node queue |ThreadPoolWriteQueue |Count |Number of write tasks in the sub\-node queue. |
|Number of Write tasks rejected by nodes |ThreadPoolWriteRejected |Count |Number of write tasks rejected per node. |
|number of active refresh threads per node |ThreadPoolActiveRefreshThreads |Count |Number of active Refresh threads per sub\-node. |
|Number of Refresh tasks in node queue |ThreadPoolRefreshQueue |Count |Number of Refresh tasks in the subnode queue. |
|Number of Refresh tasks rejected by nodes. |ThreadPoolRefreshRejected |Count |Number of Refresh tasks rejected per node. |
|Number of active Flush threads on the node |ThreadPoolActiveFlushThreads |Count |Active flush thread count in sub\-nodes. |
|Number of Flush tasks in the node queue |ThreadPoolFlushQueue |Count |Number of Flush tasks in the sub\-node queue. |
|number of flush tasks rejected per node |ThreadPoolFlushRejected |Count |Number of flush tasks rejected by sub\-nodes. |
|Number of active generic threads on node. |ThreadPoolActiveGenericThreads |Count |Number of active Generic threads in the shard node. |
|Number of Generic tasks in the node queue |ThreadPoolGenericQueue |Count |Number of general tasks in the subnode queue. |
|Number of Generic tasks rejected by the node |ThreadPoolGenericRejected |Count |Number of general tasks rejected by partition nodes. |
|Number of active ForceMerge threads on the node |ThreadPoolActiveForceMergeThreads |Count |number of active ForceMerge threads per shard |
|Number of ForceMerge tasks in the node queue |ThreadPoolForceMergeQueue |Count |Number of ForceMerge tasks in the shard node queue. |
|Number of ForceMerge tasks rejected by node |ThreadPoolForceMergeRejected |Count |number of ForceMerge tasks rejected per shard |


<span id="e3a9fc2d"></span>
### Resource metrics


|**Monitoring item name.**  |**Monitoring Item ID** |**Unit** |**Description** |
|---|---|---|---|
|Node CPU Specifications |NodeCpuQuota |Count |Total CPU cores per node. |
|Node memory specification. |NodeMemoryQuota |GiB |Total memory per node. |
|Node disk specification |NodeDiSkQuota |GiB |Total actual available disk space for user data on each node, slightly less than the instance quota due to file system metadata overhead. |
|Node CPU usage |NodeCPUUsage |% |CPU usage of each node. |
|Node memory usage rate. |ContainerMemoryRssRate |% |Node RSS memory (including JVM) usage rate. |
|Node disk usage rate |DiskUsagePercent |% |Disk usage of each node. |
|Node CPU Load_1m |NodeCpuLoad1m |None. |Node CPU load in the past 1 minute. |
|JVM memory usage rate. |JvmUsage |% |JVM memory usage rate on each node. |
|JVM young generation GC count |YoungGcCount |Count |JVM young generation garbage collection count. |
|JVM Young Generation GC Time. |YoungGcSeconds |ms |Cumulative time spent on JVM young generation garbage collection per cycle |
|JVM old generation GC count |OldGcCount |Count |Number of JVM old generation garbage collections. |
|JVM old generation GC time |OldGcSeconds |ms |Accumulated time of JVM old generation garbage collection within a single cycle. |
|Node disk write IOPS. |NodeWriteIOPS |Count/s |Disk write IO per second per node. |
|Node disk read IOPS |NodeDiskReadIOPS |Count/s |Disk read IO per second for each node. |
|Node disk write bandwidth |FsIoTotalWriteBytes |Bytes/s |disk write bandwidth of each node. |
|Node disk read bandwidth |FsIoTotalReadBytes |Bytes/s |Disk read bandwidth of each node. |
|Node network inbound packets. |NodeTransportReceivedPackages |Count |number of network packets received by each node. |
|Data inflow rate |ReceivedDataRate |KiB/s |Data reception speed of each node. |
|Node network outbound packets |NodeTransportSentPackages |Count |Number of network packets sent by each node. |
|data outflow rate |SentDataRate |KiB/s |Data transmission speed of each node. |
|Number of HTTP connections per node |NodeHttpConnections |Count |Number of HTTP connections per node. |
|Breaker tripped count |BreakersTrippedCount |Count |Number of circuit breaker triggers. |
|IOUtil |ESCloudDiskIOUtil |% |Node disk  ** ** I/O utilization. |


<span id="389666ff"></span>
### Index metrics

Elasticsearch 7.10.2 and OpenSearch 2.9.0 version instances support viewing monitoring data at the index dimension. You can select multiple indexes on the left to view their monitoring data, then see the charts for each index.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If no monitoring data is found for all indexes, try restarting the instance. For more information, see <a href="https://docs.byteplus.com/docs/cloudsearch/restarting">Restart an instance or node</a>.</div>


* <div data-tips="true" data-tips-type="tip">Having too many indexes and shards may affect the proper collection and display of index metrics. It is recommended to keep the number of indexes and shards within a reasonable range and regularly clean up unused indexes.</div>


   * <div data-tips="true" data-tips-type="tip">If you need to back up index data before cleaning, create a snapshot before deleting the index. For specific steps, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/snapshot_management_overview">Create a snapshot</a> and <a href="https://docs.byteplus.com/en/docs/cloudsearch/index_management?lang=en#e4103864">Delete an index</a>.</div>


   * <div data-tips="true" data-tips-type="tip">To automatically clean up expired indexes, use index lifecycle policies. For specific steps, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/Managing_lifecycle_policies?lang=en#1fbab583">Create a lifecycle policy</a>.</div>


   * <div data-tips="true" data-tips-type="tip">To learn how to set a more reasonable shard count, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/Estimating_instance_resources#511d9a75">Shard count estimation and rrecommendation</a>.</div>




|**Monitoring item name.**  |**Monitoring Item ID** |**Unit** |**Description** |
|---|---|---|---|
|index query rate/QPS |IndexSearchRate |Count/s |Query rate of each index. |
|Index query latency P99 |IndexSearchLatencyP99 |ms |p99 latency of each index query. |
|index query success rate |IndexSearchSuccessRatio |% |Bulk success rate for each index. |
|Index write rate / QPS |IndexBulkRate |Count/s |write rates of each index. |
|Index write latency P99 |IndexBulkLatencyP99 |ms |P99 write latency of each index. |
|index write success rate |IndexBulkSuccessRatio |% |Search success rate for each index |
|Index documentation count |IndexDocNumber |Count |Document count of each index. |
|Index storage size |IndexStoreSizeBytes |KiB |Persistent size of each index |


<span id="81ec2010"></span>
### Analytical service metrics


<Tabs>
<Tab zoneid="CVEd318928" title="Resource metrics">
<TabTitle>Resource metrics</TabTitle>


|**Monitoring item name.**  |**Monitoring Item ID** |**Unit** |**Description** |
|---|---|---|---|
|number of running nodes |* analysis_node_alive_num<br><br>* analysis_node_ds_alive_num<br><br>* analysis_node_fe_alive_num<br><br>* analysis_node_igs_alive_num |Count |Count nodes by usage:<br><br><br>* Number of running analytical services MS nodes<br><br>* Number of running analytical services DS nodes<br><br>* Number of running analytical services FE nodes<br><br>* Number of running analytical services IGS nodes |
|CPU specifications |analysis_node_cpu_quota |Core |CPU specifications for each node type. |
|CPU usage |analysis_node_cpu_usage_percent |% |CPU usage of the node types. |
|Memory specification |analysis_node_memory_quota |GiB |Memory specifications of each node type. |
|Memory usage |analysis_node_memory_usage_percent |% |Node memory usage by type. |



</Tab>
<Tab zoneid="Hyx0YmrYMW" title="Read and write metrics">
<TabTitle>Read and write metrics</TabTitle>


|**Monitoring item name.**  |**Monitoring Item ID** |**Unit** |**Description** |
|---|---|---|---|
|Connections |analysis_node_query_connection_total |Count |Number of connections to analytical services. |
|Query QPS |analysis_node_query_total_qps |None. |Query QPS of analytical services. |
|Query average latency |analysis_node_query_latency_avg |ms |Analyze the average query latency of the analytical services. |
|Data write throughput |analysis_node_streaming_write_bytes_per_second |None. |Analytical services data write throughput. |



</Tab>
</Tabs>
