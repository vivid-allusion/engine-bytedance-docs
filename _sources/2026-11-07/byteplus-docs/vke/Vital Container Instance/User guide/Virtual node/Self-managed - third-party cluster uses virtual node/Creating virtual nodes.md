---
title: "Creating virtual nodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-virtual-node"
---

By registering and managing virtual nodes on the cloud, VCI elastically schedules resources for business workloads in Kubernetes clusters to the cloud, fully expanding the computing resource capacity of on\-premises clusters. This topic describes how to create virtual nodes by using the console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"> [<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: This feature is currently at the beta stage. Submit an application if you need to use it.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Virtual nodes support association with self\-managed Kubernetes clusters and VKE clusters. Before creating a virtual node, you need to obtain the Kubeconfig file for the target cluster:


* Kubeconfig for self\-managed Kubernetes clusters: It can be obtained by using an account with admin permissions.

* Kubeconfig for VKE clusters: For detailed instructions, see [Managing cluster access credentials](https://docs.volcengine.com/docs/6460/2301425).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Vital Container Instance** \> **Virtual node**, and then click **Create virtual node**.

3. On the **Create virtual node** page, specify the required parameters in the **Virtual node configuration ** step.

   
   |Parameter |Description |
   |---|---|
   |**Basic configuration** ||
   |Name |Set a name for the virtual node based on on\-screen prompts. The name must be unique within the same VPC. |
   |VPC |Select a VPC for the virtual node. A VPC provides an isolated, self\-configurable, and self\-managed virtual network environment for virtual nodes. If no VPC is available, follow the steps described in [Creating VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) to create one. |
   |Subnet |Select a subnet under the selected VPC to provide a subnet segment for the virtual node network. If there are no available subnets, click **Creating subnets** to create one. For details, see [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Security group |Select the security group for the virtual node network to ensure the security and normal functionality of the virtual node. |
   |**Target cluster configuration** ||
   |Kubeconfig |The KubeConfig of the target Kubernetes cluster to which the virtual node will connect. |
   |**Node configuration** ||
   |Node label |Labels in VKE function identically to Kubernetes labels. Labels can be used to define attributes for virtual nodes. These attributes facilitate node filtering.<br><br>Click **Add node labels** and enter a key and its value. |
   |Taint |Taints allow a virtual node to evict specific pods and therefore prevent those pods from being scheduled to the virtual node.<br><br>Click **Add taint** and enter the **Key**, **Value**, and **Effect** based on prompts. You can specify one of the following effects for a taint:<br><br><br>* **NoSchedule**: If a node has a taint whose effect is NoSchedule, the system does not schedule pods to the node.<br><br>* **NoExecute**: Pods that do not tolerate this taint are evicted from nodes with this effect; pods that tolerate it are not evicted.<br><br>* **PreferNoSchedule**: The system attempts to avoid scheduling pods to nodes with taints that are not tolerated by the pods, but it is not guaranteed. |
   

4. Click **Next: Configuration confirmation** to confirm the virtual node configuration and read the terms of service.

5. If you confirm the configuration and have no objections to the terms of service, select the **I have read and agree to Vital Kubernetes Engine Specific Terms of Service** checkbox and click **Confirm** to create the virtual node.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Creating the virtual node is expected to take 5 minutes. Please wait patiently. When the status changes to <strong>Running</strong>, the virtual node has been created successfully. You can start using the elastic scheduling capabilities of VCI resources.   </div>
   

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [Elastically using VCI for self-managed Kubernetes clusters](https://docs.byteplus.com/en/docs/vke/Elastically-using-VCI-for-self-managed-Kubernetes-clusters)

* [CreateVirtualNode](https://docs.byteplus.com/en/docs/vke/CreateVirtualNode)
