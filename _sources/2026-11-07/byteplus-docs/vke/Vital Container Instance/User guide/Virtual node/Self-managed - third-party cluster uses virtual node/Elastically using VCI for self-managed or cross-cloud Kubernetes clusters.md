---
title: "Elastically using VCI for self-managed or cross-cloud Kubernetes clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Elastically-using-VCI-for-self-managed-Kubernetes-clusters"
---

VCI provides a fast path for self\-managed on\-premises Kubernetes clusters or third\-party cloud Kubernetes clusters to elastically utilize BytePlus container resources. This topic mainly describes the solution for elastic scheduling to the cloud using VCI in self\-managed or cross\-cloud Kubernetes clusters.

<span id=".5pa55qGI5LuL57uN"></span>
## Solution introduction

By registering and managing virtual nodes on the cloud, the resources that business workloads in Kubernetes clusters depend on are elastically scheduled to the cloud. This fully expands the computing resource capacity of on\-premises clusters.

A virtual node provided by VCI corresponds to a native Kubernetes node and is compatible with native Kubernetes node APIs and scheduling semantics. When a pod needs to be scheduled to a virtual node, the virtual node automatically creates and comprehensively manages the underlying VCI resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: virtual node support is in the <strong>beta</strong> stage. To use it, submit an application.</div>


<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Constraints

Due to public cloud security requirements and limitations inherent to virtual nodes, VCI currently does not support Kubernetes features such as HostPath and DaemonSet. For detailed explanations and alternative solutions, see [Kubernetes restrictions](https://docs.byteplus.com/en/docs/vke/VCI-limits#.a3ViZXJuZXRlcy3pmZDliLY=) in the VCI documentation.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Establish network connectivity.

   You need to establish the network connection between the control plane of your self\-managed or cross\-cloud Kubernetes cluster and the BytePlus VPC according to your actual application networking. For details, see [VPC application scenarios](https://docs.byteplus.com/en/docs/vpc/Application-scenarios).

2. Prepare the environment.

   Obtain the KubeConfig file of your self\-managed Kubernetes cluster.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to obtain it using an account with admin permissions.   </div>
   

3. Create virtual nodes and deploy them to your self\-managed or cross\-cloud Kubernetes cluster in a standardized manner.

   * For information about how to create virtual nodes using the console, see [Creating virtual nodes](https://docs.byteplus.com/en/docs/vke/Creating-a-virtual-node).

   * For information about how to create virtual nodes using an OpenAPI call, see [CreateVirtualNode.](https://docs.byteplus.com/en/docs/vke/CreateVirtualNode)

4. Prepare for workload scheduling.

   For some system components in self\-managed Kubernetes clusters, such as DaemonSet components, you must configure node anti\-affinity for the registered virtual nodes to prevent these system components from being scheduled to virtual nodes.

5. Scheduling workloads. You can use two methods to schedule VCI pods to virtual nodes in your self\-managed or cross\-cloud Kubernetes cluster:

   * Standard VCI usage:

      1. Deploy the vci\-admission add\-on in self\-managed or cross\-cloud Kubernetes clusters. For details, see [volcengine-vci-admission](https://github.com/volcengine/volcengine-vci-admission).

      2. Use the VCI\-related label `vke.volcengine.com/burst-to-vci: enforce` to directly schedule VCI pods to your virtual nodes. For details, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).

   * Native Kubernetes pod scheduling:

      Use native Kubernetes scheduling capabilities to schedule pods to specified virtual nodes. For details, see the [official Kubernetes documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/).

6. (Optional) Delete the virtual nodes.

   When a virtual node is no longer needed, call [DeleteVirtualNode](https://docs.byteplus.com/en/docs/vke/DeleteVirtualNode) to delete it.
