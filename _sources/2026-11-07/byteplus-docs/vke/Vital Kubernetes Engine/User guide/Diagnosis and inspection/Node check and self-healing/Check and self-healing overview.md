---
title: "Check and self-healing overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Check_and_self-healing_overview"
---

The check and self\-healing feature detects common node faults and performs corresponding mitigation and self\-healing operations. This helps you quickly identify node exceptions, reduce the impact of faults, and improve cluster stability. This topic describes the workflow of check and self\-healing, fault types, events, and metrics.

> **tip**

> This feature is available only to enterprises. If you cannot view the corresponding page in the console, make sure that your account has completed enterprise verification.

## Check and self\-healing process

VKE provides the node check and self\-healing feature. The system periodically checks nodes based on the configured rules. If a node fails, node events will be recorded, and self\-healing will be performed.

* **Failure detection**: The system detects node failures by actively probing for node failures and listening for Elastic Compute Service (ECS) operation and maintenance events. The system generates Kubernetes logs based on node status and reports failures to the monitoring system, which enables you to obtain failure details as early as possible.

* **Mitigation process**: The system performs business mitigation operations, including **cordoning nodes** and **draining nodes**, to minimize the impact of failures. It also supports process intervention after the corresponding operations are complete, which allows you to add specified labels to failed nodes for easier identification and handling.

* **Self\-healing process**: The system restarts failed processes or failed nodes in an attempt to resolve the failures. After completion, check the self\-healing results. If the failures have been resolved, uncordon the nodes and resume normal scheduling for the nodes.

The following figure shows the workflow for node checks and self\-healing.

> **tip**

> The node check and self\-healing feature provides different troubleshooting processes. This allows you to select an appropriate process based on your business requirements.

* > **Anomaly prompt**: Only includes **Anomaly prompt**.

* > **Cordon nodes**: Includes **Anomaly prompt**, **Process intervention (optional)**, and **Cordon nodes**.

* > **Drain nodes**: Includes **Anomaly prompt**, **Process intervention (optional)**, **Cordon nodes**, and **Node draining**.

* > **Auto recovery**: Includes **Anomaly prompt**, **Process intervention (optional)**, **Cordon nodes**, **Node draining**, **Auto recovery**, and **Uncordon (optional)**.

## Failure type

### GPU failures

The following troubleshooting policies are provided for GPU failures: **exception notification**, **cordoning node**, **draining node**, and **self\-healing**. The following table describes the events, metrics, and self\-healing policies for each check item.

> **warning**

> The monitoring feature for XID in GPU check items is being phased out. For details, see [\[Product update\] "XID exception" check item added to the check and self\-healing feature](https://docs.byteplus.com/en/docs/vke/Product-update_XID-exception-check-item-added-to-the-check-an-self-healing-feature). VKE has added the [XID exception](https://docs.byteplus.com/en/docs/90/114018#C4uWKSk9) check item to identify and process GPU failures caused by XID exceptions. Compatibility logic during the phase‑out is as follows:

* > Before XID monitoring is officially phased out, both **GPU failure** and **XID exception** check items include XID\-related check items. If you configure the corresponding check and self\-healing rules at the same time, the system will preferentially use the **XID exception** rule.

* > After XID monitoring is officially phased out, XID\-related check items will no longer be included in the **GPU failure** check item. If you already use the node check and self\-healing feature, we recommend promptly reviewing your existing rule configurations and making necessary adjustments based on your business requirements.

|Check item |Event |Description |Metric and exception scenario |Self\-healing policy |
|---|---|---|---|---|
|GPU disconnection failure |GpuCardFallen |A GPU falls off the bus on a node. |* (Being phased out) XID 79<br><br>* GPU Num<br><br>* Revision |Restart the node. |
|GPU internal failure |GpuUnknownError |An internal failure occurs on the node GPU. |\- |Restart the node. |
|Recoverable GPU memory failure |GpuMemoryErrorRecoverable |A recoverable GPU memory failure occurs on a node. |* (Being phased out) XID 48, 63, and 94<br><br>* GPU Remapped Pending<br><br>* GPU DRAM Uncorrectable \> 60<br><br>* GPU DRAM correctable \> 1000<br><br>* Retired Pages Pending Page Blacklist |Restart the node. |
|Unrecoverable GPU memory failure |GpuMemoryErrorUnrecoverable |An unrecoverable GPU memory failure occurs on a node. |* (Being phased out) XID 64, 95, and 140<br><br>* GPU Remapping Failure<br><br>* GPU SRAM Uncorrectable \> 0<br><br>* Retired Pages Single Bit ECC \> 60<br><br>* Retired Pages Double Bit ECC \> 5<br><br>* GpuAggL1UncorrMemEccErrs + GpuAggL2UncorrMemEccErrs + GpuAggRegisterFile \> 5 |Restart the node. |
|GPU runtime failure |GpuRuntimeError |A failure occurs on a GPU runtime\-related add\-on of a node. |Container Runtime Error |Restart the node. |
|GPU runtime warning |GpuRuntimeWarning |A warning message is generated for a GPU runtime\-related add\-on of a node, but user processes are not necessarily affected. |\- |Restart the node. |
|GPU link failure |GpuLinkError |A GPU link failure occurs on a node, or the bandwidth utilization is low. |* (Being phased out) XID 74<br><br>* PCIe link generation does not match the GPU type.<br><br>* NVLink link count does not match the GPU type.<br><br>* NVLink is not active on the 8\-GPU model. |Restart the node. |
|GPU link performance degradation |GpuLinkUnhealthy |The node GPU link is available, but has slowed down. |The current value of PCIe link width is less than the maximum value. |Restart the node. |
|GPU driver failure |GpuDriverError |A GPU driver hardware failure occurs on a node. |* (Being phased out) XID 119 and 120<br><br>* DriverNotLoaded<br><br>* Nvml Init Error |Restart the node. |
|GPU driver warning |GpuDriverWarning |A warning message is generated for a GPU driver of a node, but user processes are not necessarily affected. |\- |Restart the node. |

### XID exceptions

> Note

> This feature is only available in some regions. For details, see [\[Product update\]: "XID exception" check item added to the check and self\-healing feature](https://docs.byteplus.com/en/docs/vke/Product-update_XID-exception-check-item-added-to-the-check-an-self-healing-feature).

XID exception scenarios support common NVIDIA XID and provide **node draining** and **self\-healing** policies. The following table lists the corresponding event and self\-healing policies for each check item.

|**Check item** |**Event** |**Supported XID types** |Self\-healing policy |
|---|---|---|---|
|NvidiaXID[Code]Error<br><br> |NvidiaXID[Code]Error |* 48: A multi\-bit ECC memory error occurred. It cannot be fixed and is usually accompanied by XID 63 or 64.<br><br>* 63: A multi\-bit ECC error has been isolated. Affected memory pages have been retired. GPUs can continue to be used.<br><br>* 64: A multi\-bit ECC error failed to be isolated. Affected memory pages cannot be retired. You need to pay attention to GPU health status.<br><br>* 74: An NVLink link error occurred, which may affect multi‑GPU communication performance or stability.<br><br>* 79: A GPU became disconnected. It usually requires restarting the node or reinserting the GPU.<br><br>* 94: An ECC error has been suppressed, and the GPU continues to run. We recommend monitoring whether it persists.<br><br>* 95: An ECC error failed to be suppressed. The GPU may not be able to handle subsequent memory errors as expected.<br><br>* 119: The GPU System Processor (GSP) response timed out. It is usually caused by a firmware exception and requires a restart to recover.<br><br>* 120: A GSP running error occurred. A GPU firmware exception occurred, which usually requires a node restart.<br><br>* 140: An exception occurred in multi‑bit ECC error isolation (same as XID 64). Memory pages failed to be retired.<br><br>* 143: A GPU initialization error occurred. The GPU initialization failed, which may cause the GPU to become unavailable to drivers or applications. |Node draining and restart |

> **tip**

> In check items and events, [Code] in NvidiaXID[Code]Error indicates the specific error code, such as NvidiaXID48Error.

### Node failures

The following troubleshooting policies are provided for node failures: **exception notification**, **cordoning node**, **draining node**, and **self\-healing**. The following table describes the events and self\-healing policies for each check item.

|Check item |Event |Description |Self\-healing policy |
|---|---|---|---|
|ECS instance failure |NodeFailure |When an ECS instance fails, nodes on the ECS instance are quickly removed, which reduces business downtime from five minutes to one minute, and the failure is automatically responded to and recovered. |Cold migrate nodes |

The event descriptions of the "ECS Fault" check items are provided in the following table. You can choose to listen to all events or specific events based on your requirements.

|Event types |Event name |Event description and impact |
|---|---|---|
|SystemMaintenance_Redeploy |Instance redeployment due to system maintenance |The ECS instance host (physical machine) or dedicated host is detected to be in a subhealthy state, such as CPU overheating, power failure, or fan malfunction, posing a risk of crash. |
|InfrastructureUpgrade_Redeploy |Instance redeployment due to infrastructure upgrade |As the business evolves and the health status of ECS instance hosts (physical machines) changes, some aging or underperforming infrastructure will be upgraded or retrofitted. |
|SystemFailure_Redeploy |Instance redeployment due to system failure<br><br> |A failure is detected on the ECS instance host (physical machine) or dedicated host, causing a system crash. The instance needs to be redeployed to a new host to resume operation. Otherwise, the services it offers will be unavailable. |
|DiskErrorDetected |Disk anomaly |A hard disk failure is detected on a local instance. The read/write operations failed. You need to authorize redeployment of the instance to a new host or replace the hard disk. Otherwise, the instance will stop running. |
|SystemMaintenance_StopAndRepair |Instance stopped due to system maintenance<br><br> |The ECS instance host (physical machine) is detected to be in a subhealthy state, such as CPU overheating, power failure, or fan malfunction, posing a risk of crash. A shutdown and in\-place repair are required.<br><br>> **tip**<br><br><br>> [**Beta \- apply for trial**]: This feature is currently in beta for ECS products. To listen for this event, contact your account manager to apply for a trial and enable event sending.<br> |

> **tip**

> When ECS generates relevant events, you need to perform different O&M operations depending on the event type.

### System and add\-on failures

The following troubleshooting policies are provided for system and add\-on failures: **exception notification** and **self\-healing**. The following table describes the events and self\-healing policies for each check item.

|Check item |Event |Description |Self\-healing policy |
|---|---|---|---|
|kubelet failure |KubeletUnhealthy |An error occurs when kubelet is running, which results in the unavailability of the node. |Restart the kubelet service. |
|Runtime failure |RuntimeUnhealthy |An error occurs when containerd/docker is running, which results in the unavailability of the node. |Restart the containerd service. |
|Time synchronization service error |NTPProblem |An exception occurs on Chrony. |Restart the Chrony service. |
|Read\-only node file system |ReadonlyFilesystem |The file system on the node became read\-only, which causes services running on the node to malfunction. |Restart the node. |
|Node kernel failure |KernelOops |Kernel errors exist on the node, which affect the normal operation of VKE on the node. |Restart the node. |
|Node kernel deadlock |KernelHasDeadlock |A deadlock occurs in the node kernel. |Restart the node. |
|GPU device plugin reported an exception |AcceleratorDevicePluginUnhealthy |The persistent connection between the GPU (NPU) device add\-on and kubelet was disconnected. As a result, the reported node GPU resource capacity is 0, and new GPU workloads cannot be scheduled to the node. |Restart the add\-on Pod |
|RDMA device plugin reported an exception |RDMADevicePluginUnhealthy |The persistent connection between the RDMA device add\-on and kubelet was disconnected. As a result, the reported node RDMA resource capacity is 0, and new RDMA workloads cannot be scheduled to the node. |Restart the add\-on Pod |

> **tip**

> When repairing **kubelet failures** and **runtime failures**, the system checks whether the kubelet and containerd services are running as expected at the same time. If failures occur in both services, the failures will be simultaneously repaired.

### Custom failures

VKE has various preset check items for common node resources and provides self\-healing policies. If the preset check items do not meet requirements, you can also create custom check items based on NodeCondition information. For details, see [Custom node check items](https://docs.byteplus.com/en/docs/vke/Custom_Node_check_and_self-healing).

## Check and self\-healing events

After a node pool is bound to a check and self\-healing rule, the system periodically checks nodes based on the configured rule. If a node fails, node events will be recorded. You can view the corresponding events in the **event center**. The following table shows the correspondence between check items and events.

|Event |Event description |Message |Message description |Event category |
|---|---|---|---|---|
|NodeRepair |Start self\-healing |Node {nodename} begin to repair |Start troubleshooting |Normal |
|NodeRepairAction |Self\-healing |Node {nodename} status is now: NodeCordon |Scheduling is prohibited when exceptions occur |Warning |
|||Node {nodename} status is now: NodeDrainStart |Start draining a node |Warning |
|||Node {nodename} status is now: NodeDrainCompleted |Node draining is complete |Normal |
|||Node {nodename} status is now: InstanceReboot |Restart the node after it is drained |Normal |
|||Node {nodename} status is now: InstanceForceReboot |Forcibly restart a node without draining |Warning |
|||Node {nodename} status is now: NotReady |Set the status of a node to NotReady |Warning |
|||Node {nodename} status is now: Evicting |Start evicting the backend pods |Warning |
|||Node {nodename} status is now: RecreateStatefulsetPod_ |Recreate a StatefulSet Pod |Normal |
|NodeRepairActionFailed |Failed to perform self\-healing |Node {nodename} status is now: NodeIngressControllerExist |Check whether the ingress\-controller pod is running on the node before node draining. |Warning |
|||Node {nodename} status is now: NodeBindPodExist |Check whether workloads that are strongly bound to the node are running on the node before node draining. |Warning |
|||Node {nodename} status is now: NodeSingleInstanceWorkloadExist |Check whether single\-replica workloads are running on the node before node draining. |Warning |
|||Node {nodename} status is now: NodeStaticPodExist |Check whether static pods are running on the node before node draining. |Warning |
|||Node {nodename} status is now: {GPU failure event} AfterRepairAction |After self\-healing, failure still exists |Warning |
|||Node {nodename} status is now: EvictionFailed |Failed to evict the backend pods |Warning |
|||Node {nodename} status is now: RecreateStatefulsetPodFailed |Failed to recreate a StatefulSet pod |Warning |
|||Node {nodename} status is now: RecreateDaemonSetPodFailed |Failed to recreate a DaemonSet pod |Warning |
|||Node {nodename} status is now: NodeRepairActionTerminated |The self\-healing operation is terminated. |Normal |
|NodeRepairActionSucceeded |Self\-healing succeeded. |{GPU failure event}RecoveredAfterRepairAction |After self\-healing, check whether the issue is fixed. |Normal |

## Node failure metrics

### Metric descriptions

The node check and self\-healing feature exposes node failures in the format of metrics to the monitoring system. You can trace the time when failures occurred and locate specific resources based on metrics and labels. To use this feature, enable the cloud native observability feature in the cluster. For more information, see [Enabling cloud native observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

The following table describes node failure metrics.

|Project |Description |
|---|---|
|Metric name |`aiops_resource_status` |
|Metric type |Gauge |
|Label value |* `name`: The registered name of the node in the cluster, such as `172.31.32.45`.<br><br>* `resource_name`: the resource name, such as `ncmj2h***`, which is used to locate a specific resource.<br><br>* `resource_kind`: Set the value to `VkeNode`, which indicates that the resource type is the VKE node.<br><br>* `account_id`: the BytePlus account ID, such as `21001***`.<br><br>* `cluster_id`: the cluster ID, such as `cd03r***`. |
|Metric value |The value is in float64 format. Different numbers indicate different failures. |

In node failure metrics, different types of failures correspond to different values. For details, see the following table.

|Failure event |Value when a failure occurs |Error code (binary) |Error code (decimal) |
|---|---|---|---|
|GpuCardFallen |1 |10000000000000000000 |524288 |
|GpuMemoryErrorRecoverable |1 |01000000000000000000 |262144 |
|GpuMemoryErrorUnrecoverable |1 |00100000000000000000 |131072 |
|GpuLinkError |1 |00010000000000000000 |65536 |
|GpuLinkUnhealthy |1 |00001000000000000000 |32768 |
|GpuDriverError |1 |00000100000000000000 |16384 |
|GpuDriverWarning |1 |00000010000000000000 |8192 |
|GpuRuntimeWarning |1 |00000001000000000000 |4096 |
|GpuRuntimeError |1 |00000000100000000000 |2048 |
|GpuUnknownError |1 |00000000010000000000 |1024 |
|KubeletUnhealthy |1 |00000000001000000000 |512 |
|RuntimeUnhealthy |1 |00000000000100000000 |256 |
|NTPProblem |1 |00000000000010000000 |128 |
|FilesystemError |1<br><br>1 |00000000000001000000 |64 |
|KernelOops |1 |00000000000000100000 |32 |
|NodeResourceLeak |1 |00000000000000010000 |16 |
|NodeFailure |1 |00000000000000001000 |8 |
|NodeNotReady |1 |00000000000000000100 |4 |
|ReadonlyFilesystem |1 |00000000000000000010 |2 |
|KernelHasDeadlock |1 |00000000000000000001 |1 |
|No failure |\- |00000000000000000000 |0 |

> **tip**

> If a node has multiple types of failures at the same time, the error codes will be combined. For example, when both the GpuCardFallen and KernelHasDeadlock failures occur on a node, the error code is `10000000000000000001`, which is `524289` in decimal.

### Metric usage

After you receive a metric\-based node failure alert, you can view node events to further understand the details of the failure.

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Nodes** \> **Node**.

4. In the node list, click the name of the target node to go to its details page. Click the **Event** tab to view node events.

> **warning**

> By default, the events of nodes for VKE clusters are retained for only one hour. To retain node failure details for a longer period, you can install the event\-collector add\-on to export cluster events to Torch Log Service (TLS), which helps you query and retrieve them later.

When you query event information for a node, you can filter events by the event type `reason = AIOpsResourceStatus`. The `Message` parameter stores the details of a failure. If multiple types of failures occur on a node, multiple events will be pushed.

`Message` is a JSON string whose structure is as follows:

```json
{
    "Type":                "Fault type",
    "LastTransitionTime":  "Fault most recent trigger time",
    "Message":             "Failure details"
}
```
