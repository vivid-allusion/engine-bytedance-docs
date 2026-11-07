---
title: "Managing read-only nodes"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes"
---

Document Database for MongoDB supports the read\-only node function. Read\-only nodes can provide separate connection addresses, which are suitable for direct connection access by independent systems and applications, expand the read request capabilities of primary and secondary nodes, and help relieve the data reading pressure on primary and secondary nodes.

<span id=".5Yqf6IO9566A5LuL"></span>
## Introduction

A large number of read requests can bring great data reading pressure to the primary and secondary nodes of MongoDB, which may lead to problems such as high latency and slow response to business requests. To share the data reading requests of primary and secondary nodes, MongoDB provides read\-only nodes with independent addresses. You can add read\-only nodes according to business needs when creating MongoDB instances to meet the requirements of business read\-write separation and relieve the access pressure on primary and secondary nodes.

<span id=".5Yqf6IO95LyY5Yq_"></span>
## Advantages


* Synchronize data from the primary node or secondary node with the lowest latency through the operation log (Oplog), and apply it to scenarios with a large number of read requests to relieve the access pressure on primary and secondary nodes.

* When there are two or more read\-only nodes, read request load balancing can be achieved through the read\-only node connection addresses. For more details about read\-only connection addresses, refer to [Read-only node address](https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes#.5Y-q6K-76IqC54K55Zyw5Z2A).

* Read\-only nodes have independent connection addresses and do not interfere with the connections of existing primary and secondary nodes, which are suitable for direct connection access by independent systems and applications.

* Read\-only nodes adopt the same node specifications as primary and secondary nodes and automatically synchronize data from the primary node or secondary node with the lowest latency without additional maintenance.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|Limits |Description |
|---|---|
|Supported instance or component type |Only replica set instances and Shard in sharding cluster instances support adding read\-only nodes. |
|Connection address |The connection address restrictions for read\-only nodes vary depending on the type of MongoDB instance. Among them:<br><br><br>* Replica set instance<br><br>   * Support the use of read\-only nodes in either public network or private network connection addresses.<br><br>   * If there are read\-only nodes in a replica set instance, when public network resolution is enabled, the public network resolution function will also be enabled for the internal network addresses of the read\-only nodes. For more details, refer to [Enabling or disabling public network resolution](https://docs.byteplus.com/en/docs/mongodb/set-public-network-resolution).<br><br>* Sharding cluster instance<br><br>   Only support the use of read\-only nodes in the private network connection addresses of Shard. |
|Quantity limits |Different MongoDB instance types support different numbers of read\-only nodes to be added. Among them:<br><br><br>* Replica set instance: Each instance can add up to 5 read\-only nodes.<br><br>* Sharding cluster instance: Only Shard supports adding read\-only nodes, and each Shard can add up to 5 read\-only nodes. |
|Configuration change |* The specifications of read\-only nodes are consistent with those of the primary and secondary nodes of the instance (or Shard). Therefore, when upgrading or downgrading the specifications of a replica set instance or the specifications of Shard nodes in a sharding cluster, the specifications of the added read\-only nodes will also be changed synchronously.<br><br>* For replica set instances, changing the number of read\-only nodes is mutually exclusive with other configuration change operations of the instance. That is, when changing the node specification or storage space, changing the number of read\-only nodes simultaneously is not supported.<br><br>* Only when there are no read\-only nodes in a sharding cluster instance and the configurations (including node specifications and storage space) of all Shard are the same, is the function of batch modifying Shard configurations supported.<br><br><br>For more details about changing instance configurations, refer to [Changing instance configurations](https://docs.byteplus.com/en/docs/mongodb/change-instance-config). |
|Others |* Read\-only nodes are only accessible for read requests and do not participate in the election of primary and secondary nodes.<br><br>* The data replication method between read\-only nodes and primary or secondary nodes is asynchronous replication. Under normal circumstances, there is a millisecond\-level delay, and a second\-level delay may occur when the write pressure on the primary node is high. |


<span id=".5LiN5ZCM57G75Z6L55qE6IqC54K55a-55q-U"></span>
## Comparison of different types of nodes

Document Database for MongoDB supports four types of nodes: primary nodes, secondary nodes, hidden nodes, and read\-only nodes. The usage scenarios and precautions of different types of nodes are different. The specific differences are shown in the following table.


|Node type |Usage scenario |Precautions |
|---|---|---|
|Primary node |Also known as the primary database, it can provide read and write functions. When the cluster status is normal, all data from clients will be written to the primary node. |* There can only be one primary node in each replica set instance.<br><br>* There can only be one primary node in each Shard of a sharding cluster instance. |
|Secondary node |Ensure high availability. Synchronize the data of the primary node through oplog (operation log) and can become the new primary node through election when the primary node fails. |* When the primary node fails, the secondary node supports being promoted to the primary node to execute and respond to data read and write requests.<br><br>* When clients connect to the secondary node, they can only read data and cannot write data. |
|Hidden node |Only used to ensure high availability and is invisible to users. Synchronize the data of the primary node through oplog and can replace the failed node to become the new secondary node to ensure high availability when the secondary node fails. |* There can only be one hidden node in each replica set instance.<br><br>* There can only be one hidden node in each Shard of a sharding cluster.<br><br>* Hidden nodes only participate in voting to select the primary node and cannot be elected as the primary node. |
|Read\-only node |Mainly applicable to scenarios with a large amount of data read requests. It synchronizes data from the primary node or secondary node through the operation log (oplog), and the system automatically routes read requests to the read\-only node to relieve the access pressure on the primary node. |* Read\-only nodes have independent connection addresses, which are suitable for direct connection access by independent systems and applications and do not interfere with the connections of existing primary and secondary nodes.<br><br>* Read\-only nodes will not be elected as the primary node and will not participate in voting to elect the primary node.<br><br>* The data replication method between read\-only nodes and the primary node or secondary node is asynchronous replication. |


<span id=".6K6h6LS56K-05piO"></span>
## Billing instruction

The price of a single read\-only node is the same as the price of a single node of the corresponding specification in a replica set instance or a Shard of a sharding cluster instance. For details about the price of a single MongoDB node, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/mongodb/billing-item-price#.6K6h566X6IqC54K55Lu35qC8).

<span id=".5Y-q6K-76IqC54K55Zyw5Z2A"></span>
## Read\-only node address

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only when there are read\-only nodes in the instance can you see the connection addresses of the read\-only nodes.</div>


* <div data-tips="true" data-tips-type="tip">When connecting to the instance through the read\-only node addresses, read requests will only be sent to the read\-only nodes.</div>


* <div data-tips="true" data-tips-type="tip">When a read\-only node in the instance fails, read requests will automatically switch to the next read\-only node without affecting the read operations of the application. If all read\-only nodes fail, read requests will fail to execute.</div>


* <div data-tips="true" data-tips-type="tip">You can use the read\-only node connection addresses to connect to the MongoDB instance through tools such as Mongo Shell. For more information, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell">Connect to instance via Mongo shell tool</a>.</div>



The connection address format of MongoDB read\-only nodes is as follows.

```Bash
mongodb://<user>:<password>@<host1>:3717,<host2>:3717,...,<hostN>:3717/?authSource=admin&readPreference=secondary&readPreferenceTags=role:readonly&replicaSet=<replicaSetId>&retryWrites=true
```


The explanations of the relevant parameters in the connection address are shown in the following table.


|Parameter |Required |Description |Example |
|---|---|---|---|
|`<user>` |Required |The name of the database account. |`root` |
|`<password>` |Required |The password of the database account. |`Pwd_123456` |
|`<host>:3717` |Required |The domain name and port number correspond to the read\-only node. The default port number is 3717.<br><br>Currently, only replica set instances and Shard in sharding cluster instances support connection via read\-only nodes. Among them:<br><br><br>* Replica set instance<br><br>   * A private network connection address containing all read\-only nodes is provided separately.<br><br>   * You can also apply for a separate public network connection address for read\-only nodes according to your business needs. For specific procedures, refer to [Applying for public address](https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address).<br><br>* Sharding cluster instance<br><br>   Only the private network address of Shard will contain the connection address of read\-only nodes. |* Example of the connection address domain name of the read\-only node of a replica set instance:<br><br>   `mongoreplicae047fe00****100.mongodb.ibytepluses.com:3717`<br><br>* Example of the connection address domain name of the read\-only node of a sharding cluster instance (take Shard 0 as an example):<br><br>   `mongoshard9a2ab41e****s0100.mongodb.ibytepluses.com:3717` |
|`authSource` |Required |Set the name of the authentication database. The default authentication database is `admin`.<br><br>The database account must be authenticated under the affiliated database to be authenticated successfully. |`authSource=admin` |
|`readPreference` |Optional |Used to implement read/write splitting and load balancing for highly available addresses. This parameter can send write requests to the primary node and randomly send read requests to secondary nodes and read\-only nodes. The available values are as follows:<br><br><br>* `readPreference=primary`: Read requests are only sent to the primary node.<br><br>* `readPreference=primaryPreferred`: Prefer reading from the primary node. If the primary node fails, send read requests to the secondary nodes and read\-only nodes.<br><br>* `readPreference=secondary`: Read only from secondary nodes and read\-only nodes. If both secondary nodes and read\-only nodes fail, the read request fails and will not be sent to the primary node.<br><br>* `readPreference=secondaryPreferred`: Read from secondary nodes and read\-only nodes preferentially. If both secondary nodes and read\-only nodes fail, this parameter sends the read request to the primary node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more details about the <code>readPreference</code> parameter, refer to <a href="https://www.mongodb.com/docs/v6.0/core/read-preference/">Read Preference</a>.</div><br> |`readPreference=secondary` |
|`readPreferenceTags` |Optional |This parameter can prioritize sending read requests to the nodes corresponding to the tags. The available values are as follows:<br><br><br>* `readPreferenceTags=role:electable`: Read from secondary nodes first.<br><br>* `readPreferenceTags=role:readonly`: Read from read\-only nodes first.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For those instances created before November 27, 2025, if you need to set <code>readPreferenceTags=role:electable</code>, you need to enable the Read/write <strong>splitting enhancement</strong> feature first on the <strong>Connectivity</strong> tab of the instance. <strong>Read/write splitting</strong> enhancement feature switch once been turned on, it cannot be turned off. For more details, please refer to <a href="https://docs.byteplus.com/en/docs/mongodb/read_write_splitting">Read/write splitting</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">MongoDB instances created on or after November 27, 2025, support setting <code>readPreferenceTags=role:electable</code> by default. You can directly set this parameter in the connection address.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is usually used together with the <code>readPreference</code> parameter to implement read\-write separation functionality, but it is incompatible with the <code>primary</code> mode.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The setting of <code>readPreferenceTags=role:readonly</code> will only take effect when there are read\-only nodes in the instance. For the usage method of read\-only nodes, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node">Adding or removing read\-only nodes</a>.</div><br><br><br><br><div data-tips="true" data-tips-type="tip">For more details about the <code>readPreferenceTags</code> parameter, please see <a href="https://www.mongodb.com/docs/v6.0/reference/connection-string-options/#mongodb-urioption-urioption.readPreferenceTags">readPreferenceTags</a>.</div><br> |`readPreferenceTags=role:readonly` |
|`replicaSet` |Required |This parameter can send read requests to all nodes of a replica set instance or Shard in a sharding cluster instance. The value is the unique identification ID of the instance's high availability connection address. |`replicaSet=rs-mongo-replica-e047fe003****` |
|`retryWrites` |Required |Document Database for MongoDB adds the `&retryWrites=true` field by default at the end of each connection address to ensure the reconnection mechanism. |`retryWrites=true` |


Examples of read\-only connection addresses.


<Tabs>
<Tab zoneid="w9M2CL4DjI" title="Replica set instance">
<TabTitle>Replica set instance</TabTitle>

The example of the connection address for routing read requests to the read\-only nodes of the replica set is as follows.

```Bash
mongodb://root:Pwd_123456@mongoreplicae047fe00****0100.mongodb.ibytepluses.com:3717/?authSource=admin&readPreference=secondary&readPreferenceTags=role:readonly&replicaSet=rs-mongo-replica-e047fe00****&retryWrites=true
```



</Tab>
<Tab zoneid="fmuG4fVzM8" title="Sharding cluster instance">
<TabTitle>Sharding cluster instance</TabTitle>

The example of the connection address for routing read requests to the read\-only nodes of the Shard (taking Shard 0 as an example) in the sharding cluster instance is as follows.

```Bash
mongodb://root:Pwd_123456@mongoshard9a2ab41e****s00.mongodb.ibytepluses.com:3717,mongoshard9a2ab41e****s01.mongodb.ibytepluses.com:3717,mongoshard9a2ab41e****s0100.mongodb.ibytepluses.com:3717/?authSource=admin&readPreference=secondary&readPreferenceTags=role:readonly&replicaSet=rs-mongo-shard-9a2ab41e****-s0&retryWrites=true
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Although the sharding cluster instance only supports the use of read\-only nodes in Shard, you can route read requests to read\-only nodes through the <code>readPreferenceTags=role:readonly</code> parameter in the Mongos connection address.</div>


<div data-tips="true" data-tips-type="default">The example of Mongos read\-only connection addresses in a sharding cluster instance are as follows.</div>


<div data-tips="true" data-tips-type="default">```Bash
mongodb://<user>:<password>@mongoshard9a2ab41e****0.mongodb.ibytepluses.com:3717,mongoshard9a2ab41e****1.mongodb.ibytepluses.com:3717/?authSource=admin&readPreference=secondary&readPreferenceTags=role:readonly&retryWrites=true
```
</div>



</Tab>
<Tab zoneid="ZThbRLTbuH" title="">
<TabTitle></TabTitle>




</Tab>
</Tabs>


<span id=".5L2_55So5Y-q6K-76IqC54K5"></span>
## Using read\-only nodes


* You can directly add read\-only nodes to the newly created instance when creating an instance or restoring an instance. For specific operation steps, refer to:

   * [Create Instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance)

   * [Recovery from backup files](https://docs.byteplus.com/en/docs/mongodb/recovery-from-backup-file)

   * [Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point)

   * [Recovery from deleted instance](https://docs.byteplus.com/en/docs/mongodb/recovery_from_a_deleted_instance)

* After the instance is successfully created, you can also change the number of read\-only nodes of the instance, including adding and deleting read\-only nodes. For specific procedures, refer to [Adding or removing read-only nodes](https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node).
