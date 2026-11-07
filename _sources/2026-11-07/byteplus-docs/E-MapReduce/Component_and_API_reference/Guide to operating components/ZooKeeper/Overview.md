---
title: "Overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/zk_overview"
---

Apache ZooKeeper is the open\-source implementation of the Google Chubby project. It was once a subproject of Hadoop and has been widely used in the big data field. ZooKeeper is inspired by the file system API and provides a set of simple APIs that enable developers to implement common coordination tasks, including electing a primary node, managing group membership, and managing metadata.

<span id="_1-适用的场景"></span>
## **1 Applicable scenarios**

Coordinating multiple tasks in distributed systems. For example:


* Typical primary\-secondary work patterns: when a secondary node is idle, it notifies the primary node that it can accept work, or when there is no primary node, many nodes need to elect a primary node.

* Distributed locks

* Metadata storage: because of ZooKeeper's sequential access and the design of storing all data in memory, ZooKeeper is also used by many systems as metadata storage. Well\-known open\-source projects that depend on ZooKeeper include Apache HBase, Apache Kafka, Apache HDFS, ClickHouse, Apache Flink, and many others.


<span id="_2-不适用的场景"></span>
## **2 Inapplicable scenarios**


* Not suitable for massive data storage, although it can be regarded as a strongly consistent key\-value store. When designing systems, coordination metadata should be separated from application data.

* Not suitable for fine\-grained locks. If distributed locks are too fine\-grained, it will place significant pressure on the server side and make the business extremely unstable.


<span id="_3-注意事项"></span>
## 3 Important notes


* The current SLA for ZooKeeper is 99.95%. When designing systems, you should consider the possibility of ZooKeeper being temporarily unavailable; otherwise, the impact of ZooKeeper being unavailable will be greatly amplified. There are many situations where ZooKeeper may be unavailable: hardware or software failures on the majority of nodes, network isolation or increased latency between nodes, network isolation or increased latency between client and server, and more.

* Once the data volume exceeds 1 GB, you should reconsider whether using ZooKeeper as metadata storage is appropriate.

* Once the lock granularity within a single system exceeds 1,000 locks or more than 100 clients compete for a single lock, you should reconsider whether using ZooKeeper as a coarse\-grained lock is appropriate.

* The ZooKeeper parameter jute.maxbuffer limits the size of request packets. The current default is 1 MB. If there are too many children under a znode, the .getChildren() return may exceed this limit, resulting in an error. When there is a requirement, first consider whether zk is being used correctly, such as having too many children under a single znode or too much data in a single znode, and so on. If there is indeed a requirement, it is possible to appropriately increase the value (both the client and server need to be configured).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f419792e32647b929ff130be59baee1b.png) </span>


* **To ensure the stability of components in the cluster, users are not advised to develop custom programs using zk.**
