---
title: "Restart a cluster"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/restart-a-cluster"
---

<span id="集群列表"></span>
## Cluster list

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f1409a91d064713b51f58dd1ad24910~tplv-goo7wpa0wc-image.image) </span>

**How to use:** 


1. Enter the ByteHouse Enterprise Edition Console.

2. Select Navigation Cluster Management \> Cluster List.


List information is as follows:


* Cluster name: Name when creating the cluster, unique across the account.

* State: Includes "Running", "Error", "Failed to create", "Deactivated".

* Region: Shows the region and availability zone where the cluster is located.

* Specification: The cluster specifications chosen during creation, display information includes node specifications, storage capacity, number of nodes and copy mode (single replica/dual replica).

* Health Level: Cluster health is determined through reference conclusions drawn from health indicators across multiple dimensions, with four health grades: Critical, Fail, Pass, and Good.

* Engine: This is the ByteHouse database engine version.

* Billing: Displays the payment mode and expiry date.

* Actions: Actions supported by the cluster include **restarting the cluster**, **parameter configuration (modify configuration) and changing specifications**, among others.


<span id="重启集群"></span>
## Restart a cluster

**Prerequisites:** 


* The user is either the ClusterAdmin or SystemAdmin role of the current cluster.

* The cluster is either in "Running" or "Error" state.


**How to use:** 


1. Visit Manage clusters \> Cluster list;

2. In the Actions on the right side of the designated cluster, select "Restart Cluster".

3. The cluster enters the "Restarting" state, and the cluster nodes will restart in batches.

   * For a single\-copy cluster, the cluster is not searchable and cannot import data at this time; the cluster restores after the restart is complete.

   * For a dual\-copy cluster, the cluster is searchable and can import data at this time; the cluster restores after the restart is complete.

4. After the cluster restart is complete, it will return to the "Running" state.


<span id="配置下发"></span>
## Configuration issued

**Prerequisites:** 


* The operating user is the ClusterAdmin role or the SystemAdmin role of the current cluster.

* The cluster is in the "Running" or "Error" state.


**How to use:** 


1. Visit Manage clusters \> Cluster List;

2. In the Actions on the right side of the designated cluster, select "Deploy Configuration".

3. Modify the configuration file and click "Deploy Configuration", and the deployment will be carried out immediately.

4. After deployment, the system will indicate "Partially activated for the user, the rest will need a restart to activate." If you modified non\-user configurations, refer to "Cluster Restart" for the subsequent restart operations.
