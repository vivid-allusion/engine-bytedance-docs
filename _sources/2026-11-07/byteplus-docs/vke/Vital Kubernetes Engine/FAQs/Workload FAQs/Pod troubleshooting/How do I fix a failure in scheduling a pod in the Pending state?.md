---
title: "How do I fix a failure in scheduling a pod in the Pending state?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Pod-in-the-Pending-state_not-successfully-scheduled"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

The pod remains in the **Pending** state for an extended period and is not scheduled.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis


1. View pod event information to preliminarily determine the cause of the pending pod. For details, see [Viewing pod information](https://docs.byteplus.com/en/docs/vke/Viewing-pod-details).

2. Based on the event details, identify the specific reason.

   
   |Event message example |Reason for scheduling failure |Solution |
   |---|---|---|
   |No nodes available to schedule pods |The pod fails to be scheduled onto a node because the cluster does not have available nodes. |[No available nodes in the cluster](https://docs.byteplus.com/en/docs/vke/Pod-in-the-Pending-state_not-successfully-scheduled#.6ZuG576k5peg5Y-v55So6IqC54K5) |
   |0/3 nodes are available: 3 Insufficient cpu.<br><br>0/2 nodes are available: 2 Insufficient memory. |The pod fails to be scheduled onto a node due to insufficient node resources (CPU and memory). |[Insufficient node resources](https://docs.byteplus.com/en/docs/vke/Pod-in-the-Pending-state_not-successfully-scheduled#.6IqC54K56LWE5rqQ5LiN6Laz) |
   |0/1 nodes are available: 1 node(s) had taints that the pod didn't tolerate. |Nodes have taints that cannot be tolerated by the pod. |[Intolerable node taints for the pod](https://docs.byteplus.com/en/docs/vke/Pod-in-the-Pending-state_not-successfully-scheduled#.6IqC54K55LiK5a2Y5ZyoLXBvZC3ml6Dms5Xlrrnlv43nmoTmsaHngrk=) |
   |0/2 nodes are available: 1 node(s) didn't match node selector, 1 node(s) didn't match pod affinity rules, 1 node(s) didn't match pod affinity/anti\-affinity. |Node affinity, pod affinity, or pod anti\-affinity configured on the workload to which the pod belongs do not match any existing node. |[Pod affinity mismatch with nodes](https://docs.byteplus.com/en/docs/vke/Pod-in-the-Pending-state_not-successfully-scheduled#.6IqC54K55LiOLXBvZC3nmoTkurLlkozmgKfkuI3ljLnphY0=) |
   


<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

<span id=".6ZuG576k5peg5Y-v55So6IqC54K5"></span>
### No available nodes in the cluster


1. Log in to the [VKE console](https://console.byteplus.com/vke).  In the left navigation bar, click **Cluster**.

2. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Node**.

3. On the **Node** page, check whether there are available nodes (those in the **Running** state).

   * If no node exists, add new nodes or existing ECS instances to the cluster. For details, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes) and [Adding existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes). 

   * If the cluster has nodes but none of them are in the **Running** state, fix the abnormal node status. If nodes are available and have sufficient resources, the pod can be scheduled. For information about how to fix abnormal nodes, see [Node and node pool FAQs](https://docs.byteplus.com/en/docs/vke/Node-and-NodePool-FAQs).


<span id=".6IqC54K56LWE5rqQ5LiN6Laz"></span>
### Insufficient node resources


1. Log in to the [VKE console](https://console.byteplus.com/vke).  In the left navigation bar, click **Cluster**.

2. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Node**.

3. On the **Node** page, view the CPU and memory resource usage of available nodes (in the **Running** state).

   If node resources are insufficient, follow the instructions below:

   * If the number of nodes is too small, add new nodes to the cluster to ensure that node resources meet pod scheduling requirements. For details, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes).

   * If the specifications of individual nodes are too small, add nodes with larger specifications to ensure sufficient CPU and memory resources. For details, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes) and [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

   * Delete unnecessary pods on existing nodes to free up node resources. For details, see [Deleting pods](https://docs.byteplus.com/en/docs/vke/Managing-pods#.5Yig6Zmk5a655Zmo57uE).

   * Adjust the resource quota (request and limit) of the container in the pod so that it can be scheduled onto a node. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workloads).


<span id=".6IqC54K55LiK5a2Y5ZyoLXBvZC3ml6Dms5Xlrrnlv43nmoTmsaHngrk="></span>
### Intolerable node taints for the pod


1. Log in to the [VKE console](https://console.byteplus.com/vke).  In the left navigation bar, click **Cluster**.

2. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Node**.

3. On the **Node** page, click the node name to enter the **Node details page**.

4. On the **Node details page**, view the taints of the node and process the scheduling issue between the Pod and the node as needed.

   * Modify the **scheduling policy** of the workload to which the pod belongs to tolerate the taints. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workloads).

   * Batch update node taints by modifying the node pool configuration. For details, see [Editing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools). You can also edit or delete node taints individually.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">System taints cannot be deleted.      </div>
      

   * For more methods, see the [Kubernetes documentation](https://kubernetes.io/zh-cn/docs/concepts/scheduling-eviction/taint-and-toleration/#taint-based-evictions).


<span id=".6IqC54K55LiOLXBvZC3nmoTkurLlkozmgKfkuI3ljLnphY0="></span>
### Pod affinity mismatch with nodes


1. Log in to the [VKE console](https://console.byteplus.com/vke).  In the left navigation bar, click **Cluster**.

2. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Node**.

3. On the **Node** page, find the target node, and in the **Actions** column on the right side, click `...` \> **Label management** to view node labels.

4. Based on node labels, adjust the **scheduling policy** of the workload corresponding to the pod. The following figure uses a Deployment as an example. For details, see [Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments). For more information about affinity, see the [Kubernetes documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/).

   * Change **Node affinity scheduling** from **Forced scheduling** to **Priority scheduling**.

   * Adjust pod affinity or anti\-affinity to ensure that a node can match this pod.
