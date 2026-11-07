---
title: "Dynamo integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Dynamo_integration"
---

Vital Managed Service for Prometheus (VMP) enables monitoring of Dynamo instances deployed in Vital Kubernetes Engine (VKE) clusters.

<span id="tSOykBrA"></span>
## Background

NVIDIA Dynamo is an open\-source, high\-throughput, low\-latency, distributed inference framework for serving generative AI models in distributed environments. It features large language model (LLM)\-specific optimizations. NVIDIA Dynamo tackles efficiency and cost issues in large\-scale inference with its core capabilities, such as prefill\-decode (PD) disaggregation, high\-performance data transfer protocols, distributed key\-value (KV) cache, KV cache\-aware scheduling, multi\-level KV cache offloading, and adaptive GPU scheduling.

You can use VMP to monitor Dynamo instances deployed in VKE clusters to enable alerting and optimization for key metrics.

<span id="XsF9YhCN"></span>
## Prerequisites


* VMP

   * A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* VKE

   * VKE has been activated.

   * A cluster has been created. For more details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * A Dynamo instance has been deployed in the cluster.

   * Cloud native observability has been enabled for the cluster, and prometheus\-agent has been installed in the cluster. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The VMP workspace and the VKE cluster must be deployed in the same region.</div>


<span id="L6wgUmWN"></span>
## Procedure

<span id="XKV2O3yv"></span>
### Configure an integration task


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Integration Center \> Component**. On the page that appears, find and click **Dynamo** to configure an integration task.

4. Configure the deployment environment of the collector. Click **VKE environment** and select an associated cluster.

5. Click **Create Integration Task** to specify the details of the integration task.



|Parameter |Description |
|---|---|
|**Basic information** ||
|Task name |Specify the name of the integration task. It can contain Chinese characters, letters (uppercase and lowercase), digits, and underscores (`_`), and must be 1 to 40 characters in length. |
|Project |The project to which the instance belongs. ‌A project is a resource management mechanism that  provides to enable grouping of cloud resources by project. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, as well as cost calculation across cloud resources.  |
|Tags |Labels of the instance. A tag is a key\-value pair that allows you to classify and aggregate cloud resources from different dimensions. You can use tags for resource authorization and bill splitting. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can add up to 50 labels.</div><br> |
|**Scrape configuration** ||
|Metric scraping interval |Configure the collection interval of the collector. |
|JobLabel |You can select labels from Kubernetes Pod objects, and the label value will be used as the job label for all metrics. For example, if you set the JobLabel parameter to `foo` and the Pod label is `foo: bar`, the system will add a `job="bar"` label to all collected metrics. If this parameter is left empty, the default job label for the metrics consists of the namespace and name of the PodMonitor object, which is in the format `<namespace>/<name>`. |
|Namespace |Specify the namespace where the collection target is deployed in the cluster. Values:<br><br><br>* **arbitrary**: indicates that metrics of resources in any namespace in the cluster can be collected.<br><br>* **custom**: indicates that you can specify custom namespaces in the cluster, and only metrics of resources in the specified namespaces can be collected. For example, if you set the value to `default`, only metrics of resources in the default namespace can be collected. |
| LabelSelector |Select collection targets by using the labels of Kubernetes Pod objects. |



6. Click **Confirm** to complete the configuration.


<span id="mZb4zJEd"></span>
### Obtain monitoring dashboards

Click the **Effect preview** tab to view sample monitoring dashboards. Click **Get the Grafana template** to download the Grafana monitoring dashboard template in JSON format.

<span id="Vfkp4gvM"></span>
### Query metrics

Click the **Acquisition metric** tab to view the list of metrics for the collection targets.

<span id="jJPp6Lu0"></span>
### View preset alerts

Click the **Alert template** tab to view the preset alert templates for Dynamo. Click **Turn on alert**. You are redirected to the alert group creation page, where you can swiftly create and enable alerts based on the current alert template.

<span id="Twjtv2CO"></span>
## Validate results

After the configuration is complete, you can view the status and details of the task. Check whether the integration task is running as expected.


1. In the left navigation bar, click **Access center \> Access task**.

2. Click **VKE environment** **.**  You can view the status of the integration task in the task list.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3ef1718c0ce5f03367d6001c980b83f3.png) </span>

After the integration task is created, you can perform the following O&M operations:


* Click the **name of the task** to go to the task details page.

* Click **Edit** in the **Actions** column to edit the task.

* Click **Suspend task** in the **Actions** column to suspend the task.

* Click **Delete** in the **Actions** column to delete the integration task.


<span id="diRalLoY"></span>
## Monitoring information

<span id="fzOKePUX"></span>
### Query metrics

You can quickly query and display metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

<span id="AZS6XXRC"></span>
### Create dashboards

You can install Grafana in a VKE cluster or an ECS instance and then use Grafana to view metrics and create dashboards.


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id="6s5Jijau"></span>
### Configure alerts

You can configure alerts in the alerting center of VMP. For more details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).
