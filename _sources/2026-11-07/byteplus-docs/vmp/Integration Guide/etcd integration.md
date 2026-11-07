---
title: "etcd integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ETCD_integration"
---

Vital Managed Service for Prometheus (VMP) allows you to monitor ETCD instances that are deployed in Vital Kubernetes Engine (VKE) clusters.

<span id="jgaPcrht"></span>
## Background

ETCD is an open source, distributed, consistent key\-value store used for shared configuration, service discovery, and scheduler coordination of distributed systems or machine clusters. ETCD helps facilitate more secure automatic updates, coordinates work being scheduled to hosts, and assists in setting up the container overlay networking.

You can use VMP to monitor core metrics such as the status of ETCD nodes deployed in VKE clusters, data consistency, request latency, and storage performance in real time. This ensures the stability of distributed system configuration management and service discovery.

<span id="XWZJ36Ui"></span>
## Prerequisites


* VMP

   * A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* VKE

   * VKE has been activated.

   * A cluster has been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * An ETCD instance is deployed in the cluster.

   * Cloud native observability has been enabled for the cluster, and prometheus\-agent has been installed in the cluster. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The VMP workspace and the VKE cluster must be deployed in the same region.</div>


<span id="tII1YJoW"></span>
## Procedure

<span id="GSAt578a"></span>
### Configure an integration task


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Integration Center \> Component**. On the page that appears, find and click **ETCD** to configure the integration task.

4. Configure the deployment environment of the collector. Click **VKE environment** and select an associated cluster.

5. Click **Create Integration Task** to specify the details of the integration task.

   
   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |Task name |Specify the name of the integration task. It can contain Chinese characters, letters (uppercase and lowercase), digits, and underscores (`_`), and must be 1 to 40 characters in length. |
   |**Scrape configuration** ||
   |JobLabel |You can select labels from Kubernetes Pod objects, and the label value will be used as the job label for all metrics. For example, if you set the JobLabel parameter to `foo` and the Pod label is `foo: bar`, the system will add a `job="bar"` label to all collected metrics. If this parameter is left empty, the default job label for the metrics consists of the namespace and name of the PodMonitor object, which is in the format `<namespace>/<name>`. |
   |Metric scraping interval |Configure the collection interval of the collector. |
   |Namespace |Configure the namespace where the collection target is deployed in the cluster. Values:<br><br><br>* **arbitrary**: indicates that metrics of resources in any namespace in the cluster can be collected.<br><br>* **custom**: indicates that you can specify custom namespaces in the cluster, and only metrics of resources in the specified namespaces can be collected. For example, if you set the value to `default`, only metrics of resources in the default namespace can be collected. |
   |Metric acquisition port |Configure the metric port for the collection target. You can set the value to a port name or a port number. |
   |Metric acquisition path |Configure the metric path of the collection target. |
   | LabelSelector |Select collection targets by using the labels of Kubernetes Pod objects. |
   |**Advanced configuration** ||
   |Metric Relabel configuration |Configure metric relabeling. For more details, refer to [Metric relabeling](https://docs.byteplus.com/en/docs/vmp/Metric_relabel). |
   

6. Click **Confirm** to complete the configuration.


<span id="zR4dxGFw"></span>
### Obtain monitoring dashboards

Click the **Effect preview** tab to view sample monitoring dashboards. Click **Get the Grafana template** to download the Grafana monitoring dashboard template in JSON format.

<span id="aFYTJ9ET"></span>
### Query metrics

Click the **Acquisition metric** tab to view the list of metrics for the collection targets.

<span id="ajPkFNre"></span>
### View preset alerts

Click the **Alert template** tab to view the preset alert templates for ETCD. Click **Turn on alert**. You are redirected to the alert group creation page, where you can swiftly create and enable alerts based on the current alert template.

<span id="ofLEnR4V"></span>
## Validate results

After the configuration is complete, you can view the status and details of the integration task to check whether the task is running as expected.


1. In the left navigation bar, click **Integration Center \> Integration task**.

2. Click **VKE environment** **.**  You can view the status of the integration task in the task list.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4b72fc4119199ac89b5c1c060113820d.png) </span>

After the integration task is created, you can perform the following O&M operations:


* Click the **name of the task** to go to the task details page.

* Click **Edit** in the **Actions** column to edit the task.

* Click **Suspend task** in the **Actions** column to suspend the task.

* Click **Delete** in the **Actions** column to delete the integration task.


<span id="mogYnyrT"></span>
## Monitoring information

<span id="dCQMS13o"></span>
### Query metrics

You can quickly query and display metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

<span id="FHINMBvw"></span>
### Create dashboards

You can install Grafana in a VKE cluster or an ECS instance and then use Grafana to view metrics and create dashboards.


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id="4jSmAmNM"></span>
### Configure alerts

You can configure alerts for Nacos instances in the Alert Center of VMP. For details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).
