---
title: "Classic Load Balancer (CLB) Monitoring Metrics Upgrade Notice"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CLB-Monitoring-Metrics-Upgrade-Notice"
---

Dear BytePlus User, To further enhance the stability and scalability of our Classic Load Balancer (CLB) service, we will be performing an upgrade of its monitoring metrics.

<span id="e0HHqGsd"></span>
## Upgrade time

August 25, 2025

<span id="91xiGgje"></span>
## Upgrade content


|Newly Added Metrics |||Replaced Metrics |||
|---|---|---|---|---|---|
|**Metric name** |**MetricName** |**SubNamespace** |**Metric name** |**MetricName** |**SubNamespace** |
|Outbound bandwidth utilization |load_balancer_out_bandwidth_utilization |loadbalancer |inbound and outbound bandwidth utilization |load_balancer_in_out_bandwidth_utilization |loadbalancer<br><br> |
|Inbound bandwidth utilization |load_balancer_in_bandwidth_utilization |loadbalancer ||||
|Inbound bandwidth |instance_traffic_rx |loadbalancer |Inbound bandwidth |load_balancer_in_bytes |loadbalancer |
|Outbound bandwidth |instance_traffic_tx |loadbalancer |Outbound bandwidth |load_balancer_out_bytes |loadbalancer |
|Inbound Discarded Bandwidth |instance_drop_traffic_rx |loadbalancer |Inbound Discarded Bandwidth |load_balancer_in_drop_bytes |loadbalancer |
|Outbound discarded bandwidth |instance_drop_traffic_tx |loadbalancer |Outbound discarded bandwidth |load_balancer_out_drop_bytes |loadbalancer |
|Inbound bandwidth |listener_traffic_rx |listener |Inbound bandwidth |listener_in_bytes |listener |
|Outbound bandwidth |listener_traffic_tx |listener |Outbound bandwidth |listener_out_bytes |listener |
|Inbound Discarded Bandwidth |listener_drop_traffic_rx |listener |Inbound Discarded Bandwidth |listener_in_drop_bytes |listener |
|Outbound discarded bandwidth |listener_drop_traffic_tx |listener |Outbound discarded bandwidth |listener_out_drop_bytes |listener |
|Outbound bandwidth utilization |cluster_out_bandwidth_utilization |exclusive_cluster |inbound and outbound bandwidth utilization |cluster_in_out_bandwidth_utilization |exclusive_cluster<br><br> |
|Inbound bandwidth utilization |cluster_in_bandwidth_utilization |exclusive_cluster ||||
|Inbound bandwidth |cluster_traffic_rx |exclusive_cluster |Inbound bandwidth |cluster_in_bytes |exclusive_cluster |
|Outbound bandwidth |cluster_traffic_tx |exclusive_cluster |Outbound bandwidth |cluster_out_bytes |exclusive_cluster |
|Inbound Discarded Bandwidth |cluster_drop_traffic_rx |exclusive_cluster |Inbound Discarded Bandwidth |cluster_in_drop_bytes |exclusive_cluster |
|Outbound discarded bandwidth |cluster_drop_traffic_tx |exclusive_cluster |Outbound discarded bandwidth |cluster_out_drop_bytes |exclusive_cluster |


<span id="bY4gwtjG"></span>
## Upgrade impacts


* No impact on operation of your cloud product instances or business services

* Relevant charts will be removed from the monitoring dashboard, and the corresponding metrics will no longer be available for querying

* Existing alert rules that contain deprecated metrics will be marked with a warning icon (!). These rules will cease to execute as they now include metrics that are no longer available. Remove the deprecated metrics from these alert rules

* For existing alert templates, if they contain deprecated metrics and are not updated or the outdated indicators are removed, saving the template will not be permitted.


If you have any questions, you can log in to the BytePlus official website [https://www.volcengine.com](https://www.volcengine.com), go to the **Console**, and click **Create Ticket** in the upper\-right corner of the page to submit your inquiry. Alternatively, you can contact your Customer Success Manager.

Thank you for your continued support of BytePlus!
