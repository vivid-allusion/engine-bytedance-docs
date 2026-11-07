---
title: "Local disk specifications"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/product-specification"
---

This topic describes the specifications supported by BytePlus Document Database for MongoDB instances with local disk storage.

<span id="FiurFYyE"></span>
## Compute node specifications

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Document Database for MongoDB instances with local disk storage provide three different types of node specifications: . For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/storage_type">Specification types</a>.</div>


* <div data-tips="true" data-tips-type="default">The node type in replica set instances is Mongod. Each replica set instance is currently fixed at 3 nodes and cannot be changed.</div>


* <div data-tips="true" data-tips-type="default">Each sharding cluster instance can contain 2~32 Mongos nodes and 2~32 shards (each shard contains 3 nodes).</div>


* <div data-tips="true" data-tips-type="default">The recommended number of connections in the table below refers to the recommended number of connections for a single node. You can also modify the number of connections for a single node by using the <code>net.maxIncomingConnections</code> parameter. For more information about the <code>net.maxIncomingConnections</code> parameter, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/supported-parameter">Supported parameters</a>. For parameter modification methods, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-parameter">Modifying instance parameters</a>.</div>



<span id=".5Ymv5pys6ZuG5a6e5L6L"></span>
### General\-purpose specifications

<span id="UEpbI046"></span>
#### Replica set instance


|Specification code |CPU and memory |Recommended number of connections |
|---|---|---|
|mongo.2c4g |2 cores 4 GiB |2000 |
|mongo.4c8g |4 cores 8 GiB |4000 |
|mongo.4c16g |4 cores 16 GiB |6000 |
|mongo.4c32g |4 cores 32 GiB |8000 |
|mongo.8c16g |8 cores 16 GiB |16000 |
|mongo.8c32g |8 cores 32 GiB |16000 |
|mongo.8c64g |8 cores 64 GiB |16000 |
|mongo.16c32g |16 cores 32 GiB |24000 |
|mongo.16c64g |16 cores 64 GiB |24000 |
|mongo.16c128g |16 cores 128 GiB |24000 |
|mongo.32c64g |32 cores 64 GiB |24000 |
|mongo.32c128g |32 cores 128 GiB |42000 |
|mongo.32c256g |32 cores 256 GiB |42000 |
|mongo.60c120g |60 cores 120 GiB |64000 |
|mongo.60c240g |60 cores 240 GiB |64000 |
|mongo.90c360g |90 cores 360 GiB |64000 |
|mongo.120c480g |120 cores 480 GiB |64000 |


<span id=".5YiG54mH6ZuG576k5a6e5L6L"></span>
#### Sharding cluster instance


<Tabs>
<Tab zoneid="cGeiJoXppl" title="Mongos">
<TabTitle>Mongos</TabTitle>


|Specification code |CPU and memory |Recommended number of connections |
|---|---|---|
|mongo.mongos.2c4g |2 cores 4 GiB |2000 |
|mongo.mongos.4c8g |4 cores 8 GiB |4000 |
|mongo.mongos.4c16g |4 cores 16 GiB |6000 |
|mongo.mongos.4c32g |4 cores 32 GiB |8000 |
|mongo.mongos.8c16g |8 cores 16 GiB |16000 |
|mongo.mongos.8c32g |8 cores 32 GiB |16000 |
|mongo.mongos.8c64g |8 cores 64 GiB |16000 |
|mongo.mongos.16c32g |16 cores 32 GiB |24000 |
|mongo.mongos.16c64g |16 cores 64 GiB |24000 |
|mongo.mongos.16c128g |16 cores 128 GiB |24000 |
|mongo.mongos.32c64g |32 cores 64 GiB |24000 |
|mongo.mongos.32c128g |32 cores 128 GiB |42000 |
|mongo.mongos.32c256g |32 cores 256 GiB |42000 |
|mongo.mongos.60c120g |60 cores 120 GiB |64000 |



</Tab>
<Tab zoneid="MJjHEQJaM1" title="Shard">
<TabTitle>Shard</TabTitle>


|Specification code |CPU and memory |Recommended number of connections |
|---|---|---|
|mongo.shard.2c4g |2 cores 4 GiB |2000 |
|mongo.shard.4c8g |4 cores 8 GiB |4000 |
|mongo.shard.4c16g |4 cores 16 GiB |6000 |
|mongo.shard.4c32g |4 cores 32 GiB |8000 |
|mongo.shard.8c16g |8 cores 16 GiB |16000 |
|mongo.shard.8c32g |8 cores 32 GiB |16000 |
|mongo.shard.8c64g |8 cores 64 GiB |16000 |
|mongo.shard.16c32g |16 cores 32 GiB |24000 |
|mongo.shard.16c64g |16 cores 64 GiB |24000 |
|mongo.shard.16c128g |16 cores 128 GiB |24000 |
|mongo.shard.32c64g |32 cores 64 GiB |24000 |
|mongo.shard.32c128g |32 cores 128 GiB |42000 |
|mongo.shard.32c256g |32 cores 256 GiB |42000 |
|mongo.shard.60c120g |60 cores 120 GiB |64000 |
|mongo.shard.60c240g |60 cores 240 GiB |64000 |
|mongo.shard.90c360g |90 cores 360 GiB |64000 |
|mongo.shard.120c480g |120 cores 480 GiB |64000 |



</Tab>
<Tab zoneid="wTScfCC4xk" title="ConfigServer">
<TabTitle>ConfigServer</TabTitle>


|Specification code |CPU and memory |Recommended number of connections |
|---|---|---|
|mongo.config.2c4g |2 cores 4 GiB |2000 |
|mongo.config.4c8g |4 cores 8 GiB |4000 |
|mongo.config.4c16g |4 cores 16 GiB |6000 |
|mongo.config.4c32g |4 cores 32 GiB |8000 |
|mongo.config.8c16g |8 cores 16 GiB |16000 |
|mongo.config.8c32g |8 cores 32 GiB |16000 |
|mongo.config.8c64g |8 cores 64 GiB |16000 |
|mongo.config.16c32g |16 cores 32 GiB |24000 |
|mongo.config.16c64g |16 cores 64 GiB |24000 |
|mongo.config.32c64g |32 cores 64 GiB |24000 |



</Tab>
</Tabs>


<span id="GCaoaYEO"></span>
## Storage specifications

The storage space for Document Database for MongoDB instances is divided into single\-shard or single\-node storage, and maximum available storage.

<span id=".5Y2V5YiG54mH5oiW5Y2V6IqC54K55a2Y5YKo56m66Ze0"></span>
### Single\-shard or single\-node storage

This refers to the replica set storage space specifications selected when purchasing an instance, or the storage space specifications of Shard and ConfigServer nodes in a sharding cluster instance.

Different instance types and node types support different storage specifications. The specific specifications are shown in the table below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Node specifications are different, and the supported storage space ranges are also different. For the specific value range of storage space, refer to the console. If you need more storage, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support to increase the storage space limit.</div>



|Instance (or component) type ||Specification code |Storage range |
|---|---|---|---|
|Replica set instance ||mongo.storage<br><br> |The supported storage space range varies with different node specifications:<br><br><br>* 2 cores 4 GiB to 4 cores 32 GiB: 100 GiB to 2,000 GiB.<br><br>* 8 cores 16 GiB and above: 200 GiB to 3,000 GiB. |
|Sharding cluster instance |Shard ||The supported storage space range varies with different node specifications:<br><br><br>* 2 cores 4 GiB ~ 4 cores 32 GiB: 100 GiB ~ 2,000 GiB.<br><br>* 8 cores 16 GiB and above: 200 GiB ~ 3,000 GiB. |
||ConfigServer node ||The supported storage space range for all node specifications is: 20 GiB \- 2000 GiB. |


<span id="f60XnNXz"></span>
### Maximum available storage

It refers to the disk space available for storing business data. You can view the instance's maximum available storage space information on the instance information page. For specific procedures, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance).

The calculation method of maximum available storage capacity varies with the instance type. The specific calculation method is shown in the table below.


|Instance type |Replica set |Sharding cluster |
|---|---|---|
|Maximum available storage |Single node storage specification |Number of shards x Single\-shard storage + ConfigServer storage |
