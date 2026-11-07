---
title: "Change log of metrics for HBase table database"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Tablestore_HBase_edition_metric_change_announcement"
---

The Cloud Monitor team will soon adjust the metrics for the HBase table database to provide a more accurate and comprehensive monitoring experience.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For cloud product metrics and details, see <a href="https://console.byteplus.com/cloud_monitor/docs">Cloud product metrics query</a>.</div>


<span id="OzURI5cB"></span>
## August 2026


|MetricName |SubNamespace |Types |Descriptions |Impacts |
|---|---|---|---|---|
|JobDelayTime |Bard |Metric deprecation |\- |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* The related charts have disappeared from the monitoring dashboard, and the corresponding metrics cannot be specified during metric queries.<br><br>* If an exclamation mark (!) is added before an existing alert rule, it indicates that the alert rule contains a deprecated metric, and the alert will no longer be triggered. You need to remove the deprecated metric from the alert rule.<br><br>* If you do not remove or update the deprecated metric for an existing alert template, you cannot save the template.<br><br>* If you have configured this metric by using a [custom observability dashboard](https://docs.byteplus.com/en/docs/Observability_Platform/Quickly_start_using_custom_dashboards), the related monitoring data will be unavailable. |
|ServerCrashTime |Master ||||
|RegionserverCount |||||
|ClusterSpaceQuotaLimitNew |Cluster ||||
|ClusterWriteRequestCount |||||


&nbsp;

<span id="PfEbBqJY"></span>
## March 2026


|MetricName |SubNamespace |Types |Descriptions |Impacts |
|---|---|---|---|---|
|ClusterSpaceQuotaUsageNew |Cluster |Metric deprecation |\- |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* The related charts have disappeared from the monitoring dashboard, and the corresponding metrics cannot be specified during metric queries.<br><br>* If an exclamation mark (!) is added before an existing alert rule, it indicates that the alert rule contains a deprecated metric, and the alert will no longer be triggered. You need to remove the deprecated metric from the alert rule.<br><br>* If you do not remove or update the deprecated metric for an existing alert template, you cannot save the template.<br><br>* If you have configured this metric by using a [custom observability dashboard](https://docs.byteplus.com/en/docs/Observability_Platform/Quickly_start_using_custom_dashboards), the related monitoring data will be unavailable. |


<span id="OilAaqDl"></span>
##
