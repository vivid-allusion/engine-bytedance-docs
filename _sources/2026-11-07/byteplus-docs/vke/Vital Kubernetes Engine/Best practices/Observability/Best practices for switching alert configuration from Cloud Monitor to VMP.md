---
title: "Best practices for switching alert configuration from Cloud Monitor to VMP"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Best_practices_for_switching_alert_configuration_from_Cloud_Monitor_to_VMP"
---

After the Cloud Monitor add\-on (metrics\-collector) in a container cluster is decommissioned, the corresponding alert rules cannot be directly used or migrated to Vital Managed Service for Prometheus. This article introduces how to configure Cloud Monitor alert rules on Vital Managed Service for Prometheus.

<span id="IT0Ol6Vn"></span>
## Background information

Vital Kubernetes Engine (VKE) will discontinue the metrics\-collector add\-on service on October 9, 2025, UTC+8. Metrics\-collector add\-ons installed in existing container clusters will also be discontinued then. Once the add\-on stops working, Cloud Monitor will no longer support metrics monitoring for container clusters. We recommend using [cloud native observability](https://docs.byteplus.com/en/docs/vke/Observability-overview).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more details, refer to <a href="https://docs.byteplus.com/en/docs/vke/Product-Change-Cloud-Monitor-collection-addon-decommission-announcement">product announcement</a>.</div>


The cloud native observability service stores the metrics collected from the cluster in the workspace of Vital Managed Service for Prometheus. For details, refer to [Basic observability overview](https://docs.byteplus.com/en/docs/vke/Monitoring-overview). Vital Managed Service for Prometheus provides a maintenance\-free, high\-performance, and highly stable cluster monitoring and alert service. You can view cluster metrics or preset cluster dashboards in the Vital Managed Service for Prometheus console. For details on specific operations, refer to the following documents:


* [Metric query](https://docs.byteplus.com/en/docs/vmp/explore-metrics)

* [Preset dashboard](https://docs.byteplus.com/en/docs/vmp/Dashboard-overview)


Due to the differences in alert configuration methods between Cloud Monitor and VMP, alert rules from Cloud Monitor cannot be directly used or migrated to VMP. You need to manually configure the required alerts in VMP according to the procedure and the metric mapping list provided below.

<span id="uxBIXQWy"></span>
## Procedure

The following uses the **cluster CPU usage** metric as an example to explain alert rule configuration. We will cover the steps in the Vital Managed Service for Prometheus (VMP) console.


1. Log in to the [VMP console](https://console.byteplus.com/prometheus).

2. In the top navigation bar, choose the target region.

3. Click **Alert Center \> Alert rule** in the navigation bar on the left. Click **Create**, then select **Create manually** from the dropdown menu.

4. Configure the basic information.

   
   |**Configuration items** |**Descriptions** |
   |---|---|
   |Name |Configure the name of the alert rule. |
   |Description |Description for alert rule configuration. |
   

5. Configure alert trigger conditions.

   
   |**Configuration items** |**Descriptions** |
   |---|---|
   |Workspace |Select the workspace bound to the cluster from the drop\-down list for cloud\-native observability configuration. |
   |Query statement |Use standard PromQL statements to configure monitoring objects or metrics. This article uses the PromQL statements for the **cluster CPU usage** metric, `sum by(cluster)(rate(container_cpu_usage_seconds_total{cluster=~"$Cluster",id=~"/"}[5m]))`, as an example. For more metric details, refer to the [metric comparison list](https://docs.byteplus.com/en/docs/90/69157#QM6orgpr) below. |
   |Trigger policy |Configure alert trigger policy. Specify alert level, condition, threshold, and condition duration.<br><br><br>* Check P0, P1, or P2 to set different alert levels. If unchecked, the alert for that level will not be set.<br><br>* **Comparison condition**: Specify the comparison condition between the PromQL statements and the threshold. Supports multiple comparison conditions, including: **Greater than**, **Greater than or equal to**, **Less than**, **Less than or equal to**, **Equal to**, and **Not equal to**.<br><br>* **Threshold**: The threshold configured for the metric.<br><br>* **Condition duration**: The duration for which the configured metric meets the condition, including:<br><br>   * **Trigger immediately**: When alert conditions are met, trigger the alert immediately.<br><br>   * **1 min**: The alert is triggered if the alert condition is met and remains true for 1 minute.<br><br>   * **2 min**: The alert is triggered after the alert condition is met and remains true for 2 minutes.<br><br>   * **5 min**: After the alert condition is met and has persisted for 5 minutes, the alert is triggered.<br><br>   * **10 min**: The alert is triggered after the alert condition is met and has persisted for 10 minutes. |
   

6. Configure alert notifications.

   
   |**Configuration items** |**Descriptions** |
   |---|---|
   |Notification policy |Select the alert notification policy from the dropdown menu. The system uses the alert levels and contact groups configured in the notification policy to send alerts to designated contacts. For details, refer to [Creating an alert notification policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules). |
   |Aggregation policy |Select an alert aggregation policy in the dropdown menu. For details, refer to [Create alert aggregation policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules). |
   

7. Click **Confirm** to complete the configuration.


<span id="QM6orgpr"></span>
## Subsequent configuration

After alert rule configuration is complete, you also need to configure alert contacts, alert contact groups, and notification policies in Vital Managed Service for Prometheus, and confirm the channels for receiving alerts. For details, refer to [Alert Center best practices](https://docs.byteplus.com/en/docs/vmp/alerting-center-practices).

<span id="QM6orgpr"></span>
## Metric mapping list

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For cluster metrics provided by Cloud Monitor, please refer to <a href="https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_VKE">Cloud Monitor metric query</a>.</div>


<span id="Cuxq49YT"></span>
### Cluster

**Parameters**

When configuring alert rules, if the PromQL statements contains the following parameters, you must modify them to match the actual values of your cluster.


|Parameters |Descriptions |
|---|---|
|`$Cluster` |Cluster ID, such as `cd2qjv390rjo2***`. You can obtain the cluster ID on the cluster overview page. For more details, refer to [Cluster basic information](https://docs.byteplus.com/en/docs/vke/Cluster-basics). |


**metric**


|Cloud Monitor metrics |Descriptions |**PromQL statements** |**Units** |
|---|---|---|---|
|Cluster_MemoryUsed |Cluster memory usage |`sum by (cluster) (container_memory_working_set_bytes{cluster=~"$Cluster", id=~"/"})` |Bytes(SI) |
|Cluster_MemoryUsage |Cluster memory utilization |`(sum by (cluster) (container_memory_working_set_bytes{cluster=~"$Cluster",id=~"/"}) / sum by (cluster) (machine_memory_bytes{cluster=~"$Cluster"}))*100` |Percent |
|Cluster_CPUUsed |Cluster CPU usage |`sum by(cluster)(rate(container_cpu_usage_seconds_total{cluster=~"$Cluster",id=~"/"}[5m]))` |Core |
|Cluster_CPUUsage |Cluster CPU usage |`(sum(rate(container_cpu_usage_seconds_total{cluster=~"$Cluster",id=~"/"}[5m])) by (cluster) / sum(machine_cpu_cores{cluster=~"$Cluster"}) by (cluster)) * 100` |Percent |
|Cluster_NodeCount |Number of cluster nodes |`count(kube_node_info{cluster=~"$Cluster"})` |Count |


<span id="v9kU8PdV"></span>
### Namespace

**Parameters**

When configuring alert rules, if the PromQL statements contains the following parameters, you need to modify them to match the actual values of your cluster.


|Parameters |Descriptions |
|---|---|
|`$Cluster` |Cluster ID, for example `cd2qjv390rjo2***`. You can obtain the cluster ID on the cluster overview page. For details, refer to [Cluster basic information](https://docs.byteplus.com/en/docs/vke/Cluster-basics). |
|`$Namespace` |A namespace name, for example, `kube-system`. |


**metric**


|**Cloud Monitor metrics** |**Descriptions** |**PromQL statements** |**Units** |
|---|---|---|---|
|Namespace_CPUUsed |Namespace CPU usage |`sum by(cluster, namespace) (rate(container_cpu_usage_seconds_total{cluster=~"$Cluster", namespace!="", namespace=~"$Namespace",container="", name=""}[5m]))` |Core |
|Namespace_MemoryUsed |Namespace memory usage |`sum by(cluster, namespace) (container_memory_working_set_bytes{cluster=~"$Cluster", namespace!="", namespace=~"$Namespace",container="", name=""})` |Bytes(SI) |


<span id="kE93cUJt"></span>
### Node

**Parameters**

When configuring alert rules, the PromQL statements contains the following parameters, which you must modify to reflect the actual values of your cluster.


|Parameter |Descriptions |
|---|---|
|`$Cluster` |Cluster ID, for example `cd2qjv390rjo2***`, can be obtained on the cluster overview page. For details, refer to the Viewing cluster information. |
|`$Node` |Node IP address, for example, `192.168.1.10`. |


**metric**


|Cloud Monitor metrics |**Descriptions** |**PromQL statements** |**Units** |
|---|---|---|---|
|Node_PodCount |Pod count |`count by(cluster, node)(kube_pod_info{cluster=~"$Cluster", node=~"$Node"})` |Count |
|Node_CPURequestUsage |Node CPU allocation rate (request) |`sum(kube_pod_container_resource_requests{cluster=~"$Cluster",resource="cpu", node=~"$Node"}) by (cluster,node,resource,unit) / ON(cluster,node,resource,unit) kube_node_status_allocatable{cluster=~"$Cluster"} * 100` |Percent |
|Node_MemoryRequestUsage |Node memory allocation rate (request) |`sum(kube_pod_container_resource_requests{cluster=~"$Cluster",resource="memory", node=~"$Node"}) by (cluster,node,resource,unit) / ON(cluster,node,resource,unit) kube_node_status_allocatable{cluster=~"$Cluster"} * 100` |Percent |
|Node_CPULimitUsage |Node CPU allocation rate (limit) |`sum(kube_pod_container_resource_limits{cluster=~"$Cluster",resource="cpu", node=~"$Node"}) by (cluster,node,resource,unit) / ON(cluster,node,resource,unit) kube_node_status_allocatable{cluster=~"$Cluster"} * 100` |Percent |
|Node_MemoryLimitUsage |Node memory allocation rate (limit) |`sum(kube_pod_container_resource_limits{cluster=~"$Cluster",resource="memory", node=~"$Node"}) by (cluster,node,resource,unit) / ON(cluster,node,resource,unit) kube_node_status_allocatable{cluster=~"$Cluster"} * 100` |Percent |
|Node_CPUUsage |Node CPU usage |`rate(container_cpu_usage_seconds_total{cluster=~"$Cluster",id=~"/", node=~"$Node"}[5m]) / ON(cluster, node) machine_cpu_cores{cluster=~"$Cluster"} * 100` |Percent |
|Node_MemoryUsage |The node memory usage rate<br><br> |`container_memory_working_set_bytes{cluster=~"$Cluster",id=~"/", node=~"$Node"} / ON(cluster, node) machine_memory_bytes{cluster=~"$Cluster"} * 100` |Percent |


<span id="Ad5UZU5y"></span>
### PersistentVolumeClaim

**Parameters**

When configuring alert rules, the PromQL statements contains the following parameters, which you must update to the actual values of your cluster.


|Parameters |Descriptions |
|---|---|
|`$Cluster` |Cluster ID, for example `cd2qjv390rjo2***`, can be obtained on the cluster overview page. For details, refer to [Cluster Basic Information](https://docs.byteplus.com/en/docs/vke/Cluster-basics). |
|`$Namespace` |Namespace name, for example, `kube-system`. |
|`$PersistentVolumeClaim` |PersistentVolumeClaim name, for example, `ebs-demo`. |


**metric**


|Cloud Monitor metric |**Descriptions** |**PromQL statements** |**Units** |
|---|---|---|---|
|PersistentVolumeClaim_VolumeUsage |PersistentVolumeClaim capacity usage rate |`kubelet_volume_stats_used_bytes{cluster=~"$Cluster", namespace=~"$Namespace", persistentvolumeclaim=~"$PersistentVolumeClaim"}/kubelet_volume_stats_capacity_bytes{cluster=~"$Cluster", namespace=~"$Namespace", persistentvolumeclaim=~"$PersistentVolumeClaim"} * 100` |Percent |
|PersistentVolumeClaim_INodeUsage |PersistentVolumeClaim inode usage rate |`kubelet_volume_stats_inodes_used{cluster=~"$Cluster", namespace=~"$Namespace", persistentvolumeclaim=~"$PersistentVolumeClaim"}/kubelet_volume_stats_inodes{cluster=~"$Cluster", namespace=~"$Namespace", persistentvolumeclaim=~"$PersistentVolumeClaim"} * 100` |Percent |


<span id="kCx82hrg"></span>
### Deployment

**Parameters**

When configuring alert rules, if the PromQL statements contains the following parameters, you need to modify them to match the actual values of your cluster.


|Parameter |Descriptions |
|---|---|
|`$Cluster` |Cluster ID, for example `cd2qjv390rjo2***`, can be obtained on the cluster overview page. For details, refer to [Cluster basic information](https://docs.byteplus.com/en/docs/vke/Cluster-basics). |
|`$Namespace` |Namespace name, for example `kube-system`. |
|`$Deployment` |Deployment name, for example `metrics-server`. |


**metric**


|**Cloud Monitor metrics** |**Descriptions** |**PromQL statements** |**Unit** |
|---|---|---|---|
|Deployment_MemoryUsed |Deployment memory usage |`sum(kube_replicaset_owner{cluster=~"$Cluster",owner_kind="Deployment",owner_is_controller="true", namespace=~"$Namespace",owner_name=~"$Deployment"} * ON(cluster, namespace, replicaset) group_right(owner_name) label_join(kube_pod_owner{cluster=~"$Cluster",namespace=~"$Namespace",owner_kind="ReplicaSet",owner_is_controller="true"},"replicaset", "" ,"owner_name") * ON(cluster, namespace, pod) group_right sum by(cluster, namespace, pod)(container_memory_working_set_bytes{cluster=~"$Cluster", name="", container="", pod!=""}))` |Bytes(SI) |
|Deployment_CPUUsage |Deployment CPU usage (of limit) |`avg(kube_replicaset_owner{cluster=~"$Cluster",owner_kind="Deployment",owner_is_controller="true", namespace=~"$Namespace",owner_name=~"$Deployment"} * ON(cluster, namespace, replicaset) group_right(owner_name) label_join(kube_pod_owner{cluster=~"$Cluster",namespace=~"$Namespace",owner_kind="ReplicaSet",owner_is_controller="true"},"replicaset", "" ,"owner_name") * ON(cluster, namespace, pod) group_right sum by(cluster, namespace, pod)(rate(container_cpu_usage_seconds_total{cluster=~"$Cluster", name="", container="", pod!=""}[5m])) / ON(cluster, namespace, pod) sum by(cluster, namespace, pod) (kube_pod_container_resource_limits{cluster=~"$Cluster", namespace=~"$Namespace", resource="cpu", unit="core"}) * 100)` |Percent |
|Deployment_MemoryUsage |Deployment memory usage (as a percentage of limit) |`avg(kube_replicaset_owner{cluster=~"$Cluster",owner_kind="Deployment",owner_is_controller="true", namespace=~"$Namespace",owner_name=~"$Deployment"} * ON(cluster, namespace, replicaset) group_right(owner_name) label_join(kube_pod_owner{cluster=~"$Cluster",namespace=~"$Namespace",owner_kind="ReplicaSet",owner_is_controller="true"},"replicaset", "" ,"owner_name") * ON(cluster, namespace, pod) group_right sum by(cluster, namespace, pod)(container_memory_working_set_bytes{cluster=~"$Cluster", name="", container="", pod!=""}) / ON(cluster, namespace, pod) sum by(cluster, namespace, pod)(kube_pod_container_resource_limits{cluster=~"$Cluster", namespace=~"$Namespace", resource="memory", unit="byte"})) * 100` |Percent |
|Deployment_CPUUsed |Deployment CPU usage |`sum(kube_replicaset_owner{cluster=~"$Cluster",owner_kind="Deployment",owner_is_controller="true", namespace=~"$Namespace",owner_name=~"$Deployment"} * ON(cluster, namespace, replicaset) group_right(owner_name) label_join(kube_pod_owner{cluster=~"$Cluster",namespace=~"$Namespace",owner_kind="ReplicaSet",owner_is_controller="true"},"replicaset", "" ,"owner_name") * ON(cluster, namespace, pod) group_right sum by(cluster, namespace, pod)(rate(container_cpu_usage_seconds_total{cluster=~"$Cluster", name="", container="", pod!=""}[5m])))` |Core |
|Deployment_GPU_Usage |Deployment GPU usage |`avg(kube_replicaset_owner{cluster=~"$Cluster",owner_kind="Deployment",owner_is_controller="true", namespace=~"$Namespace",owner_name=~"$Deployment"} * ON(cluster, namespace, replicaset) group_right(owner_name) label_join(kube_pod_owner{cluster=~"$Cluster",namespace=~"$Namespace",owner_kind="ReplicaSet",owner_is_controller="true"},"replicaset", "" ,"owner_name") * ON(cluster, namespace, pod) group_right sum by(cluster, namespace, pod)(DCGM_FI_DEV_GPU_UTIL{cluster=~"$Cluster", namespace=~"$Namespace"}))` |Percent |
|Deployment_GPU_Memory_Usage |Deployment GPU memory utilization |`avg(kube_replicaset_owner{cluster=~"$Cluster",owner_kind="Deployment",owner_is_controller="true", namespace=~"$Namespace",owner_name=~"$Deployment"} * ON(cluster, namespace, replicaset) group_right(owner_name) label_join(kube_pod_owner{cluster=~"$Cluster",namespace=~"$Namespace",owner_kind="ReplicaSet",owner_is_controller="true"},"replicaset", "" ,"owner_name") * ON(cluster, namespace, pod) group_right sum by(cluster, namespace, pod)(DCGM_FI_DEV_FB_USED{cluster=~"$Cluster", namespace=~"$Namespace"} / (DCGM_FI_DEV_FB_FREE + DCGM_FI_DEV_FB_USED)))*100` |Percent |


<span id="wsmeu8OT"></span>
### StatefulSet

**Parameters**

When configuring alert rules, if the PromQL statements contains the following parameters, you need to modify them to match the actual values of your cluster.


|Parameters |Descriptions |
|---|---|
|`$Cluster` |Cluster ID, such as `cd2qjv390rjo2***`, can be obtained on the cluster overview page. For details, refer to [Cluster basic information](https://docs.byteplus.com/en/docs/vke/Cluster-basics). |
|`$Namespace` |Namespace name, for example `kube-system`. |
|`$StatefulSet` |StatefulSet name, for example, `vmagent-prometheus-agent`. |


**metric**


|**Cloud Monitor metrics** |**metric** |**PromQL** |**Unit** |
|---|---|---|---|
|StatefulSet_CPUUsed |StatefulSet CPU usage |`sum(kube_pod_owner{cluster=~"$Cluster",namespace=~"$Namespace",owner_kind="StatefulSet",owner_is_controller="true", owner_name=~"$StatefulSet"} * ON(cluster, namespace, pod) group_right sum by(cluster, namespace, pod)(rate(container_cpu_usage_seconds_total{cluster=~"$Cluster", name="", container="", pod!=""}[5m])))` |Core |
|StatefulSet_MemoryUsed |StatefulSet memory usage |`sum(kube_pod_owner{cluster=~"$Cluster",namespace=~"$Namespace",owner_kind="StatefulSet", owner_name=~"$StatefulSet"} * ON(cluster, namespace, pod) group_right sum by(cluster, namespace, pod)(container_memory_working_set_bytes{cluster=~"$Cluster", name="", container="", pod!=""}))` |Bytes(SI) |
|StatefulSet_CPUUsage |StatefulSet CPU usage (as a percentage of limit) |`avg(kube_pod_owner{cluster=~"$Cluster",namespace=~"$Namespace",owner_kind="StatefulSet",owner_is_controller="true", owner_name=~"$StatefulSet"} * ON(cluster, namespace, pod) group_right sum by(cluster, namespace, pod)(rate(container_cpu_usage_seconds_total{cluster=~"$Cluster", name="", container="", pod!=""}[5m])) / ON(cluster, namespace, pod) sum by(cluster, namespace, pod) (kube_pod_container_resource_limits{cluster=~"$Cluster", namespace=~"$Namespace", resource="cpu", unit="core"}) * 100)` |Percent |
|StatefulSet_MemoryUsage |StatefulSet memory usage (as a percentage of limit) |`avg(kube_pod_owner{cluster=~"$Cluster",namespace=~"$Namespace",owner_kind="StatefulSet", owner_name=~"$StatefulSet"} * ON(cluster, namespace, pod) group_right sum by(cluster, namespace, pod)(container_memory_working_set_bytes{cluster=~"$Cluster", name="", container="", pod!=""}) / ON(cluster, namespace, pod) sum by(cluster, namespace, pod)(kube_pod_container_resource_limits{cluster=~"$Cluster", namespace=~"$Namespace", resource="memory", unit="byte"})) * 100` |Percent |
|StatefulSet_GPU_Usage<br><br> |StatefulSet GPU utilization |`avg(kube_pod_owner{cluster=~"$Cluster",namespace=~"$Namespace",owner_kind="StatefulSet", owner_name=~"$StatefulSet"} * ON(cluster, namespace, pod) group_right sum by(cluster, namespace, pod)(container_memory_working_set_bytes{cluster=~"$Cluster", name="", container="", pod!=""}) / ON(cluster, namespace, pod) sum by(cluster, namespace, pod)(DCGM_FI_DEV_GPU_UTIL{cluster=~"$Cluster", namespace=~"$Namespace"}))` |Percent |
|StatefulSet_GPU_Memory_Usage |StatefulSet GPU memory utilization |`avg(kube_pod_owner{cluster=~"$Cluster",namespace=~"$Namespace",owner_kind="StatefulSet", owner_name=~"$StatefulSet"} * ON(cluster, namespace, pod) group_right sum by(cluster, namespace, pod)(container_memory_working_set_bytes{cluster=~"$Cluster", name="", container="", pod!=""}) / ON(cluster, namespace, pod) sum by(cluster, namespace, pod)(DCGM_FI_DEV_FB_USED{cluster=~"$Cluster", namespace=~"$Namespace"} / (DCGM_FI_DEV_FB_FREE + DCGM_FI_DEV_FB_USED))) * 100` |Percent |


<span id="8i3GV4UD"></span>
### Pods

**Parameters**

When configuring alert rules, if the PromQL statements contain the following parameters, you need to modify them to match the actual values of your cluster.


|Parameters |Descriptions |
|---|---|
|`$Cluster` |You can obtain the cluster ID, for example `cd2qjv390rjo2***`, on the cluster overview page. For details, refer to [Cluster basic information](https://docs.byteplus.com/en/docs/vke/Cluster-basics). |
|`$Namespace` |Namespace name, for example, `kube-system`. |
|`$Pod` |Pod name, for example `csi-ebs-node-hs***`. |


**metric**


|**Cloud Monitor metrics** |**Descriptions** |**PromQL statements** |**Unit** |
|---|---|---|---|
|Pod_CPUUsed |Pod CPU usage |`rate(container_cpu_usage_seconds_total{cluster=~"$Cluster", namespace=~"$Namespace",name="", container="", pod=~"$Pod"}[5m])` |Core |
|Pod_MemoryUsed |Pod memory usage |`container_memory_working_set_bytes{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod", name="", container=""}` |Bytes(SI) |
|Pod_CPUUsage |Pod CPU usage (as a percentage of the limit) |`rate(container_cpu_usage_seconds_total{cluster=~"$Cluster", namespace=~"$Namespace",name="", container="", pod=~"$Pod"}[5m]) / ON(cluster,namespace,pod) group_left sum by(cluster,namespace,pod)(kube_pod_container_resource_limits{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod", resource="cpu", unit="core"}) * 100` |Percent |
|Pod_MemoryUsage |Pod memory usage (% of limit) |`container_memory_working_set_bytes{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod", name="", container=""} / ON(cluster,namespace,pod) group_left sum by(cluster,namespace,pod)(kube_pod_container_resource_limits{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod", resource="memory", unit="byte"}) * 100` |Percent |
|Pod_NetworkReceiveBytesRate |Pod inbound network traffic rate |`rate(container_network_receive_bytes_total{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod"}[5m])` |Bytes/second(SI) |
|Pod_NetworkTransmitBytesRate |Pod outbound network traffic rate |`rate(container_network_transmit_bytes_total{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod"}[5m])` |Bytes/second(SI) |
|Pod_NetworkReceiveLossPacketRate |Pod inbound network packet loss rate |`rate(container_network_receive_packets_dropped_total{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod"}[5m])/rate(container_network_receive_packets_total{}[5m]) * 100` |Percent |
|Pod_NetworkTransmitLossPacketRate |Pod outbound packet loss rate |`rate(container_network_transmit_packets_dropped_total{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod"}[5m])/rate(container_network_transmit_packets_total{}[5m]) * 100` |Percent |
|Pod_Status |Pod running status |`sum by(cluster,namespace,pod)(kube_pod_status_phase{phase=~"Running\|Succeeded", cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod"})` |None |
|Pod_Readiness |Pod readiness status |`kube_pod_status_ready{condition="true",cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod"}` |None |


<span id="kO1R10Oi"></span>
### Containers

**Parameters**

When configuring alert rules, the PromQL statements contains the following parameters, which you must modify to match the actual values of your cluster.


|Parameters |Descriptions |
|---|---|
|`$Cluster` |Cluster ID, such as `cd2qjv390rjo2***`. You can obtain the cluster ID on the cluster overview page. For details, refer to [Cluster basic information](https://docs.byteplus.com/en/docs/vke/Cluster-basics). |
|`$Namespace` |A namespace name, for example, `kube-system`. |
|`$Pod` |Pod name, for example, `csi-ebs-node-hs***`. |
|Container |Container name, for example `csi-ebs-driver`. |


**Metrics**


|Cloud Monitor metrics |**Descriptions** |**PromQL statements** |**Unit** |
|---|---|---|---|
|Container_MemoryUsed<br><br> |Container memory usage |`container_memory_working_set_bytes{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod", container=~"$Container"}` |Bytes(SI) |
|Container_CPUUsage |Container CPU usage (% of limit) |`rate(container_cpu_usage_seconds_total{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod", container=~"$Container"}[5m]) / ON(cluster, namespace, pod, container)kube_pod_container_resource_limits{resource="cpu", unit="core"} * 100` |Percent |
|Container_MemoryUsage |Container memory usage (as a percentage of limit) |`container_memory_working_set_bytes{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod", container=~"$Container"}/ ON(cluster, namespace, pod, container)kube_pod_container_resource_limits{resource="memory", unit="byte"} * 100` |Percent |
|Container_CPUUsed |Container CPU usage |`rate(container_cpu_usage_seconds_total{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod", container=~"$Container"}[5m])` |Core |
| Container_GPU_Memory_Usage<br><br> |Container GPU memory utilization |`DCGM_FI_DEV_FB_USED{cluster=~"$Cluster", namespace=~"$Namespace", pod=~"$Pod", container=~"$Container"} / (DCGM_FI_DEV_FB_FREE + DCGM_FI_DEV_FB_USED) * 100` |Percent |


<span id="2o1R4yBF"></span>
## FAQs


1. How to choose between free and paid metrics

   Vital Managed Service for Prometheus supports the pay\-as\-you\-go postpaid method and provides workspaces with different storage durations, such as 15 days, 30 days, and more. For workspaces with a storage duration of 15 days, basic metrics are free. Therefore, if you need free metrics, you can use the following methods:

   * It is recommended to create a workspace with a 15\-day storage duration and bind it to the cluster. For details, refer to [Enable observation](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

   * After enabling the observation feature for clusters and add\-ons, you can configure the corresponding collection rules and disable metrics that do not need to be collected. For details, refer to [Vital Kubernetes Engine Observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

2. For the billing description for Vital Managed Service for Prometheus, refer to [product billing](https://docs.byteplus.com/en/docs/vmp/pay-as-you-go).

3. For details about the metrics supported by Container Observability, refer to [Vital Kubernetes Engine metrics](https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-Vital-Kubernetes-Engine).


&nbsp;

&nbsp;
