---
title: "Prometheus federation integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Federate_API_Integration"
---

Vital Managed Service for Prometheus (VMP) allows you to scrape specified time series by using the federate endpoint of a workspace to achieve data aggregation for multiple Prometheus services. This topic describes how to obtain the federate endpoint of a workspace and scrape time series.

<span id="QA49IEr8"></span>
## Background

The federate endpoint allows a Prometheus service to scrape selected time series from another Prometheus service to achieve data aggregation for multiple Prometheus services. This enables a scalable Prometheus monitoring system.

<span id="WAiLiL8D"></span>
### Hierarchical federation

Hierarchical federation allows Prometheus to scale to environments with tens of data centers and millions of nodes. In this case, the federation topology resembles a tree, where higher\-level Prometheus servers collect aggregated time series data from a large number of subordinate Prometheus servers.

For example, a user may have many data centers, each of which is equipped with a separate Prometheus server. The servers collect the data of data centers in high detail (instance\-level drill\-down). A set of global Prometheus services is provided to collect and store only aggregated data from those local services (job\-level drill\-down). This provides both an aggregated global view and detailed local views.

<span id="nfmUNn8S"></span>
### Cross\-service federation

In cross\-service federation, a Prometheus server of a service is configured to scrape selected data from a Prometheus server of another service. This enables alerting and queries for two datasets in a single server.

For example, a Vital Kubernetes Engine (VKE) cluster running multiple services may expose information about basic resource usage on the cluster, such as memory and CPU usage. On the other hand, a service running on the cluster only exposes application\-specific service metrics. In most cases, these two sets of metrics are scraped by separate Prometheus servers. When you use cross\-service federation, the cluster metric data and application metric data are aggregated, and you can use the two sets of metrics to measure the health of the infrastructure and the application.

<span id="wkEeXQIy"></span>
## Prerequisites


* A Vital Managed Service for Prometheus (VMP) workspace has been created. For more details, refer to [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* The federated API address of another Prometheus instance is obtained.


<span id="fUkFRmYB"></span>
## Limits

When you use the federate endpoint to export metrics, you cannot export **basic cloud service metrics**, which are free of charge with a 15\-day storage duration in workspaces. For more details, see [Pay-as-you-go](https://docs.byteplus.com/en/docs/vmp/pay-as-you-go).

<span id="8mA6DytX"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Integration Center \> Component**. On the page that appears, click **Prometheus Federation** to configure the integration task.

4. Configure the deployment environment of the collector. Click **VKE environment** and select an associated cluster.

5. Click **Create Integration Task** to specify the details of the integration task.

   
   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |Task name |Specify the name of the integration task. |
   |**Scrape configuration** ||
   |Metric scraping interval |Configure the collection interval of the collector. |
   |Authentication Method |Specify an authentication method for the target Prometheus instance. Valid values:<br><br><br>* **No certification**: No authentication is required.<br><br>* **Basic Auth**: Basic Auth is used for authentication. When you select this authentication method, you need to configure the username and password for authentication. |
   |Acquisition target |Configure the federated API address of the target Prometheus instance,<br><br>**such as** `http://query.prometheus-demo/api/v1/federate`. |
   |Data filtering |Filter metrics of the target Prometheus instance by using metric labels,<br><br>**such as** `job="prometheus"` or `__name__=~"job:.*"`. Regular expressions are supported. You can configure both **AND** rules and **OR** rules.<br><br><br>* **AND** rule: Metrics will be collected only if they contain all specified labels.<br><br>* **OR** rule: Metrics will be collected if they contain one of the specified labels.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You must configure at least one data filtering rule.</div><br> |
   

6. Click **Confirm** to complete the configuration.


<span id="ah5C3seB"></span>
## Validate results

<span id="UsDwPH5h"></span>
### View the integration task

After the configuration is complete, you can view the status and details of the task. Check whether the target task runs as expected.


1. In the left navigation bar, click **Integration Center \> Integration task**.

2. Click **VKE environment** **.**  You can view the status of the integration task in the task list.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6fe2a2f5a489b5a44dc8335b4eabf166.png) </span>

After the integration task is created, you can perform the following O&M operations:


* Click the **name of the task** to go to the task details page.

* Click **Edit** in the **Actions** column to edit the task.

* Click **Suspend task** in the **Actions** column to suspend the task.

* Click **Delete** in the **Actions** column to delete the corresponding integration task.


<span id="PliTd7Av"></span>
### Query task metrics

Click **Explore** in the left navigation pane. On the page that appears, use the `up` statement to view the status of collection jobs for the integration task. In this example, the statement is `up{job="staticScrape/vmp-system/federation-ead***"}`. When the metric value is 1, it indicates that the collector is created and working as expected.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b2739965b269ac654bd22236241fcfa.png) </span>

<span id="qBoDfWg3"></span>
## Monitoring information

<span id="aputlnjo"></span>
### Query metrics

You can quickly query and display metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b7ab7eb8e245e75580d79cdf01b71b30.png) </span>

<span id="WK0oJxIZ"></span>
### Create dashboards

You can install Grafana in a VKE cluster or an ECS instance and then use Grafana to view metrics and create dashboards.


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id="L0MYXCfb"></span>
### Configure alerts

You can configure alerts for monitoring targets in the alert center of VMP. For details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).
