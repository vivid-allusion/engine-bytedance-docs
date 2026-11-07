---
title: "Adding worker nodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Adding-nodes"
---

Worker nodes in a cluster provide computing and storage resources for your applications. As your business grows, you may need to scale out your worker nodes. Vital Kubernetes Engine (VKE) supports auto scaling and manual scaling. This topic describes the steps and parameter settings of adding a new worker node to a cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* For manual scaling, a node pool has already been created. For details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

* Your BytePlus account balance is sufficient.  For details, see [Billing center](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you manually add a node of the <strong>Pay\-as\-you\-go</strong> or <strong>Spot instance</strong> type, the system checks your account balance. Ensure that your account balance is not less than USD 100.   </div>
   

<span id=".6Ieq5Yqo5omp5a65"></span>
## Auto scaling

Auto scaling is based on CA rules. CA adds nodes within predefined resource limits to respond to increasing resource requests of Pods in the cluster. For details about auto scaling, see [Cluster Autoscaler](https://docs.byteplus.com/en/docs/vke/How-Cluster-Autoscaler-works).

<span id=".5omL5Yqo5omp5a65"></span>
## Manual scaling

You can manually add new worker nodes to the cluster to meet growing resource demand. The following content describes two manual scale\-out methods.

<span id=".6YCa6L-H5omp5a655bey5pyJ6IqC54K55rGg5paw5aKe6IqC54K5"></span>
### Adding nodes by scaling out an existing node pool


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar of VKE, click **Cluster**.

3. In the cluster list, click the name of the target cluster to which you want to add nodes.

4. Select one of the following scaling methods:

   
   <Tabs>
   <Tab zoneid="DjcnxszMif" title="Method 1">
   <TabTitle>Method 1</TabTitle>
   
   1. In the left navigation bar of the cluster management page, click **Nodes** \> **Node**.
   
   2. On the **Node** page, click **Scale out**.
   
   3. On the **Scale out** page, select the node pool to which you want to add worker nodes, and set the number of worker nodes to add.
   
      
      |**Parameter** |**Description** |
      |---|---|
      |Node pool |Select the node pool where you want to add new nodes. Newly added nodes inherit configurations from the node pool, such as the availability zone, subnet, node instance specification, system configurations, security settings, labels, and taints. |
      |Number of new nodes |Follow the on\-screen prompts to enter a valid number within the node quota range. |
      
   
   4. Click **Confirm**.
   
      If the **status** of the node changes from **Creating** to **Running**, the node has been added.
   
   
   </Tab>
   <Tab zoneid="YmhGlrYm1H" title="Method 2">
   <TabTitle>Method 2</TabTitle>
   
   1. In the left navigation bar of the cluster management page, select **Nodes** \> **Node pool**.
   
   2. On the **Node pool** page, find the node pool where you want to add nodes and click **Scaling** in the **Actions** column.
   
   3. In the **Adjust quantity** dialog box, adjust the number of nodes in the node pool.
   
      
      |**Parameters** |**Description** |
      |---|---|
      |Node pool name |The name of the current node pool. This parameter cannot be adjusted. |
      |Number of nodes |Increase the number of worker nodes. You cannot exceed the upper limit on the number of nodes for the node pool.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Newly added nodes inherit configurations from the node pool, such as the availability zone, subnet, node instance specification, system configurations, security settings, labels, and taints.</div><br> |
      
   
   4. Click **Confirm**.
   
      If the **status** of the node pool changes from **Scaling** to **Running**, new nodes have been added. You can also check nodes within the node pool by clicking the node pool name and then navigating to the **Node list** tab on the **Node pool details page**.
   
   
   </Tab>
   </Tabs>
   


<span id=".6YCa6L-H5Yib5bu66IqC54K55rGg5paw5aKe6IqC54K5"></span>
### Adding nodes by creating a node pool

You can scale out a cluster by creating new node pools. For details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).
