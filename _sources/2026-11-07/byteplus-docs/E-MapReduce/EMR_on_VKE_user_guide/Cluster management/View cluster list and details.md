---
title: "View cluster list and details"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/vke_view_cluster_list_and_details"
---

This article describes how to view an overview of the clusters under your account.

<span id="c03b9428"></span>
## View basic information of a VKE cluster

After a cluster is created, you can monitor and manage the cluster. Select a cluster and click the cluster name to enter the cluster details page, where you can view the cluster's basic configuration, network information, and deployed node information.

<span id="a2f22c92"></span>
### Procedure


1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. On the EMR on VKE page, click the **name** of the cluster you want to view.

3. On the **cluster details** page, you can view the following information.

   
   |Name |Description |
   |---|---|
   |Cluster name |Virtual cluster name |
   |Cluster ID |Virtual cluster ID |
   |Associated project |Project where the virtual cluster resides |
   |Created by |Creator of the virtual cluster |
   |Label |Labels on the virtual cluster |
   |Deployment region |Region where the virtual cluster resides |
   |Product version |Virtual cluster version |
   |Runtime |Running duration of the virtual cluster |
   |Creation time |Creation time of the virtual cluster |
   |VPC |Network information of the virtual cluster. Click to view VPC details. |
   |Public IP |Public IP of the virtual cluster, which allows nodes and applications in the VKE cluster to access the public network. Click to view public IP details. |
   |Resource type |Existing VKE resources / Create new VKE resources |
   |Associated VKE cluster |VKE cluster where the virtual cluster is deployed. Click to go to the VKE cluster. |
   |Pod taint tolerance |Taint information of the Pod: NoSchedule / NoExecute / PreferNoSchedule |
   |Enable Elastic Container Instance (VCI) to run jobs |Only Spark and Ray jobs are supported. Can be enabled or disabled. |
   |Service |Services deployed on the virtual cluster |
   


<span id="29c522e0"></span>
## View the running status of the VKE cluster

Users can view the running status of all VKE clusters through the management console.

<span id="e572444b"></span>
### Procedure


1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. On the EMR on VKE page, you can view the cluster list.

   
   |Name |Description |Filter criteria / Sorting |
   |---|---|---|
   |Cluster name / ID |Name and ID of the virtual cluster. Click the cluster name to enter the cluster details page. |Supports fuzzy search by cluster name and exact search by cluster ID. |
   |Cluster status |Cluster status. Only clusters whose status is not Released or Initialization Failed are displayed. |Supports multi\-select filtering. |
   |Associated VKE cluster |The VKE cluster where the virtual cluster resides. Click to navigate to the VKE cluster. |Supports multi\-select filtering. |
   |Creation time |The time when the cluster was created. |Supports querying by time range, with time accurate to the day.<br><br>Supports sorting. By default, the most recently created clusters are listed first. |
   |Actions |Supported actions for the cluster:<br><br>Delete: Release the current cluster. For more information, see [Release clusters](https://docs.byteplus.com/docs/E-MapReduce/104399)[Release cluster](https://docs.byteplus.com/en/docs/E-MapReduce/Release_cluster). | |
   


<span id="6ae10950"></span>
### Cluster status


|Status |Note |
|---|---|
|Initializing |The initial status after clicking Create for the virtual cluster, indicating that the cluster is initializing resources and deploying applications. |
|Initialization failed |Status after cluster creation fails. The main reasons are:<br><br><br>1. Cluster resource initialization failed (such as network configuration, insufficient VKE resources, and so on).<br><br>2. Application deployment failed (VKE node Pod specifications do not meet the deployment requirements for service Pods, or components associated with the application, such as rds and tos, cannot communicate with the VKE network).<br><br>3. Creation timed out. |
|Running |The virtual cluster is in a normal running state. EMR management capabilities are available. |
|Exception |The virtual cluster cannot provide services in this state, and this state cannot be recovered.<br><br>The main reasons for exceptions are:<br><br><br>1. The referenced VKE cluster for the virtual cluster has been deleted.<br><br>2. The number of available nodes in the referenced VKE cluster for the virtual cluster is zero.<br><br>3. The VKE cluster is in Deleting, Stopped, or Failed status. |
|Deleting |The virtual cluster is being deleted. |
|Deleted |The virtual cluster has been deleted. |
|Changing |When service parameters are modified, restarted, or nodes change in a running virtual cluster, the virtual cluster enters a changing state. During this time, applications deployed in the VKE cluster may be temporarily unavailable. |
