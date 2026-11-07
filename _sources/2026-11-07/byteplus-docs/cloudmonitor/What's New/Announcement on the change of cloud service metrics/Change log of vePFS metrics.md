---
title: "Change log of vePFS metrics"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Announcement_on_the_Change_of_PFS_Metrics"
---

The Cloud Monitor team will soon adjust the monitoring metrics for vePFS, aiming to provide you with a more accurate and comprehensive monitoring experience.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For cloud product metrics and details, see <a href="https://console.byteplus.com/cloud_monitor/docs">Cloud product metrics query</a>.</div>


<span id="L7J3Nvj8"></span>
## February 2025


|MetricName |SubNamespace |Type |Description |Impact |
|---|---|---|---|---|
|ClientReadBandwith |bandwidth |Metric deprecation |The metric is deprecated and replaced with `ClientReadBandwidth`. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* The related charts have disappeared from the monitoring dashboard, and the corresponding metrics cannot be specified during metric queries.<br><br>* If an exclamation mark (!) is added before an existing alert rule, it indicates that the alert rule contains the deprecated metric, and the alert will no longer be triggered. You need to remove the deprecated metric from the alert rule.<br><br>* If you do not remove or update the deprecated metric for an existing alert template, you cannot save the template.<br><br>* If you have configured this metric by using a [custom observability dashboard](https://docs.byteplus.com/en/docs/Observability_Platform/Quickly_start_using_custom_dashboards), the related monitoring data will be unavailable. |
|ClientWriteBandwith |bandwidth |Metric deprecation |The metric is deprecated and replaced with `ClientWriteBandwidth`. ||
|ClientReadBandwidth |bandwidth |Unit change |The metric unit is changed from `Count/Second` to `Bytes/Second(SI)`. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* Monitoring dashboards will display data based on the updated metrics.<br><br>* Alert rules remain unchanged and active. Alert notifications will be sent according to the units configured in alert rules. |
|ClientWriteBandwidth |bandwidth |Unit change |||
|ClientFsReadBandwidth |bandwidth |Unit change |||
|ClientFsWriteBandwidth |bandwidth |Unit change |||


<span id="L7J3Nvj8"></span>
## January 2025


|MetricName |Type |Description |Impact |
|---|---|---|---|
|FilesetQoSIOPSUsedRatio |Metric deprecation |\- |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* The related charts have disappeared from the monitoring dashboard, and the corresponding metrics cannot be specified during metric queries.<br><br>* If an exclamation mark (!) is added before an existing alert rule, it indicates that the alert rule contains the deprecated metric, and the alert will no longer be triggered. You need to remove the deprecated metric from the alert rule.<br><br>* If you do not remove or update the deprecated metric for an existing alert template, you cannot save the template. |
|FilesetQoSEtUsedRatio |Metric deprecation |\- ||
|MkdirLatency |Metric deprecation |\- ||
|RmdirLatency |Metric deprecation |\- ||
|CreateLatency |Metric deprecation |\- ||
|RemoveLatency |Metric deprecation |\- ||
|ClientFsReadBandwith |Metric deprecation |\- ||
|ClientFsWriteBandwith |Metric deprecation |\- ||
