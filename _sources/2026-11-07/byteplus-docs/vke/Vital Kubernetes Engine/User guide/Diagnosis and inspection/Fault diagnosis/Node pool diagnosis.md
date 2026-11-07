---
title: "Node pool diagnosis"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/NodePool-diagnosis"
---

Cluster diagnosis helps you identify risks in various resources within VKE clusters, such as node pools, nodes, and pods. This topic describes how to configure the node pool diagnosis feature.

<span id=".6YWN572u6K-K5pat"></span>
## Configuring diagnosis


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Diagnosis**. On the page that appears, click **Create diagnosis task** to configure a node diagnostic task.

   
   |Parameter |Description |
   |---|---|
   |Diagnosis type |Specify the type of resource to be diagnosed. For this example, select **Node pool**. |
   |Node pool management |In the **All node pools** list on the left side, select the node pools on which you need to perform diagnosis, and add them to the **Selected node pool** list on the right side. |
   

4. Click **Confirm** to complete the configuration. The system will start the diagnosis and generate a diagnostic report.


<span id=".5p-l55yL6K-K5pat57uT5p6c"></span>
## Viewing diagnostic results

After the diagnostic task is complete, if it is in the **Anomaly** state, it indicates that risks exist in the node pool. You can click **View details** in the **Actions** column that corresponds to the target diagnostic task to view the diagnostic report.

The diagnostic result will display all diagnostic items, including successful, failed, and warning ones. You need to view these items on the **Pending** tab and resolve the issues.

<span id=".5LiL6L296K-K5pat5oql5ZGK"></span>
## Downloading diagnostic reports

After the diagnostic task is complete, you can download the diagnostic report in PDF format.


1. After the diagnostic task is complete, click **View details** in the **Actions** column that corresponds to the target diagnostic task to view the diagnostic result.

2. Click **Download the report** in the upper\-right corner to download the diagnostic report in PDF format.


<span id=".6K-K5pat6aG56K-05piO5ZKM5L-u5aSN5bu66K6u"></span>
## Diagnostic item descriptions and fix suggestions


|Diagnostic item |Check content |Fix suggestions |Reference |
|---|---|---|---|
|Scale\-out records within the last six hours |Check whether the cluster failed to scale out in the last six hours. Scale\-out failure may result in insufficient resources in the cluster, which affects normal business scheduling. |* Check the reason for the scale\-out failure.<br><br>* Manually scale out the cluster. |* [node pools](https://docs.byteplus.com/en/docs/vke/Scaling-a-NodePool)[node pools](https://docs.byteplus.com/en/docs/vke/Scaling-a-NodePool)<br><br>* [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes) |
|Scale\-in records within the last six hours |Check whether the cluster failed to scale in within the latest six hours. If the cluster failed to scale in, idle resources may exist in the cluster, which will result in resource waste. |* Check the reason for the scale\-in failure.<br><br>* Manually scale in the cluster. |* [node pools](https://docs.byteplus.com/en/docs/vke/Scaling-a-NodePool)[node pools](https://docs.byteplus.com/en/docs/vke/Scaling-a-NodePool)<br><br>* [Managing nodes](https://docs.byteplus.com/en/docs/vke/Managing-nodes) |
|Status check of node pool  |Check whether the node pool is not in the **Running** state. If the node pool is in an abnormal status, the resources in the node pool will become unavailable. |Troubleshoot based on the node pool status. |[Node pool status](https://docs.byteplus.com/en/docs/vke/Resource-status-description#.6IqC54K55rGg) |
|Cluster status |Check whether the cluster is not in the **Running** state. If the cluster is in an abnormal status, the resources in the node pool will become unavailable. |* If the cluster is in the `Updating[ClusterVersionUpgrading]` state, you can wait for the cluster upgrade to complete.<br><br>* If the cluster is in another abnormal status, contact technical support. |[Cluster status](https://docs.byteplus.com/en/docs/vke/Resource-status-description#.6ZuG576k) |
|ECS inventory |Check whether the ECS instance type used in the current node pool has sufficient stock. If the ECS instance type is sold out, nodes of this type cannot be created, which results in node pool scale\-out failure. |* Create node pools with other ECS instance types.<br><br>* Modify the instance type of the node pool. |* [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool)<br><br>* [Managing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools) |
|EIP capacity |Check whether the remaining EIP capacity is less than 1. If EIPs are insufficient and the automatic binding of EIPs to nodes is enabled for the node pool, the node pool will fail to scale out. |[Submit an application](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=vke) to increase the quota. |[Dependent underlying cloud service quotas](https://docs.byteplus.com/en/docs/vke/Limits#.5L6d6LWW5bqV5bGC5LqR5Lqn5ZOB6YWN6aKd6ZmQ5Yi2) |
|VKE cluster node quota |Check the node quota of the cluster. If the quota is used up, nodes will be unable to be added to the node pool, which results in scale\-out failure. |[Submit an application](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=vke) to increase the quota. |[Cluster-related quotas](https://docs.byteplus.com/en/docs/vke/Limits#.6ZuG576k6YWN6aKd6ZmQ5Yi2) |
|Remaining available IPs in the VPC subnet |Check whether the number of remaining IP addresses in the VPC is less than 5. If IP addresses in the VPC are used up, ECS instances cannot be created, and the node pool will fail to scale out. |None |None |
|VPC security group |Check the VPC security group. The configuration of security group rules affects internal network connectivity within the cluster. |None |[Configuring security groups](https://docs.byteplus.com/en/docs/vke/Security-group-settings) |
|Whether autoscaling is enabled |Check whether autoscaling is enabled for the node pool. If autoscaling is not enabled, the nodes in the node pool may be overloaded and cannot be autoscaled. |Enable the autoscaling feature for the node pool. |[Configuring node pool autoscaling](https://docs.byteplus.com/en/docs/vke/Scaling-a-NodePool) |
|CA add\-on status |Check whether the cluster autoscaling add\-on (cluster\-autoscaler) is installed in the cluster, and whether the add\-on is in a normal status. If the add\-on is not installed or in an abnormal status, the node pool cannot be autoscaled. |Install the cluster autoscaling add\-on (cluster\-autoscaler) and make sure that the add\-on works as expected. |[Install the add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.Y2x1c3Rlci1hdXRvc2NhbGVyLee7hOS7tg==) |
