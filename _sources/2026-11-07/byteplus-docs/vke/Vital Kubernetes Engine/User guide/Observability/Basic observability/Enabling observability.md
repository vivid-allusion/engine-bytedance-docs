---
title: "Enabling observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability"
---

Cloud\-native basic observability provides fully managed, high\-performance, and highly stable cluster observability and alerting services. This topic introduces common concepts in basic observability and how to enable the cloud\-native basic observability feature.

<span id="sjIDZGHv"></span>
## Background

<span id="OlB2c9W3"></span>
### Metric scope

In VKE clusters, the metric scope for cloud\-native basic observability is divided into three tiers: basic, standard, and full metrics. This tiered design helps you make reasonable tradeoffs between observability scope, usage cost, and troubleshooting depth. The scope of the three tiers expands progressively, enabling you to select the observability level genuinely needed at the current stage, based on cluster scale, business complexity, and operational goals. This approach prevents initial over\-provisioning or observability insufficiency.


|Metric scope |Description |
|---|---|
|Basic |Basic metrics of the monitored object. They provide insights into the basic status of the object and resource usage. This option is suitable for initial observability setup or scenarios where the focus is on core operational health. |
|Standard | **[Recommended]**  Basic and important metrics of the monitored object. The combination of basic and important metrics provides a more comprehensive view of the object's status. This option is suitable for scenarios that require routine inspection, stability analysis, and regular issue identification. |
|Full |Basic, important, and advanced metrics of the monitored object. This tier includes all metrics of the monitored object. This option is suitable for scenarios that require high observability, in\-depth analysis, and complex troubleshooting based on comprehensive data. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The billing method and cost vary based on the observability metric scope and the VMP workspace's storage duration. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/pay-as-you-go">Pay\-as\-you\-go</a>.</div>


<span id="8hOkQPES"></span>
### Collectors

Cloud\-native basic observability is implemented on the [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus) service and uses the prometheus\-agent add\-on as the collector in clusters. The add\-on collects and monitors metrics for cluster infrastructure resources, control\-plane components, and custom applications. When you install the prometheus\-agent in your cluster, the system automatically deploys core add\-ons (such as vmagent, vmoperator, kube\-state\-metrics, and node\-exporter) and related custom resources (such as ServiceMonitor and PodMonitor). For details about the add\-on, see [prometheus-agent](https://docs.byteplus.com/en/docs/vke/prometheus-agent-add-on).

<span id="oyhDp1qE"></span>
## Common operations

<span id="li7zkcIU"></span>
### Enable basic observability


<Tabs>
<Tab zoneid="O9nhbdxH30" title="Enable for existing clusters">
<TabTitle>Enable for existing clusters</TabTitle>

To enable basic observability in an existing cluster, follow the steps below:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. Bind a VMP workspace.

   1. In the left navigation pane, click **Operation and maintenance configuration**. In the **Container observability** configuration section, click the **Configure now** link.

   2. In the pop\-up dialog box, select a VMP workspace to be bound to the cluster.

4. Install the collector add\-on.

   1. In the left navigation bar, click **Addons**.

   2. Click the **Monitoring** tab. Find the prometheus\-agent add\-on, hover over the add\-on card, and click **Deploy**. For add\-on configuration instructions, see [prometheus-agent](https://docs.byteplus.com/en/docs/vke/prometheus-agent-add-on).

5. Enable basic observability.

   1. In the left navigation pane, click **Cloud native observability** \> **Overview** to enter the service activation page.

   2. Click **Activate basic observability** to enable cloud\-native basic observability.

   3. (Optional) Configure observability enhancement. This option allows you to enable observability for major cluster add\-ons (such as core\-dns and vpc\-cn) with a click. You can also enable observability for individual add\-ons as needed. For details, see [Basic observability](https://docs.byteplus.com/en/docs/vke/Basic-observability).

   4. (Optional) Configure network and application observability. This feature monitors the network performance of workloads and the application performance of each interface, and generates a topology without modifying the application. Additionally, it can further trace interface calls with response errors or excessively long response times. For details, see [Enabling full-stack observability](https://docs.byteplus.com/en/docs/vke/Network-and-application-observability).


</Tab>
<Tab zoneid="T648RkuGMb" title="Enable when creating clusters">
<TabTitle>Enable when creating clusters</TabTitle>

In the **Cluster configuration** step of cluster creation, go to the **Operation and maintenance configuration** section, where you select the observability metric type and VMP workspace for the cluster, and set whether to enable observational enhancement. If you complete the settings, the system automatically installs the prometheus\-agent add\-on during cluster creation. For details, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).


</Tab>
</Tabs>


<span id="5k8vJqnx"></span>
### Modify the metric scope

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Modifying the metric scope will change the number of metrics collected in your cluster. Expanding the metric scope will incur additional costs. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/pay-as-you-go">Pay\-as\-you\-go billing</a>.</div>



1. In the left navigation bar of the cluster management page, click **Observability settings**.

2. In the upper\-right corner of the configuration page, click **Modify the default metric scope**.

3. In the pop\-up window, select the desired metric scope and check the **Instant effective for installed add\-ons** option.

4. Click **Confirm**.


<span id="6aspxsAV"></span>
### Change workspaces


1. In the left navigation pane of the cluster management page, click **Operation and maintenance configuration**.

2. In the **Container observability** configuration section, to the right of the **Prometheus workspace** field, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2e7231e96e2b591cdea9af98e0ff9f73.png) </span> to change the workspace.

3. In the pop\-up window, select the desired workspace and check the **I have been informed and agreed that the Prometheus workspace of the alert rule group will be revised and updated together** option.

4. Click **Confirm**.


<span id="OSk9dlH9"></span>
## Viewing observability configuration

After enabling cloud\-native basic observability, click **cloud\-native observability** \> **Overview** in the left navigation pane. Then, select the **Observability overview** tab to view the cluster observability overview.


* **Observability settings overview**: Displays the VMP workspace bound to the cluster and collector status.

* **Basic observability overview**: Displays the proportion of add\-ons with basic observability enabled in the cluster and the metric tier.

   
   |Parameter |Description |
   |---|---|
   |Enabled add\-ons |Displays the number of add\-ons that have observability enabled in the cluster and the total number of add\-ons that support observability. |
   |Default metric tier |Displays the metric scope for cluster observability. You can click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d417ad8b312a133f7a218c4920ca8072.png) </span> to modify the observability metric scope. |
   |Percentage of enabled basic metrics |The ratio of enabled basic metrics to all basic metrics for add\-ons that have observability enabled. You can click **Go to settings** to select or deselect metrics for the target add\-on. For details, see [Basic observability](https://docs.byteplus.com/en/docs/vke/Basic-observability). |
   |Percentage of enabled non\-basic metrics |The ratio of enabled non\-basic metrics to all non\-basic metrics for add\-ons for which observability is enabled. You can click **Go to settings** to select or deselect metrics for the target add\-on. For details, see [Basic observability](https://docs.byteplus.com/en/docs/vke/Basic-observability). |
   |Enhanced observability |The status of the observability enhancement feature. You can click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d417ad8b312a133f7a218c4920ca8072.png) </span> to enable or disable observability for major cluster add\-ons, such as core\-dns and vpc\-cni. You can also enable observability for individual add\-ons as needed. For details, see [Basic observability](https://docs.byteplus.com/en/docs/vke/Basic-observability).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A green add\-on mark in the console, for example, <img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c86735e1085f843181cdd12869bb365.png" width="68px" />, indicates that the add\-on is installed in the cluster.</div><br> |
   

* **Full\-stack observability overview**: Displays the status of the full\-stack observability feature. Click **Enable** to configure the full\-stack observability feature. For details, see [Enabling full-stack observability](https://docs.byteplus.com/en/docs/vke/Network-and-application-observability).


<span id="JtXUyWjj"></span>
## Viewing cluster overview

After you enable cloud\-native basic observability, you can view the cluster monitoring overview, including node status and workload performance overview.

<span id="LPXQ8Nge"></span>
### Node

The node section provides node status and resource usage for all nodes in the cluster.


* **Node status**: Displays cluster node statistics, including the total number of nodes in each of the following states: Ready, Not Ready, Disk pressure, Memory pressure, PID pressure, and Network unavailable.

* **Resource usage**: Displays the top 5 list of all nodes in the current cluster for metrics such as the CPU utilization, memory utilization, inbound network traffic, outbound network traffic, disk utilization, disk I/O saturation, file descriptor saturation, and inode saturation.

1. In the left navigation pane of the cluster management page, select **Cloud native observability** \> **Overview**. Then, select the **Monitoring overview** tab.

2. In the **Node** section, view cluster node information.


<span id="lwAVWUSP"></span>
### Application performance overview

The application performance overview provides performance information for all workloads in the cluster, such as the error rates and response time (P90).


1. In the left navigation pane of the cluster management page, select **Cloud native observability** \> **Overview**. Then, select the **Monitoring overview** tab.

2. In the **Workload performance overview** section, view the workload performance information.
