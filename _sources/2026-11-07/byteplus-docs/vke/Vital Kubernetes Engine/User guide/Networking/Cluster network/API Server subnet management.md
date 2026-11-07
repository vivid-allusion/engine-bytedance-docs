---
title: "API Server subnet management"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Modifying-API-server-subnets"
---

The control plane nodes in a Vital Kubernetes Engine (VKE) cluster manage and control the entire cluster. By configuring multiple subnets across different availability zones, you can distribute the master nodes and provide disaster recovery for the API server, which further improves the high availability of the cluster. This topic describes how to manage the API Server's subnet configuration.

<span id="52eyGgll"></span>
## Background

As the core management unit of a Kubernetes cluster, the control plane hosts critical components such as the API Server, etcd, and Controller Manager. It serves as the central hub for cluster scheduling, service discovery, and resource orchestration. Its network connectivity and high availability directly impact the overall stability of the cluster. When the API Server operates in single\-subnet mode, limitations gradually emerge in scenarios such as business expansion, multi\-availability zone disaster recovery construction, and network plan adjustments. A single\-subnet failure may directly affect the overall availability of the API Server. IP address resources may become insufficient, and it is difficult to meet the requirements for fine\-grained network isolation and security policy enforcement.

VKE supports dynamically adding and deleting API Server subnets in the console. When a cluster evolves from a single\-subnet architecture to a multi\-subnet, multi\-availability zone architecture, adding subnets enables cross\-availability zone deployment of the API Server, improving disaster recovery capabilities and network elasticity. When subnet plan changes, resources become redundant, or policies are adjusted, unused API Server subnets can be deleted to optimize network topology, reclaim IP resources, and simplify O&M management. This enables smooth upgrading of the API Server network architecture and lifecycle management without the need to rebuild the cluster.

<span id="wJxtNnP1"></span>
## Add subnet

<span id=".5L2_55So6ZmQ5Yi2"></span>
### Usage limits


* You can add up to 6 subnets per cluster, with up to 3 availability zones and a maximum of 2 subnets per availability zone.

* Adding a subnet will trigger an API Server rolling update. The cluster status will change to **Updating**. The service will not be interrupted. However, we recommend performing this operation in off\-peak hours.

* In IPv4/IPv6 dual\-stack scenarios, a dual\-stack subnet is required.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. Click the name of the target cluster, and in the left navigation pane, click **Overview**.

4. On the **Overview** tab, under **Cluster API Server configuration**, click **Edit** next to the subnet.

5. Select the subnet(s) to add, and click **Confirm** to add the subnet to the API Server. When the cluster status changes from **Updating** to **Running**, the addition is successful.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend configuring multiple subnets for different availability zones to improve the high availability of the cluster.   </div>
   

<span id="Zzf2Awc8"></span>
## Delete subnet

<span id="mYpcK3md"></span>
### Usage limits


* At least 1 API Server subnet must be retained.

* The number of allocable IP addresses in the remaining subnets must be greater than 6 to ensure that the API Server can scale up to the maximum supported number of replicas.

* Deleting a subnet will trigger an API Server rolling update. The cluster status will change to **Updating**. The service will not be interrupted. However, we recommend performing this operation in off\-peak hours.


<span id="Ms1CXp9e"></span>
### Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. Click the name of the target cluster, and in the left navigation pane, click **Overview**.

4. On the **Overview** tab, under **Cluster API Server configuration**, click **Edit** next to the subnet.

5. Deselect the subnet, click **Confirm**, and the API Server subnets will be deleted. When the cluster status changes from **Updating** to **Running**, the deletion is successful.
