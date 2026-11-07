---
title: "Viewing preset monitoring dashboard"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/view-monitoring-dashboard"
---

Cloud Monitor provides a monitoring dashboard service for Cache for Redis. The monitoring dashboard pre\-sets key monitoring indicators (such as CPU usage) for aggregated proxy nodes and aggregated data nodes in Redis instances. At the same time, it supports viewing the same monitoring indicators of multiple Redis instances for comparison to help you quickly grasp the operating conditions of different instances. Besides the aggregated metrics monitoring dashboard, Cloud Monitor offers **commonly used Redis data plane monitoring** predefined dashboards. These dashboards organize panels by **instance + node** dimensions. After selecting an instance ID, you can view all key monitoring charts for proxy nodes (Proxy) and server nodes (Server) under that instance at once (e.g., CPU utilization, total QPS, peak network input/output rate, average request response latency, etc.). They display non\-aggregated detailed curves for each node, which helps quickly pinpoint load imbalances on single nodes or single shards.

<span id=".6aKE572u55uR5o6n5oyH5qCH"></span>
## Predefined monitoring indicators

Cache for Redis predefines some key monitoring indicators for aggregated proxy nodes and aggregated server nodes in the monitoring dashboard. The specific indicator details are shown in the following table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details about monitoring metrics, refer to <a href="https://docs.byteplus.com/en/docs/redis/monitoring-metric">Monitoring metrics</a>.</div>



<Tabs>
<Tab zoneid="Skcvqm8F0A" title="Aggregated proxy">
<TabTitle>Aggregated proxy</TabTitle>


|Metric name |MetricName (for API use) |Unit |Conversion standard |Limits |Aggregation method |
|---|---|---|---|---|---|
|CPU usage |AggregatedCpuUtil |% |Not involved |CPU usage of proxy node. |Average data across all nodes. |
|Total QPS |AggregatedTotalQps |Count/s |SI(1000) |Total QPS on proxy node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The total QPS of the Redis instance includes not only the read and write operations sent by the client to the proxy node, but also other operations sent by the client, such as AUTH, INFO, SELECT, etc. All these operations will be recorded in total QPS.</div><br> |Total data across all nodes. |
|Peak connections used |AggregatedPeakUsedConn |Count |SI(1000) |Peak number of client connections connected to proxy node per second. |Total data across all nodes. |
|Network peak input rate |AggregatedNetworkPeakReceiveThroughput |B/s |SI(1000) |Peak network traffic flows into proxy node per second. |Total data across all nodes. |
|Network peak output rate |AggregatedNetworkPeakTransmitThroughput |B/s |SI(1000) |Peak network traffic flows out of proxy node per second. |Total data across all nodes. |
|Average request response latency |AggregatedAvgQueryLatency |μs |Converted based on international unit system |Average latency of server node's response when proxy node executes commands. |Average data across all nodes. |





</Tab>
<Tab zoneid="b0us7IlErU" title="Aggregated server node">
<TabTitle>Aggregated server node</TabTitle>


|Metric name |MetricName (for API use) |Unit |Conversion standard |Limits |Aggregation method |
|---|---|---|---|---|---|
|CPU usage |AggregatedCpuUtil |% |Not involved |CPU usage of server node. |Average data across all nodes. |
|Memory usage |AggregatedMemUtil |% |Not involved |Memory usage of server node. |Average data across all nodes. |
|Key hit rate |AggregatedKeyHitRate |% |Not involved |Hit ratio when reading keys on server node. |Average data of all master nodes. |
|Total number of keys |AggregatedTotalKey |Count |SI(1000) |Total number of keys stored on server node. |Total data across all master nodes. |
|Total historically expired keys |AggregatedTotalExpiredKey |Count |SI(1000) |Total number of all expired keys since server node started. |Total data across all master nodes. |
|Keys with expiration set |AggregatedKeyWithExpiration |Count |SI(1000) |Total number of keys that have set expiration times since server node started. |Total data across all master nodes. |





</Tab>
<Tab zoneid="IYs5hkaqC1" title="Proxy">
<TabTitle>Proxy</TabTitle>


|Metric name |MetricName (for API use) |Unit |Conversion standard |Limits |
|---|---|---|---|---|
|CPU usage |CpuUtil |% |Not involved |CPU usage of proxy node. |
|Total QPS |TotalQps |Count/s |SI(1000) |Total QPS on proxy node.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The total QPS of the Redis instance includes not only the read and write operations sent by the client to the proxy node, but also other operations sent by the client, such as AUTH, INFO, SELECT, etc. All these operations will be recorded in total QPS.</div><br> |
|Network peak input rate |NetworkPeakReceiveThroughput |B/s |SI(1000) |Peak network traffic flows into proxy node per second. |
|Network peak output rate |Not supported consuming monitoring data via API |B/s |SI(1000) |Peak network traffic flows out of proxy node per second. |
|Average request response latency |AvgQueryLatency |μs |Converted based on international unit system |Average latency of server node's response when proxy node executes commands. |





</Tab>
<Tab zoneid="UEeHWO88Ry" title="Server">
<TabTitle>Server</TabTitle>


|**Metric name** |**MetricName (for API use)**  |**Unit** |**Conversion standard** |**Limits** |
|---|---|---|---|---|
|CPU usage |CpuUtil |% |Not involved |CPU usage of server node. |
|Memory usage |MemUtil |% |Not involved |Memory usage of server node. |
|Total number of keys |TotalKey |Count |SI(1000) |Total number of keys stored on server node. |
|Total QPS |TotalQps |Count/s |SI(1000) |Total QPS on server nodes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This metric is only available in Redis 7.0 instances.</div><br> |





</Tab>
</Tabs>


&nbsp;

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The Cache for Redis only supports viewing monitoring indicator data within the last 30 days. For more details, refer to [Monitoring cloud service](https://docs.byteplus.com/en/docs/cloudmonitor/Monitoring-cloud-service).

* The query interval in the monitoring dashboard is a maximum of 14 days.

* The monitoring dashboard supports selecting a maximum of 50 Redis instances for viewing at one time. For more details, refer to [Monitoring dashboard](https://docs.byteplus.com/en/docs/cloudmonitor/Monitoring-dashboard).


<span id="GCs2W18x"></span>
## Procedure


<Tabs>
<Tab zoneid="TQRRkaNUqT" title="Viewing monitoring dashboard">
<TabTitle>Viewing monitoring dashboard</TabTitle>

1. Log in to [Observability Platform](https://console.byteplus.com/observe/cloud-monitor).

2. In the left\-side navigation pane, select **Cloud Monitor** \> **Monitoring Dashboard**.

3. In the cloud product list on the **Dashboard best** practice page, ** ** click<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cad27cf4c326d9892fb605720a944843.png) </span>icon on the right side of Database, and then click **Cache for Redis/Default indicator market**.

4. On the monitoring dashboard page of **Cache for Redis**, set the following query conditions according to business needs.

   
   |Query condition |Description |
   |---|---|
   |Query time |Set the query time for the monitoring dashboard at the top of the page. By default, it selects to query the monitoring indicator data for the last 1 day.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can click the time query shortcut keys (such as <strong>1 hour</strong>, <strong>3 hours</strong>, and so on) to quickly specify the query time range.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only support viewing monitoring indicator data within the last 30 days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The query interval in the monitoring dashboard is a maximum of 14 days.</div><br> |
   |Query object |Click the instance resource drop\-down list and select the instance to be viewed in the pop\-up dialog box.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can first select the region and project in the pop\-up dialog box, and then enter the instance ID of Redis in the ResourceID search box for filtering.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A maximum of 50 Redis instances can be selected for viewing at the same time.</div><br> |
   

5. After setting the above query conditions, the **Aggregated proxy** and **Aggregated server** sections automatically display the chart details of the corresponding monitoring metrics for the qualifying Redis instances.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can hover over any point on the chart to view the metric value at that specific time. If you selected multiple instances in the query conditions, you can also sort by metric value.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details on preset monitoring metrics for Cache for Redis, refer to <a href="https://docs.byteplus.com/en/docs/redis/view-monitoring-dashboard#.6aKE572u55uR5o6n5oyH5qCH">Predefined monitoring indicators</a>.   </div>
   


</Tab>
<Tab zoneid="PhxzjHZRoo" title="View preset dashboard">
<TabTitle>View preset dashboard</TabTitle>

1. Log in to [Observability Platform](https://console.byteplus.com/observe/cloud-monitor).

2. In the left navigation pane, select **Custom Dashboard** to go to the **Dashboard management** page.

3. On the **Dashboard management** page, select **Built\-in dashboard**.

4. In the **Built\-in dashboard** list, click **Common monitoring of Redis data surface** to view monitoring data for all server nodes and proxy nodes under the selected instance.


</Tab>
</Tabs>


&nbsp;
