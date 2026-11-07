---
title: "Billing items and prices"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/billing-item-price"
---

This topic describes the billing items and price details for Document Database for MongoDB.

<span id=".6K6h6LS56aG5"></span>
## Billing items

The following billing items are involved when using Document Database for MongoDB

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following billable items all support two billing methods: subscription and pay\-as\-you\-go. For more information about billing methods, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/pay-as-you-go">Pay\-as\-you\-go</a> and <a href="https://docs.byteplus.com/en/docs/mongodb/subscription">Subscription</a>.</div>



|Instance type |Billing items |Billed or not |
|---|---|---|
|Replica set instance |Compute node |Yes, charges are based on node specifications and usage duration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">MongoDB supports adding read\-only nodes to replica set instances. The node specifications and billing rules for read\-only nodes are consistent with other nodes (including primary, secondary, and hidden nodes). For more details on different node types, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes#.5LiN5ZCM57G75Z6L55qE6IqC54K55a-55q-U">Comparison of different types of nodes</a>.</div><br> |
||Storage space |Yes, charges will be based on the amount of stored data and storage duration.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you are using a FlexPL<strong> </strong>volume instance (all volumes described in this topic are <strong>data disks</strong>), the storage space cost is the volume capacity cost. For more <a href="https://docs.byteplus.com/en/docs/mongodb/Storage_type?lang=en">details</a> on volume storage types and volume capacity costs, refer to Storage types and <a href="https://docs.byteplus.com/en/docs/26444/434935">Volume billing</a>.</div><br> |
||Backup |No, the backup feature and the storage space used for backup files are currently free of charge. |
|Sharding cluster instance |Shard node |Yes, charges are based on the number of Shards the number of nodes per shard, node specifications, and usage duration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">MongoDB supports adding read\-only nodes to the shard of sharding cluster instances. The node specifications and billing rules for read\-only nodes are consistent with those of other nodes (including primary, secondary, and Hidden nodes). For more details on different node types, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes#.5LiN5ZCM57G75Z6L55qE6IqC54K55a-55q-U">Comparison of different types of nodes</a>.</div><br> |
||Mongos node |Yes, charges are based on the number of Mongos nodes, node specifications, and usage duration. |
||ConfigServer node |Yes, charges are based on the number of ConfigServer nodes, node specifications, and usage duration. |
||Storage space |Yes, charges will be based on the amount of stored data and storage duration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only Shard and ConfigServer nodes will be billed for the storage space.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you are using a FlexPL volume instance (all volumes described in this topic are <strong>data disks</strong>), the storage space cost is the volume capacity cost. For more details on volume storage types and volume capacity costs, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/Storage_type?lang=en">Storage types</a> and <a href="https://docs.byteplus.com/en/docs/26444/434935">Volume billing</a>.</div><br> |
||Backup |No, the backup feature and the storage space used for backup files are currently free of charge. |


<span id=".6K6h566X6IqC54K55Lu35qC8"></span>
## Compute node price


<Tabs>
<Tab zoneid="GVzVX6ghVa" title="Replica set instance">
<TabTitle>Replica set instance</TabTitle>

* **Calculation method**

   Total computing node cost = Unit price of a single computing node × Number of nodes (currently fixed at 3 nodes) × Usage duration.

* **Unit price of a single computing node**

   For pricing details and annual discount information for a single computing node in a MongoDB instance, refer to [MongoDB price calculator](https://www.byteplus.com/en/pricing?product=veDB+for+DocumentDB&tab=2).


</Tab>
<Tab zoneid="TymNq8dfmm" title="Sharding cluster instance">
<TabTitle>Sharding cluster instance</TabTitle>

* **Calculation method**

   Total compute node cost = Mongos compute node cost + Shard compute node cost + ConfigServer compute node cost. Among them:

   * Mongos compute node cost = Unit price of a single Mongos compute node × Number of Mongos nodes (currently fixed at 3 nodes) × Usage duration.

   * Shard compute node cost = Unit price of a single Shard compute node × Number of Shard shards × Number of nodes per Shard (currently fixed at 3 nodes) × Usage duration.

   * ConfigServer compute node cost = Unit price of a single ConfigServer compute node × Number of ConfigServer nodes (currently fixed at 3 nodes) × Usage duration.

* **Unit price of a single compute node**

   For pricing details and subscription discount information for individual Mongos, Shard, and ConfigServer compute nodes in MongoDB instances, see the [MongoDB price calculator](https://www.byteplus.com/en/pricing?product=veDB+for+DocumentDB&tab=2).


</Tab>
</Tabs>


<span id="Q1b61CAH"></span>
## Storage price

<span id="sIXrEJ8d"></span>
### Volume instance

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Whether it is a FlexPL volume replica set instance or a FlexPL volume sharding cluster instance, the storage space specification code is <code>mongo.essdflexpl</code>.</div>


* <div data-tips="true" data-tips-type="default">When using FlexPL volume instances (all volumes described in this topic are <strong>data disks</strong>), the storage space fee is the volume capacity fee. For more <a href="https://docs.byteplus.com/en/docs/mongodb/Storage_type?lang=en">details</a> on volume storage types and volume capacity fees, see Storage Types and <a href="https://docs.byteplus.com/en/docs/26444/434935">Volume billing</a>.</div>




<Tabs>
<Tab zoneid="t1svCLaToe" title="Replica set instance">
<TabTitle>Replica set instance</TabTitle>

* **Calculation method**

   Total storage space cost = Unit price of single\-node storage space × Number of nodes (currently fixed at 3 nodes) × Storage space size × Usage duration.

* **Unit price of single\-node storage space**

   For pricing details and subscription discount information for single\-node storage space in MongoDB instances, see the [MongoDB price calculator](https://www.byteplus.com/en/pricing?product=veDB+for+DocumentDB&tab=2).


</Tab>
<Tab zoneid="QE4L7u7iNk" title="Sharding cluster instance">
<TabTitle>Sharding cluster instance</TabTitle>

* **Calculation method**

   Total storage cost = Shard storage cost + ConfigServer storage cost. Among them:

   * Shard storage cost = Unit price of storage space per Shard node × Number of Shard shards × Number of nodes per Shard (currently fixed at 3 nodes) × Storage size × Usage duration.

   * ConfigServer storage cost = Unit price of single ConfigServer node storage space × Number of ConfigServer nodes (currently fixed at 3 nodes) × Storage space size × Usage duration.

* **Unit price of single node storage space**

   For pricing details and annual discount information on single Shard and ConfigServer node storage space in MongoDB instances, refer to the [MongoDB price calculator](https://www.byteplus.com/en/pricing?product=veDB+for+DocumentDB&tab=2).


</Tab>
</Tabs>


<span id="MLrjPbip"></span>
### Local disk instance

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Whether it is a local disk replica set instance or a local disk sharding cluster instance, the storage space specification code is <code>mongo.storage</code>.</div>



<Tabs>
<Tab zoneid="n5HcUZlihI" title="Replica set instance">
<TabTitle>Replica set instance</TabTitle>

* **Calculation method**

   Total storage cost = Unit price of single\-node storage × Number of nodes (currently fixed at 3 nodes) × Storage size × Usage duration.

* **Unit price of single\-node storage space**

   For pricing details of single\-node storage space in MongoDB instances and subscription discount information, refer to [MongoDB price calculator](https://www.byteplus.com/en/pricing?product=veDB+for+DocumentDB&tab=2).


</Tab>
<Tab zoneid="BOVDspfggs" title="Sharding cluster instance">
<TabTitle>Sharding cluster instance</TabTitle>

* **Calculation method**

   Total storage cost = Shard storage cost + ConfigServer storage cost. Among them:

   * Shard storage cost = Unit price per Shard node storage space × Number of Shards × Number of nodes included in a single Shard (currently fixed at 3 nodes) × Storage size × Duration.

   * ConfigServer storage cost = Unit price per ConfigServer node storage space × Number of ConfigServer nodes (currently fixed at 3 nodes) × (Storage size \- 20 GiB) × Duration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each local disk MongoDB sharding cluster instance's ConfigServer component has a free storage quota of 20 GiB.   </div>
   

* **Unit price for single node storage**

   For pricing details and annual discount information regarding the storage space of single Shard and ConfigServer nodes in MongoDB instances, refer to the  and [MongoDB price calculator](https://www.byteplus.com/en/pricing?product=veDB+for+DocumentDB&tab=2).


</Tab>
</Tabs>


<span id="9RLTyQLV"></span>
## Purchase example

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following purchase examples do not consider any product discounts or variants, and are only used as an example purchase reference. The specific purchase fee is subject to the actual order result of the console.</div>



<Tabs>
<Tab zoneid="Jynt90o680" title="Replica set instance">
<TabTitle>Replica set instance</TabTitle>


|Billing method |Pay\-as\-you\-go |Subscription |
|---|---|---|
|Usage scenario |Purchase a replica set instance with the following configuration:<br><br><br>* Storage type: Local disk<br><br>* Specification type: General\-purpose<br><br>* Node specification: 4 cores 8 GiB<br><br>* Number of nodes: 3 nodes by default<br><br>* Storage space: 200 GiB<br><br>* Usage duration: 720 hours (that is 30 days) |Purchase a replica set instance with the following configuration:<br><br><br>* Storage type: Local disk<br><br>* Specification type: General purpose<br><br>* Node specification: 4 cores 8 GiB<br><br>* Number of nodes: 3 nodes by default<br><br>* Storage space: 200 GiB<br><br>* Purchase duration: 1 month |
|Expense to pay |* Compute node expense: 0.1354 USD/node/hour x 3 nodes x 720 hours = 292.464 USD<br><br>* Storage expense: 0.000292 USD/GiB/node/hour x 3 nodes x 200 GiB x 720 hours = 126.144 USD<br><br><br>In summary, total expense: 292.464 USD + 126.144 USD = 418.608 USD |* Compute node expense: 65 USD/node/month x 3 nodes x 1 month = 195 USD<br><br>* Storage expense: 0.140000 USD/GiB/node/month x 3 nodes x 200 GiB x 1 month = 84 USD<br><br><br>In summary, total expense: 195 USD + 84 USD = 279 USD |



</Tab>
<Tab zoneid="cu7SjoEVH4" title="Sharding cluster instance">
<TabTitle>Sharding cluster instance</TabTitle>


|Billing method |Pay\-as\-you\-go |Yearly or monthly subscription |
|---|---|---|
|Usage scenario |Purchase a sharding cluster instance with the following configuration:<br><br><br>* Storage type: Local disk<br><br>* Instance type: General purpose<br><br>* Mongos<br><br>   * Node specification: 4 cores 8 GiB<br><br>   * Number of nodes: 2<br><br>* Shard<br><br>   * Number of shards: 2<br><br>   * Nodes per shard: Each shard includes 3 nodes by default<br><br>   * Node specification: 4 cores 8 GiB<br><br>   * Storage space: 200 GiB<br><br>* ConfigServer<br><br>   * Node specification: 4 cores 8 GiB<br><br>   * Number of nodes: 3 nodes by default<br><br>   * Storage space: 200 GiB<br><br>* Usage duration: 720 hours (that is 30 days) |Purchase a sharding cluster instance with the following configuration:<br><br><br>* Storage type: Local disk<br><br>* Specification type: General purpose<br><br>* Mongos<br><br>   * Node specification: 4 cores 8 GiB<br><br>   * Number of nodes: 2<br><br>* Shard<br><br>   * Number of shards: 2<br><br>   * Nodes per shard: Each shard includes 3 nodes by default<br><br>   * Node specification: 4 cores 8 GiB<br><br>   * Storage space: 200 GiB<br><br>* ConfigServer<br><br>   * Node specification: 4 cores 8 GiB<br><br>   * Number of nodes: 3 nodes by default<br><br>   * Storage space: 200 GiB<br><br>* Purchase duration: 1 month |
|Expense to pay |* Mongos:<br><br>   Compute node expense: 0.1354 USD/node/hour x 2 nodes x 720 hours = 194.976 USD<br><br>* Shard:<br><br>   * Compute node expense: 0.1354 USD/node/shard/hour x 2 shards x 3 nodes x 720 hours = 584.928 USD<br><br>   * Storage expense: 0.000292 USD/GiB/node/shard/hour x 2 shards x 3 nodes x 200 GiB × 720 hours = 252.288 USD<br><br>* ConfigServer<br><br>   * Compute node expense: 0.1354 USD/node/hour x 3 nodes x 720 hours = 292.464 USD<br><br>   * Storage expense: 0.000292 USD/GiB/node/hour x 3 nodes x (200 \- 20) GiB × 720 hours = 113.5296 USD<br><br><br>In summary, total expense: 194.976 USD + 584.928 USD + 252.288 USD + 292.464 USD + 113.5296 USD = 1438.1856 USD |* Mongos:<br><br>   Compute node expense: 65 USD/node/month x 2 nodes x 1 month = 130 USD<br><br>* Shard:<br><br>   * Compute node expense: 65 USD/node/shard/month x 2 shards x 3 nodes x 1 month = 390 USD<br><br>   * Storage expense: 0.140000 USD/GiB/node/shard/month x 2 shards x 3 nodes x 200 GiB × 1 month = 168 USD<br><br>* ConfigServer<br><br>   * Compute node expense: 65 USD/node/month x 3 nodes x 1 month = 195 USD<br><br>   * Storage expense: 0.140000 USD/GiB/node/month x 3 nodes x (200 \- 20) GiB x 1 month = 75.6 USD<br><br><br>In summary, total expense: 130 USD + 390 USD + 168 USD + 195 USD + 75.6 USD = 958.6 USD |



</Tab>
</Tabs>
