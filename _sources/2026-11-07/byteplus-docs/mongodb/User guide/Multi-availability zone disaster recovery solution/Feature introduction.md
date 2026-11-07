---
title: "Feature introduction"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/feature-introduction"
---

Document Database for MongoDB supports setting multi\-availability zone deployment when creating or restoring data to a new instance. Compared to single availability zone deployment, multi availability zone deployment has higher disaster recovery capability and can withstand server room level failures. This topic describes MongoDB's availability zone deployment methods.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Multiple availability zone deployment is only supported in regions with 3 or more availability zone resources. Currently, only the following regions support 3 or more availability zone resources:

   * China (Shanghai)

   * China (Beijing)

   * China (Guangzhou)

* FlexPL volumes currently support multi\-AZ deployment in China (Shanghai) and single\-AZ deployment in China (Beijing) and China (Guangzhou).

* Deployment across availability zones can improve availability, but there may be a network latency of 2 ms to 3 ms.


<span id=".5Y-v55So5Yy66YOo572y5pa55byP"></span>
## Availability zone deployment method

Document Database for MongoDB implements zone\-disaster recovery through multi\-availability zone deployment. Different instance types have different node deployment strategies.

<span id=".5Ymv5pys6ZuG5a6e5L6L"></span>
### Replica set instance


|Deployment method |Node deployment policy |
|---|---|
|Multi\-availability zone deployment |One replica set instance contains three replicas, that is, three nodes by default. These three nodes are deployed in three different availability zones under the same region and exchange information with each other through the internal network. When the communication of the primary availability zone fails, the system automatically switches the traffic from the primary node to a secondary node to ensure the high availability of the entire replica set instance. |
|Single availability zone deployment |All nodes in replica set instance are deployed in the same availability zone. |


The availability zone deployment architecture diagram for replica set instances is shown below.


<Tabs>
<Tab zoneid="xHMLL4GBIW" title="Multi-availability zone deployment">
<TabTitle>Multi-availability zone deployment</TabTitle>

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_41f3192579c6f0d1b6c065c647d37ec9.png) </span>


</Tab>
<Tab zoneid="T6UNixTHsA" title="Single availability zone deployment">
<TabTitle>Single availability zone deployment</TabTitle>

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_14a25c3000e7b56986f2515b9843e38c.png) </span>


</Tab>
</Tabs>


<span id=".5YiG54mH6ZuG576k5a6e5L6L"></span>
### Sharding cluster instance


|Deployment method |Node deployment policy |
|---|---|
|Multi\-availability zone deployment |Components of a sharding cluster instance are deployed in three different availability zones under the same region and exchange information with each other through the internal network. When the communication of the primary availability zone fails, the system automatically switches the traffic from the primary node to a secondary node to ensure the high availability of the entire sharding cluster instance.<br><br><br>* **Mongos nodes**: Evenly deployed across all availability zones. One sharding cluster instance contains two Mongos nodes by default, which are deployed in two different availability zones. When a third node is added, the node is deployed in the third availability zone by default, and subsequently added nodes are deployed in other availability zones in turn.<br><br>* **Shard**: The primary node of each shard is deployed in the primary availability zone by default. Secondary and hidden nodes are deployed in two different secondary availability zones. The availability zone deployment method of nodes of new shards is the same as that of nodes of existing shards.<br><br>   For example, the primary nodes of both shard 1 and shard 2 are deployed in the primary availability zone A, while the secondary and hidden nodes are deployed in the secondary availability zones B and C in turn. If shard 3 is added, the primary node of shard 3 is also deployed in the primary availability zone A, while its secondary and hidden nodes are deployed in the secondary availability zones B and C in turn.<br><br>* **ConfigServer nodes**: The primary node, secondary nodes, and hidden nodes of each ConfigServer are deployed in three different availability zones. |
|Single availability zone deployment |All Mongos nodes, shards, and ConfigServer nodes of one sharding cluster instance are deployed in the same availability zone. |


The availability zone deployment architecture diagram for sharding cluster instances is shown below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each Mongos node in a MongoDB instance has the same function. To simplify the illustration, only the connection between Mongos Node 1 and the ConfigServer and Shard nodes is shown below. All other Mongos nodes connect in the same way as Mongos Node 1.</div>



<Tabs>
<Tab zoneid="d4whGDVgxh" title="Multi-availability zone deployment">
<TabTitle>Multi-availability zone deployment</TabTitle>

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2558b6a5c78c964fbfeadd51b96c8180.png) </span>


</Tab>
<Tab zoneid="GDFFWMNZ6i" title="Single availability zone deployment">
<TabTitle>Single availability zone deployment</TabTitle>

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4b274f9a2e7592d4ec87c17181bc5463.png) </span>


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Relevant documents


* [Deploying in multiple availability zones](https://docs.byteplus.com/en/docs/mongodb/deploy-multi-az)

* [Viewing availability zone of instance](https://docs.byteplus.com/en/docs/mongodb/view-az)
