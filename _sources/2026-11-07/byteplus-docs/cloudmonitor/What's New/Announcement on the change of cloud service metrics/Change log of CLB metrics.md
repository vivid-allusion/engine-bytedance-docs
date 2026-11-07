---
title: "Change log of CLB metrics"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Cloud_Load_Balancer_metrics_change_notice"
---

The Cloud Monitor team will soon adjust the monitoring metrics for CLB, aiming to provide you with a more accurate and comprehensive monitoring experience.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For cloud product metrics and details, see <a href="https://console.byteplus.com/cloud_monitor/docs">Cloud product metrics query</a>.</div>


<span id="gEoKT3lB"></span>
## August 2025


|MetricName |SubNamespace |Types |Descriptions |Impacts |
|---|---|---|---|---|
|load_balnacer_in_out_bandwidth_utilization |loadbalancer |Scheduled metric deprecation |The metric is replaced with load_balancer_out_bandwidth_utilization. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* Charts in monitoring dashboards can be displayed as expected, and the corresponding metrics remain available for queries.<br><br>* You can still use the metrics to configure alerts. Existing alert rules function as expected, and users can receive alert notifications based on the corresponding rules.<br><br>* Existing alert rules can be viewed, edited, and saved as expected.<br><br>* When you add an alert rule, the metrics can be displayed as expected, but they are marked as scheduled for deprecation. If all metrics in a dimension are scheduled for deprecation, the dimension will be hidden.<br><br>* Metrics scheduled for deprecation cannot be used to configure alert templates in the console. In existing alert templates, metrics can be displayed as expected, but are marked as scheduled for deprecation. You can save existing templates that contain metrics scheduled for deprecation. |
|load_balancer_in_bytes |loadbalancer |Scheduled metric deprecation |The metric is replaced with instance_traffic_rx. ||
|load_balancer_out_bytes |loadbalancer |Scheduled metric deprecation |The metric is replaced with instance_traffic_tx. ||
|load_balancer_in_drop_bytes |loadbalancer |Scheduled metric deprecation |The metric is replaced with instance_drop_traffic_rx. ||
|load_balancer_out_drop_bytes |loadbalancer |Scheduled metric deprecation |The metric is replaced with instance_drop_traffic_tx. ||
|listener_in_bytes |listener |Scheduled metric deprecation |The metric is replaced with listener_traffic_rx. ||
|listener_out_bytes |listener |Scheduled metric deprecation |The metric is replaced with listener_traffic_tx. ||
|listener_in_drop_bytes |listener |Scheduled metric deprecation |The metric is replaced with listener_drop_traffic_rx. ||
|listener_out_drop_bytes |listener |Scheduled metric deprecation |The metric is replaced with listener_drop_traffic_tx. ||


<span id="zs09eyD1"></span>
##
