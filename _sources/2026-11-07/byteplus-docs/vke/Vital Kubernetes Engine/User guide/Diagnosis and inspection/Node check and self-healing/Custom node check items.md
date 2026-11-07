---
title: "Custom node check items"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Custom_Node_check_and_self-healing"
---

If the preset exceptions or check rules in node self\-healing cannot meet your requirements, you can create check items based on NodeCondition information. This article introduces the basic concepts, data structure, and parameter meanings of custom check items.

<span id="ybbi2x71"></span>
## Background information

<span id="u7B6xdtO"></span>
### What is NodeCondition?

In a Kubernetes cluster, NodeCondition describes the current operational status of a node. It accurately reflects attributes such as node availability, readiness, or resource pressure using the "key\-value pair + status + timestamp" form. Kubernetes controllers, such as kubelet and scheduler, continuously update these conditions, and the scheduler also uses NodeCondition to decide whether to schedule a pod to the node.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For NodeCondition details, see the <a href="https://kubernetes.io/docs/reference/node/node-status/">official documentation</a>.</div>


<span id="et3EV4pI"></span>
### NodeCondition structure

NodeCondition consists of the following fields:


|**Field** |**Description** |
|---|---|
|Type |The NodeCondition type (such as Ready and MemoryPressure). This field identifies the node status to be checked. |
|Status |The NodeCondition status. Possible values include:<br><br><br>* **True**: The condition is true.<br><br>* **False**: The condition is false.<br><br>* **Unknown**: Unknown. |
|Reason |Short reason for the status transition (such as KubeletNotReady or MemoryPressure). |
|Message |Detailed message of the status transition (For example, kubelet is down: postStart hook failed). |
|LastHeartbeatTime |The timestamp of the last heartbeat update for this NodeCondition. |
|LastTransitionTime |The timestamp of the last transition of this NodeCondition status. |


You can run the `kubectl describe node {node-name}` command to view the NodeCondition information of a specific node. In the command, `{node-name}` is the name of the specific node.

```Bash
Conditions:
  Type                 Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----                 ------  -----------------                 ------------------                ------                       -------
  Ready                True    2025-12-05T10:00:00Z              2025-12-01T08:00:00Z              KubeletReady                 kubelet is posting ready status
  MemoryPressure       False   2025-12-05T10:00:00Z              2025-12-01T08:00:00Z              KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure         False   2025-12-05T10:00:00Z              2025-12-01T08:00:00Z              KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure          False   2025-12-05T10:00:00Z              2025-12-01T08:00:00Z              KubeletHasSufficientPID      kubelet has sufficient PID available
  NetworkUnavailable   False   2025-12-05T10:00:00Z              2025-12-01T08:00:00Z              RouteCreated                 RouteController created all required routes
```


<span id="MnRNtZ28"></span>
### Common NodeCondition types

Kubernetes defines a set of standard NodeCondition types that cover the core states of a node.

<span id="iSDYMjLA"></span>
#### Ready (readiness)

This is the most important NodeCondition type for a node. It directly determines whether the node can have pods scheduled to it:


* When `Status` is `True`, the node is healthy, kubelet is running normally, network/storage is available, and the scheduler can schedule pods to this node.

* When `Status` is `False`, the node is unavailable (for example, due to reasons like kubelet not working and network failure), pods scheduled to this node will be evicted, and no new pods will be scheduled to this node.

* When `Status` is `Unknown`, kube\-apiserver has not received a kubelet heartbeat for longer than the `node-monitor-grace-period` (default: 40 seconds), so the node is considered "disconnected", and the scheduler will also avoid scheduling pods to this node.


<span id="rOzoZF0P"></span>
#### Pressure (resource pressure)

When this condition is triggered, the node enters a resource pressure state. The scheduler will restrict or prohibit scheduling of new pods to this node, and the kubelet may evict pods from this node.


|**Condition type** |**Trigger** |
|---|---|
|MemoryPressure |Node memory is insufficient. For example, available memory is below the memory threshold specified for kubelet (example: `memory.available < 100Mi`). |
|DiskPressure |The disk capacity on the node is insufficient. For example, available space in the root partition or container runtime partition is below the threshold. |
|PIDPressure |Too many processes exist on the node, and the number of available processes is lower than the threshold. |


<span id="RQCI8hjj"></span>
#### NetworkUnavailable (unavailable network)


* When `Status` is `True`, the node network is not ready. For example, the CNI add\-on is not configured or network route creation fails.

* When `Status` is `False`, the node network is normal and pods can communicate normally.


<span id="wptH6SET"></span>
## Configuring custom check items

<span id="zVYXijQk"></span>
### Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster to go to the cluster management page.

4. In the left navigation bar, click **Health check & auto recovery**. On the page that appears, click **custom check item** to configure check items using YAML code.

5. Click **save** to complete the configuration.


<span id="wptH6SET"></span>
### Data structure

The node check and self\-healing feature allows you to use YAML code to configure custom check items based on NodeCondition. The following code is a code example:

```JSON
IncidentTypeDefinitions:
  - Code: "GpuHealthAbnormal"
    Name: "GpuHealthAbnormal"
    Description: "GPU card overheating"
    ResourceType: "VkeNode"
    EventProvider: "NodeCondition"
    DetectionConfig:
      NodeCondition:
        Type: "Ready"
        Status: "False"
        Reason: "GpuHealthAbnormal"
        Message: "GPU temperature exceeds threshold (85°C), fan speed abnormal"
  - Code: "NodeNotReady"
    Name: "NodeNotReady"
    Description: "Cluster nodes are not ready"
    ResourceType: "VkeNode"
    EventProvider: "NodeCondition"
    DetectionConfig:
      NodeCondition:
        Type: "Ready"
        Status: "False"
        Reason: "^KubeletNotReady$"
        Message: "^kubelet is not running$"
```


<span id="zdw1dAM7"></span>
### Parameter description

The following table describes variable parameters that can be used in custom error codes.


|Parameters |Data type |Required |Configuration examples |Parameter description |
|---|---|---|---|---|
|Code |String |Yes |GpuHealthAbnormal |The failure code. It can contain only uppercase letters, lowercase letters, and digits. |
|Name |String |Yes |Abnormal GPU health status |The failure name. |
|Description |String |No |GPU temperature is too high |Failure description. |
|ResourceType |String |Yes |VkeNode |The type of resource with this failure. Currently, the supported resource type is  `VkeNode`, which indicates a VKE cluster node failure. |
|EventProvider |String |Yes |NodeCondition |The failure event source. The supported source is `NodeCondition`, which indicates the failure event is from a node. |
|DetectionConfig.NodeCondition.Type |String |Yes |Ready |The condition type (for example, Ready and DiskPressure). This field identifies a certain status type of the node. |
|DetectionConfig.NodeCondition.Status |String |Yes |False |The status. Possible values:<br><br><br>* **True**: The condition is true.<br><br>* **False**: The condition is false.<br><br>* **Unknown**: Unknown. |
|DetectionConfig.NodeCondition.Reason |String |no |`^KubeletNotReady$` |Short reason for the status transition (For example, `KubeletNotReady`). Regular expression matching is supported. If the match is successful, this condition will be designated as a custom failure. |
|DetectionConfig.NodeCondition.Message |String |no |`^kubelet is not running$` |Detailed message of the status transition (for example, `kubelet is not running`). Regular expression matching is supported. If the match is successful, this condition will be designated as a custom failure. |
