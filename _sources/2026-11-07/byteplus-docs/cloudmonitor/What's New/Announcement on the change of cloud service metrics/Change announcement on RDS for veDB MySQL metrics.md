---
title: "Change announcement on RDS for veDB MySQL metrics"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Change_announcement_on_RDS_for_veDB_MySQL_metrics"
---

The Cloud Monitor team will soon adjust the monitoring metrics for RDS for veDB MySQL, aiming to provide you with a more accurate and comprehensive monitoring experience.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For cloud product metrics and details, see <a href="https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_RabbitMQ">Cloud product metrics query</a>.</div>


<span id="Ewzg31Cx"></span>
## May 2026


|MetricName |SubNamespace |Types |Description |变更影响 |
|---|---|---|---|---|
|PodCpuUtil_V2 |Pod |Metric deprecation |\- |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* The related charts have disappeared from the monitoring dashboard, and the corresponding metrics cannot be specified during metric queries.<br><br>* If an exclamation mark (!) is added before an existing alert rule, it indicates that the alert rule contains a deprecated metric, and the alert will no longer be triggered. You need to remove the deprecated metric from the alert rule.<br><br>* If you do not remove or update the deprecated metric for an existing alert template, you cannot save the template.<br><br>* If you have configured this metric by using a custom dashboard created through the Grafana add\-on, the related monitoring data will be unavailable.<br><br>* If you have configured this metric by using a [custom observability dashboard](https://docs.byteplus.com/en/docs/Observability_Platform/Quickly_start_using_custom_dashboards), the related monitoring data will be unavailable. |


<span id="QhJWKmbu"></span>
## February 2025


|MetricName |Type |Description |Impacts |
|---|---|---|---|
|InnodbRowLockCurrentWaits |Metric deprecation |\- |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* The related charts have disappeared from the monitoring dashboard, and the corresponding metrics cannot be specified during metric queries.<br><br>* If an exclamation mark (!) is added before an existing alert rule, it indicates that the alert rule contains a deprecated metric, and the alert will no longer be triggered. You need to remove the deprecated metric from the alert rule.<br><br>* If you do not remove or update the deprecated metric for an existing alert template, you cannot save the template.<br><br>* If you have configured this metric by using a custom dashboard created through the Grafana add\-on, the related monitoring data will be unavailable.<br><br>* If you have configured this metric by using a [custom observability dashboard](https://docs.byteplus.com/en/docs/Observability_Platform/Quickly_start_using_custom_dashboards), the related monitoring data will be unavailable. |
