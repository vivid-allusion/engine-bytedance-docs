---
title: "Features"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/feature-faq"
---

This topic summarizes the instance features FAQs for Document Database for MongoDB.

<span id=".5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5piv5ZCm5pSv5oyB5aSa5paH5qGj5LqL5Yqh5Yqf6IO977yf"></span>
### Does Document Database for MongoDB support multi\-document transactions?

Yes. Document Database for MongoDB currently offers MongoDB 4.2, 4.4, 5.0, 6.0, 7.0, 8.0 and 8.3. The supported multi\-document transaction feature is consistent with that of open\-source MongoDB. For more details, refer to [Transactions](https://www.mongodb.com/docs/v4.4/core/transactions/).

<span id=".5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5piv5ZCm5pSv5oyB5bWM5aWX5paH5qGj77yf"></span>
### Does Document Database for MongoDB support nested documents?

Yes. For example, the content in the example below is a nested document.

```JavaScript
{
    "_id": ObjectId("66ee651d8d1acb8a892c****"),
    "item":"journal",
    "qty":25,
    "size":{
        "h":14,
        "w":21,
        "uom":"cm"
    },
    "status":"A"
}
```


<span id=".5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5aaC5L2V5aSE55CG6IqC54K55pWF6Zqc77yf"></span>
### How does Document Database for MongoDB address node failures?

Document Database for MongoDB offers two architecture types: replica set and sharding cluster. For more information about the product architecture, refer to [Product architecture](https://docs.byteplus.com/en/docs/mongodb/about-mongodb#.5Lqn5ZOB5p625p6E). The instances of each architecture address node failures with different mechanisms.


<Tabs>
<Tab zoneid="QCk4cqcfQw" title="Replica set instance">
<TabTitle>Replica set instance</TabTitle>

Replica set instances provide three nodes by default for application access. If the primary node fails, secondary node is elected as the new primary. If secondary node fails, hidden node replaces the failed node as a new secondary, continues providing service, and checks and repairs the failed node. This process is completely transparent to the application and may result in a temporary disconnection lasting less than 30 seconds, so we recommend you add a reconnection mechanism to the design of your application.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="0">warning</div>


<div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">Do not connect applications in the production environment directly to the primary node in the replica set, but via the address under the <strong>Connectivity</strong> tab in the <a href="https://console.byteplus.com/db/mongodb/list">MongoDB console</a>. if a node fails, the read and write operations of the application will not be affected by the node switchover.</div>



</Tab>
<Tab zoneid="uemiYjbBve" title="Sharding cluster instance">
<TabTitle>Sharding cluster instance</TabTitle>

A sharding cluster instance is mainly composed of Shards, Mongos nodes, and ConfigServer nodes:


* Both Shard and ConfigServer components adopt three\-node replica set architecture. When one of the nodes fails, the system will replace the failed node with a hidden node to ensure service continuity, and then inspect and repair the failed node. This process is completely transparent to the application and may result in a temporary disconnection lasting less than 30 seconds, so we recommend you add a reconnection mechanism to the design of your application.

* The Mongos component adopts two\-node architecture. When a Mongos node fails, the services associated with it will be unavailable.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not connect applications in the production environment to a single Mongos node, but to all Mongos nodes via the private address under the <strong>Connectivity</strong> tab in the <a href="https://console.byteplus.com/db/mongodb/list">MongoDB console</a>. In this way, if a Mongos node fails, the client can automatically perform a failover, distributing requests to healthy Mongos nodes.   </div>
   


</Tab>
</Tabs>


<span id=".5a6e5L6L56OB55uY5L2_55So546H6LaF6L-H5aSa5bCR77yM5a6e5L6L5Lya5ouS57ud5YaZ5YWl5pWw5o2u77yf"></span>
### At what disk utilization percentage will the instance reject data writes?

When the instance disk utilization exceeds 95%, the instance will prohibit data writing. Only data read operations are allowed on the instance, while write operations will result in an `Out of diskSpace` error. This threshold is a fixed security policy of the product and **cannot be adjusted or disabled**. When disk utilization drops to 95% or below, the system automatically resumes data write services. We recommend that you closely monitor business changes and instance usage. Expand instance storage space in a timely manner before disk utilization exceeds the appropriate threshold. For specific procedures, refer to [Instance configuration modification](https://docs.byteplus.com/en/docs/mongodb/solutions-for-spec-modification).

You can monitor the instance's disk utilization through the MongoDB console. For specific procedures, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/mongodb/view-monitoring-data).

You can also create alert policies using the Cloud Monitor's alerts and monitoring service. You will receive timely notifications when disk utilization exceeds a custom threshold. For specific procedures on creating an alert policy, refer to [Setting alerts](https://docs.byteplus.com/en/docs/mongodb/set-alert).

<span id=".bW9uZ29kYi3kuI3lkIzniYjmnKzmlK_mjIHnmoTlip_og73nibnmgKfmnInkvZXlt67liKvvvJ8="></span>
### What are the differences in features supported by different MongoDB versions?

Document Database for MongoDB, 4.2, 4.4, 5.0, 6.0, 7.0, 8.0, and 8.3. Different versions support different features. For specific feature differences[](https://docs.byteplus.com/en/docs/mongodb/features), refer to the Features.
