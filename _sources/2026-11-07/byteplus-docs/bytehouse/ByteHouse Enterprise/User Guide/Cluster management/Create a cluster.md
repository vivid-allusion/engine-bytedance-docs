---
title: "Create a cluster"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/create-a-cluster"
---

This article details how to create a ByteHouse Enterprise Edition cluster.

**Steps:** 


1. Access navigation bar **cluster management** Button to enter the cluster list page. Select "New Cluster" in the upper right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9f7d94e77c645a580385958a1475d98~tplv-goo7wpa0wc-image.image) </span>

2. Select the desired configuration one by one according to the interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a913e79dbe134cd1bb7d2b08c1ab1464~tplv-goo7wpa0wc-image.image) </span>

   Among them, the concept definition is as follows:

   * **Region:**  It is the geographical region of the BytePlus data center, divided into different regions according to the geographical location. After an instance is created, the geography of the instance cannot be changed.

   * **Availability zone:**  It is a collection of one or more physical data centers. In the same region, the power network of the availability area is independent of each other, that is, the failure of one availability area will not affect other availability areas in the same region. Availability areas in different regions are isolated from each other, and availability areas in the same region can communicate with each other.

   * **Payment method:**  ByteHouse Enterprise Edition currently only supports Monthly Flat mode. For billing details, please refer to: [Pricing rules](https://docs.byteplus.com/docs/bytehouse/pricing-rules).

   * **Specifications:**  Specifications for a single compute node, ranging from 4\-core 16 GB to 64\-core 256 GB. Compute specifications are positively correlated with cluster performance.

   * **Replica mode:** 

      * **Single replica:**  A sharding (Shard) of a ByteHouse cluster contains only one node (Node). When a single node fails/when the cluster restarts, the cluster will not be queryable and cannot be imported.

      * **Multiple copy:**  One sharding (Shard) of the ByteHouse cluster contains two nodes (Nodes) to achieve high availability, and the cluster can still provide services normally even when a single node fails/the cluster restarts.

   * **Number of nodes:**  Number of nodes in the cluster, if double replica is selected, the number of nodes must be even.

   * **Single\-node storage space:**  The data disk space of a single node, that is, the space available to ByteHouse.

      * Under a single replica, the overall storage of the cluster is `storage space of a single node * Number of nodes`. The capacity is`storage space of a single node * Number of nodes`.

      * Under dual replication, the overall storage of the cluster is `storage space of a single node * Number of nodes`The capacity is`storage space of a single node * Number of nodes/2`.

   * **Private network:**  A private network (VPC) builds an isolated, self\-configured, and managed virtual network environment for resources on the cloud. For details, see [Private network document](https://docs.byteplus.com/en/docs/vpc/What-is-VPC), it is recommended to configure the ByteHouse cluster and upstream data sources (such as Kafka, MySQL, etc.) in a VPC for easy network access.

   * **Subnet:**  A subnet is an Internet Protocol Address block within a private network. After a private network is created, a private network can be divided into one or more network modules by creating a subnet. For details, see [subnet document](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

   * **Security group:**  A security group is a logical grouping that provides access policies for Cloud as a Service with the same security protection requirements and mutual trust within the same private network. It is an important means of cyber security isolation. For details, see [Security group documentation](https://docs.byteplus.com/en/docs/vpc/Security-group-overview) Please ensure that the current security group allows access to port 8123,9000 of ByteHouse.

   * **Duration:**  Duration of your purchase, ranging from 1 month to 3 years.

   * **Auto\-renew:**  7 days before the cluster expires, the system will automatically deduct the renewal fee from your account balance. For details, refer to [Automatic renewal](https://docs.byteplus.com/docs/bytehouse/billing-method#%E8%87%AA%E5%8A%A8%E7%BB%AD%E8%B4%B9).

   * **Cluster name:**  The cluster name displayed on the console will also be used as the cluster name in the ByteHouse configuration file. The cluster name is unique within the account.

   * **Description:**  Description of the cluster.

3. In addition, you can choose to open a trial of advanced features according to your needs. For specific charges, please refer to the charging instructions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c252a0f4a687489babe4b48187672b7f~tplv-goo7wpa0wc-image.image) </span>

4. After selecting all the information, tick "I have read and agree to the relevant agreement", and click Confirm order to complete the creation of the cluster.

5. After the cluster shows the "running" state, it can be accessed normally.
