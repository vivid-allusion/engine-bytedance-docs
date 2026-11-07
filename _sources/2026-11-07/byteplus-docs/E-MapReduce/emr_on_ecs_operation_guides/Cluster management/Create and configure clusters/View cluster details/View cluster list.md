---
title: "View cluster list"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/view_cluster_list_and_details"
---

After creating a cluster, regardless of whether the cluster has been released, you can monitor its status and obtain detailed information about its execution and any errors that may occur.

<span id="前提条件"></span>
## **Prerequisites**

Clusters have been created. Refer to [Create clusters](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later).

<span id="查看集群列表"></span>
## **View cluster list**


1. Log in to the .

2. In the top menu bar, select the region as needed.

3. Click Cluster Management \- Cluster List in the left menu to view.


<span id="集群列表"></span>
## **Cluster list**

The cluster list displays clusters whose status is not Released or Initialization Failed in a table format. The information is described as follows.


|Name |Description |Filter/sort criteria |
|---|---|---|
|Favorite cluster |Click ⭐️ to favorite the cluster |Favorited clusters appear at the top of search results |
|Cluster name |Cluster name and cluster ID. Click the cluster name to enter the cluster details page |Supports fuzzy search by cluster name and exact search by cluster ID |
|Cluster type |Cluster type |Supports multi\-select filtering |
|Cluster status |The cluster's status: Only clusters whose status is not Released or Initialization Failed are displayed. For details, see [View cluster status](https://docs.byteplus.com/docs/E-MapReduce/Cluster_status) |Supports multi\-select filtering |
|Public address |Public address bound to cluster nodes |*  |
|Payment type |Cluster payment type |Supports multi\-select filtering |
|Running time |Running time from creation to present |*  |
|Creation time |Cluster creation time |Supports queries by time range, with time accurate to the day<br><br>Supports sorting. By default, the most recently created clusters appear at the top, but favorited clusters are prioritized |
|Operation |Supported cluster operations:<br><br>Scale out: Entry point for the cluster scale\-out feature. For more information, see [Scale clusters](https://docs.byteplus.com/docs/E-MapReduce/Scale_up_clusters)<br><br>Release: Release the current cluster. Only Pay\-As\-You\-Go clusters support release. For more information, see [Release clusters](https://docs.byteplus.com/docs/E-MapReduce/Release_clusters)<br><br>Restart: Restart the current cluster.<br><br>Switch from Pay\-As\-You\-Go to Subscription: Convert a Pay\-As\-You\-Go cluster to a Subscription cluster. Subscription clusters cannot be converted to Pay\-As\-You\-Go. |*  |


<span id="历史集群列表"></span>
## **Historical cluster list**

The historical cluster list displays only clusters whose status is Released or Initialization Failed in a table format.


|Name |Description |Filter/sort criteria |
|---|---|---|
|Favorite cluster |Not supported |*  |
|Cluster name |Same as in the cluster list ||
|Cluster type |Same as in the cluster list ||
|Cluster status |Cluster status. Only clusters whose status is not Released or Initialization Failed are displayed. |Supports multi\-select filtering |
|Public address |Same as in the cluster list ||
|Payment type |Same as in the cluster list ||
|Running time |Duration from cluster creation to the current status |*  |
|Creation time |Same as in the cluster list ||
|release time |Cluster release time |Supports sorting. By default, the most recently released clusters are listed first. |
