---
title: "Metrics"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Metrics"
---

Cloud Monitor metrics consist of multiple parameters. This topic describes the metric parameters of Cloud Monitor and the methods of querying metrics.

<span id="kq5wXukO"></span>
## Metric composition

Metrics in Cloud Monitor consist of MetricName, Namespace, and SubNamespace. The following table describes the common parameters.


|Metric parameters |Descriptions |
|---|---|
|Namespace |Indicates the namespace of a cloud product. For example, the namespace of ECS is `VCM_ECS`. |
|SubNamespace |Indicates the sub\-category of metrics for a cloud product. For example, in ECS, <br><br><br>* `Instance` indicates the basic instance metrics in ECS.<br><br>* `GPU` indicates the GPU metrics in ECS.<br><br>* `Storage` indicates the storage metrics in ECS. |
|MetricName |Indicates the specific metric name. For example, in ECS, `CpuTotal` indicates the CPU utilization metric of an ECS instance. |


<span id="NjTtt55w"></span>
## Metrics queries

Cloud Monitor provides a metric query page for cloud products. For details, see [Cloud Monitor metric queries](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Metrics can be used for alerting and consumption:</div>


   * <div data-tips="true" data-tips-type="warning">Metrics for alerting: This type of metric can be used to configure alert tasks.</div>


   * <div data-tips="true" data-tips-type="warning">Metrics for consumption: This type of metric can be consumed through the Exporter or API.</div>


* <div data-tips="true" data-tips-type="warning">Whether IEC is included in MetricUnit indicates different unit bases.</div>


   * <div data-tips="true" data-tips-type="warning">With IEC: The unit base is 1024.</div>


   * <div data-tips="true" data-tips-type="warning">Without IEC: The unit base is 1000.</div>



<span id="f6XYHEuy"></span>
## Metric change announcement

You can view the cloud metric change announcements to learn about metric changes for the corresponding products. For details, see [Cloud product metric change announcements](https://docs.byteplus.com/en/docs/cloudmonitor/Announcement_on_the_change_of_cloud_service_metrics).
