---
title: "Monitoring metrics"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/monitoring-metric"
---

Cache for Redis not only supports displaying monitoring metrics for individual proxy nodes and server nodes but can also provide aggregated presentation of certain monitoring metrics within these nodes. This topic describes supported monitoring and alert metrics and related information.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* By default, Cloud Monitor aggregates data at a 30\-second granularity. However, when you view monitoring data, the fetched data is aggregated and displayed according to different periods and methods, based on the selected query time range. For specific rules, refer to [Viewing data in Cloud Service Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor#.5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u).

* Currently, you can view monitoring data details for up to the last 15 days. For more information about how to view monitoring data, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/redis/view-monitoring-data).

* Monitoring metrics for proxy nodes and some regular monitoring metrics for server nodes support aggregated display. For the aggregation method of each monitoring metric item, refer to the detailed explanations of aggregation methods in the monitoring metric table.

* The units adopted in the monitoring metrics table are all base units. You can find details of the exact units used for each monitoring item on the console. The units displayed on the console will be adjusted based on the monitoring values and applying certain conversion criteria.

   
   |Unit type |Specific units included |Conversion standards |
   |---|---|---|
   |Capacity\-related units |* B<br><br>* B/s |The capacity\-related units of Redis monitoring metrics support the following two conversion standards:<br><br><br>* According to the SI standard, 1,000 is used as the prefix for unit conversion. During conversion, prefixes such as K (Kilo, which means 1,000), M (Mega, which means 1,000,000), G (Giga, which means 1,000,000,000) and so on, will be added before the base unit.<br><br>   For example, the base unit of **Maximum bytes per response** is B (that is Byte). If the monitoring value of **Maximum bytes per response** is large, the unit on the console may be adjusted to KB, MB, GB, and so on.<br><br>* According to the IEC standard, 1,024 is used as the prefix for unit conversion.<br><br>   For example, the base unit of **Used memory** is B (that is Byte). If the monitoring value of **Used memory** is large, the unit on the console may be adjusted to KiB, MiB, GiB, and so on. |
   |Quantity\-related units |* Count<br><br>* Count/s |According to the SI standard, 1,000 is used as the prefix for unit conversion. During conversion, prefixes such as K (Kilo, which means 1,000), M (Mega, which means 1,000,000), G (Giga, which means 1,000,000,000) and so on, will be added before the base unit.<br><br>For example, the base unit of **Peak connections used** is Count. If the monitoring value of **Peak connections used** is large, the unit on the console may be adjusted to KCount/s, MCount, GCount, etc. |
   |Time\-related units |µs |Conversion is carried out according to the international system of units, such as microseconds (µs), milliseconds (ms), seconds (s), minutes (min), hours (h), etc. |
   |Other units |% |Unit conversion is not involved. |
   

* Some monitoring metrics (such as **Used connections** and **Connection usage**) are the monitoring metrics supported by the old version of the instance. The new version of the instance has already adopted optimized new metrics (such as **Peak connections used** and **Peak connection usage**). We recommend you [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/) to upgrade the instance version as soon as possible to obtain a better monitoring and alarming experience. After the version upgrade, new version instances will no longer display the relevant monitoring metrics from old version instances.

* When collecting monitoring data for metrics such as **P95 query latency** or **P99 query latency**, response latency or request time of blocking commands is not calculated. Block commands include all the commands in the table below.

   
   |Command group |Commands |
   |---|---|
   |List |BLPOP, BRPOP, BRPOPLPUSH |
   |Sorted Set |BZPOPMIN, BZPOPMAX |
   |Stream |XREAD, XREADGROUP |
   


<span id=".55uR5o6n5oyH5qCH6KGo"></span>
## Monitoring metrics table

Detailed descriptions of various monitoring metrics for Redis instances are provided in the table below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData">GetMetricData</a> interface to query the data of various monitoring metrics of the Redis Community Edition instance. When calling this interface for querying, you need to obtain the relevant information of the following monitoring metrics:</div>



* <div data-tips="true" data-tips-type="tip"><code>Namespace</code>: The product space to which the monitoring metric to be queried belongs.</div>


   <div data-tips="true" data-tips-type="tip">The name of the product space of the Cache for Redis Community Edition is <code>VCM_Redis</code>.   </div>
   

* <div data-tips="true" data-tips-type="tip"><code>SubNamespace</code>: The dimension to which the metric to be queried belongs.</div>


   <div data-tips="true" data-tips-type="tip">Cache for Redis Community Edition supports viewing metrics in four dimensions: <code>proxy</code> (proxy node), <code>aggregated_proxy</code> (aggregated proxy node), <code>server</code> (server node), and <code>aggregated_server</code> (aggregated server node).   </div>
   

* <div data-tips="true" data-tips-type="tip"><code>MetricName</code>: The name of the monitoring metric to be queried.</div>


   <div data-tips="true" data-tips-type="tip">For details of the <code>MetricName</code> corresponding to each monitoring metric of Cache for Redis Community Edition, refer to <a href="https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_Redis">Query of monitoring metrics of Cache for Redis Community Edition</a>.   </div>
   


<span id=".6IGa5ZCI5Luj55CG6IqC54K5"></span>
### Aggregated proxy


<Tabs>
<Tab zoneid="pOOqECNWX9" title="Routine monitoring">
<TabTitle>Routine monitoring</TabTitle>


|Metric name |MetricName (for API use) |Unit |Conversion standard |Limits |Aggregation method |
|---|---|---|---|---|---|
|CPU usage |AggregatedCpuUtil |% |Not involved |CPU usage of proxy node. |Average data across all nodes. |
|Total QPS |AggregatedTotalQps |Count/s |SI(1000) |Total QPS on proxy node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The total QPS of the Redis instance includes not only the read and write operations sent by the client to the proxy node, but also other operations sent by the client, such as AUTH, INFO, SELECT, etc. All these operations will be recorded in total QPS.</div><br> |Total data across all nodes. |
|Read QPS |AggregatedReadQps |Count/s |SI(1000) |Read QPS on proxy node. |Total data across all nodes. |
|Write QPS |AggregatedWriteQps |Count/s |SI(1000) |Write QPS on proxy node. |Total data across all nodes. |
|Used connections<br><br>(Only supported by old version instances) |AggregatedUsedConn |Count |SI(1000) |Number of client connections already connected to proxy node. |Total data across all nodes. |
|Connection usage<br><br>(Only supported by old version instances) |AggregatedConnUtil |% |Not involved |Ratio of the used connections to the total connections supported by instance. |Average data across all nodes. |
|Peak connections used<br><br>(Only supported by new version instances) |AggregatedPeakUsedConn |Count |SI(1000) |Peak number of client connections connected to proxy node per second. |Total data across all nodes. |
|Peak connection usage<br><br>(Only supported by new version instances) |Not supported consuming monitoring data via API |% |Not involved |Ratio of the peak connections used to the total connections supported by instance. |Total data across all nodes. |
|Network peak input rate |AggregatedNetworkPeakReceiveThroughput |B/s |SI(1000) |Peak network traffic flows into proxy node per second. |Total data across all nodes. |
|Network peak output rate |AggregatedNetworkPeakTransmitThroughput |B/s |SI(1000) |Peak network traffic flows out of proxy node per second. |Total data across all nodes. |
|Maximum bytes per response |AggregatedResponseMaxBytes |B |SI(1000) |Maximum bytes per response on proxy node. |Maximum data across all nodes. |
|P95 query latency |AggregatedP95QueryLatency |μs |Converted based on international unit system |The request latency at the 95% position when all the request durations from the proxy node to the server node are arranged from low to high. |Maximum data across all nodes. |
|P99 query latency |AggregatedP99QueryLatency |μs |Converted based on international unit system |The request latency at the 99% position when all the request durations from the proxy node to the server node are arranged from low to high. |Maximum data across all nodes. |
|Average request response latency |AggregatedAvgQueryLatency |μs |Converted based on international unit system |Average latency of server node's response when proxy node executes commands. |Average data across all nodes. |
|Maximum number of bytes per request |AggregatedQueryMaxBytes |B |SI(1000) |Maximum number of bytes per request on the proxy node. |Average data across all nodes. |
|Availability zone network peak input rate |AzAggregatedNetworkPeakReceiveThroughput |B/s |SI(1000) |Peak network traffic flows into the proxy node in certain availability zone per second. |Total data across all nodes in same availability zone. |
|Availability zone network peak output rate |AzAggregatedNetworkPeakTransmitThroughput |B/s |SI(1000) |Peak network traffic flows out of the proxy node in certain availability zone per second. |Total data across all nodes in same availability zone. |





</Tab>
<Tab zoneid="WNct7lbrvU" title="Single command monitoring">
<TabTitle>Single command monitoring</TabTitle>


|Metric name |MetricName (for API use) |Unit |Conversion standard |Limits |Aggregation method |
|---|---|---|---|---|---|
|QPS distribution of each command in Bitmap group |AggregatedBitmapCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Bitmap group. |Total data across all nodes. |
|QPS distribution of each command in Connection group |AggregatedConnectionCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Connection group. |Total data across all nodes. |
|QPS distribution of each command in Generic group |AggregatedKeysCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Generic group. |Total data across all nodes. |
|QPS distribution of each command in Geo group |AggregatedGeoCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Geo group. |Total data across all nodes. |
|QPS distribution of each command in Hash group |AggregatedHashCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Hash group. |Total data across all nodes. |
|QPS distribution of each command in Hyperloglog group |AggregatedHyperloglogCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Hyperloglog group. |Total data across all nodes. |
|QPS distribution of each command in List group |AggregatedListCmdQps |Count/s |SI(1000) |The QPS distribution of each command in List group. |Total data across all nodes. |
|QPS distribution of each command in PubSub group |AggregatedPubSubCmdQps |Count/s |SI(1000) |The QPS distribution of each command in PubSub group. |Total data across all nodes. |
|QPS distribution of each command in Scripting group |AggregatedScriptingCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Scripting group. |Total data across all nodes. |
|QPS distribution of each command in Server group |AggregatedServerCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Server group. |Total data across all nodes. |
|QPS distribution of each command in Set group |AggregatedSetCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Set group. |Total data across all nodes. |
|QPS distribution of each command in SortedSet group |AggregatedSortedSetCmdQps |Count/s |SI(1000) |The QPS distribution of each command in SortedSet group. |Total data across all nodes. |
|QPS distribution of each command in Stream group |AggregatedStreamCmdQps |Count/s |SI(1000) |QPS distribution of each command in Stream group. |Total data across all nodes. |
|QPS distribution of each command in String group |AggregatedStringCmdQps |Count/s |SI(1000) |The QPS distribution of each command in String group. |Total data across all nodes. |
|QPS distribution of each command in Transaction group |AggregatedTransactionCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Transaction group. |Total data across all nodes. |





</Tab>
</Tabs>


<span id="ED5Cvy3Y"></span>
### Aggregated server node


<Tabs>
<Tab zoneid="eXRBhus3gE" title="Routine monitoring">
<TabTitle>Routine monitoring</TabTitle>


|Metric name |MetricName (for API use) |Unit |Conversion standard |Limits |Aggregation method |
|---|---|---|---|---|---|
|CPU usage |AggregatedCpuUtil |% |Not involved |CPU usage of server node. |Average data across all nodes. |
|Memory usage |AggregatedMemUtil |% |Not involved |Memory usage of server node. |Average data across all nodes. |
|Used memory |AggregatedUsedMem |B |IEC(1024) |Memory usage of server node. |Total data across all nodes. |
|Total number of keys |AggregatedTotalKey |Count |SI(1000) |Total number of keys stored on server node. |Total data across all master nodes. |
|Keys expired per second |AggregatedExpiredKeyPerSec |Count/s |SI(1000) |Number of keys expired per second on server node. |Total data across all master nodes. |
|Total historically expired keys |AggregatedTotalExpiredKey |Count |SI(1000) |Total number of all expired keys since server node started. |Total data across all master nodes. |
|Keys evicted per second |AggregatedEvictedKeyPerSec |Count/s |SI(1000) |Number of keys that are evicted per second on the server node. |Total data across all master nodes. |
|Total historically evicted keys |AggregatedTotalEvictedKey |Count |SI(1000) |Total number of all evicted keys since server node started. |Total data across all master nodes. |
|Keys with expiration set |AggregatedKeyWithExpiration |Count |SI(1000) |Total number of keys that have set expiration times since server node started. |Total data across all master nodes. |
|Key hit rate |AggregatedKeyHitRate |% |Not involved |Hit ratio when reading keys on server node. |Average data of all master nodes. |
|Keys hit per second |AggregatedKeyHitPerSec |Count/s |SI(1000) |Number of keys that are hit per second on server node. |Total data across all master nodes. |
|Keys missed per second |AggregatedKeyMissPerSec |Count/s |SI(1000) |Number of keys that are missed per second on server node. |Total data across all master nodes. |
|Average execution time |AggregatedAvgExecutionTime |μs |Converted based on international unit system |Average time consumption for server nodes to execute request commands. |Average data across all nodes. |
|Network peak input rate |AggregatedNetworkPeakReceiveThroughput |B/s |SI(1000) |Peak network traffic flows into proxy node per second.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In some scenarios (for example, where there are large key writes), the monitored value of the network peak input rate may exceed the current default bandwidth of the instance.</div><br> |Total data across all nodes. |
|Network peak output rate |AggregatedNetworkPeakTransmitThroughput |B/s |SI(1000) |Peak network traffic flows out of proxy node per second.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In some scenarios (for example, where there are large key reads), the monitored value of the network peak output rate may exceed the current default bandwidth of the instance.</div><br> |Total data across all nodes. |
|Total QPS |TotalQps |Count/s |SI(1000) |Total QPS on server nodes. |Total data across all nodes. |
|Write QPS |WriteQps |Count/s |SI(1000) |Read QPS on server nodes. |Total data across all nodes. |
|Read QPS |ReadQps |Count/s |SI(1000) |Write QPS on server nodes. |Total data across all nodes. |
|Total blocked client connections<br><br> |AggregatedBlockedClients<br><br> |Count |SI(1000) |Number of client connections currently suspended by blocked commands and awaiting wakeup. |Total data across all nodes. |





</Tab>
<Tab zoneid="T4No0hB9oz" title="Single command monitoring">
<TabTitle>Single command monitoring</TabTitle>


|Metric name |MetricName (for API use) |Unit |Conversion standard |Limits |Aggregation method |
|---|---|---|---|---|---|
|QPS distribution of each command in Bitmap group |AggregatedBitmapCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Bitmap group. |Total data across all nodes. |
|QPS distribution of each command in Connection group |AggregatedConnectionCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Connection group. |Total data across all nodes. |
|QPS distribution of each command in Generic group |AggregatedKeysCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Generic group. |Total data across all nodes. |
|QPS distribution of each command in Geo group |AggregatedGeoCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Geo group. |Total data across all nodes. |
|QPS distribution of each command in Hash group |AggregatedHashCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Hash group. |Total data across all nodes. |
|QPS distribution of each command in Hyperloglog group |AggregatedHyperloglogCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Hyperloglog group. |Total data across all nodes. |
|QPS distribution of each command in List group |AggregatedListCmdQps |Count/s |SI(1000) |The QPS distribution of each command in List group. |Total data across all nodes. |
|QPS distribution of each command in PubSub group |AggregatedPubSubCmdQps |Count/s |SI(1000) |The QPS distribution of each command in PubSub group. |Total data across all nodes. |
|QPS distribution of each command in Scripting group |AggregatedScriptingCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Scripting group. |Total data across all nodes. |
|QPS distribution of each command in Server group |AggregatedServerCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Server group. |Total data across all nodes. |
|QPS distribution of each command in Set group |AggregatedSetCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Set group. |Total data across all nodes. |
|QPS distribution of each command in SortedSet group |AggregatedSortedSetCmdQps |Count/s |SI(1000) |The QPS distribution of each command in SortedSet group. |Total data across all nodes. |
|QPS distribution of each command in Stream group |AggregatedStreamCmdQps |Count/s |SI(1000) |QPS distribution of each command in Stream group. |Total data across all nodes. |
|QPS distribution of each command in String group |AggregatedStringCmdQps |Count/s |SI(1000) |The QPS distribution of each command in String group. |Total data across all nodes. |
|QPS distribution of each command in Transaction group |AggregatedTransactionCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Transaction group. |Total data across all nodes. |





</Tab>
</Tabs>


<span id=".5Luj55CG6IqC54K5"></span>
### Proxy


<Tabs>
<Tab zoneid="obZfqLXUNr" title="Routine monitoring">
<TabTitle>Routine monitoring</TabTitle>


|Metric name |MetricName (for API use) |Unit |Conversion standard |Limits |
|---|---|---|---|---|
|CPU usage |CpuUtil |% |Not involved |CPU usage of proxy node. |
|Total QPS |TotalQps |Count/s |SI(1000) |Total QPS on proxy node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The total QPS of the Redis instance includes not only the read and write operations sent by the client to the proxy node, but also other operations sent by the client, such as AUTH, INFO, SELECT, etc. All these operations will be recorded in total QPS.</div><br> |
|Read QPS |ReadQps |Count/s |SI(1000) |Read QPS on proxy node. |
|Write QPS |WriteQps |Count/s |SI(1000) |Write QPS on proxy node. |
|Used connections<br><br>(Only supported by old version instances) |UsedConn |Count |SI(1000) |Number of client connections already connected to proxy node. |
|Connection usage<br><br>(Only supported by old version instances) |ConnUtil |% |Not involved |Ratio of the used connections to the total connections supported by instance. |
|Peak connections used<br><br>(Only supported by new version instances) |PeakUsedConn |Count |SI(1000) |Peak number of client connections connected to proxy node per second. |
|Peak connection usage<br><br>(Only supported by new version instances) |PeakConnUtil |% |Not involved |Ratio of the peak connections used to the total connections supported by instance. |
|Network peak input rate |NetworkPeakReceiveThroughput |B/s |SI(1000) |Peak network traffic flows into proxy node per second. |
|Network peak output rate |Not supported consuming monitoring data via API |B/s |SI(1000) |Peak network traffic flows out of proxy node per second. |
|Maximum bytes per response |ResponseMaxBytes |B |SI(1000) |Maximum bytes per response on proxy node. |
|P95 query latency |P95QueryLatency |μs |Converted based on international unit system |The request latency at the 95% position when all the request durations from the proxy node to the server node are arranged from low to high. |
|P99 query latency |P99QueryLatency |μs |Converted based on international unit system |The request latency at the 99% position when all the request durations from the proxy node to the server node are arranged from low to high. |
|Average request response latency |AvgQueryLatency |μs |Converted based on international unit system |Average latency of server node's response when proxy node executes commands. |
|New connections per second |NewConnReceivedPerSec |Count/s |SI(1000) |Number of new client connections established to proxy node per second. |
|Maximum number of bytes per request |QueryMaxBytes |B |SI(1000) |Maximum number of bytes per request on the proxy node. |





</Tab>
<Tab zoneid="OIUydkOKQd" title="Single command monitoring">
<TabTitle>Single command monitoring</TabTitle>


|Metric name |MetricName (for API use) |Unit |Conversion standard |Limits |
|---|---|---|---|---|
|QPS distribution of each command in Bitmap group |BitmapCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Bitmap group. |
|QPS distribution of each command in Connection group |ConnectionCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Connection group. |
|QPS distribution of each command in Generic group |KeysCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Generic group. |
|QPS distribution of each command in Geo group |GeoCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Geo group. |
|QPS distribution of each command in Hash group |HashCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Hash group. |
|QPS distribution of each command in Hyperloglog group |HyperloglogCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Hyperloglog group. |
|QPS distribution of each command in List group |ListCmdQps |Count/s |SI(1000) |The QPS distribution of each command in List group. |
|QPS distribution of each command in PubSub group |PubSubCmdQps |Count/s |SI(1000) |The QPS distribution of each command in PubSub group. |
|QPS distribution of each command in Scripting group |ScriptingCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Scripting group. |
|QPS distribution of each command in Server group |ServerCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Server group. |
|QPS distribution of each command in Set group |SetCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Set group. |
|QPS distribution of each command in SortedSet group |SortedSetCmdQps |Count/s |SI(1000) |The QPS distribution of each command in SortedSet group. |
|QPS distribution of each command in Stream group |StreamCmdQps |Count/s |SI(1000) |QPS distribution of each command in Stream group. |
|QPS distribution of each command in String group |StringCmdQps |Count/s |SI(1000) |The QPS distribution of each command in String group. |
|QPS distribution of each command in Transaction group |TransactionCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Transaction group. |





</Tab>
</Tabs>


<span id=".5pWw5o2u6IqC54K5"></span>
### Server


<Tabs>
<Tab zoneid="Mrl7Y7azbQ" title="Routine monitoring">
<TabTitle>Routine monitoring</TabTitle>


|Metric name |MetricName (for API use) |Unit |Conversion standard |Limits |
|---|---|---|---|---|
|CPU usage |CpuUtil |% |Not involved |CPU usage of server node. |
|Memory usage |MemUtil |% |Not involved |Memory usage of server node. |
|Used memory |UsedMem |B |IEC(1024) |Memory usage of server node. |
|Total number of keys |TotalKey |Count |SI(1000) |Total number of keys stored on server node. |
|Keys expired per second |ExpiredKeyPerSec |Count/s |SI(1000) |Number of keys expired per second on server node. |
|Total historically expired keys |TotalExpiredKey |Count |SI(1000) |Total number of all expired keys since server node started. |
|Keys evicted per second |EvictedKeyPerSec |Count/s |SI(1000) |Number of keys that are evicted per second on the server node. |
|Total historically evicted keys |TotalEvictedKey |Count |SI(1000) |Total number of all evicted keys since server node started. |
|Keys with expiration set |KeyWithExpiration |Count |SI(1000) |Total number of keys that have set expiration times since server node started. |
|Key hit rate |KeyHitRate |% |Not involved |Hit ratio when reading keys on server node. |
|Keys hit per second |KeyHitPerSec |Count/s |SI(1000) |Number of keys that are hit per second on server node. |
|Keys missed per second |KeyMissPerSec |Count/s |SI(1000) |Number of keys that are missed per second on server node. |
|Average execution time |AvgExecutionTime |μs |Converted based on international unit system |Average time consumption for server nodes to execute request commands. |
|Primary node or not |IsPrimary |None |Not involved |Whether the current server node is a primary node, with the following values:<br><br><br>* 0: It is not a primary node.<br><br>* 1: It is a primary node. |
|Memory used by Lua scripts |Not supported consuming monitoring data via API |B |IEC(1024) |Memory used by the Lua scripts executed on the server node. |
|Inbound bandwidth utilization<br><br>(Only supported by new version instances) |NetworkReceiveThroughputUtil |% |Not involved |Peak bandwidth utilization inbound to server nodes per second. |
|Outbound bandwidth utilization<br><br>(Only supported by new version instances) |NetworkTransmitThroughputUtil |% |Not involved |Peak bandwidth utilization outbound from server nodes per second. |
|Network peak input rate |NetworkPeakReceiveThroughput |B/s |SI(1000) |Peak network traffic flows into proxy node per second.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In some scenarios (for example, where there are large key writes), the monitored value of the network peak input rate may exceed the current default bandwidth of the instance.</div><br> |
|Network peak output rate |NetworkPeakTransmitThroughput |B/s |SI(1000) |Peak network traffic flows out of proxy node per second.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In some scenarios (for example, where there are large key reads), the monitored value of the network peak output rate may exceed the current default bandwidth of the instance.</div><br> |
|Blocked client Connections<br><br> |BlockedClients |Count |SI(1000) |Number of client connections currently suspended by blocked commands and awaiting wakeup. |





</Tab>
<Tab zoneid="CYUN9NyRu4" title="Single command monitoring">
<TabTitle>Single command monitoring</TabTitle>


|Metric name |MetricName (for API use) |Unit |Conversion standard |Limits |
|---|---|---|---|---|
|QPS distribution of each command in Bitmap group |BitmapCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Bitmap group. |
|QPS distribution of each command in Connection group |ConnectionCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Connection group. |
|QPS distribution of each command in Generic group |KeysCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Generic group. |
|QPS distribution of each command in Geo group |GeoCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Geo group. |
|QPS distribution of each command in Hash group |HashCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Hash group. |
|QPS distribution of each command in Hyperloglog group |HyperloglogCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Hyperloglog group. |
|QPS distribution of each command in List group |ListCmdQps |Count/s |SI(1000) |The QPS distribution of each command in List group. |
|QPS distribution of each command in PubSub group |PubSubCmdQps |Count/s |SI(1000) |The QPS distribution of each command in PubSub group. |
|QPS distribution of each command in Scripting group |ScriptingCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Scripting group. |
|QPS distribution of each command in Server group |ServerCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Server group. |
|QPS distribution of each command in Set group |SetCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Set group. |
|QPS distribution of each command in SortedSet group |SortedSetCmdQps |Count/s |SI(1000) |The QPS distribution of each command in SortedSet group. |
|QPS distribution of each command in Stream group |StreamCmdQps |Count/s |SI(1000) |QPS distribution of each command in Stream group. |
|QPS distribution of each command in String group |StringCmdQps |Count/s |SI(1000) |The QPS distribution of each command in String group. |
|QPS distribution of each command in Transaction group |TransactionCmdQps |Count/s |SI(1000) |The QPS distribution of each command in Transaction group. |





</Tab>
</Tabs>


<span id=".5bi46KeB6Zeu6aKY"></span>
### Top 5 dashboard


|**Metric category** |**Metric name** |**MetricName (for API use)**  |**Unit** |**Conversion standard** |**Limits** |
|---|---|---|---|---|---|
|CPU usage |Peak CPU usage<br><br> |CpuUtilMax |% |Not involved |Top 5 server nodes by CPU usage within the selected time period. |
|Memory usage |Memory usage |MemUtil |% |Not involved |The Top 5 server nodes with the highest memory utilization within the selected time period. |
|Inbound bandwidth<br><br> |Network peak input rate |NetworkPeakReceiveThroughput |Bytes/Second |SI(1000)<br><br> |Top 5 nodes with the highest peak network traffic flowing into server nodes per second during the selected period. |
|Outbound bandwidth |Network peak output rate |NetworkPeakTransmitThroughput |Bytes/Second |SI(1000)<br><br> |Top 5 server nodes by peak outbound network traffic per second during the selected time period. |
|Proxy node connection usage rate<br><br>(Only supported by new version instances) |Peak connection usage |PeakConnUtil<br><br> |% |Not involved |Top 5 peak connection usage of proxy nodes within the selected time period. |
|Server node connection usage rate<br><br>(Only supported by new version instances) |Peak connection usage |PeakConnUtil |% |Not involved |Top 5 peak connection usage rates of server nodes during the selected period. |


<span id="BSoYosbi"></span>
## FAQs


* **Q**: I sent a command request to a Redis instance, but why are the QPS distribution monitoring metric values for this command different between the **Single command monitoring** of the proxy node and the server node?

   **A**: Cache for Redis provides QPS\-related monitoring metrics for proxy nodes and server nodes. The QPS\-related monitoring metrics for both collect data from different sources, as follows:

   * QPS\-related monitoring metrics on the proxy node collect command request data sent by clients to the proxy node.

   * QPS\-related monitoring metrics on the server node collect command request data forwarded by the Proxy to the server node.

   When you send a command request to a Redis instance, the QPS distribution monitoring metric values for that command may differ under the **Single command monitoring** tab for proxy nodes and server nodes. In some instances, the commands displayed by the proxy node and server node may even be different. For specific reasons, refer to the table below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information about Redis multi\-key commands, refer to <a href="https://docs.byteplus.com/en/docs/redis/command-limit#.5aSaLWtleS3lkb3ku6TpmZDliLY=">Limits on multiple key commands</a>.   </div>
   

   
   |Scene classification ||Description |Command request forwarding schematic |
   |---|---|---|---|
   |The QPS monitoring metric values displayed on the **Single command monitoring** tab differ between the proxy node and server node for the same command request |The QPS value of the proxy node is greater than that of the server node |Some commands (such as `PING`, `ECHO`, `TIME`, etc.) will not be forwarded to the server node after being sent to the proxy node. The proxy node will directly back the command result, then the command request will only be collected by the proxy node, not by the server node. Therefore, the QPS value of the command request on the proxy node will be greater than that of the server node.<br><br>For example, after you send the `PING` command to Redis, the proxy node will directly back `Pong` without forwarding the command request to the server node. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f68da062b8eaf7dd6e6a7ceb6348a543.png) </span> |
   ||The QPS value of the proxy node equals that of the server node |In the following case, the QPS value of the proxy node will be equal to the single key command request sent by the server node:<br><br><br>* Sent a single key command request to Redis that does not require cross\-slots.<br><br>   For example, you send an `INCR number_key1` command request to Redis, which will first be sent from your client side to the proxy node (that is, collected by the proxy node), and then the proxy node will send the command to the server node where `key1` is located (that is, collected by the server node). At this time, the QPS value of the command request on the proxy node will be equal to the value of the server node.<br><br>* Multi\-key command requests sent to Redis that require cross\-slot operations, but construct keys in the same slot using hash tags within the command.<br><br>   For example, you send Redis a command request for `RENAME {key} _1 {key} _2` (where `key1` and `key2` are on different server nodes 1 and 2). The command request will first be sent from your client side to the proxy node (that is, collected by the proxy node), and then the proxy node will send the command to the server node 2 where `key2` is located (that is, collected by server node 2). At this time, the QPS value of the command request on the proxy node will be equal to the value of the server node. |* Sent a single key command request to Redis that does not require cross\-slots.<br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_edbe0f590cb2ec91cd60ea5a3b1ec0b2.png) </span><br><br>* Multi\-key command requests sent to Redis that require cross\-slot operations, but construct keys in the same slot using hash tags within the command.<br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0871c696ce7822a8002ffe8fee655c33.png) </span> |
   ||The QPS value of the proxy node is less than that of the server node |Partially supports multi\-key commands across slots. When forwarded from the proxy node to the Server node, these commands may be split into multiple commands and sent separately to the Server nodes where the keys reside.<br><br>For example, you send an `MGET key1 key2 key3` command to Redis, where `key1` is on server node 1, and `key2` and `key3` are both on server node 2.<br><br>This command request is first sent from your client to the proxy node (that is, collected by the proxy node). Then, the proxy node splits this command into two commands: `GET key1` and `MGET key2 key3`, and sends them separately to server node 1 and server node 2 (that is, collected by server node 1 and server node 2, respectively). At this point, the QPS value for this command request on the proxy node will be lower than that on the server nodes. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c551a5daf0b51a474a08767bcb98b40.png) </span> |
   |For the same command request, different commands are displayed under the **Single command monitoring** tab on proxy nodes and server nodes ||Some multi\-key commands that span slots may be rewritten when forwarded from proxy node to server node.<br><br>For example, if you send an `MGET key1 key2` command to Redis, where `key1` is on server node 1 and `key2` is on server node 2.<br><br>Then, after this command request is sent from the client to the proxy node, it will be rewritten as two commands, `GET key1` and `GET key2`, and sent respectively to server node 1 and server node 2. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a4bba274e232cfde72d94ef707477e00.png) </span> |
   

* **Q**: Why is the sum of instance's read QPS and write QPS not equal to the total QPS in the monitoring metrics?

   **A**: Because the total QPS of Redis instances includes not only the read and write operations sent by the client to the Proxy node, but also other operations sent by the client, such as AUTH, INFO, and SELECT. They are all recorded in total QPS.


&nbsp;

&nbsp;
