---
title: "Cluster topologies"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cluster-topology"
---

Cluster topologies provide network topology information for workload resources in clusters. This topic describes how to view cluster topologies.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Cloud\-native observability has been enabled. For details, see [Enabling cloud-native observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* Network and application observability has been enabled. For details, see [Enabling full-stack observability](https://docs.byteplus.com/en/docs/vke/Network-and-application-observability).

* To ensure that topology charts can be displayed as expected, you need to configure the following eBPF metrics. For details, see [Enabling full-stack observability](https://docs.byteplus.com/en/docs/vke/Network-and-application-observability).

   * For network metrics, you need to select at least the **inbound traffic**, **outbound traffic**, and **packet loss** metrics.

   * For application metrics, you need to enable at least one of **HTTP** or **DNS**.


<span id=".5p-l55yL5ouT5omR"></span>
## Viewing topologies


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster.

4. In the left navigation bar of the cluster management page, click **Monitoring center** \> **Cluster topology**. View the topology charts of workload resources.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a24af03f634dffc743f2cd17a2059be.png) </span>

The following table describes the operations that you can perform in the topology chart.


|No. |Description |
|---|---|
|① |Select the namespace for which you want to view its resource topologies from the **Namespace** drop\-down list. |
|② |Specify a query time period, and you can manually refresh the topology chart. |
|③ |Collect statistics. The number of different types of workloads is summarized and displayed in the topology chart. |
|④ |Search for information in the topology chart. You can search for nodes in the topology chart by name and type. Nodes that meet the criteria will be highlighted. |
|⑤ |Edit the topology chart. You can zoom in, zoom out, auto\-fit, and configure display settings for the topology chart. |


<span id=".6YWN572u5ouT5omR"></span>
## Configuring topologies

In the topology chart, you can specify the metric thresholds and colors for nodes and connections. You can use colors to highlight nodes or connections that require special attention.

On the right side of the topology chart, click the edit icon. In the configuration panel that appears, configure the metric thresholds and colors for nodes and connections.


|Parameters |Description |
|---|---|
|Node display settings |* Click **Node display metrics** to enable node color configuration. If you disable this configuration, nodes will not be marked with colors.<br><br>* Select the type of node metric from the **Metric type** drop\-down list. The types include error rate, average response time, and QPS.<br><br>* Configure colors for different thresholds in the **Node color** section. |
|Connection display settings |* Click **Connect display metrics** to enable connection color configuration. If you disable this configuration, connections will not be marked with colors.<br><br>* Select the type of node metric from the **Metric type** drop\-down list. The types include error rate and average response time.<br><br>* Configure colors for different thresholds in the **Connect color** section. |


<span id=".5p-l55yL6IqC54K56L-e57q_"></span>
## Viewing node connections


1. In the topology chart, move the pointer over the connection between nodes to view the overview information of the networks between two applications. The information includes the error rate, P90 response time, average response time, and QPS.

2. Click a connection. In the panel that appears, you can view the details about the networks between the two applications. The details include:

   * Click the **Network performance observability** tab to view network metrics, such as TCP network traffic, network packet loss, TCP retransmissions, and the number of TCP connections.

   * Click the **Application performance observability** tab to view application metrics, including HTTP metrics and DNS metrics.


<span id=".5p-l55yL5bqU55So"></span>
## Viewing applications


1. In the topology chart, move the pointer over a node to view its application overview information. The information includes the workload type, namespace, error rate, average response time, P90 response time, QPS, and other information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Click <strong>View resource details</strong> to go to the resource monitoring page and view resource details. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-explore">Resource retrieval</a>.   </div>
   

2. Click a node to view the details of the application in the pop\-up page.

   * Application overview: Includes the number of ready pods, the number of updated pods, the number of available pods, running time, and other information.

   * Click the **Basic monitoring** tab to view the basic resource metrics of the application, such as CPU usage and memory usage.

   * Click the **Application performance observability** tab to view the performance metrics of the application when it functions as a server or client under different protocols (such as HTTP(S) and DNS). The metrics include QPS, P90 response latency, and other metrics. In the span list, you can view the information about the application, such as call results, status code, and response latency.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If you set the Storage configuration parameter of full\-stack observability to APMPlus, you can click APMPlus in the <strong>Actions</strong> column to go to the APMPlus console and view the trace monitoring information of the application.      </div>
      

   * Click the **Network performance observability** tab to view the network metrics of the application when it functions as a server or client. The metrics include TCP network traffic, TCP packet loss, UDP network traffic, the number of UDP packets, and other metrics.
