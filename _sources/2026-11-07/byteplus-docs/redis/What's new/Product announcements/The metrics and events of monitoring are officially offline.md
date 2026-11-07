---
title: "The metrics and events of monitoring are officially offline"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/The_metrics_and_events_of_monitoring_are_officially_offline"
---

To provide a higher\-quality monitoring and alerting service, Cache for Redis has officially taken some monitoring metrics and events offline.

<span id="offline-time"></span>
## Offline time

November 12, 2024.

<span id="offline-explanation-and-replacement-solutions"></span>
## Offline explanation and replacement solutions

<span id="details-of-offline-monitoring-metrics"></span>
### Details of offline monitoring metrics

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details of the metrics supported by Cache for Redis, refer to <a href="https://vsop-online.bytedance.net/doc/manage/detail/6293/6293/71170">Monitoring metrics</a>.</div>


The old monitoring metrics `NetworkReceiveThroughput` and `NetworkTransmitThroughput` could only be used for monitoring and not for alerting and consumption. Therefore, to facilitate the timely detection and location of network\-related performance of Redis instances, Cache for Redis has upgraded the old monitoring metrics `NetworkReceiveThroughput` and `NetworkTransmitThroughput` to the new monitoring metrics `NetworkPeakReceiveThroughput` and `NetworkPeakTransmitThroughput` that support monitoring, alerting, or consumption. The details of the monitoring metric upgrade plan are shown in the following table.


|Metric dimension<br><br>(SubNamespace) |Original monitoring metric information ||Upgraded metric ||
|---|---|---|---|---|
||Monitoring metric name<br><br>(MetricName) |Metric purpose |Monitoring metric name<br><br>(MetricName) |Metric purpose |
|Proxy node<br><br>(proxy) |Network output rate<br><br>(NetworkTransmitThroughput) |Only for monitoring, not for alerting and consumption. |Network peak output rate<br><br>(NetworkPeakTransmitThroughput) |Only for monitoring and alerting, not for consumption. |
||Network input rate<br><br>(NetworkReceiveThroughput) ||Network peak input rate<br><br>(NetworkPeakReceiveThroughput) |Can be used for monitoring, alerting, and consumption. |
|Aggregated proxy node<br><br>(aggregated_proxy) |Network output rate<br><br>(AggregatedNetworkTransmitThroughput) ||Network peak output rate<br><br>(AggregatedNetworkPeakTransmitThroughput) ||
||Network input rate<br><br>(AggregatedNetworkReceiveThroughput) ||Network peak input rate<br><br>(AggregatedNetworkPeakReceiveThroughput) ||
|Data node<br><br>(server) |Network output rate<br><br>(NetworkTransmitThroughput) ||Network peak output rate<br><br>(NetworkPeakTransmitThroughput) ||
||Network input rate<br><br>(NetworkReceiveThroughput) ||Network peak input rate<br><br>(NetworkPeakReceiveThroughput) ||
|Aggregated data node<br><br>(aggregated_server) |Network output rate<br><br>(AggregatedNetworkTransmitThroughput) ||Network peak output rate<br><br>(AggregatedNetworkPeakTransmitThroughput) ||
||Network input rate<br><br>(AggregatedNetworkReceiveThroughput) ||Network peak input rate<br><br>(AggregatedNetworkPeakReceiveThroughput) ||


<span id="details-of-the-offline-event"></span>
### Details of the offline event

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details of the events supported by Cache for Redis, refer to <a href="https://vsop-online.bytedance.net/doc/manage/detail/6293/6293/131569">Event monitoring</a>.</div>


The details of the event that needs to be taken offline at this time and the replacement solution are shown in the table below.


|Old events to be taken offline ||New events for replacement ||
|---|---|---|---|
|Event name |Event code |Event name |Event code |
|Instance primary\-secondary switch (Failover) (Deprecated) |redis: **Maintenance**:Instance Failover |Instance primary\-secondary Switch (Failover) |redis: **Exception**:InstanceFailover |


<span id="offline-impact"></span>
## Offline impact


* After the monitoring metrics and events are upgraded, **the original monitoring metrics and events in the above tables will be taken offline**. The offline metrics will not be able to obtain corresponding monitoring data, and the offline events will not be able to be used for event alerting rules.

* Replace the corresponding monitoring metrics and events in a timely manner before the old metrics and old events are taken offline.
