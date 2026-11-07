---
title: "Managing nodes of managed clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-nodes"
---

The existing clusters can be managed on the node management page. This topic introduces the scenarios, impacts, and procedures of operation related to node management.

<span id=".5Y2V5Liq5pON5L2c6IqC54K5"></span>
## Operation of a single node

<span id=".5LiL57q_6IqC54K5"></span>
### Taking nodes offline

During routine cluster maintenance, nodes may need to go offline to ensure data security in scenarios such as upgrades, node scale\-out, maintenance downtime, node reclaim, and change operations. For more best practices, see [Safely taking nodes offline](https://docs.byteplus.com/en/docs/vke/Safely-undeploying-nodes).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">When a node is taken offline, all pods on that node (except DaemonSet) will be migrated to other nodes in the cluster. The node will then be set to unschedulable status, so new pods cannot be scheduled on it. This action may adversely affect business operations. We recommend performing this action during low\-traffic hours.</div>


* <div data-tips="true" data-tips-type="warning">Taking a node offline will reduce the remaining ResourceQuota of the cluster to which the node belongs. If the cluster does not have sufficient resource reservations, this action will adversely affect the scheduling of new services and the running of existing workloads.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke). In the left navigation bar, click **Cluster**.

2. Click the target cluster name, then in the left navigation bar, select **Nodes** \> **Node**.

3. Click **Go offline** in the `Actions` column of the target node.

4. In the pop\-up window, click **Confirm** to proceed.


<span id=".5bCB6ZSB6IqC54K5"></span>
### Cordoning nodes

Unlike taking nodes offline, the action of cordoning nodes does not migrate pods to other nodes in the cluster. Instead, the node is set to cordoned and unschedulable status, and the pods already running on the node are not affected.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cordoning a node will reduce the remaining ResourceQuota of the cluster to which the node belongs. If the cluster does not have sufficient resource reservation, this action will affect the scheduling of new services and the running of existing workloads.</div>



2. Click the target cluster name. In the left navigation bar, select **Nodes** \> **Node**.

3. Click **Cordon** in the `...` menu to the right of the target node.

4. In the pop\-up window, click **Confirm** to proceed.


<span id=".572u5Li65Y-v6LCD5bqm"></span>
### Switching to schedulable

You can restore scheduling capability for nodes to allow them to accept new pods. After a node is restored to schedulable status, the remaining ResourceQuota of the cluster to which the node belongs will increase.


2. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Nodes** \> **Node**.

3. Click **Make it schedulable** in `...` menu to the right of the target node.

4. In the pop\-up window, click **Confirm** to proceed.


<span id=".5qCH562-566h55CG"></span>
### Label management

Assigning different labels to nodes allows you to define various attributes, making batch filtering and similar operations more convenient. You can manage node labels in the Vital Kubernetes Engine (VKE) console, including adding, editing, and deleting node labels.


2. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Nodes** \> **Node**.

3. Click **Label Management** in the `...` menu to the right of the target node to go to the **Label** tab, where you can manage labels for the node.


<span id=".5rGh54K5566h55CG"></span>
### Taint management

Applying one or more taints to a node allows the node to reject specific pods, preventing those pods from being scheduled on the node. You can manage node taints in VKE console, including adding, editing, and deleting node taints.


2. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Nodes** \> **Node**.

3. Click **Taint management** in `...` menu to the right of the target node to go to the **Taint** tab, where you can manage taints for the node.


<span id="ecs-terminal"></span>
### ECS terminal

Log in to the node console using ECS Terminal, where you can manage the node using the command line. For details, see [Log in to Linux instances via the console](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).


2. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Nodes** \> **Node**.

3. Find the target node and click  `...` \> **ECS Terminal ** to connect to the console using the ECS terminal, where you can manage the node.


<span id=".5p-l55yL55uR5o6n"></span>
### Viewing monitoring data

VKE allows you to view node\-related metrics and dashboards by using the cloud native observability feature. The alerting feature of Vital Managed Service for Prometheus (VMP) pushes alerting messages based on alerting rules. This achieves real\-time monitoring of node health status.


2. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Nodes** \> **Node**.

3. Click `...` \> **View monitoring** in the Actions column of the target node to go to the node monitoring page of cloud native observability, where you can view the monitoring dashboards related to the node. For more details, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).


<span id=".56e76Zmk6IqC54K5"></span>
### Removing nodes

The nodes that are no longer needed can be removed, provided that the action will not adversely affect the ongoing business.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This action will cause the pods on the node to be automatically migrated to other nodes. We recommend doing it during low\-traffic hours.</div>


* <div data-tips="true" data-tips-type="warning">For a node of the Pay\-as\-you\-go or spot instance type, the removal operation allows you to <strong>destroy and release the node</strong>. For a node of the subscription type, the action only excludes it from the node list. If the corresponding Elastic Compute Service (ECS) instance is required to be released, see <a href="https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription#.6YCA6K6i6K-05piO">Canceling Elastic Compute Service subscription</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you destroy and release a node, the data on the system volume and data volume will be deleted. This action cannot be undone. You need to proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">If the node pool where the node resides has enabled <strong>Automatic binding of Elastic IP Addresses</strong>, the bound IP addresses will be released along with the deletion and release of the node.</div>


* <div data-tips="true" data-tips-type="warning">If you do not destroy and release the node, the corresponding ECS instance will start to reinstall the operating system and clear the data on the system volume of the instance. When reinstalling the operating system, ECS will forcibly shut down Bare Metal instances and some High Performance Computing Optimized GPU instances. For details, see <a href="https://docs.byteplus.com/en/docs/ecs/StopInstance">Shutting down instances</a>.</div>


* <div data-tips="true" data-tips-type="warning">If <strong>Buy affinity group</strong> (beta) has been enabled for the node pool to which the target node belongs, the number of nodes must be an integer multiple of the affinity group size. Therefore, you cannot remove a single node. You can remove nodes by using the following methods:</div>


   * <div data-tips="true" data-tips-type="warning">Remove entire groups of nodes in a batch, with an affinity group as the minimum unit. For example, if the affinity group size of the current node pool is 2, you need to remove 2 nodes in the same affinity group at the same time. To remove multiple affinity groups, you need to select all nodes in each group. For the instructions on how to remove nodes in a batch, see the <strong>Remove nodes in a batch</strong> section.</div>


   * <div data-tips="true" data-tips-type="warning">Scale in the node pool. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Scaling_out-in_node_pools">Scaling node pools</a>.</div>


2. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Nodes** \> **Node**.

3. Click **Remove** in `...` menu to the right of the target node.

4. In the pop\-up window, select the options as needed. Then, click **Remove** to remove the node.

   
   |Parameter |Description |
   |---|---|
   |Synchronously destroy nodes of the pay\-as\-you\-go or spot instance type |Whether to destroy nodes synchronously when removing them?<br><br><br>* **Enable**: Nodes of pay\-as\-you\-go and spot instance types will be destroyed when removed.<br><br>* **Disable**: Nodes will not be destroyed when removed. |
   |Migrate all pods on the node except DaemonSet and set the node to unschedulable status before removal. |Whether to drain the node first before removal.<br><br><br>* **Enable**: drains the node before removal, which means migrating all pods on it (except DaemonSet) elsewhere and setting it to unschedulable status.<br><br>* **Disable**: does not drain the node before removal. |
   


<span id=".5pWF6Zqc6K-K5pat"></span>
### Diagnosis

The diagnosis of nodes can help users identify potential risks that may exist within a VKE cluster, including abnormal node status, excessive node workload, node network failures, and node kernel errors.


2. Click the target cluster name. In the left navigation bar, select **Nodes** \> **Node**.

3. Select **Diagnosis** in `...` menu to the right of the target node.

4. In the new page, create diagnostic tasks for this node. For details, see [Node diagnosis](https://docs.byteplus.com/en/docs/vke/Node-diagnosis).


<span id=".5om56YeP5pON5L2c6IqC54K5"></span>
## Batch management of nodes

VKE allows batch management of nodes, making it easy to quickly perform operations across multiple nodes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Virtual nodes cannot be managed in batch.</div>



2. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Nodes** \> **Node**.

3. Select the nodes you want and click **Batch operation** on the page, and then select the operation as needed.


The following content includes descriptions for each option in the Batch operations menu.

<span id=".5om56YeP6L-Q57u0"></span>
### Batch operation and maintenance

You can create batch O&M jobs for ECS nodes. Batch Job is a native automated O&M tool provided by BytePlus. It allows you to conveniently run O&M commands on one or more targets without passwords, logins, or bastion hosts. For details, see [Batch jobs](https://docs.byteplus.com/en/docs/ecs/Overview-of-cloud-assistant).


1. Before performing batch operation and maintenance on nodes, install the batch job client on each node. For details, see [Installing batch job clients](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client).

2. Select the nodes you want and click **Batch operation** \> **Batch operation and maintenance** on the page.

3. In the pop\-up window, click **Confirm** to proceed.


<span id=".5om56YeP572u5Li65Y-v6LCD5bqm"></span>
### Batch set to schedulable

This option can switch the nodes that have been cordoned or taken offline to the schedulable status, making them available again to accommodate new pods. This action will increase the remaining ResourceQuota of the cluster to which this node belongs.


1. Select the desired nodes and click **Batch operation** \> **Enable scheduling in batches** on the page.

2. In the pop\-up window, click **Make it schedulable** to proceed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only the nodes that have been cordoned or taken offline can be set to schedulable status.   </div>
   

<span id=".5om56YeP5bCB6ZSB"></span>
### Batch cordon

This option can cordon nodes in batch. The existing pods on the nodes will not be affected.


1. Select the nodes you want and click **Batch operation** \> **Batch cordon** on the page.

2. In the pop\-up window, click **Cordon** to proceed.


<span id=".5om56YeP5LiL57q_"></span>
### Batch offline

This option can take nodes offline in batch. For details, see [Taking nodes offline](https://docs.byteplus.com/en/docs/vke/Managing-nodes#.5LiL57q_6IqC54K5) mentioned earlier in this topic.


1. Select the nodes you want and click **Batch operation** \> **Batch offline ** on the page.

2. In the pop\-up window, click **Go offline** to proceed.


<span id=".5om56YeP56e76Zmk"></span>
### Batch removal

This option can remove nodes in batches. For details, see [Removing nodes](https://docs.byteplus.com/en/docs/vke/Managing-nodes#.56e76Zmk6IqC54K5) mentioned earlier in this topic.


1. Select the nodes you want and click **Batch operation** \> **Batch removal** on the page.

2. In the pop\-up window, click **Remove** to proceed.

   
   |Parameter |Description |
   |---|---|
   |Synchronously destroy nodes of the pay\-as\-you\-go or spot instance type |Whether to destroy nodes synchronously when removing them?<br><br><br>* **Enable**: Nodes of pay\-as\-you\-go and spot instance types will be destroyed when removed.<br><br>* **Disable**: Nodes will not be destroyed when removed. |
   |Migrate all pods on the node except DaemonSet and set the node to unschedulable status before removal. |Whether to drain the node first before removal.<br><br><br>* **Enable**: drains the node before removal, which means migrating all pods on it (except DaemonSet) elsewhere and setting it to unschedulable status.<br><br>* **Disable**: does not drain the node before removal. |
   


<span id=".6YCa6L-H6IqC54K55rGg6aG16Z2i566h55CG6IqC54K5"></span>
## Managing nodes on the node pool page

On the **Node pool** page, you can also manage nodes in the node pool by bringing them online, taking them offline, removing them, or cordoning them, either individually or in batches.


2. Click the target cluster name. In the left navigation bar, click **Node pool**.

3. Select the **Node list** tab, and then perform operations on the nodes as needed.
