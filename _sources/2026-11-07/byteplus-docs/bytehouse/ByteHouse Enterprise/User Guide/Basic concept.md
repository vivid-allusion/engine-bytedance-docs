---
title: "Basic concept"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/concept"
---

<span id="b01f5721"></span>
# Physical concept


* **Area (Region):**  It is the geographical region of the BytePlus data center, divided into different regions according to the geographical location. After an instance is created, the geography of the instance cannot be changed.

* **Availability Zone (AZ):**  It is a collection of one or more physical data centers. In the same region, the power network of the availability area is independent of each other, that is, the failure of one availability area will not affect other availability areas in the same region. Availability areas in different regions are isolated from each other, and availability areas in the same region can communicate with each other.


<span id="bb1465e2"></span>
# Cluster


* **Cluster:**  A cluster is a set of independent servers located in the corresponding availability area, interconnected through a network, to provide complete ByteHouse services. A ByteHouse cluster provides a complete set of data management, data import, and data query services. Between different clusters, data is isolated from each other (cluster A cannot access cluster B's data), and the performance of query and import is isolated (query import of cluster A will not affect the performance of cluster B).

* **Node:**  It refers to a server in a cluster.

* **Shard:**  In the ByteHouse cluster, the data can be split into different nodes through the shard key, so that the total amount of data storage, import performance, and query performance increases with the growth of the cluster size. Each piece of data after splitting is called a shard.

* **Replica:**  In the ByteHouse cluster, it can be configured to copy a sharding data and store it in multiple nodes, so that the access of the cluster is not affected in the event of a single node failure. Each piece of data is a copy. ByteHouse Enterprise Edition supports 2 replica modes:

   * **Single replica mode:**  A shard of a ByteHouse cluster contains only one node. When a single node fails/when the cluster restarts, the cluster will not be queryable and cannot be imported.

   * **Dual replica mode:**  One sharding of the ByteHouse cluster contains two nodes, which realizes high availability, and the cluster can still provide services normally even when a single node fails/the cluster restarts.

* **Size:**  CPU/memory size for a single compute node. You can choose from 4 Core 16 GB to 64 Core 256 GB. Compute specifications are positively correlated with cluster performance.

* **Number of nodes (Count):**  Number of nodes in the cluster, if dual replica is selected, the number of nodes must be even.

* **Single\-node storage (Storage):**  The data disk space of a single node, that is, the space available to ByteHouse.

   * Under a single replica mode, the overall storage of the cluster is `single node storage space * number of nodes` . The capacity is `single node storage space * number of nodes`.

   * Under dual replica mode, the overall storage of the cluster is `single node storage space * number of nodes` .The capacity is `single node storage space * number of nodes/2`.


<span id="a61878b9"></span>
# Network


* **Private network (VPC, Virtual Private Cloud):**  Private networks build isolated, self\-configured, and managed virtual network environments for resources on the cloud. For details, see [Private network document](https://docs.byteplus.com/en/docs/vpc/What-is-VPC), it is recommended to configure the ByteHouse cluster and upstream data sources (such as Kafka, MySQL, etc.) in a VPC for easy network access.

* **Subnet:**  A subnet is an Internet Protocol Address block within a private network. After a private network is created, a private network can be divided into one or more network modules by creating a subnet. For details, see [subnet document](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

* **Security Group:**  A security group is a logical grouping that provides access policies for Cloud as a Service with the same security protection requirements and mutual trust within the same private network. It is an important means of cyber security isolation. For details, see [Security group document](https://docs.byteplus.com/en/docs/vpc/Security-group-overview). Please ensure that the current security group allows access to port 8123,9000 of ByteHouse.
