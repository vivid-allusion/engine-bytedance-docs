---
title: "Node management"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Node_management"
---

EMR on VKE supports management of dedicated nodes and node pools within clusters. This document describes how to manage dedicated nodes.

<span id="df4f7614"></span>
## Managing nodes in an existing VKE cluster


1. Log in to [EMR Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. On the **Cluster Details** page, click **Node Management** to enter the node pool list page.

   
   |Name |Description |
   |---|---|
   |Node pool name |Name of the VKE cluster node pool |
   |type |VKE cluster node pool type:<br><br><br>* Standard<br><br>* Managed |
   |Instance specification |ECS instance type, CPU, and memory information of the VKE cluster node pool |
   |GPU card |Specifications and quantity of GPU cards |
   |Available nodes / Total nodes |Number of nodes in Running status in the current node pool / total number of nodes in the current node pool |
   |Auto scaling |Whether auto scaling is enabled<br><br><br>* Disabled: Click **to enable** auto scaling<br><br>* Enabled: You can view scaling settings |
   |Taint |Node name, taint key, value, and effect information |
   |Expansion |Number of nodes in the scaled node pool |
   |Remove |Remove dedicated node; node pool resources will not be deleted |
   


<span id="a4ef22e8"></span>
### Dedicated node pool management

<span id="2a8ef7c8"></span>
#### Expand a node pool

This operation expands the node pool and brings the expanded instances under management as dedicated nodes.


1. Click **Expansion**.

2. Enter the target number of instances.

3. Select **I agree to the E\-MapReduce Service Terms**, click **Confirm** to complete the expansion of the node pool.


<span id="b5c30765"></span>
#### Add a dedicated node pool

Currently, two methods are supported: **add an existing node pool** and **create a new node pool**.


* Add an existing node pool.

   1. Click **Add Dedicated Node Pool**, and select **Add an existing node pool** on the pop\-up page.

   2. Select the required node pool(s).

   3. Click **Confirm** to complete adding the dedicated node pool.

* Create a new node pool.

   4. Click **Add an existing node pool**, and select **Create New Node Pool** on the pop\-up page.

   5. Configure the required node pool.

   6. Select **I agree to the E\-MapReduce Service Terms**, click **Confirm** to complete adding the dedicated node pool.


<span id="d2e7853c"></span>
#### Remove a dedicated node pool

Select the node pool to remove, and click **Remove\>Confirm**.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After removing the dedicated node pool, subsequent Pods will not be able to run on this node pool.</div>


<span id="10d50965"></span>
### Dedicated node management


1. Log in to [EMR Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. On the **Cluster Details** page, click **Nodes** to enter the node list page.

   
   |Name |Description |
   |---|---|
   |Node name/ID |Name and ID of the VKE cluster node |
   |Associated node pool |Name of the associated node pool |
   |Availability zone |Availability zone where the node is located |
   |Instance type |ECS instance type, CPU, and memory information of the VKE cluster node pool |
   |GPU card |Specifications and quantity of GPU cards |
   |Taint |Node name, taint key, value, and effect information |
   |Remove |Remove dedicated node; node resources will not be deleted |
   


<span id="2b688844"></span>
#### Add dedicated nodes

Currently, two methods are supported: **add existing nodes** and **create new nodes**.


* Add existing dedicated nodes.

   1. Click the **Add dedicated node**button.

   2. Select **Add Existing Nodes** as the node type.

   3. Select the required nodes.

   4. Click **Confirm** to complete adding dedicated nodes.

* Add newly created dedicated nodes.

   1. Click the **Add Dedicated Node** button.

   2. Select **Create New Nodes** as the node type.

   3. Fill in the associated node pool and the number of nodes.

   4. Click **Confirm** to complete adding dedicated nodes.


<span id="510341a7"></span>
#### Remove dedicated nodes


1. Select the node(s) to remove, and click **Remove**.

2. In the pop\-up window, click **Confirm**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After removing the dedicated node, subsequent Pods will not be able to run on that node.   </div>
   

<span id="e6b35afe"></span>
## Managing nodes in a newly purchased VKE cluster


1. Log in to [EMR Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. On the **Cluster Details** page, click **Node Management** to enter the **Node Pool List** page.

   
   |Name |Description |
   |---|---|
   |Node pool name |Name of the VKE cluster node pool |
   |type |Type of the VKE cluster node pool:<br><br><br>* Standard<br><br>* Managed |
   |State |Node pool status:<br><br><br>* Creating<br><br>* Running<br><br>* Updating<br><br>* Deleting<br><br>* Failed<br><br>* Scaling |
   |Subnet |Node pool subnet information |
   |Instance specification |ECS instance specifications for the node pool |
   |GPU card |Specifications and quantity of GPU cards |
   |Available nodes / Total nodes |Number of nodes in the node pool currently in Running status / total number of nodes in the node pool |
   |Auto scaling |Whether auto scaling is enabled<br><br><br>* Disabled: Click **to enable** auto scaling<br><br>* Enabled: You can view scaling settings |
   |Billing type |Billing type of the node pool<br><br><br>* Pay\-As\-You\-Go<br><br>* Subscription |
   |Scale in or out |Expand or shrink the number of nodes in the node pool |
   |Delete |Delete the dedicated node pool and its resources at the same time |
   


<span id="203ef7cf"></span>
### Modify node pool name


1. On the **Node Pool List** page, click the **Edit** button next to the corresponding node pool name.

2. Enter the target node pool name in the **Node Pool Name** dialog.

3. Click **Confirm** to complete the modification.


<span id="53a6a527"></span>
### Node scaling

This operation will scale the node pool and manage the expanded instances as dedicated nodes.


1. Click **Scale** and enter the number of nodes in the dialog.

2. Select **I agree to the E\-MapReduce Service Terms** and click **Confirm** to complete the scaling operation.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The price displayed for configuration costs is the cost of the node pool under the current configuration.   </div>
   

<span id="8265ad66"></span>
### Add node pool


1. Click **Add Dedicated Node Pool**.

2. On the **Add node pool**page, fill in the node pool name, subnet, instance type, cloud disk information, number of nodes, and access credentials.

3. After completing the information, click **Confirm** to create a new node pool.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Node pool names cannot be duplicated within the same cluster.</div>


<span id="6d8a0c94"></span>
### Delete node pool

Select the node pool to delete and click **Delete\>Confirm**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The node pool can only be deleted when the number of nodes in the node pool is 0.</div>
