---
title: "SGLang integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/SgLang_Integration"
---

Vital Managed Service for Prometheus (VMP) allows you to monitor SGLang instances that are deployed in Vital Kubernetes Engine (VKE) clusters.

<span id="miYhAd4C"></span>
## Background

SGLang serves as a fast serving framework for large language models (LLMs) and vision language models. SGLang makes your interaction with models faster and more controllable by co\-designing the backend runtime and frontend language. SGLang provides the following core features:


* **Fast backend runtime**: provides efficient serving with RadixAttention for prefix caching, jump\-forward constrained decoding, continuous batching, paged attention, tensor parallelism, FlashInfer kernel, and quantization (AWQ/FP8/GPTQ/Marlin).

* ****Flexible frontend language: offers an intuitive interface for programming LLM applications, including chained generation calls, advanced prompting, control flow, multi\-modal inputs, parallelism, and external interactions.


You can use VMP to monitor SGLang instances that are deployed in VKE clusters to achieve key metric alerting and optimization.

<span id="wwQazlQX"></span>
## Prerequisites


* VMP

   * A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* VKE

   * VKE has been activated.

   * A cluster has been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * An SGLang instance is deployed in the cluster.

   * Cloud native observability has been enabled for the cluster, and prometheus\-agent has been installed in the cluster. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The VMP workspace and the VKE cluster must be deployed in the same region.</div>


<span id="36F7raOo"></span>
## Procedure

<span id="75p0dHF3"></span>
### Configure an integration task


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Integration Center \> Component**. On the page that appears, click **SGLang** to configure the integration task.

4. Configure the deployment environment of the collector. Click **VKE environment** and select an associated cluster.

5. Click **Create Integration Task** to specify the details of the integration task.

   
   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |Task name |Specify the name of the integration task. |
   |**Scrape configuration** ||
   |JobLabel |You can select labels from Kubernetes Pod objects, and the label value will be used as the job label for all metrics.<br><br>**For example**, if you set the JobLabel parameter to `foo` and the Pod label is `foo: bar`, the system will add a `job="bar"` label to all collected metrics. If this parameter is left empty, the default job label for the metrics consists of the namespace and name of the PodMonitor object, which is in the format `<namespace>/<name>`. |
   |Metric scraping interval |Configure the collection interval of the collector. |
   |Namespace |Specify the namespace where the collection target is deployed in the cluster. Values:<br><br><br>* **arbitrary**: indicates that metrics of resources in any namespace in the cluster can be collected.<br><br>* **custom**: indicates that you can specify custom namespaces in the cluster, and only metrics of resources in the specified namespaces can be collected. For example, if you set the value to `default`, only metrics of resources in the default namespace can be collected. |
   |Metric acquisition port |Configure the metric port for the collection target. You can set the value to a port name or a port number. |
   |Metric acquisition path |Configure the metric path of the collection target. |
   | LabelSelector |Select collection targets by using the labels of Kubernetes Pod objects. |
   |**Advanced configuration** ||
   |Metric Relabel configuration |Configure metric relabeling. For more details, refer to [Metric relabeling](https://docs.byteplus.com/en/docs/vmp/Metric_relabel). |
   

6. Click **Confirm** to complete the configuration.


<span id="MnbdawDh"></span>
### Obtain monitoring dashboards

Click the **Effect preview** tab to view sample monitoring dashboards. Click **Get the Grafana template** to download the Grafana monitoring dashboard template in JSON format.

<span id="wOqF6HLK"></span>
### Query metrics

Click the **Acquisition metric** tab to view the list of metrics for the collection targets.

<span id="fcC04eZm"></span>
### View preset alerts

Click **the Alert tem**plate tab to view the preset alert templates for SGLang. Click **Turn on alert**. You are redirected to the alert group creation page, where you can swiftly create and enable alerts based on the current alert template.

<span id="JQ9Tywwp"></span>
## Validate results

After the configuration is complete, you can view the status and details of the task. Check whether the integration task is running as expected.


1. In the left navigation bar, click **Access center \> Access task**.

2. Click **VKE environment** **.**  You can view the status of the integration task in the task list.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_40e5ef285394bbb9b836d7b689011302.png) </span>

After the integration task is created, you can perform the following O&M operations:


* Click the **name of the task** to go to the task details page.

* Click **Edit** in the **Actions** column to edit the task.

* Click **Suspend task** in the **Actions** column to suspend the task.

* Click **Delete** in the **Actions** column to delete the integration task.


<span id="H81Q8Jkx"></span>
## Monitoring information

<span id="5rniLEnF"></span>
### Query metrics

You can quickly query and display metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

<span id="0vxbawph"></span>
### Create dashboards

You can install Grafana in a VKE cluster or an ECS instance and then use Grafana to view metrics and create dashboards.


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id="Px8zieFm"></span>
### Configure alerts

You can configure alerts in the alerting center of VMP. For more details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).
