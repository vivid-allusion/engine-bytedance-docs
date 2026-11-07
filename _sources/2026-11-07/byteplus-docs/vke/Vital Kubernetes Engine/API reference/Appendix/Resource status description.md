---
title: "Resource status description"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Resource-status-description"
---

This topic describes the status and status transitions of resources, such as clusters, node pools, and nodes, during the calling of VKE APIs.

<span id=".6YCa55So54q25oCB6K-05piO"></span>
## General status description

VKE uses 2\-tuples `{Phase, [Conditions1, Conditions2, ...]}` to indicate the status of resources, such as clusters, nodes, and node pools.


* `Phase`: Indicates the atomic status of a resource.

* `Conditions`: An array that indicates the reason why a resource enters a specific atomic state and the limitations under the atomic state.

   For example, `{Creating, [Progressing]}` indicates that a resource is being created. `{Failed, [Balance, ResourceCleanupFailed]}` indicates that a node fails to be removed, and its corresponding ECS instance is suspended due to overdue payments.

* `*`: Indicates a wildcard.

   For example, `{Running, [*]}` indicates that `Phase is Running`, and `Conditions` match all states.


<span id=".6ZuG576k"></span>
## cluster


|Phase |Conditions.Type |Corresponding status in console |Description |
|---|---|---|---|
|Creating |Progressing |Creating |The cluster is being created. |
|Running |Ok |Running |The cluster is running as expected. |
|Updating |[Progressing, UpdatingCluster] |Updating cluster configuration |The configurations of the cluster are being updated, such as enabling or disabling public access, and adding or deleting cluster subnets. |
||[Progressing, SyncingAddon] |Updating add\-on |An add\-on in the cluster is being changed, such as an add\-on upgrade, a configuration update, and deletion. |
||[Progressing, SyncingNodePool] |Updating node pool |A node pool in the cluster is being changed, such as node pool creation, deletion, or scaling. |
||ClusterVersionUpgrading |Upgrading |The cluster version is being upgraded. |
|Deleting |Progressing |Deleting |The cluster is being deleted. |
|Stopped |Balance |Shutdown due to arrears |The cluster is suspended due to overdue payments. |
|Failed |CreateError |Failed to create |The cluster creation fails due to reasons other than insufficient quota, overdue payments, and insufficient inventory. |
||ResourceCleanupFailed |Deletion failed |The cluster fails to be deleted because resources associated with the cluster, such as CLB instances and NAT Gateways, cannot be deleted. |
||Unknown |Abnormal |An error occurs due to an unknown reason. |


<span id=".6IqC54K55rGg"></span>
## Node pool management


|Phase |Conditions.Type |Corresponding status in console |Description |
|---|---|---|---|
|Creating |Progressing |Creating |The node pool is being created. |
|Running |Ok |Running |The node pool is running as expected. |
||ScalingFailed |Running (scaling exception) |The node pool fails to scale. |
|Updating |Progressing |Updating |The configurations of the node pool are being updated. |
||ClusterVersionUpgrading |Upgrading |The version of nodes in the node pool is being upgraded. |
|Deleting |Progressing |Deleting |The node pool is being deleted. |
|Failed |ResourceCleanupFailed |Deletion failed |The resources associated with the node pool, such as ECS instances, cannot be deleted, which results in node pool deletion failure. |
||Unknown |Failed to create |An error occurs due to an unknown reason. |
||ClusterNotRunning |Abnormal |The node pool enters this state when a cluster instance enters the `{Stopped, [*]}` or `{Starting, [*]}` state due to overdue payments or other reasons. |
|Scaling |Progressing |In scaling |The node pool is being scaled. The node pool enters the **In scaling** state in the following scenarios:<br><br><br>* Add a node to the node pool.<br><br>* A node is removed from the node pool.<br><br>* A node in the node pool enters the `{Creating, [Progressing]}` or `{Deleting, [Progressing]}` state. |


<span id=".6IqC54K5"></span>
## Nodes


|Phase |Conditions.Type |Corresponding status in console |Schedulable |Description |
|---|---|---|---|---|
|Creating |Progressing |Creating |No |The node is being created. The node enters the **Creating** state in the following scenarios:<br><br><br>* The node enters the `{Creating, [Progressing]}` state when the node pool automatically scales out nodes.<br><br>* The ECS instance node enters the `{Creating, [Progressing]}` state when you call the [CreateNodes](https://docs.byteplus.com/en/docs/vke/CreateNodes) API to manually add the node to a node pool. |
|Running |Ok |Running |Yes |The node is running as expected. |
||Unschedulable |Running |No |The node is running as expected, but cannot be scheduled because it is cordoned or drained. |
|Updating |Progressing |Updating |No |The node is being updated. |
||ClusterVersionUpgrading |Upgrading |No |The node version is being upgraded. |
|Deleting |Progressing |Removing |No |The node is being removed. The node enters the **Removing** state in the following scenarios:<br><br><br>* The node enters the `{Deleting, [Progressing]}` state when the node pool automatically scales in nodes.<br><br>* The node enters the `{Deleting, [Progressing]}` state when you call the [DeleteNodes](https://docs.byteplus.com/en/docs/vke/DeleteNodes) API to manually remove the node from a node pool. |
|Failed |InitializeFailed |Failed to create |No |When an ECS instance is added as a node to a VKE node pool, it fails to be initialized (For example, the ECS instance is in an abnormal state), or the node pool fails to automatically scale out nodes. |
||NotReady |Abnormal |No |The ECS instance that corresponds to the node is suspended, or the add\-ons of the node, such as kubelet, are not running as expected. |
||Balance |Abnormal (shutdown due to arrears) |No |The ECS instance where the node is located is suspended caused by overdue payments. The ECS instance that corresponds to the node is suspended caused by overdue payments. |
||ResourceCleanupFailed |Removal failed |No |The resources associated with the node, such as ECS instances, cannot be deleted, which results in node deletion failure. |
||Unknown |Failed to create |No |The node fails to be created caused by an unknown reason or exception. |


<span id=".6Jma5ouf6IqC54K5"></span>
## Virtual node


|Phase |Conditions.Type |Corresponding status in console |Description |
|---|---|---|---|
|Creating |Progressing |Creating |The virtual node is being created. |
|Running |Ok |Running |The virtual node is running as expected. |
|Deleting |Progressing |Deleting |The virtual node is being deleted. |
|Failed |Unavailable |Abnormal |The virtual node does not function as expected, caused by reasons such as network disconnection and operational exceptions. |
||CreateFailed |Failed to create |The virtual node cannot be created due to various reasons. |


<span id=".57uE5Lu2"></span>
## Add\-ons


|Phase |Conditions.Type |Corresponding status in console |Description |
|---|---|---|---|
|Creating |Progressing |Installing |The add\-on is being installed. |
|Running |Ok |Installed |The add\-on is running as expected. |
|Updating |Progressing |Updating |The add\-on is being updated, including an add\-on configuration update or a version update. |
|Deleting |Progressing |Uninstalling |The add\-on is being uninstalled. |
|Failed |NameConflict |Fail |The add\-on fails to be installed due to a conflict between resource names in the cluster and the add\-on name. |
||CrashLoopBackOff |Abnormal |The add\-on fails to start. |
||ImagePullBackOff |Fail |The image required by the add\-on fails to be pulled. |
||ClusterNotRunning |Abnormal |The add\-on enters this state when a cluster instance enters the `{Stopped, [*]}` or `{Starting, [*]}` state due to overdue payments or other reasons. |
||Degraded |Abnormal |Add\-ons are running as expected, but some unmanaged add\-ons are upgraded or rolled back, or the number of pod instances does not meet the expected number of replicas (at least 1). |
||SchedulingFailed |Fail |No suitable nodes exist to schedule and run add\-ons. |
||ResourceCleanupFailed |Uninstallation failed |The add\-on fails to be uninstalled because CRD resources or other associated cloud service resources, such as ALB resources that correspond to Ingresses, fail to be cleaned up during the uninstallation of the add\-on. |
||Unknown |Fail |An error occurs for an unknown reason. |


<span id=".6ZWc5YOP57yT5a2Y"></span>
## Image cache


|Phase |Conditions.Type |Corresponding status in console |Description |
|---|---|---|---|
|Creating |Progressing |Creating |The image cache is being created. |
|Deleting |Progressing |Deleting |The image cache is being deleted. |
|Updating |Progressing |Updating |The image cache is being updated. |
|Ready |Ok |Created/Available |The image cache is created and is available. |
||UpdateFailed |Update failed |The image cache fails to be updated. |
||CreationFailed |Failed to create: Instance creation failure |The Pod that the image cache depends on fails to be created, such as a scheduling failure and a cloud disk creation failure. |
|Failed |Balance |Failed to create: Overdue payments |The pod instance resource creation fails due to overdue payments. |
||Unknown |Fail: Unknown reason |The error caused by an unknown reason. |
