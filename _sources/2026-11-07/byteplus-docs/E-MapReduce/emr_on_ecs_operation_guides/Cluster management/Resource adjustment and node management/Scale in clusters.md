---
title: "Scale in clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs-scale_down_clusters"
---

When there is excess computing resource in an E\-MapReduce (EMR) cluster, you can reduce the number of node groups to save costs. This article introduces how to scale down clusters.

<span id="_1-使用限制"></span>
# Limits


* The cluster status must be Running.

* Only task and core node groups support scaling down. Among them, only core node groups in EMR version 3.12.0 and above support scaling up.

* To scale down core node groups in EMR version 3.11.0 and below, you can manually scale down by unsubscribing the corresponding node instances in the ECS console. Before unsubscribing, make sure to migrate HDFS data to avoid data loss caused by shutting down nodes. For detailed operations, see [Manual scale down of core node groups (EMR version 3.11.0 and below).](https://docs.byteplus.com/docs/E-MapReduce/ecs-scale_down_clusters#ac00be86).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, Task nodes in Subscription clusters do not support scaling in.</div>


* <div data-tips="true" data-tips-type="tip">The Core node group stores data. After scaling out, it is not recommended to destroy it to avoid potential data security risks.</div>



<span id="14cac756"></span>
# Preparation

Confirm that the services of the relevant node groups have stopped. For detailed operations, see [Stop node component services](https://docs.byteplus.com/docs/E-MapReduce/ecs-scale_down_clusters#e6f6bad7).

<span id="_2-操作步骤"></span>
# procedure


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?).

2. In the left navigation pane, click **Resources \> on ECS \> Cluster details \> Nodes**, and go to the **Nodes** page.

3. Click the **scaling** button in the Actions column of the target node group.

4. In the scale\-down dialog box, configure the scale\-down settings and specify the number of nodes to retain.

5. Select to agree to the E\-MapReduce service terms, and click the **Confirm** button to submit. This completes the disk scale\-down operation.

6. After scaling down, manually restart the services for each node group.


<span id="e6f6bad7"></span>
# Stop node component services

If the nodes selected for scaling down have the following component services installed, stop these component services before releasing the nodes. Otherwise, task scheduling failures and data security issues may occur.

<span id="c5ca05d3"></span>
## Stop YARN NodeManager


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?), and in the left navigation bar, click **Resources \> on ECS \> Cluster details \> Service list \> YARN** to enter the YARN service details page.

2. On the **Deployment topology** tab, click the **NodeManager** component's **Stop** button in the Actions column.


<span id="d7ca0b65"></span>
## Stop HDFS DataNode


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?), and in the left navigation bar, click **Resources \> on ECS \> Cluster details \> Service list \> HDFS** to enter the HDFS service details page.

2. On the **Deployment topology** tab, click the **DataNode** component's **Stop** button in the Actions column.


<span id="de94e737"></span>
## Stop HBase RegionServer


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?), and in the left navigation bar, click **Resources \> on ECS \> Cluster details \> Service list \> HBase** to enter the HBase service details page.

2. On the **Deployment topology** tab, click the **RegionServer** component's **Stop** button in the Actions column.


<span id="f69385e9"></span>
## Stop StarRocks BE


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?), and in the left navigation bar, click **Resources \> on ECS \> Cluster details \> Service list \> StarRocks** to enter the StarRocks service details page.

2. On the **Deployment topology** tab, click the **BE** component's **Stop** button in the Actions column.


<span id="1ca4cd1b"></span>
## Stop Doris BE


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?), and in the left navigation bar, click **Resources \> on ECS \> Cluster details \> Service list \> Doris** to enter the Doris service details page.

2. On the **Deployment topology** tab, click the **BE** component's **Stop** button in the Actions column.


<span id="ac00be86"></span>
# Manual scale down of core node groups (EMR version 3.11.0 and below).


1. Take down Datanode nodes. In **Cluster details\>**  **Service list \> HDFS\>Deployment topology**, click the "take down" button for the core node **take down** and wait until the core node is taken down. After the node is taken down, HDFS data is automatically migrated to other nodes.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1e5a7f5913349978b5dc4cb5ad50b47~tplv-goo7wpa0wc-image.image) </span>

2. To unsubscribe or release instances, click the node ID to go to the instance details page:

   * Subscription → follow the refund process. For detailed operations, see [Refund policy](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription).

   * Pay\-as\-you\-go → directly delete the instance. For detailed operations, see [Delete instance](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances).
