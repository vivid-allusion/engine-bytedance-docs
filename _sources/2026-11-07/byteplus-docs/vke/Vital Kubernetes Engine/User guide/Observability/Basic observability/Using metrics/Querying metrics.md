---
title: "Querying metrics"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Querying_metrics"
---

Querying metrics helps you view cluster metric integration status and metric descriptions in VKE monitoring scenarios. It allows you to determine metric availability, understand metric meanings, and complete observability configuration. This topic describes how to view metric integration status, enable inactive metrics, and query metric details.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When metrics show no data or their meanings are unclear in the monitoring dashboard, we recommend first checking the integration status via <a href="https://docs.byteplus.com/en/docs/90/118262#9n8FklI0">Integrated metric query</a>, and then verifying observability components or viewing metric descriptions by following the on\-screen guidance.</div>


<span id="9n8FklI0"></span>
## Integrated metric query

When viewing monitoring data of clusters, nodes, or workloads in the monitoring dashboard, you can view integrated and non\-integrated metrics in the current cluster via Metric management. For non\-integrated metrics, the page provides an observability configuration entry to help you enable relevant observability capabilities.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This feature displays metric integration status in the cluster:</div>


   * <div data-tips="true" data-tips-type="default">"Integrated" means the current cluster has completed metric collection and configuration. Metrics can be used for monitoring dashboards, alert rules, or observability component queries.</div>


   * <div data-tips="true" data-tips-type="default">"Non\-integrated" means the product supports the metric, but the current cluster has not yet completed collection configuration. Therefore, related monitoring panels or alerts may not display data.</div>


* <div data-tips="true" data-tips-type="default">If multiple panels in the monitoring dashboard show no data, first check whether observability components such as <a href="https://docs.byteplus.com/en/docs/vke/prometheus-agent-add-on">prometheus\-agent</a> and <a href="https://docs.byteplus.com/en/docs/vke/core-dns-add-on">coredns</a> are running healthily. When an add\-on is not installed, is being installed, or is running abnormally, metrics may temporarily have no data.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, select **Monitoring center \> Monitoring dashboard**.

3. In the top action bar of the page, click **Integrated metric management** to enter the metric management page.

4. On the metric management page that appears, view the number of integrated and non\-integrated metrics of the current cluster.

   * In the left category area, select a target metric category.

   * In the right metric list, view the metric names, descriptions, and integration status under that category.

5. To quickly locate a metric, enter a metric display name, raw metric name, alias, or description keyword in the search box.

6. To integrate more metrics, click **View observability configuration** on the page and follow the on\-screen guidance to enable observability components or add metric integrations.


<span id="uussBph4"></span>
## Metric description query

When you need to understand the meaning, unit, statistical scope, or applicable objects of a monitoring metric, you can enter the metric details page to view the full description. The metric details page centrally displays monitoring metric information supported by VKE, helping reduce troubleshooting and alert configuration costs when interpreting monitoring curves.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The metric details page displays metric names, labels, units, types, and descriptions supported by VKE. The page content is based on system\-maintained metric metadata. When metrics are added or updated in the system, the metric details page will synchronously display the latest descriptions.</div>


<span id="FNOo2mnd"></span>
### Metric composition

Metrics in VKE follow the open\-source Prometheus definition and are mainly composed of a metric name and a label.


* Each metric has a name. For example:

   * `node_cpu_seconds_total` \- CPU usage time of the node

   * `node_filesystem_free_bytes` \- Free space of the file system

   * `kube_pod_status_ready` \- Whether the pod is in the Ready state

* Each metric can have multiple labels in the format of `label="value"`. For example:

   * `node_cpu_seconds_total{cluster="cd9g2v12r7***",host_ip="10.10.128.2"}`

   * `kube_pod_status_ready{namespace="default"}`


<span id="GwPAX2nV"></span>
### Querying metrics


1. VKE provides a metric query page for viewing complete metric descriptions.

   1. Log in to the [VKE console](https://console.byteplus.com/vke).

   2. Go to the [VKE metric query](https://console.byteplus.com/vke/monitor-metrics?hiddenNavbar=true) page to query specific metrics.

2. On the metric query page, you can view detailed descriptions of different resource metrics.

   * In the left category navigation, select the metric category you want to view.

   * In the metric description table on the right, view the metric name, labels, unit, metric type, and description.

3. To find a specified metric, enter the metric name in the search box.
