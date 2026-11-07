---
title: "Serverless StarRocks high availability best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_StarRocks_high_availability_best_practices"
---

<span id="_1-fe高可用实践"></span>
## FE high availability best practices

For EMR Serverless StarRocks instances, you can select high availability during creation.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d889b2aaa00f35ccaedf125af64fb37.png) </span>

After creation is complete, directly access the corresponding internal network address to access the PLB with load balancing enabled. At this point, the load balancer will poll connections based on the status of the FE nodes to achieve high availability.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b122f0d424f67cfb1ce17b5acb2c724c.png) </span>

<span id="_1-1-通过代码均衡负载"></span>
### Load balancing through code

You can implement retry and load balancing in application layer code. When a specific connection fails, the code should control the system to automatically retry on other connections. With this approach, you need to configure multiple StarRocks frontend node addresses.

<span id="_1-2-通过-jdbc-connector-均衡负载"></span>
### Load balancing through JDBC Connector

If you use the MySQL JDBC Connector to connect to StarRocks, you can use JDBC's automatic retry mechanism for retry and load balancing.

```sql
jdbc:mysql:loadbalance://[host1][:port],[host2][:port][,[host3][:port]]...[/[database]][?propertyName1=propertyValue1[&propertyName2=propertyValue2]...]
```


<span id="_2-be高可用实践"></span>
## BE high availability best practices

<span id="_2-1-存算一体的高可用实践"></span>
### Integrated storage and compute high availability best practices

By default, StarRocks clusters already have high availability capabilities. High availability is achieved through three BE nodes. StarRocks supports Tablet multi\-replica storage (three by default), and multiple replicas ensure high reliability of data storage and high availability of services. With three replicas, an abnormality in one node does not affect service availability, and the cluster's read and write services can continue normally. Increasing the number of replicas also helps improve the system's high\-concurrency query capability.

When the number of BE nodes changes (such as during scaling), StarRocks can automatically add or remove nodes without stopping the service. Node changes trigger automatic migration of Tablets. When nodes are added, some Tablets are automatically balanced to the new nodes to ensure more balanced data distribution within the cluster; when nodes are reduced, Tablets on the machines to be taken down are automatically balanced to other nodes, thereby automatically ensuring that the number of replicas remains unchanged. Administrators can easily achieve elastic scaling without manually redistributing data.

The advantage of the integrated storage and compute architecture lies in its extremely fast query performance, but there are also some limitations:


* High cost: Three replicas are required to ensure data reliability. As users store increasing amounts of data, storage resources must be continuously expanded, resulting in wasted compute resources.

* Complex architecture: The integrated storage\-compute architecture must maintain consistency across multiple data replicas, increasing system complexity.

* Insufficient elasticity: In the integrated storage\-compute model, scaling up or down triggers data rebalancing, leading to a suboptimal elasticity experience.


<span id="_2-2-存算分离的高可用实践"></span>
### High availability practices for storage\-compute separation

Clusters with storage\-compute separation also feature three CN nodes and further achieve high availability at the storage layer. StarRocks storage\-compute separation technology decouples compute and storage based on the existing integrated storage\-compute architecture. In the new storage\-compute separation architecture, data is persistently stored in more reliable and cost\-effective remote object storage (such as TOS) or HDFS. CN local disks are used only to cache hot data to accelerate queries. When local cache hits occur, storage\-compute separation can deliver the same query performance as the integrated storage\-compute architecture. With the storage\-compute separation architecture, users can dynamically add or remove compute nodes, achieving scaling within seconds. Storage\-compute separation significantly reduces data storage and expansion costs, facilitates resource isolation, and enables elastic scaling of compute resources. Similar to the integrated storage\-compute architecture, the storage\-compute separation version maintains a similarly streamlined architecture. The entire system still consists of only FE and CN service processes, and the only additional requirement for users is to provide backend object storage.

In version v3.1 and above, StarRocks storage\-compute separation clusters are composed of FE and CN. In storage\-compute separation clusters, CN replaces BE found in integrated clusters.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c5209a9cff5699f976526004546a6cde.png) </span>

Compared to the integrated storage\-compute architecture, StarRocks' storage\-compute separation architecture offers the following advantages:


* Cost\-effective and seamlessly scalable storage.

* Elastic and scalable compute capacity. Because data is not stored on CN nodes, the cluster can scale up or down without cross\-node data migration or shuffle.

* Local disk cache for hot data to improve query performance.

* Optionally import data asynchronously to object storage to improve import efficiency.

* [Storage-compute separation best practices](https://docs.byteplus.com/docs/E-MapReduce/109144)。
