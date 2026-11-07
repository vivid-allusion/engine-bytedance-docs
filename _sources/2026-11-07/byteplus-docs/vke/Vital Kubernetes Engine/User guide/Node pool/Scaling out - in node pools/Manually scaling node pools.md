---
title: "Manually scaling node pools"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Scaling-a-NodePool"
---

You can adjust the expected number of nodes in a node pool to scale the node pool and keep the number of nodes at the expected value. This improves O&M efficiency. Scale\-out ensures sufficient node resources to support stable business operations. Scale\-in releases idle resources and reduces resource costs. This topic describes how to manually scale node pools.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">VKE node pools also support autoscaling. You can choose from elasticity solutions such as node autoscaling, instant node elasticity, and elastic scheduled scale\-out to supplement node capacity in the cluster based on workloads or predictable traffic peaks. For details, see the following documentation:</div>



* <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler"> node autoscaling (Cluster AutoScaler) node autoscaling (Cluster AutoScaler)</a></div>


* <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/vke/Configure_node_instant_autoscaler_Karpenter">Configuring node instant autoscaling (Karpenter)</a></div>


* <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/vke/Elastic_scheduled_scale-out">Elastic scheduled scale\-out</a></div>



<span id="7HFCgYoa"></span>
## Usage limits


* When you delete or release VKE\-associated nodes in ECS, VKE adjusts the nodes based on the expected number of nodes. For details, see [FAQ](https://docs.byteplus.com/en/docs/vke/How_does_the_expected_number_of_nodes_change).

* Node pools with different billing modes have different scaling restrictions. Carefully read the information displayed in the console before adjusting the **number of nodes**.

* The default node pool`vke-default-nodepool` can only be scaled out.

* Manual scale\-in will remove nodes. Note the following:

   * The pods on the removed nodes will be deleted, which may trigger rescheduling. If rescheduling fails, your business may be affected. Make sure that the cluster has sufficient resources for rescheduling. We recommend that you perform this operation during off\-peak hours.

   * By default, manual scale\-in destroys and releases nodes, and deletes data from both system volumes and data volumes. The data cannot be restored. Proceed with caution.


<span id="IgM4yYjF"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the right page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

4. Find the target node pool and click **Scaling** in the **Actions** column. Adjust the expected number of nodes for the current node pool as needed.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The number of nodes is the expected total number of nodes, not the number of nodes to add. For example, there are already 3 nodes in the current node pool before scale\-out. If you set the <strong>number of nodes</strong> to 5, the system will automatically add 2 more nodes, instead of adding 5 more nodes.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the node pool has <strong>Buy affinity group</strong> (beta) enabled, the <strong>Number of nodes</strong> must be an integer multiple of the affinity group size. Otherwise, scaling cannot be completed. To change the affinity group size, see <a href="https://docs.byteplus.com/en/docs/vke/Managing-NodePools">Managing node pools</a>.   </div>
   

5. Click **Confirm**.


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate result

After the configuration is complete, the node pool enters the **In scaling** state. After node pool scaling is complete, you can view the scaling record and details about the node pool.


1. Click the node pool name to go to the node pool details page.

2. Click the **Scaling record** tab to view scaling details of the node pool, including scaling activities, status, number of changed instances, and number of instances after the change.

   You can filter the scaling records based on conditions and time. Multiple filter conditions can be configured, and the relationship between them is **AND**. You can use the following keywords:

   * **Scaling record ID**: Filter records by scaling record ID. You can find it in the **Scaling activity** column of the scaling records. For example, `s-42ccnt`.

   * **Node ID**: Filter records by node ID. You can view node IDs in the **Number of changed instances** column that corresponds to a scaling record.

   * **Scaling type**: Filter records by scaling type. Supported options include **Scale in** and **Scale out**.
