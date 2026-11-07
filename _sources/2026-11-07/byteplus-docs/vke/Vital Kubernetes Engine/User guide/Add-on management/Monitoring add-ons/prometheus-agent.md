---
title: "prometheus-agent"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/prometheus-agent-add-on"
---

The prometheus\-agent add\-on is a core metric collection add\-on of the VKE cluster. It is used for collecting cluster metric data and reporting it to the VMP workspace. This topic introduces the core resources, recommended specifications, and configuration instructions for this add\-on.

<span id="Xim9sMCk"></span>
## Add\-on overview

The prometheus\-agent add\-on is a cluster metric collection add\-on, which is used to collect cluster metric data and send the data to VMP. After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|vmagent\-prometheus\-agent |StatefulSet |The core collector add\-on. It is used for pulling data from various metric sources, such as kubelet and node\-exporter, and remotely writing data to VMP workspaces. |
|prometheus\-agent\-vmoperator |Deployment |The automatic management and O&M controller (Operator). It is used to listen to and manage custom resource definitions (CRDs) such as ServiceMonitor and PodMonitor, and convert them into collection configurations that can be recognized by vmagent. |
|prometheus\-agent\-kube\-state\-metrics |StatefulSet |It exposes the metadata metrics of Kubernetes API objects, such as the status, labels, and annotations of resources, such as Deployment, Pod, and Node. |
|prometheus\-agent\-horizontal\-workload\-autoscaler |StatefulSet |The intelligent autoscaler controller for the collection add\-on. It is used to automatically scale out collectors to distribute pressure when metrics surge, and to automatically scale in collectors during off\-peak hours to save cluster resources. |
|prometheus\-agent\-node\-exporter |DaemonSet |It runs on each node in the cluster for collecting metrics related to the operating system and hardware of the node, such as CPU, memory, disk, and network usage. |
|ServiceMonitor |CRD |Automatically discovers the metric endpoints of backend pods of the Service by matching the labels of the Service. It applies to scenarios where backend pods are exposed via a Service. For details, see [Configuring service discovery with a ServiceMonitor](https://docs.byteplus.com/en/docs/vke/Configuring-Service-discovery-through-ServiceMonitor). |
|PodMonitor |CRD |Automatically discovers metric endpoints by matching the labels of pods. It applies to scenarios where no Service is created, or where more fine\-grained management of collection targets is required. For details, see [Configuring service discovery with a PodMonitor](https://docs.byteplus.com/en/docs/vke/Configuring-Service-discovery-through-PodMonitor). |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.</div>


<span id="Z6sDwizv"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/prometheus-agent).

<span id="MCvRXej7"></span>
## Specification recommendations

When you install the prometheus\-agent add\-on in a container cluster, the vm\-agent collector and the kube\-state\-metrics add\-on will also be installed. The number of shards and the resource specifications of the add\-on are related to the cluster size. You can specify the initial (minimum) number of shards for the add\-on based on the cluster size. The following content describes the recommended initial (minimum) number of shards for each add\-on in clusters of different sizes with the default specifications.

The following table lists the default resource specifications of the vm\-agent collector and the kube\-state\-metrics add\-on.


|Resource specification |vm\-agent |kube\-state\-metrics |
|---|---|---|
|CPU request |2 Core |0.2 Core |
|Memory request |2 GiB |512 MiB |
|CPU limit |4 Core |0.8 Core |
|Memory limit |4 GiB |2 GiB |


The following table lists the recommended initial (minimum) number of shards for the vm\-agent collector and the kube\-state\-metrics add\-on in clusters of different sizes.


|Cluster size |Initial (minimum) number of shards for vm\-agent |Initial (minimum) number of shards for kube\-state\-metrics |
|---|---|---|
|10 nodes, 500 pods |1 |1 |
|100 nodes, 5000 pods |2 |2 |
|200 nodes, 10000 pods |4 |4 |
|500 nodes, 25000 pods |10 |10 |


<span id="LZDZMgBN"></span>
## Installing add\-ons

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The prometheus\-agent add\-on cannot be used together with the VM Agent collector that is installed through the script. Before you install the add\-on, make sure that no such VM Agent collector exists in your cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/Deploying-the-VM-Agent">Deploying VM Agent</a>.</div>


* <div data-tips="true" data-tips-type="warning">For prometheus\-agent <strong>v2.0.1</strong> and earlier, you need to configure a managed Prometheus workspace for the add\-on, including the username and password for the workspace. Meanwhile, you also need to ensure the add\-on and the cluster are bound to the same workspace. Otherwise, you will not be able to view cluster monitoring metrics and dashboards on the <strong>Prometheus monitoring</strong> page.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Monitoring** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and specify the related parameters for the add\-on.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |This parameter is fixed as "Custom Deployment deployment" and does not support custom configuration. |
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on VCIs, which are the virtual nodes in the cluster. Fees will be incurred if you deploy the add\-on on VCI. For detailed fee descriptions, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |VM\-agent resource |Configure the default resources of the vm\-agent collector, including the CPU request, CPU limit, memory request, and memory limit. |
   |kube\-state\-metrics Resource configuration |Configure the default resources of the kube\-state\-metrics add\-on, including the CPU request, CPU limit, memory request, and memory limit.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Due to the limitations of the kube\-state\-metrics add\-on (for example, the number of targets that each add\-on instance can collect is limited), we recommend increasing the number of shards to enhance the metric collection capability of the kube\-state\-metrics add\-on in large clusters.</div><br> |
   |VM\-agent initial shard number |Specify the initial number of shards for the vm\-agent collector. |
   |kube\-state\-metrics Initial shard count |Specify the initial number of shards for the kube\-state\-metrics add\-on. |
   |Addon scaling |Specify whether to enable the autoscaling feature for the vm\-agent collector and the kube\-state\-metrics add\-on.<br><br><br>* **Disable**: The add\-on uses the specified initial shard count. Autoscaling will not be triggered when resource utilization increases.<br><br>* **Enable**: Specify the maximum number of shards for the add\-on. The add\-on automatically scales in and out based on resource utilization using the following logic:<br><br>   * **vm\-agent scale\-out**: Automatic scale\-out is triggered when the utilization of any resource (CPU or memory) exceeds 70%.<br><br>   * **vm\-agent scale\-in**: Automatic scale\-in is triggered when the utilization of all resources (CPU and memory) is less than 30%.<br><br>   * **kube\-state\-metrics scale\-out**: Automatic scale\-out is triggered when the utilization of any resource (CPU or memory) exceeds 70%.<br><br>   * **kube\-state\-metrics scale\-in**: Automatic scale\-in is triggered when the utilization of all resources (CPU and memory) is less than 70%.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The scaling cooldown period of vm\-agent is 30 minutes. kube\-state\-metrics scales based on HPA.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After you configure the autoscaling feature for the add\-on, make sure that cluster resources are sufficient. Otherwise, add\-on scale\-out may fail due to insufficient resources.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When scaling the vm\-agent collector and kube\-state\-metrics add\-on, we recommend configuring the number of shards for the kube\-state\-metrics add\-on as an integer multiple of the number of vm\-agent collector shards, to ensure load balancing. For example, the ratio of the <code>number of shards for the kube-state-metrics add-on</code> to the <code>number of shards for the vm-agent collector</code> is <code>1:1</code> or <code>2:1</code>.</div><br> |
   |Deploy addons |Specify whether to install the **node\-exporter** add\-on at the same time. The add\-on is installed by default. This add\-on is used to collect various software and hardware metrics of the node operating system. If you do not install this add\-on, node metrics cannot be monitored. We recommend that you use the default value.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <strong>node\-exporter</strong> add\-on is deployed through the DaemonSet method. Therefore, when you install the add\-on on VCI, the add\-on is deployed on ECS nodes. For more information, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-limits">VCI limit</a>.</div><br> |
   |Node Label Selector |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   |Pod scheduling based on taints and tolerations |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After you enable this feature, you can set taint toleration values. The core workloads of the add\-on can be scheduled onto nodes with specified taints. |
   |**Advanced settings** ||
   |Discovery Role |Select a service discovery method. Valid values: Endpoints and EndpointSlices. By default, a single Endpoints resource supports up to 1,000 backends. Starting from Kubernetes v1.21, the [EndpointSlices](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/) resource was introduced to address this issue. Therefore, Prometheus also supports the EndpointSlices [service discovery method](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#endpointslice).<br><br>The default value is EndpointSlices. If the Kubernetes version is earlier than v1.21, the Endpoints method will be automatically used. |
   |Global Labels |By default, prometheus\-agent adds fixed labels to all collected metrics.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This feature only applies to metrics collected by prometheus\-agent. The metrics of the VKE control plane add\-ons, such as kube\-apiserver, are reported by the add\-ons and will not be modified.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you add or modify global labels, the number of active time series will increase within one hour. If a large number of metrics exist, you need to evaluate whether the upper limit of active time series will be reached. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/workspaces-types">Workspace specifications</a>.</div><br><br><br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><br>* <div data-tips="true" data-tips-type="danger">By default, the automatically added label is <code>cluster:<cluster ID></code>. This label is a system\-reserved field, and we recommend that you do not overwrite it.</div><br><br><br>* <div data-tips="true" data-tips-type="danger">If you want to add a cluster name, we recommend entering a label such as <code>cluster_name</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="danger">If you enter a cluster label, the system\-reserved field will be overwritten, which will lead to the following results:</div><br><br><br>   * <div data-tips="true" data-tips-type="danger">Metrics may not be displayed in some sections on the monitoring dashboard of VKE.</div><br><br><br>   * <div data-tips="true" data-tips-type="danger">Alerting rules created based on some alerting templates will become invalid due to changes in the label of <code>cluster=~"$Cluster"</code>.</div><br> |
   |Secret access |kube\-state\-metrics can generate related metrics only if Secret permissions are included in ClusterRole. |
   

5. Click **Confirm** to finish configuration.


<span id="roCSkbPX"></span>
## Upgrading add\-ons

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="0iD6QhMn"></span>
## Related documentation


* [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability)

* [Basic observability](https://docs.byteplus.com/en/docs/vke/Monitoring-overview)

* [Configuring service discovery with a ServiceMonitor](https://docs.byteplus.com/en/docs/vke/Configuring-Service-discovery-through-ServiceMonitor)

* [Configuring service discovery with a PodMonitor](https://docs.byteplus.com/en/docs/vke/Configuring-Service-discovery-through-PodMonitor)

* [Monitoring application instances deployed in clusters](https://docs.byteplus.com/en/docs/vke/Monitoring-MySQL-databases-using-Vital-Managed-Service-for-Prometheus)

* [Monitoring Go applications in clusters](https://docs.byteplus.com/en/docs/vke/Monitoring-Golang-applications-using-Vital-Managed-Service-for-Prometheus)

* [Best practices for improving prometheus-agent stability](https://docs.byteplus.com/en/docs/vmp/Best_practices_for_improving_Prometheus-agent_stability_)
