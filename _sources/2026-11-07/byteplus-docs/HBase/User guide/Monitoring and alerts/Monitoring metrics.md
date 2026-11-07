---
title: "Monitoring metrics"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Monitoring_metrics"
---

This topic introduces the monitoring items supported by Table Storage for HBase and information related to the monitoring items.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Cloud Monitor collects data every 30 seconds by default. Based on the selected time range, the collected data is aggregated and displayed according to different periods and methods. For specific rules, refer to [Viewing Cloud Service Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor#.5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u).

* You can view detailed monitoring data for up to the last 15 days. For instructions on viewing monitoring data, see [Viewing monitoring information](https://docs.byteplus.com/en/docs/HBase/Viewing_monitoring_information).

* All units in the monitoring metrics table are base units. Refer to the console for the specific units of each metric. The units displayed in the console are dynamically adjusted based on monitoring values and specific conversion standards:

   * SI: Unit conversions are based on SI standards, using a factor of 1000. Prefixes such as K, M, and G are added to the base unit. For example, the base unit for ReadDataPerSecond is B/s. If the monitored value for the network output rate is large, the unit in the console may be adjusted to KB/s, MB/s, GB/s, etc.

   * IEC: according to IEC standards, units are converted using 1024 as the prefix. For example, the base unit for ClusterSpaceQuota(Hot storage) usage is B. If the used storage capacity is large, the unit in the console may be adjusted to KiB, MiB, GiB, etc.


<span id="qlZ8E2NS"></span>
## Monitoring metrics

You can call the [GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData) API to query monitoring metric data for your HBase instances. When you call this API, you need the following information about the monitoring metrics:


* **Namespace**: the product namespace for the monitoring metrics to be queried.

   The product namespace for the HBase instance is `VCM_HBase`.

* **SubNamespace**: The dimension of the metric to be queried.

   HBase instances support viewing monitoring metrics for three dimensions: `Cluster` (instance), `RegionServer`, and `Table`.

* **MetricName**: The name of the monitoring metric to be queried.

   The MetricName for each HBase instance monitoring metric is shown in the table below. For more details, see [Cloud Monitor Metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_HBase).


<span id=".5a6e5L6L55uR5o6n5oyH5qCH"></span>
### Instance monitoring metrics


|Metric name |MetricName |Unit |Description |
|---|---|---|---|
|CPUUsage |ClusterCpuUtil |% |Average CPU usage across all Masters and Region Servers in the instance. |
|MemoryUsage |ClusterMemUtil |% |Average memory usage across all Masters and Region Servers in the instance. |
|Memory used |ClusterUsedMem |B |The hot storage space used by the instance. |
|ClusterSpaceUsagePercent |ClusterSpaceUsagePercent |% |The real\-time percentage of the instance used hot storage space to the total hot storage space. |
|ClusterSpaceQuota(Hot storage) |ClusterSpaceQuotaUsage |B |Real\-time usage of instance storage space (hot storage). |
|Read QPS |ClusterQps |Count/s |The sum of the Read QPS of all Region Servers in the instance. |
|Write QPS |ClusterTps |Count/s |The sum of the write QPS of all Region Servers in the instance. |
|ReadDataPerSecond |ClusterNetworkTransmitThroughput |Byte/s |The sum of the network output rates of all Region Servers in the instance. |
|WriteDataPerSecond |ClusterNetworkReceiveThroughput |Byte/s |The sum of the network input rates of all Region Servers in the instance. |
|Number of RegionServers |RegionServerCount |Count |The number of Region Servers in the instance. |
|RegionServer downtime |ServerCrashTime |Count |Number of occurrences of Region Server downtime in the instance. |
|RegionCount |ServerNumRegions |Count |The number of all Regions in the instance. |
|Number of Regions in RIT State |RITRegionCount |Count |The number of regions in all RIT states in the instance. |
|Number of Tables |ServerNumTables |Count |The number of all Tables in the instance. |
|Total storage |ClusterSpaceQuotaLimit |B |The total amount of hot storage space for the instance. |
|ClusterColdSpaceQuotaUsage |ClusterColdSpaceQuotaUsage |B |Real\-time usage of instance capacity storage (cold storage). |
|ClusterColdSpaceQuotaUsagePercent |ClusterColdSpaceQuotaUsagePercent |% |The real\-time percentage of the instance's used capacity storage (cold storage) space to the total capacity storage space. |
|ThriftCallMeanTime |ThriftCallMeanTime |μs |The average time it takes for the instance server to receive a Thrift request and respond. |
|ThriftCallMaxTime |ThriftCallMaxTime |μs |The maximum time from when the instance server receives a Thrift request to when it responds. |
|Thrift request P99 response time |ThriftCallP99Time |μs |The P99 value of the time from when the ThriftServer receives the Thrift request to when it responds. |
|Get request QPS |ClusterGetNumOps |Count/s |The QPS of Get requests processed by the instance. |
|Get Request P99 Time |ClusterGetRTMean |ms |The average time for all Region Servers in the instance to process Get requests, excluding wait time. |
|GetAverageResposeTime |ClusterGetRTP99 |ms |The P99 value of Get requests processed by all Region Servers in the instance, excluding queue waiting time. |
|Get request MAX delay |ClusterGetRTMAX |ms |The maximum time for all Region Servers in the instance to process Get requests, excluding wait time. |
|Scan request QPS |ClusterScanNumOps |Count/s |The QPS of Scan requests processed by the instance. |
|AvgScanRT |ClusterScanRTMean |ms |The average time for all Region Servers in the instance to process Scan requests, excluding wait time. |
|Scan request P99 time consuming |ClusterScanRTP99 |ms |The P99 value of Scan requests processed by all Region Servers in the instance, excluding queue waiting time. |
|Scan request MAX delay |ClusterScanRTMAX |ms |The maximum time for all Region Servers in the instance to process Scan requests, excluding wait time. |
|Put request QPS |ClusterPutNumOps |Count/s |The QPS of Put requests processed by the instance. |
|PutAverageResponseTime |ClusterPutRTMean |ms |The average time for all Region Servers in the instance to process Put requests, excluding wait time. |
|Put the request P99 time |ClusterPutRTP99 |ms |The P99 value of Put requests processed by all Region Servers in the instance, excluding queue waiting time. |
|Put request MAX delay |ClusterPutRTMAX |ms |The maximum time for all Region Servers in the instance to process Put requests, excluding wait time. |
|BatchPut request QPS |ClusterBatchPutNumOps |Count/s |The QPS of BatchPut requests processed by the instance. |
|BatchPutAverageRT |ClusterBatchPutRTMean |ms |The average time for all Region Servers in the instance to process BatchPut requests, excluding wait time. |
|BatchPut request P99 time consuming |ClusterBatchPutRTP99 |ms |The P99 value of BatchPut requests processed by all Region Servers in the instance, excluding queue waiting time. |
|BatchPut request MAX delay |ClusterBatchPutRTMAX |ms |The maximum time for all Region Servers in the instance to process BatchPut requests, excluding wait time. |


<span id=".cmVnaW9uLXNlcnZlci3nm5HmjqfmjIfmoIc="></span>
### Region Server monitoring metrics


|Metric name |MetricName |Unit |Description |
|---|---|---|---|
|FullGC Duration |RegionServerGCTime |μs |The time the Region Server takes to perform FullGC. |
|Active Write Handler Usage Load |RegionServerActiveWriteHandlerRatio |% |Usage load of the Active Write Handler on the Region Server. |
|Active Read Handler Usage Load |RegionServerActiveReadHandlerRatio |% |The usage load of the Active Read Handler in the Region Server. |
|RPC request P99 response time |P99RpcCallRt |μs |The P99 value of the RPC request to response time in the Region Server, including request waiting time, processing time, etc. |
|RPC request P99 processing time |P99RpcProcessRt |μs |The p99 value of RPC request processing time in the Region Server. |
|RPC request P99 queue time |RpcQUeueTimeP99 |μs |The p99 value of the RPC request queue time in the Region Server. |
|RpcAverageRT |AvgRpcCallRt |μs |Average response time of RPC requests in Region Server, including request waiting time, processing time, etc. |
|RPC request average processing time |AvgRpcProcessRt |μs |Average processing time of RPC requests in Region Server. |
|RPC request average queuing time |RpcQueueTimeMean |μs |Average queue time for RPC requests in the Region Server. |
|RpcMaxRT |MaxRpcCallRT |μs |The maximum response time of RPC requests in the Region Server, including request waiting time, processing time, etc. |
|RpcRequestQueueLength |RpcRequestQueueLength |Count |The number of requests waiting to be processed in the Region Server RPC request queue. |
|CompactionQueueLength |CompactionQueueLength |Count |The number of compaction tasks waiting to be executed in the Region Server. |
|FlushQueueSize |FlushQueueLength |Count |The number of Flush tasks waiting to be executed in the Region Server. |
|RegionCount |RegionCount |Count |The number of Regions held by the Region Server. |
|CPUUsage |CpuUtil |% |The CPU usage of the Region Server. |
|MemoryUsage |MemUtil |% |Memory usage of the Region Server. |
|ReadDataPerSecond |NetworkTransmitThroughput |Byte/s |The network output rate of the Region Server. |
|WriteDataPerSecond |NetworkReceiveThroughput |Byte/s |The network input rate of the Region Server. |
|Read QPS |Qps |Count/s |The Read QPS of the Region Server. |
|Write QPS |Tps |Count/s |The Write QPS of the Region Server. |
|BlockCacheHitCount |BlockCacheHitRate |% |The hit rate of Region Server read requests hitting BlockCache. |
|Get request QPS |RegionServerGetNumOps |Count/s |The QPS of Get requests processed by the Region Server. |
|GetAverageResposeTime |AvgGetRt |μs |The average time it takes for a Region Server to process a Get request, excluding wait time. |
|Get Request P99 Time |P99GetRt |μs |The P99 value of the Get request processed by the Region Server, excluding queue waiting time. |
|Get Request MAX Time |MAXGetRt |μs |The maximum processing time for Get requests by the Region Server, excluding wait time. |
|Scan request QPS |RegionServerScanNumOps |Count/s |The QPS of Scan requests processed by the Region Server. |
|AvgScanRT |AvgScanRT |μs |The average time it takes for a Region Server to process a Scan request, excluding wait time. |
|Scan request P99 time consuming |P99ScanRT |μs |The P99 value of Scan requests processed by the Region Server, excluding queue waiting time. |
|Scan request MAX time |MAXScanRT |μs |The maximum time it takes for a Region Server to process a Scan request, excluding wait time. |
|PUT request QPS |RegionServerPutNumOps |Count/s |The QPS of Put requests processed by the Region Server. |
|PutAverageResponseTime |AvgPutRt |μs |The average time it takes for a Region Server to process a Put request, excluding wait time. |
|Put the request P99 time |P99PutRt |μs |The P99 value of the Region Server processing the Put request, excluding queue waiting time. |
|Put request MAX time |MAXPutRt |μs |The maximum processing time for Put requests by the Region Server, excluding wait time. |
|BatchPUT request QPS |RegionServerBatchPutNumOps |Count/s |The QPS of BatchPut requests processed by the Region Server. |
|BatchPutAverageRT |AvgBatchPutRt |μs |The average time it takes for a Region Server to process a BatchPut request, excluding wait time. |
|BatchPut request P99 time consuming |P99BatchPutRt |μs |The P99 value of the Region Server processing the BatchPut request, excluding queue waiting time. |
|BatchPut request MAX time |MAXBatchPutRt |μs |The maximum processing time for BatchPut requests by the Region Server, excluding wait time. |


<span id=".dGFibGUt55uR5o6n5oyH5qCH"></span>
### Table monitoring metrics


|Metric name |MetricName |Unit |Description |
|---|---|---|---|
|QPS |TablesReadRequestCount |Count/s |The QPS of the statistics table. |
|TPS |TableWriteRequestCount |Count/s |TPS of the statistics table. |
|Table Read Call Total Mean Time |rpcReadCallTotalTimeMean |μs |Average response time of all read requests to the statistical table. |
|Read request P99 response time |rpcReadCallTotalTimeMax |μs |The P99 response time of all read requests for the statistics table. |
|MAX response time for read requests |rpcReadCallTotalTimeMaxReal |μs |Maximum response time for all read requests on the statistics table. |
|Table Write Call Total Mean Time |rpcWriteCallTotalTimeMean |μs |Average response time of all write requests to the statistics table. |
|Write request P99 response time |rpcWriteCallTotalTimeMax |μs |The P99 response time of all write requests to the statistics table. |
|Write request MAX response time |rpcWriteCallTotalTimeMaxReal |μs |Maximum response time for all write requests to the statistics table. |
|Hot Storage Space Usag |HotStorageSpaceUsage |B |Real\-time usage of storage space (hot storage) of the statistics table. |
|Cold storage space usage |ColdStorageSpaceUsage |B |Statistics the real\-time usage of the capacity storage space (cold storage) of the table. |


<span id="Jr4b2cJV"></span>
### **ThriftServer monitoring metrics**


|**Metric name** |**MetricName** |**Unit** |**Description** |
|---|---|---|---|
|CPUUsage |rule_pod_cpu_usage |% |CPU utilization of ThriftServer. |
|MemoryUsage |rule_pod_mem_usage |% |The memory usage of the ThriftServer. |
|ThriftCallMeanTime |infcs_hbase_thrift_thrifttwo_ThriftCall_mean_us |ms |The average time it takes for the instance server to receive a Thrift request and respond. |
|Thrift request P99 response time<br><br> |infcs_hbase_thrift_thrifttwo_ThriftCall_99th_percentile_us |ms |The P99 value of the time from when the instance server receives a Thrift request to when it sends a response. |
