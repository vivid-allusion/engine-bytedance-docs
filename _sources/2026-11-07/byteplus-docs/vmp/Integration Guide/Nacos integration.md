---
title: "Nacos integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Nacos_Integration"
---

Vital Managed Service for Prometheus (VMP) allows you to monitor Nacos instances that are deployed in Vital Kubernetes Engine (VKE) clusters.

<span id="KNdW1EG7"></span>
## Background

Provided by Alibaba, Nacos is an open source platform used for dynamic service discovery, configuration management, and service management, which is dedicated to building microservice architectures. Nacos integrates features such as service registration and discovery, configuration management, and service governance, and supports Domain Name System (DNS) and Remote Procedure Call (RPC) service discovery. In addition, it provides capabilities such as dynamic configuration management and service routing for quick deployment and elastic scaling of applications. Nacos is widely used in distributed systems.

You can use VMP to monitor Nacos instances that are deployed in VKE clusters to achieve key metric alerting and optimization.

<span id="ZEfYioTK"></span>
## Prerequisites


* VMP

   * A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* VKE

   * VKE has been activated.

   * A cluster has been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * A Nacos instance is deployed in the cluster.

   * Cloud native observability has been enabled for the cluster, and prometheus\-agent has been installed in the cluster. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The VMP workspace and the VKE cluster must be deployed in the same region.</div>


<span id="80LxLI1z"></span>
## Procedure

<span id="mYSoUeDm"></span>
### Configure an integration task


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Integration Center \> Component**. On the page that appears, click **Nacos** to configure the integration task.

4. Configure the deployment environment of the collector. Click **VKE environment** and select an associated cluster.

5. Click **Create Integration Task** to specify the details of the integration task.

   
   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |Task name |Specify the name of the integration task. |
   |**Scrape configuration** ||
   |JobLabel |You can select labels from Kubernetes Pod objects, and the label value will be used as the job label for all metrics.<br><br>**For example**, if you set the jobLabel parameter to `foo` and the Pod label is `foo: bar`, the system will add a `job="bar"` label to all collected metrics. If this parameter is left empty, the default job label for the metrics consists of the namespace and name of the PodMonitor object, which is in the format `<namespace>/<name>`. |
   |Metric scraping interval |Specify the collection interval of the collector. The value must be an integer. Valid values: 1 to 600 in seconds. |
   |Namespace |Specify the namespace where the collection target is deployed in the cluster. Values:<br><br><br>* **arbitrary**: indicates that metrics of resources in any namespace in the cluster can be collected.<br><br>* **custom**: indicates that you can specify custom namespaces in the cluster, and only metrics of resources in the specified namespaces can be collected. For example, if you set the value to `default`, only metrics of resources in the default namespace can be collected. |
   |Metric acquisition port |Configure the metric port for the collection target. You can set the value to a port name or a port number. |
   |Metric acquisition path |Configure the metric path of the collection target. |
   | LabelSelector |Select collection targets by using the labels of Kubernetes Pod objects. |
   |**Advanced configuration** ||
   |Metric Relabel configuration |Configure metric relabeling. For more details, refer to [Metric relabeling](https://docs.byteplus.com/en/docs/vmp/Metric_relabel). |
   

6. Click **Confirm** to complete the configuration.


<span id="YLlHmA7u"></span>
### Obtain monitoring dashboards

Click the **Effect preview** tab to view sample monitoring dashboards. Click **Get the Grafana template** to download the Grafana monitoring dashboard template in JSON format.

<span id="AZeqtQBo"></span>
### Query metrics

Click the **Acquisition metric** tab to view the list of metrics for the collection targets.

<span id="9rmnxS6j"></span>
### View preset alerts

Click the **Alert template** tab to view the preset alert templates for Nacos. Click **Turn on alert**. You are redirected to the alert group creation page, where you can swiftly create and enable alerts based on the current alert template.

<span id="9rmnxS6j"></span>
## Validate results

After the configuration is complete, you can view the status and details of the integration task to check whether the task is running as expected.


1. In the left navigation bar, click **Integration Center \> Integration task**.

2. Click **VKE environment** **.**  You can view the status of the integration task in the task list.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2e4026a8fce6df7e5e3d75cd27cf03c1.png) </span>

After the integration task is created, you can perform the following O&M operations:


* Click the **name of the task** to go to the task details page.

* Click **Edit** in the **Actions** column to edit the task.

* Click **Suspend task** in the **Actions** column to suspend the task.

* Click **Delete** in the **Actions** column to delete the integration task.


<span id="xSEpy8Fr"></span>
## Monitoring information

<span id="SMNVC9x1"></span>
### Query metrics

You can quickly query and display metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

<span id="sKttnEz2"></span>
### Create dashboards

You can install Grafana in a VKE cluster or an ECS instance and then use Grafana to view metrics and create dashboards.


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id="9a0oIvY2"></span>
### Configure alerts

You can configure alerts for Nacos instances in the Alert Center of VMP. For details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).
