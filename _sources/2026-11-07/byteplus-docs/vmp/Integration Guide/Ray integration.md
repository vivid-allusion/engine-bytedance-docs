---
title: "Ray integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Ray_Integration"
---

Vital Managed Service for Prometheus (VMP) allows you to monitor Ray instances that are deployed in Vital Kubernetes Engine (VKE) clusters.

<span id="96vg5L5t"></span>
## Background

Ray is a distributed computing framework developed by RISELab at the University of California, Berkeley. It provides a parallel\-processing computing layer for machine learning and big data programs, reducing the difficulty of developing large\-scale end\-to\-end machine learning workflows.

You can use VMP to monitor the metrics of Ray instances deployed in VKE clusters. The metrics include the usage of cluster node resources (such as CPU, GPU, and memory), task execution latency and success rate, actor status, distributed storage performance, and other metrics. This way, you can improve the running efficiency and reliability of tasks such as distributed training and reinforcement learning, and achieve key metric alerting and optimization.

<span id="POUtTUK0"></span>
## Prerequisites


* VMP

   * A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* VKE

   * VKE has been activated.

   * A cluster has been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * A Ray instance is deployed in the cluster.

   * Cloud native observability has been enabled for the cluster, and prometheus\-agent has been installed in the cluster. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The VMP workspace and the VKE cluster must be deployed in the same region.</div>


<span id="VePJi0Uv"></span>
## Procedure

<span id="9hf9OH5w"></span>
### Configure an integration task


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click Integration **Center \> Component**. On the page that appears, find and click **Ray** to configure the integration task.

4. Configure the deployment environment of the collector. Click **VKE environment** and select an associated cluster.

5. Click **Create Integration Task** to specify the details of the integration task.



&nbsp;


|Parameter |Description |
|---|---|
|**Basic information** ||
|Task name |Specify the name of the integration task. |
|**Acquisition configuration** ||
|Metric scraping interval |Configure the collection interval of the collector. |
|JobLabel |You can select labels from Kubernetes Pod objects, and the label value will be used as the job label for all metrics.<br><br>**For example**, if you set the JobLabel parameter to `foo` and the Pod label is `foo: bar`, the system will add a `job="bar"` label to all collected metrics. If this parameter is left empty, the default job label for the metrics consists of the namespace and name of the PodMonitor object, which is in the format `<namespace>/<name>`. |
|Namespace |Specify the namespace where the collection target is deployed in the cluster. Values:<br><br><br>* **arbitrary**: indicates that metrics of resources in any namespace in the cluster can be collected.<br><br>* **custom**: indicates that you can specify custom namespaces in the cluster, and only metrics of resources in the specified namespaces can be collected. For example, if you set the value to `default`, only metrics of resources in the default namespace can be collected. |
| LabelSelector |Select collection targets by using the labels of Kubernetes Pod objects. |


6. Click **Confirm** to complete the configuration.


<span id="sUESnVqY"></span>
### Obtain monitoring dashboards

Click the **Effect preview** tab to view sample monitoring dashboards. Click **Get the Grafana template** to download the Grafana monitoring dashboard template in JSON format.

<span id="dTWNA97y"></span>
### Query metrics

Click the **Acquisition metric** tab to view the list of metrics for the collection targets.

<span id="cOd3hoZl"></span>
### View preset alerts

Click the **Alert template** tab to view the preset alert templates for Ray. Click **Turn on alert**. You are redirected to the alert group creation page, where you can swiftly create and enable alerts based on the current alert template.

<span id="5KNFfgUW"></span>
## Validate results

After the configuration is complete, you can view the status and details of the integration task to check whether the task is running as expected.


1. In the left navigation bar, click **Integration Center \> Integration task**.

2. Click **VKE environment** **.**  You can view the status of the integration task in the task list.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4ba21d9d8dee3ff5ff52f2bb909c02d.png) </span>

After the integration task is created, you can perform the following O&M operations:


* Click the **name of the task** to go to the task details page.

* Click **Edit** in the **Actions** column to edit the task.

* Click **Suspend task** in the **Actions** column to suspend the task.

* Click **Delete** in the **Actions** column to delete the integration task.


<span id="j3kcuiKV"></span>
## Monitoring information

<span id="q61DTFH5"></span>
### Query metrics

You can quickly query and display metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

<span id="iE8ABEF6"></span>
### Create dashboards

You can install Grafana in a VKE cluster or an ECS instance and then use Grafana to view metrics and create dashboards.


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id="EY3VteNb"></span>
### Configure alerts

You can configure alerts in the alerting center of VMP. For more details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).
