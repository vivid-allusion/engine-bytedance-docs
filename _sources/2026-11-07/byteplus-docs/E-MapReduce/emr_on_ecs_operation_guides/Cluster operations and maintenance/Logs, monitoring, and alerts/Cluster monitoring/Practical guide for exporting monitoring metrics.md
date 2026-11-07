---
title: "Practical guide for exporting monitoring metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Practical_guide_for_exporting_monitoring_metrics"
---

The monitoring metrics of Volcano Engine E\-MapReduce (EMR) clusters are stored in a reliable metrics center via Prometheus RemoteWrite from the machines. This metrics storage is not open to external access. To export monitoring metrics to your own metrics storage for flexible access to specific metrics, or even to retrieve all metric data, this document provides instructions for exporting monitoring metrics.

<span id="_1-使用前提"></span>
## Prerequisites

The EMR metrics system is built on Prometheus. The following steps assume that your metrics ingestion endpoint supports Prometheus Remote Write requests.

<span id="_2-具体方案"></span>
## Solutions

<span id="_2-1-需求特定指标"></span>
### Specific metric requirements

The EMR service has already been integrated with the Volcano Engine cloud monitoring product, enabling you to obtain specific metric data via the cloud monitoring OpenAPI.

Before retrieving metrics, you can first use [E-MapReduce cloud monitoring metrics](https://console.byteplus.com/cloud_monitor/docs) to view the current list of all configured metrics for the EMR product and obtain the **MetricName**.

After obtaining the MetricName, you can then use the [GetMetricsData ](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData)API to retrieve the target metric information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you require metrics beyond those listed, you can contact EMR technical support at any time via <a href="https://console.byteplus.com/workorder/create">ticket submission</a>.</div>


<span id="_2-2-通过节点公网输出指标"></span>
### Export metrics via public network nodes

To export all cluster monitoring metrics to your own metrics storage for flexible viewing, you need to export metrics directly from the cluster nodes. You can contact us directly through the [ticket submission](https://console.byteplus.com/workorder/create) mechanism. We will provide suitable scripts for implementation based on your scale and version.

When exporting metrics via the public network method, you must ensure that the security group configuration is correct to guarantee normal communication between both ends of Remote Write.
