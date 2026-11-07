---
title: "Change log of CLB dedicated cluster metrics"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Announcement_of_changes_to_Cloud_Load_Balancer_dedicated_cluster_metrics"
---

The Cloud Monitor team will soon adjust the monitoring metrics for CLB dedicated clusters, aiming to provide you with a more accurate and comprehensive monitoring experience.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For cloud product metrics and details, see <a href="https://console.byteplus.com/cloud_monitor/docs">Cloud product metrics query</a>.</div>


<span id="JCjbTejp"></span>
## August 2025


|MetricName |SubNamespace |Types |Descriptions |Impacts |
|---|---|---|---|---|
|cluster_in_out_bandwidth_utilization |exclusive_cluster |Scheduled metric deprecation |The metric is replaced with load_balancer_out_bandwidth_utilization. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* Charts in monitoring dashboards can be displayed as expected, and the corresponding metrics remain available for queries.<br><br>* You can still use the metrics to configure alerts. Existing alert rules function as expected, and users can receive alert notifications based on the corresponding rules.<br><br>* Existing alert rules can be viewed, edited, and saved as expected.<br><br>* When you add an alert rule, the metrics can be displayed as expected, but they are marked as scheduled for deprecation. If all metrics in a dimension are scheduled for deprecation, the dimension will be hidden.<br><br>* Metrics scheduled for deprecation cannot be used to configure alert templates in the console. In existing alert templates, metrics can be displayed as expected, but are marked as scheduled for deprecation. You can save existing templates that contain metrics scheduled for deprecation. |
|cluster_in_bytes |exclusive_cluster |Scheduled metric deprecation |The metric is replaced with cluster_traffic_rx. ||
|cluster_out_bytes |exclusive_cluster |Scheduled metric deprecation |The metric is replaced with cluster_traffic_tx. ||
|cluster_in_drop_bytes |exclusive_cluster |Scheduled metric deprecation |The metric is replaced with cluster_drop_traffic_rx. ||
|cluster_out_drop_bytes |exclusive_cluster |Scheduled metric deprecation |The metric is replaced with cluster_drop_traffic_tx. ||


<span id="iLP8HGuY"></span>
##
