---
title: "Calculating schedulable Pod density for nodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Pod-scheduling-density-calculation-for-nodes"
---

This topic describes how schedulable Pod density is calculated for nodes in Vital Kubernetes Engine (VKE). Based on these rules, you can choose higher\-specification and newer ECS instance types according to your workload requirements. 

<span id="N04Ag9QL"></span>
## View schedulable Pods for nodes

VKE allows you to view schedulable Pod density for nodes in the console.


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, click **Cluster**.

3. On the **Cluster** page, find the target cluster and click its name.

4. In the left navigation pane on the cluster management page, click **Nodes** \> **Node**.

5. View the schedulable Pod density for each node on the **Node** page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_348e84bacaa210eb702af10b0f957fa5.png) </span>

&nbsp;

   
   |Parameter |Description |
   |---|---|
   |Allocated amount |The number of Pods already scheduled onto the current node. |
   |Total amount |The theoretical number of schedulable Pods for the current node is the value of the kubelet parameter `max-pods` for the node.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The value displayed in the <strong>total amount</strong> column is the theoretical number of schedulable Pods. The actual number of schedulable Pods for the node depends on the network model of the cluster where the node resides, as well as the instance specification of the corresponding ECS instance. For detailed calculation methods, see the <strong>Calculate schedulable Pods for nodes</strong> section of this topic.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">VKE allows you to modify the <code>max-pods</code> value of a node by using custom kubelet parameters. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool">Specifying node kubelet parameters</a>.</div><br> |
   


<span id="uksZ0giw"></span>
## Calculate schedulable Pods for nodes

The method for calculating schedulable Pod density on nodes varies among clusters that use different container network models.

<span id=".Zmxhbm5lbC3pm4bnvqQ="></span>
### Flannel cluster

In a Flannel cluster, the actual number of schedulable Pods per node is the minimum value between the node kubelet parameter `max-pods` and the **Maximum number of Pod instances per node** parameter specified in the console. For example, if `max-pods` is set to 110 and **Maximum number of Pod instances per node** is set to 64, the actual schedulable Pod density per node in the current cluster is 64.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>Maximum number of Pod instances per node</strong> is a parameter that can be specified when you create a Flannel cluster in the console. Its value cannot be modified after the cluster is created. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-cluster">Creating managed clusters</a>.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3d97a8c94bafbe56efb48adef4d74633.png) </span>

<span id=".dnBjLWNuaS3pm4bnvqQ="></span>
### VPC\-CNI cluster

With this network model, pod density on each node depends on the ECS specification.

If the ECS instance type of a node supports Trunk ENIs and the current cluster has Trunk ENI enabled, Pod density is calculated by using the following formula:


`Pod density` = (`Total number of elastic ENIs supported by the ECS specification for the node` \- `2`) × `Number of IP addresses that can be assigned to a single ENI` + `One Pod used by the VPC-CNI add-on` + `Number of Branch`

* If the Trunk ENI mode is not enabled for the current cluster, the pod density is calculated via the following formula:

   `Pod density` = (`Total number of elastic ENIs supported by the ECS specification for the node` \- `1`) × `Number of IP addresses that can be assigned to a single ENI` + `One Pod used by the VPC-CNI add-on`


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The preceding formula calculates the Pod density assigned to a node by the cluster. To calculate the actual Pod density available to the user, subtract the Pods used by the VPC\-CNI add\-on. If the value of the node kubelet parameter <code>max-pods</code> is less than the value calculated through the preceding formula, the actual schedulable Pod density of the node is subject to the value of <code>max-pods</code>.</div>


* <div data-tips="true" data-tips-type="tip">In a VPC\-CNI cluster, the number of pods allowed on a node depends on the number of elastic network interfaces (ENI) available for an ECS instance that corresponds to a node. The formula above can help you select an appropriate ECS specification.</div>


* <div data-tips="true" data-tips-type="tip">Different specifications of ECS instances vary in the number of ENIs. For details, see <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance specifications</a>.</div>
