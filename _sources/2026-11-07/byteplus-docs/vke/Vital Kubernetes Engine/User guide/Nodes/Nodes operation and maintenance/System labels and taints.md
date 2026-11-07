---
title: "System labels and taints"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/System-labels-and-taints"
---

This topic describes the system labels and taints for nodes in a Vital Kubernetes Engine (VKE) cluster and how to manage them. When you customize labels or taints in VKE, avoid conflict with system labels or taints.

## System labels in VKE

|Label Key |Description |
|---|---|
|cluster.vke.volcengine.com/cluster\-name |Cluster ID. |
|cluster.vke.volcengine.com/machine\-name |Node ID. |
|cluster.vke.volcengine.com/machinepool\-name |The node pool ID. |
|cluster.vke.volcengine.com/machinepool\-type |Node pool types. |
|cluster.vke.volcengine.com/node\-name |Node metadata name (metadata.name). |
|machine.cluster.vke.volcengine.com/gpu\-name |Graphics card name. |
|cluster.vke.volcengine.com/hpc\-cluster\-id |ID of the high\-performance compute cluster associated with the VKE cluster. |
|cluster.vke.volcengine.com/affinity\-group\-id |ID of the affinity group associated with the VKE node pool. |

> **tip**

> In addition to the labels listed above, all other labels that contain `vke.volcengine.com` are system labels.

## System labels in Kubernetes

|Label Key |Description |
|---|---|
|kubernetes.io/os |For a description of Kubernetes system labels, see [Kubernetes documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/). |
|kubernetes.io/metadata.name ||
|kubernetes.io/hostname ||
|kubernetes.io/role ||
|node.kubernetes.io/instance\-type ||
|topology.kubernetes.io/region ||
|topology.kubernetes.io/zone ||
|node.kubernetes.io/windows\-build ||
|endpointslice.kubernetes.io/managed\-by ||
|endpointslice.kubernetes.io/skip\-mirror ||
|alpha.kubernetes.io/provided\-node\-ip ||

## System taints in VKE

|Taint Key |Description |
|---|---|
|vke.volcengine.com/node\-initializing:NoSchedule |This taint is related to node initialization when an existing node is added, and it is automatically removed after the node is added. |
|node.willDelete:NoSchedule |The taints used when deleting and draining a node. |
|ToBeDeletedByClusterAutoscaler |This is a scale\-in taint added by Cluster Autoscaler (CA). After the taint is added successfully, node draining starts, and the node is deleted by the Auto Scaling group after draining is completed. |
|DeletionCandidateOfClusterAutoscaler |This taint is added by CA before scale\-in to make the node less likely to receive scheduled pods. |

## System taints in Kubernetes

|Taint Key |Description |
|---|---|
|node.kubernetes.io/not\-ready |For a description of Kubernetes system taints, see [Kubernetes documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/). |
|node.kubernetes.io/unreachable ||
|node.kubernetes.io/unschedulable ||
|node.kubernetes.io/memory\-pressure ||
|node.kubernetes.io/disk\-pressure ||
|node.kubernetes.io/network\-unavailable ||
|node.kubernetes.io/pid\-pressure ||
|node.cloudprovider.kubernetes.io/uninitialized ||
|node.cloudprovider.kubernetes.io/shutdown ||
|node\-role.kubernetes.io/master ||
|node\-role.kubernetes.io/control\-plane ||
