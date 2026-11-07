---
title: "NAS file storage capacity metric change announcement"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/NAS_file_storage_capacity_metric_change_announcement"
---

The Cloud Monitor team will soon adjust the monitoring metrics for NAS file storage capacity cloud products, aiming to provide you with a more accurate and comprehensive monitoring experience.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For the metrics supported by cloud products and metric details, refer to <a href="https://console.byteplus.com/cloud_monitor/docs">cloud product metric query</a>.</div>


<span id="pyldhwra"></span>
## 2025\-12


|MetricName |SubNamespace |Change type |Change description |Impact |
|---|---|---|---|---|
|SmbMetaQps |qps |Metric discontinued |\- |* Does not affect the normal operation of cloud product instances and business operations.<br><br>* Relevant charts in the monitoring dashboard will disappear, and it will not be possible to specify the corresponding metric when querying metrics.<br><br>* An exclamation mark will be added before existing alert rules to indicate that the alert rule contains metrics that have been discontinued, and the alert will no longer be executed. It is necessary to delete the discontinued metrics from the alert rules.<br><br>* In existing alert templates, saving is not allowed unless the discontinued metrics are removed or updated.<br><br>* If the metric has already been configured through custom dashboard via Grafana plugin, the related monitoring will no longer be available.<br><br>* If the metric has already been configured through observability custom dashboard, the related monitoring will no longer be available. |
|SmbWriteLatency |latency |Metric discontinued |\- ||
|SmbMetaLatency |latency |Metric discontinued |\- ||
|SmbReadLatency |latency |Metric discontinued |\- ||
|SmbReadIops |iops |Metric discontinued |\- ||
|SmbWriteIops |iops |Metric discontinued |\- ||
|SmbReadBandWidth |bandwidth |Metric discontinued |\- ||
|SmbWriteBandWidth |bandwidth |Metric discontinued |\- ||


<span id="2LXEtZ1T"></span>
##
