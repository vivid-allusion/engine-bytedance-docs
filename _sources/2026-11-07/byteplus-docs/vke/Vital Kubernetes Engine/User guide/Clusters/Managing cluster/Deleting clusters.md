---
title: "Deleting clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Deleting-a-cluster"
---

If you delete a cluster, resources created in the cluster will be affected, which poses high risks. Make sure that the cluster is no longer used before deleting it. This topic describes the procedure and considerations for deleting a cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster already exists and is no longer used.

* The **deletion protection** feature is disabled for the cluster.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

Deleting a cluster will affect billing and resources created in the cluster. Exercise caution when you perform this operation. The detailed rules are as follows:


* By default, after you delete a cluster, pay\-as\-you\-go nodes in the cluster will be synchronously destroyed, but subscription nodes will only be removed.

   * After subscription nodes are removed, the operating systems of the corresponding Elastic Compute Service (ECS) instances will be reinstalled, and the data on the system volumes for the ECS instances will be cleared.

   * If pay\-as\-you\-go nodes in the cluster are not destroyed, the operating systems of the corresponding ECS instances will be reinstalled, and the data on the system volumes for the ECS instances will be cleared.

* You can choose to synchronously delete resources created within the cluster, including cloud disks, CLB instances, ALB instances, and NAT gateways.

   * After you delete a cluster, the CLB instances associated with the cluster will be deleted and cannot be retained.

   * This operation will delete the ALB instance associated with the cluster. You cannot retain the ALB instance.

   * You can choose whether to simultaneously delete NAT gateways.

   * If the cluster resources that you select for deletion are associated with other cloud services, the system will not destroy the resources. If you need to permanently delete these resources, go to the corresponding service consoles.

* By default, when you delete the cluster, the security groups associated with the cluster are synchronously deleted.

* When you delete the cluster, the trunk elastic network interfaces (ENIs) and the branch ENIs bound to the nodes will be simultaneously destroyed.

* When you delete the cluster, log projects and log topics automatically created for it (such as log topics for control plan add\-ons) will not be deleted automatically. You need to delete them manually.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For a description of control plane add\-on logs, see <a href="https://docs.byteplus.com/en/docs/vke/Collecting-control-plane-add-on-logs">Control plane add\-on logs</a>.  For instructions on deleting log projects and log topics of TLS, see <a href="https://docs.byteplus.com/en/docs/tls/Managing_projects#delete-a-project">Deleting log projects</a> and <a href="https://docs.byteplus.com/en/docs/tls/Managing_topics#.5Yig6Zmk5pel5b-X5Li76aKY">Deleting log topics</a>.   </div>
   

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Vital Kubernetes Engine (VKE) console](https://console.byteplus.com/vke). 

2. In the left navigation bar of the VKE console, click **Cluster**.

3. Find the target cluster and click `...` \> **Delete** in the Actions column.

4. Select the items that you want to synchronously delete. Click **Delete** in the lower\-right corner of the panel to delete the cluster.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

If the cluster fails to be deleted, resolve the corresponding issue, and then attempt to delete the cluster again based on the on\-screen prompts. You can also view operation logs for troubleshooting. If the cluster still fails to be deleted, [submit a ticket](https://console.byteplus.com/workorder/create) to obtain technical support.
