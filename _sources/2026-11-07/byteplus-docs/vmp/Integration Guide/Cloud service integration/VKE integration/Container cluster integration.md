---
title: "Container cluster integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/cluster-monitoring"
---

The cloud native observability feature provides O&M\-free, high\-performance, and high\-stability cluster observability and alerting services. This topic describes how to enable the cloud native observability feature for a cluster.

<span id="DzgrIL6u"></span>
## Background

The cloud native observability feature is achieved based on Vital Managed Service for Prometheus (VMP), which uses prometheus\-agent to achieve basic cluster resource observability. Therefore, before you enable the cloud native observability feature, you need to first create a VMP workspace and install the prometheus\-agent in the cluster.

<span id="Y464F17Y"></span>
### Collector

The cloud native observability feature uses the prometheus\-agent as the collector for observing basic cluster resources. When you install the prometheus\-agent in the cluster, the vm\-agent, vmoperator, kube\-state\-metrics, and node\-exporter agents are also installed. The following table describes the name, type, and feature of each agent.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When you use the prometheus\-agent, it is recommended to perform the following operations:</div>



* <div data-tips="true" data-tips-type="default">Upgrade the agent to the latest version.</div>


* <div data-tips="true" data-tips-type="default">Enable automatic scaling to prevent issues such as the out\-of\-memory (OOM) error with the agent as the scale increases.</div>




|Agent Name |Workload Type |Namespace |Description |
|---|---|---|---|
|vmagent\-prometheus\-agent |StatefulSet |kube\-system |The collector agent that collects metrics exposed by kubelet, kubelet\-cadvisor, kube\-state\-metrics, node\-exporter, dcgm, ingress\-nginx, and p2p\-accelerator in the cluster. |
|prometheus\-agent\-vmoperator |Deployment |kube\-system |The controlling agent of vm\-agent. |
|prometheus\-agent\-kube\-state\-metrics |StatefulSet |kube\-system |Provides the metric data of Kubernetes resources. |
|prometheus\-agent\-node\-exporter |DaemonSet |kube\-system |Provides the metric data of node resources. |


<span id="0kfuMWsf"></span>
### Recommended specifications

The prometheus\-agent allows you to specify its resources and number of shards. The number of shards and specifications of the agent are related to the cluster size. You can specify the initial (minimum) number of shards for the agent based on the cluster size.

The following table shows the recommended initial (minimum) number of shards for the vm\-agent collector and the kube\-state\-metrics agent in clusters of different sizes.


|Cluster Scale |vm\-agent Initial (Minimum) Number of Shards |kube\-state\-metrics Initial (Minimum) Number of Shards |
|---|---|---|
|10 nodes and 500 pods |1 |1 |
|100 nodes and 5,000 pods |2 |2 |
|200 nodes and 10,000 pods |4 |4 |
|500 nodes and 25,000 pods |10 |10 |


<span id="lMpM30LL"></span>
## Prerequisites


* A cluster has been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).


<span id="xZtFlAse"></span>
## Procedure

<span id="GlrZF7fh"></span>
### Step 1: Bind the cluster to the workspace


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the top navigation bar, select the region where your business is located.

3. In the left navigation pane, click **Cluster**. On the page that appears, find the target cluster and click the cluster name.

4. On the **Overview** page, click the **Operation and maintenance configuration** tab. Click **Configure** on the Operation and maintenance configuration tab.

5. In the Configure Prometheus workspace dialog box, select a VMP workspace to bind to the cluster.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also bind a VMP workspace to a cluster when you create the cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-cluster">Creating clusters</a>.   </div>
   

<span id="Iv1yRUuS"></span>
### Step 2: Deploy the collector


1. In the left navigation pane, click **Addons**.

2. Click the **Monitoring** tab, find the prometheus\-agent add\-on, and then click the `...` icon next to the add\-on \> **Install**.

3. Configure the parameters of the agent.

   * Configure the requirements for agent resources.

      
      |Parameters |Description |
      |---|---|
      |Deployment Method |The deployment method of the agent. The parameter is fixed and cannot be specified. |
      |Deployment form |This parameter is available in the cluster with the network model **VPC\-CNI**. You can deploy the agent on the following two types of nodes:<br><br><br>* **ECS deployment**: The agent is deployed on the Elastic Compute Service (ECS) node in the cluster.<br><br>* **VCI deployment**: The agent is deployed on Vital Container Instance (VCI), which is a virtual node in the cluster. Fees will be incurred when you deploy agents on VCI. For detailed billing information, see [Billing overview](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
      |vm\-agent resource |Configure the default resources of the vm\-agent collector, including the CPU requests, CPU upper limit, memory request, and memory upper limit. |
      |kube\-state\-metrics Resource configuration |Configure the default resource configurations of the kube\-state\-metrics agent, including the CPU request, CPU upper limit, memory request, and memory upper limit.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Due to the constraints of the kube\-state\-metrics agent (For example, the number of targets that an agent can collect is limited), it is recommended to increase the number of shards to enhance the metric collection capability of the kube\-state\-metrics agent in a large\-scale cluster.</div><br> |
      

   * Configure the initial number of shards and scaling for the agent.

      
      |Parameters |Description |
      |---|---|
      |vm\-agent initial sharding number |Specify the initial number of shards for the vm\-agent collector. |
      |kube\-state\-metrics Initial sharding |Specify the initial number of shards for the kube\-state\-metrics agent. |
      |Addon scaling |Specify whether to enable the automatic scaling feature for the vm\-agent collector and the kube\-state\-metrics agent.<br><br><br>* **Disable**: The number of shards for the agent is the specified initial number of shards. The agent will not be automatically scaled out as resource usage increases.<br><br>* **Enable**: You need to specify the maximum number of shards for the agent. The agent will be automatically scaled based on resource usage by the following rules:<br><br>   * **vm\-agent scale\-out**: vm\-agent is automatically scaled out when CPU or memory usage is greater than 70%.<br><br>   * **vm\-agent scale\-in**: vm\-agent is automatically scaled in when CPU and memory usage are less than 30%.<br><br>   * **kube\-state\-metrics scale\-out**: kube\-state\-metrics is automatically scaled out when CPU or memory usage is greater than 70%.<br><br>   * **kube\-state\-metrics scale\-in**: kube\-state\-metrics is automatically scaled in when CPU and memory usage are less than 70%.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The cooldown period of vm\-agent scaling is 30 minutes. kube\-state\-metrics is scaled through HorizontalPodAutoscaler.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After you enable the automatic scaling feature for the agent, ensure that cluster resources are sufficient. Otherwise, the agent scale\-out may fail caused by insufficient resources.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you scale out the vm\-agent collector and the kube\-state\-metrics agent, it is recommended to specify the number of shards for the kube\-state\-metrics agent as an integer multiple of the number of shards for the vm\-agent collector to ensure load balancing. For example, maintain a <code>1:1</code> or <code>2:1</code> ratio of the <code>number of shards for the kube-state-metrics agent</code> to the <code>number of shards for the vm-agent collector</code>.</div><br> |
      |Deploy agents |Specify whether to install the **node\-exporter** agent at the same time. The agent is installed by default. The agent is used to collect various software and hardware metrics of the node operating system. If the agent is not installed, node metrics cannot be monitored. It is recommended to use the default value.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <strong>node\-exporter</strong> agent is deployed as a Daemonset. Therefore, when you install the agent on VCI, the agent will be deployed on an ECS node. For more information, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-limits">VCI limits</a>.</div><br> |
      

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When the prometheus\-agent add\-on is at version <strong>v2.0.1 or earlier</strong>, you also need to configure the VMP workspace of the add\-on, as well as the authentication username and password for the workspace.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When you configure the workspace of the agent, ensure it is the workspace that is bound to the cluster. Otherwise, you will not be able to view the metrics and dashboards of the cluster on the <strong>Dashboard</strong> page in the VKE console.      </div>
      

   * Advanced configurations (The version of the prometheus\-agent needs to be v2.10.0 or later.)

      
      |Parameters |Description |
      |---|---|
      |Discovery Role |Specify whether to use the Endpoints role or the EndpointSlices role for service discovery. By default, a single Endpoints supports up to 1,000 backends. Kubernetes 1.21 or later introduces [EndpointSlices](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/) resources to avoid this issue. Therefore, Prometheus also supports [service discovery](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#endpointslice) through EndpointSlices.<br><br>The default value is EndpointSlices. If the Kubernetes version is earlier than 1.21, Endpoints is automatically used. |
      |Global Labels |The fixed labels which are added by the prometheus\-agent collector to all collected metrics by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Global labels take effect only on metrics collected by prometheus\-agent. The metrics of the control plane agent for Vital Kubernetes Engine (VKE) such as kube\-apiserver are reported by the agent and will not be modified.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you add or modify global labels, active time series will increase within 1 hour. If the metric scale is large, you need to assess whether the limit of active time series will be reached. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/workspaces-types">Workspaces specifications</a>.</div><br><br><br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><br>* <div data-tips="true" data-tips-type="danger">The default extra label that is automatically added is <code>cluster:<Cluster ID></code>. It is not recommended to override the label, which is a system reserved field.</div><br><br><br>* <div data-tips="true" data-tips-type="danger">If you want to add labels such as the cluster name, we recommend using a label similar to <code>cluster_name</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="danger">If you enter the cluster label, it will override the system reserved field, which may cause the following impacts:</div><br><br><br>   * <div data-tips="true" data-tips-type="danger">Some panels may fail to display metrics on the monitoring dashboard of VKE.</div><br><br><br>   * <div data-tips="true" data-tips-type="danger">Alert rules that are created based on some alert templates may become invalid due to changes in the <code>cluster=~"$Cluster"</code> label.</div><br> |
      |Secret access |kube\-state\-metrics will generate related metrics only if the Secret permissions are contained in ClusterRole. |
      

4. Click **Add** to complete the configuration.


<span id="mPBHe14A"></span>
### Step 3: Enable the cloud native observability feature


1. On the details page of the cluster, click **Cloud native observability** \> **Overview** in the left navigation pane to go to the feature enabling page.

2. Click **Enable basic observability** to enable the cloud\-native observability service.

3. (Optional) Enable enhanced observability. You can enable observability for major agents in the cluster with a few clicks, including core\-dns, vpc\-cni, and ingress\-nginx. You can also enable observability for a single agent based on your business requirements. For more details, refer to [basic observation](https://docs.byteplus.com/en/docs/vke/Basic-observability).

4. (Optional) Observe networks and applications. You can use this feature to observe the network performance of workloads and application performance of various interfaces and to generate topologies, without intruding into the applications. In addition, you can further track interface calls with response errors or prolonged response time. For more details, refer to [Open full stack observation](https://docs.byteplus.com/en/docs/vke/Network-and-application-observability).


<span id="nllHgseG"></span>
## Validate results

<span id="U5Utkn9e"></span>
### View observability configurations

After you enable the cloud\-native observability feature, you can click the **Observability overview** tab to view the cluster observability overview information, including:


* **Observability settings overview**: Displays the VMP workspaces bound to the cluster and the status of the collection add\-ons.

* **Basic observability overview**: Displays the proportion of add\-ons with basic observability enabled in the cluster and the metric scope. See the following table for details.



|Parameter |Description |
|---|---|
|Default metric scope |Configure the observability metric scope in the cluster. Valid values:<br><br><br>* **Basic**: The basic metrics of the monitoring object, which are used to observe the basic status and resource usage of the object.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you use a VMP workspace with a <strong>15\-day</strong> storage duration, basic metrics are free of charge. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/pay-as-you-go">Pay\-as\-you\-go</a>.   </div><br>   <br><br>* **Standard**: (Recommended) The basic metrics and important metrics of the monitoring object. In addition to basic metrics, standard metrics also include commonly used important metrics of the observability object, which can obtain more comprehensive status information of the observability object.<br><br>* **Full set of metrics**: All metrics of the observability object that include basic metrics, important metrics, and advanced metrics. |
|Percentage of enabled basic metrics |The activation rate of basic metrics for all enabled add\-ons. You can click **Go to settings** to select or deselect metrics to collect for the target add\-on. For details, see [Basic observability](https://docs.byteplus.com/en/docs/vke/Basic-observability). |
|Percentage of enabled non\-basic metrics |The activation rate of non\-basic metrics for all enabled add\-ons. You can click **Go to settings** to select or deselect metrics to collect for the target add\-on. For details, see [Basic observability](https://docs.byteplus.com/en/docs/vke/Basic-observability). |
|Enhanced observability |The status of the enhanced observability feature. You can click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d417ad8b312a133f7a218c4920ca8072.png) </span>icon to enable or disable observability for primary add\-ons in the cluster with a few clicks, such as core\-dns, vpc\-cni, and ingress\-nginx. You can also enable observability for a single agent based on your business requirements. For more details, refer to [basic observation](https://docs.byteplus.com/en/docs/vke/Basic-observability).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If an add\-on is marked in green in the console, such as <img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c86735e1085f843181cdd12869bb365.png" width="68px" />, it indicates that the add\-on is installed in the cluster.</div><br> |



* **Full\-stack observability overview**: Displays the status of the full\-stack observability feature. You can click **Enable** to configure the full\-stack observability feature. For details, see [Enabling full-stack observability](https://docs.byteplus.com/en/docs/vke/Network-and-application-observability).


<span id="HeqgvRVz"></span>
### View the cluster overview

After you enable the cloud native observability feature, you can view the cluster overview information, including node running status and workload application performance overview.

<span id="damvFRfz"></span>
#### Node

The Node section displays the status and resource usage of all nodes in the cluster.


* **Node status**: displays the statistics on nodes of the current cluster including the number of nodes in the following states: Ready, Not ready, Disk pressure, Memory pressure, PID pressure, and Network unavailable.

* **Resource usage**: displays the Top 5 lists of metrics such as CPU usage, memory usage, network inbound traffic, network outbound traffic, disk usage, disk IO saturation, file descriptor saturation, and inodes saturation of all nodes in the current cluster.

1. On the details page of the cluster, click **Cloud native observability** \> **Overview** in the left navigation pane. Then, click the **Monitoring overview** tab.

2. In **Node** section, view the monitoring information of the cluster nodes.


<span id="C29wkVEE"></span>
#### Application performance overview

The Application performance overview section displays the performance information of all workloads in the cluster, such as error rate and response time (P90).


1. On the details page of the cluster, click **Cloud native observability** \> **Overview** in the left navigation pane. Then, click the **Monitoring overview** tab.

2. In the **Application performance overview** section, view the performance monitoring information of the cluster workloads.
