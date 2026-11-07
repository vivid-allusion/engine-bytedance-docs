---
title: "Reclaiming MongoDB instance disk fragments via COMPACT command"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/compact-sharding-cluster-disk-fragment"
---

This topic describes how to recover disk fragments of MongoDB instances through the `compact` command to reduce the disk usage and improving the use efficiency.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

When you delete data from a MongoDB instance, the disk space occupied by the deleted data is not reclaimed directly but marked as idle. New data written to the instance does not occupy new disk space but reuses such disk space marked as idle. The idle disk space not used is called disk fragments. Disk fragments increase along with more and more deletion operations. More disk fragments mean lower disk usage.

The `compact` command is used to rewrite and sort all the data and indexes in MongoDB collections. It reclaims disk fragments generated after data deletion to improve the disk usage. For more information about `compact`, refer to [compact](https://www.mongodb.com/docs/manual/reference/command/compact/#dbcmd.compact).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

The Document Database for MongoDB supports instances of both replica set and sharding cluster architectures. Different instance types have different prerequisites for executing the compact command to reclaim disk space.


<Tabs>
<Tab zoneid="Iuv9376dV1" title="Replica set instance">
<TabTitle>Replica set instance</TabTitle>

The single node addresses of the primary node, secondary node, and hidden node of the instance have been obtained respectively.

After you log in to the [MongoDB console](https://console.byteplus.com/db/mongodb), you can view the connection addresses for each node in the **Single node address** table under the target replica set instance's **Connectivity** tab. For specific procedures, refer to [Viewing connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction#.5p-l55yL6L-e5o6l5Zyw5Z2A).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6956d1ca88c4b59b889389527c7cae90.png) </span>


</Tab>
<Tab zoneid="Ooq1HS3aoa" title="Sharding cluster instance">
<TabTitle>Sharding cluster instance</TabTitle>

* A private network connection address has been requested for the target shard sharding. For details, refer to [Applying for private address](https://docs.byteplus.com/en/docs/mongodb/apply-private-address).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The MongoDB sharding cluster instance only needs to reclaim the disk fragments of the corresponding node in the Shard component. Mongos and ConfigServer components do not store business data, and there are too many add and update operations and too few delete operations, so there is generally no need to reclaim disk fragments. For more information about the components of a sharding cluster instance, see <a href="https://docs.byteplus.com/en/docs/mongodb/about-mongodb#.5YiG54mH6ZuG576k">Sharding cluster</a>.   </div>
   

* The single node connection addresses for the primary node, secondary node, and hidden node in the shard have been obtained respectively.

   After logging in to the [MongoDB console](https://console.byteplus.com/db/mongodb), ** ** click ** ** the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ac21943d108c371a5d4da83f1fc6351d.png) </span> icon to the right of the target shard in the **Connection to Shard** area under the **Connectivity** tab of the target sharding cluster instance to view the connection addresses of each node in the expanded table. For specific procedures, refer to [Viewing connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction#.5p-l55yL6L-e5o6l5Zyw5Z2A).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3d24340e0a05f90ff87c018ce94c09a6.png) </span>


</Tab>
</Tabs>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* It is recommended to back up the database data before reclaiming the disk fragments. For specific methods of data backup, see [Manual backup](https://docs.byteplus.com/en/docs/mongodb/manual-backup).

* The amount of aggregated data, system load, and other factors can affect the execution time of reclaiming disk fragments.

* Before recycling disk fragments, you [can connect to instance via Mongo shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell) and enter the target database, and use the [collStats](https://www.mongodb.com/docs/v6.0/reference/command/collStats/) command to view the details of the disk space occupied by the database, so that you can confirm the reclaming effect of disk fragments after the reclamation. For specific procedure, see [Estimating reclaimable disk fragment space](https://docs.byteplus.com/en/docs/mongodb/compact-sharding-cluster-disk-fragment#.6aKE5Lyw5Y-v5Zue5pS255qE56OB55uY56KO54mH56m66Ze0).

* For MongoDB 4.4 and earlier instances, executing the `compact` command on a **non\-hidden node** causes the database to which the collection belongs to be locked and blocks read and write operations to the database. It is recommended that you strictly follow the operation sequence of this topic to reclaim disk fragments during the peak business period to reduce the impact on the business. For more information about blocked commands, see [Blocking](https://www.mongodb.com/docs/v6.0/reference/command/compact/#blocking). If you encounter problems reclaiming disk space, please [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.

* When executing the compact command, replication latency may occur. If the latency exceeds the oplog window period, it is highly likely to cause replication failure between the primary and secondary nodes, and may even lead to node exceptions. It is strongly recommended to closely monitor the [Primary-secondary delay](https://docs.byteplus.com/en/docs/mongodb/monitoring-metric) indicator of the instance and the event alarms for [oplog window being insufficient](https://docs.byteplus.com/en/docs/mongodb/event-monitoring) during the execution of the compact command. **If the replication latency is too large, please terminate the compact command operation in time.**  For more details about oplog parameters, please refer to the [Guide to setting oplog-related parameters](https://docs.byteplus.com/en/docs/mongodb/guide-to-set-oplog-related-parameters).

* To terminate the current `compact` command operation, create a new connection and use the `db.killOp(opid)` command to terminate the running `compact` operation. For more information about the `db.killOp()` command, see [db.killOp()](https://www.mongodb.com/docs/v6.0/reference/method/db.killOp/).


<span id=".6aKE5Lyw5Y-v5Zue5pS255qE56OB55uY56KO54mH56m66Ze0"></span>
## Estimating reclaimable disk fragment space


1. Connect to MongoDB instance via Mongo shell. For more information, refer to [Connect to instance via Mongo shell tool](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For MongoDB replica set instances, to reduce business impact, it is recommended that you connect to the secondary node of the replica set instance for operations.   </div>
   

2. Execute the use `<database name>` command to enter the target database.

   Example is as follows.

   ```Bash
   use test_db
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can query existing databases in the current MongoDB instance with the <code>show dbs</code> command.   </div>
   

3. View the storage status of the target collection with the `collStats` command.

   ```Bash
   db.runCommand({collStats:"<collection name>"})
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can query an existing collection in the current database with the <code>show tables</code> command.   </div>
   

   Example is as follows.

   ```Bash
   db.runCommand({collStats:"test_db_col"})
   ```
   

   In the returned results, the following information needs to be emphasized.

   * [collStats.size](https://www.mongodb.com/docs/v6.0/reference/command/collStats/#mongodb-data-collStats.size): Represents the logical storage size of the collection. You can also get this information with [db.collection.dataSize ()](https://www.mongodb.com/docs/v6.0/reference/method/db.collection.dataSize/#mongodb-method-db.collection.dataSize) command.

   * [collStats.storageSize](https://www.mongodb.com/docs/v6.0/reference/command/collStats/#mongodb-data-collStats.storageSize): Represents the physical storage size of the collection. You can also get this information with [db.collection.storageSize ()](https://www.mongodb.com/docs/v6.0/reference/method/db.collection.storageSize/#mongodb-method-db.collection.storageSize) command.

   * [collStats.freeStorageSize](https://www.mongodb.com/docs/v6.0/reference/command/collStats/#mongodb-data-collStats.freeStorageSize): Represents the free disk space in disk fragments that can be reclaimed. You can also check the `file bytes available for reuse` field under the `block-manager` structure in the returned results for information on the disk space that can be reclaimed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <a href="https://www.mongodb.com/docs/v6.0/reference/command/collStats/#mongodb-data-collStats.freeStorageSize">collStats.freeStorageSize</a> refers to the maximum disk space that can theoretically be reclaimed. However, in actual business scenarios, the real disk space that can be reclaimed is affected by various factors such as uneven data distribution, and the actual effect of disk defragmentation may be relatively limited.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you <a href="https://www.mongodb.com/docs/v6.0/reference/command/delete/">delete</a> a document with the delete command, the value of <code>size</code> decreases, but the value of <code>storageSize</code> does not necessarily decrease. You can observe the proportion of <code>freeStorageSize</code> in the <code>storageSize</code>, and when the proportion is higher, it means that the disk fragmentation rate is higher.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">MongoDB 4.4 and above only supports viewing the <code>freeStorageSize</code> field. For more information about the <code>collStats</code> command, see <a href="https://www.mongodb.com/docs/v6.0/reference/command/collStats/">collStats</a>.   </div>
   


<span id=".5Zue5pS25Ymv5pys6ZuG5a6e5L6L55qE56OB55uY56KO54mH"></span>
## Reclaiming disk fragments for instance


<Tabs>
<Tab zoneid="W9JwPt0UHb" title="Reclaiming disk fragments for Replica set instance">
<TabTitle>Reclaiming disk fragments for Replica set instance</TabTitle>

<span id="m8Z2iNNl"></span>
### Step 1: Reclaiming disk fragments of hidden node


1. In the local server or ECS where Mongo shell is installed, enter the database account number, password, and single\-node connection address of the replica set instance in the corresponding position of the following command to connect to the hidden node.

   ```Bash
   mongo "mongodb://<account_name>:<account_password>@<Single node address of Hidden node which obtained in the prerequisites section>/?authSource=admin"
   ```
   

   Example is as follows.

   ```Bash
   mongo "mongodb://root:Pwd_123@mongoreplica****2.mongodb.ibytepluses.com:3717/?authSource=admin"
   ```
   

2. Execute the `rs.isMaster()` command to confirm whether the currently connected node is a hidden node.

   Example is as follows.

   ```Bash
   rs-mongo-replica-****:SECONDARY|test rs.isMaster()
   ```
   

   Example of return results is as follows.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following example shows only some of the fields. The value of the <code>hidden</code> field in the return result is <code>true</code>, which indicates that the current connection is a hidden node.   </div>
   

   ```Bash
   {
           "hosts" : [
                   'mongoreplica****0.mongodb.ibytepluses.com:3717',
                   'mongoreplica****1.mongodb.ibytepluses.com:3717'
           ],
           "setName" : "rs-mongo-replica-****",
           "setVersion" : 12444,
           "ismaster" : false,
           "secondary" : true,
           "primary" : "mongoreplica****0.mongodb.ibytepluses.com:3717",
           "passive" : true,
           "hidden" : true,
            ....... 
   }
   ```
   

3. Execute the following `compact` command to reclaim disk fragments.

   ```Bash
   db.runCommand({compact:"<collection_name>"})
   ```
   

   This topic takes `test_collect` as an example, and the command example is as follows.

   ```Bash
   db.runCommand({compact:"test_collect"})
   ```
   

   If `"ok": 1` appears in the return result, it means that the `compact` command was executed successfully.


<span id="hS2jQ99F"></span>
### Step 2: Reclaiming disk fragments of secondary node


1. In the local server or ECS where Mongo shell is installed, enter the database account number, password, and single\-node connection address of the secondary node in the corresponding position of the following command to connect to the secondary node.

   ```Bash
   mongo "mongodb://<account_name>:<account_passwordunt_password>@<Single node address of Secondary node which obtained in the prerequisites section>/?authSource=admin"
   ```
   

   Example is as follows.

   ```Bash
   mongo "mongodb://root:Pwd_123@mongoreplica****1.mongodb.ibytepluses.com:3717/?authSource=admin"
   ```
   

   2. Execute the `rs.isMaster()` command to confirm whether the currently connected node is a secondary node.The command example is as follows.

      Example is as follows.

   ```Bash
   rs-mongo-replica-****:SECONDARY|test rs.isMaster()
   ```
   

   Example of return results is as follows.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following example shows only some of the fields. The following example shows only some of the fields. The value of the <code>secondary</code> field in the return result is <code>true</code>, which indicates that the currently connected secondary node.   </div>
   

   ```Bash
   {
           "hosts" : [
                   'mongoreplica****0.mongodb.ibytepluses.com:3717',
                   'mongoreplica****1.mongodb.ibytepluses.com:3717'
           ],
           "setName" : "rs-mongo-replica-****",
           "setVersion" : 12444,
           "ismaster" : false,
           "secondary" : true,
           "primary" : "mongoreplica****0.mongodb.ibytepluses.com:3717",
           .......
   }
   ```
   

2. Execute the `compact` command to reclaim disk fragments.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The method of executing the <code>compact</code> command from the node is the same as on the hidden node. For specific procedure, see <strong>Step 1: Reclaiming disk fragments of hidden node</strong> in the above text.   </div>
   

<span id="MUz9jUBH"></span>
### Step 3: Manually switching primary node

Manually switch the completed disk defragmentation secondary node to the primary node. For specific procedure, refer to [Switching primary node](https://docs.byteplus.com/en/docs/mongodb/switch-primary-node).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">During the process of manually switching the primary node (generally taking 30 to 60 seconds), the instance may experience 1 to 2 connection flash breaks, please operate with caution. It is recommended to perform switching operations during low\-peak business periods and ensure that the application has an automatic reconnect mechanism.</div>


* <div data-tips="true" data-tips-type="tip">Manually switching the primary node only changes the role of the node, not the availability zone and node ID where the node is located.</div>



<span id="LfNgOHWT"></span>
### Step 4: Reclaiming disk fragments of new secondary node

After the primary node is successfully switched, refer to the relevant steps of reclaiming disk fragments on the secondary node, connect to the new secondary node after the switch and complete the disk fragment reclamation. For specific procedure, see **Step 2: Reclaiming disk fragments of secondary node** in the above text.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After the disk fragment reclaimation on all nodes is completed, you can  <a href="https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell">connect to instance via Mongo shell</a> and enter the target database again, and use the <a href="https://www.mongodb.com/docs/v6.0/reference/command/collStats/">collStats</a> command to view the details of the disk space occupied by the database, so that you can confirm the disk fragment reclaiming effect after the reclaimation is completed. For specific procedure, see <a href="https://docs.byteplus.com/en/docs/mongodb/compact-sharding-cluster-disk-fragment#.6aKE5Lyw5Y-v5Zue5pS255qE56OB55uY56KO54mH56m66Ze0">Estimating reclaimable disk fragment space</a>.</div>



</Tab>
<Tab zoneid="tf1huWM7p3" title="Reclaiming disk fragments for Sharding cluster instances">
<TabTitle>Reclaiming disk fragments for Sharding cluster instances</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The MongoDB sharding cluster instance only needs to reclaim the disk fragments of the corresponding node in the Shard component. Neither the Mongos component nor the ConfigServer component stores business data, and these two components record too many add and update operations and too few delete operations, so there is no need to reclaim disk fragments.</div>


<span id="DvQ67AOS"></span>
### Step 1: Reclaiming disk fragments of hidden node on shard


1. In the local server or ECS where Mongo shell is installed, enter the database account number and password of the sharding cluster instance, as well as the single\-node connection address of the hidden node in the target shard, in the corresponding position of the following command to connect to the hidden node.

   ```Bash
   mongo "mongodb://<account_name>:<account_password>@<Single node address of Hidden node which obtained in the prerequisites section>/?authSource=admin"
   ```
   

   Example is as follows.

   ```Bash
   mongo "mongodb://root:Pwd_123@mongoshard****s02.mongodb.ibytepluses.com:3717/?authSource=admin"
   ```
   

2. Execute the `rs.isMaster()` command to confirm whether the currently connected node is a hidden node.

   Example is as follows.

   ```Bash
   rs-mongo-shard-****-s0:SECONDARY|test> rs.isMaster()
   ```
   

   Example of return results is as follows.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following example shows only some of the fields. The value of the <code>hidden</code> field in the return result is <code>true</code>, which indicates that the current connection is a hidden node.   </div>
   

   ```Bash
   {
           "hosts" : [
                   "mongoshard****s00.ibytepluses.com:3717",
                   "mongoshard****s01.ibytepluses.com:3717"
           ],
           "setName" : "rs-mongo-shard-****-s0",
           "setVersion" : 12444,
           "ismaster" : false,
           "secondary" : true,
           "primary" : "mongoshard****s00.ibytepluses.com:3717",
           "passive" : true,
           "hidden" : true,
            .......
   }
   ```
   

3. Execute the following `compact` command to reclaim disk fragments.

   ```Bash
   db.runCommand({compact:"<collection_name>"})
   ```
   

   This topic takes `test_collect` as an example, and the command example is as follows.

   ```Bash
   db.runCommand({compact:"test_collect"})
   ```
   

   If `"ok": 1` appears in the return result, it means that the `compact` command was executed successfully.


<span id="XQnDtcNv"></span>
### Step 2: Reclaiming disk fragments of secondary node on shard


1. In the local server or ECS with Mongo shell installed, enter the database account number and password of the sharding cluster instance, and the single\-node connection address of the secondary node in the target shard at the corresponding position of the following command to connect to the secondary node.

   ```Bash
   mongo "mongodb://<account_name>:<account_password>@<Single node address of Secondary node which obtained in the prerequisites section>/?authSource=admin"
   ```
   

   Example is as follows.

   ```Bash
   mongo "mongodb://root:Pwd_123@mongoshard****s01.mongodb.ibytepluses.com:3717/?authSource=admin"
   ```
   

2. Execute the `rs.isMaster()` command to confirm whether the currently connected node is a secondary node.The command example is as follows.

   Example is as follows.

   ```Bash
   rs-mongo-shard-****-s0:SECONDARY|test> rs.isMaster()
   ```
   

   Example of return results is as follows.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following example shows only some of the fields. The following example shows only some of the fields. The value of the <code>secondary</code> field in the return result is <code>true</code>, which indicates that the currently connected secondary node.   </div>
   

   ```Bash
   {
           "hosts" : [
                   "mongoshard****s00.ibytepluses.com:3717",
                   "mongoshard****s01.ibytepluses.com:3717"
           ],
           "setName" : "rs-mongo-shard-****-s0",
           "setVersion" : 12444,
           "ismaster" : false,
           "secondary" : true,
           "primary" : "mongoshard****s00.ibytepluses.com:3717",
           .......
   }
   ```
   

3. Execute the `compact` command to reclaim disk fragments.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The method of executing the <code>compact</code> command from the node is the same as on the hidden node. The method of executing the compact command from the node is the same as on the hidden node. For specific command details and examples, see <strong>Step 1: Reclaiming disk fragments of hidden node on shard</strong> in the above text.   </div>
   

<span id="t32FweAN"></span>
### Step 3: Manually switching primary node

Manually switch the completed disk defragmentation secondary node to the primary node. For specific procedure, refer to [Switching primary node](https://docs.byteplus.com/en/docs/mongodb/switch-primary-node).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">During the process of manually switching the primary node (generally taking 30 to 60 seconds), the instance may experience 1 to 2 connection flash breaks, please operate with caution. It is recommended to perform switching operations during low\-peak business periods and ensure that the application has an automatic reconnect mechanism.</div>


* <div data-tips="true" data-tips-type="warning">Manually switching the primary node only changes the role of the node, not the availability zone and node ID where the node is located.</div>



<span id="Aaux6IPQ"></span>
### Step 4: Reclaiming disk fragments of new secondary node on shard

After the primary node is successfully switched, refer to the relevant steps of reclaiming the disk fragments on the secondary node, connect to the new secondary node after the switch and complete the disk fragment reclamation. For specific procedure, see **Step 2: Reclaiming disk fragments of secondary node on shard** in the above text.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After the disk fragment reclamation on all nodes is completed, you can again <a href="https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell">connect to instance via Mongo shell</a> and enter the target database, use the <a href="https://www.mongodb.com/docs/v6.0/reference/method/db.stats/">db.stats()</a> command to view the disk space occupied by the database details, and compare it with the disk space data before reclamation to confirm the disk fragment reclaiming effect. For specific procedure, see <a href="https://docs.byteplus.com/en/docs/mongodb/compact-sharding-cluster-disk-fragment#.6aKE5Lyw5Y-v5Zue5pS255qE56OB55uY56KO54mH56m66Ze0">Estimating reclaimable disk fragment space</a>.</div>



</Tab>
</Tabs>
