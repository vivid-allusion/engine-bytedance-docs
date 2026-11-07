---
title: "Feature overview"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Feature_overview"
---

Cloud Monitor allows you to export monitoring data to VMP or self\-managed Prometheus by using the exporter. This topic describes cloud products for which you can export monitoring data by using the exporter.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>[Beta \- apply for trial]</strong>: This feature is currently in the public beta stage and is temporarily available for free. To use this feature, enable pay\-as\-you\-go first and then contact your account manager.</div>


<span id="KfetbQeb"></span>
## Considerations


* After the resources and metadata of a cloud product change, approximately 10 minutes are taken for the corresponding information exported by the Exporter to take effect.

* The instance metadata fields that can be exported are subject to the actual fields returned by the `/meta/object` endpoint of the Exporter.

* For cloud products for which you can export the ProjectName field, you can filter data by ProjectName during export. In this way, only metrics from the specified Projects are exported.

* A metric is uniquely identified by the combination of Namespace, SubNamespace, and MetricName because the same metric name can be reused across different cloud products.

   * **Namespace**: Cloud product. For the namespace of each cloud service, see [Cloud service metrics](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics).

   * **SubNamespace**: Sub\-category of metrics for a cloud product. For details, see the SubNamespace field of each cloud product on the [Cloud Monitor metric queries](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page.

   * **MetricName**: Metric name. For details, see the MetricName field of each cloud product on the [Cloud Monitor metric queries](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page.


<span id="jXnYGILE"></span>
## Supported cloud services

Currently, you can export the metrics of some cloud products to Prometheus by using the exporter. For details, see [Supported cloud products](https://console.byteplus.com/cloud_monitor/exporter).
