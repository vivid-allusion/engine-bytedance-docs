---
title: "User guide for MongoDB sharding cluster"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/ug-for-sharding-cluster"
---

MongoDB instances support sharding cluster architecture and provide horizontal scaling MongoDB services. Sharding clusters automatically split large collections across nodes to meet capacity and performance requirements in large\-scale, high\-performance scenarios. This topic provides suggestions for how to use the MongoDB sharding cluster.

<span id=".5YiG54mH6ZuG576k5L2_55So5Zy65pmv"></span>
## Application scenarios of sharding cluster

We recommend using the MongoDB sharding cluster in the following scenarios:


* There are bottlenecks in the available RAM or disk space.

* The read\-write capabilities cannot be expanded due to limits of resources, such as the standalone CPU, memory, and network interface.


<span id=".5YiG54mH5L2_55So5rOo5oSP5LqL6aG5"></span>
## Precautions for using sharding


* All collections that need to be sharded must ensure that there is an index on the shard key. This index can be either an index of the shard key itself or a compound index. Therefore, when setting the shard key, the following points should be noted:

   * If you need to set a shard key for an existing collection (i.e., a collection with existing data), you must first create an index for the shard key, and then perform sharding through the [sh.shardCollection()](https://www.mongodb.com/docs/v7.0/reference/method/sh.shardCollection/) command. For the specific method of creating an index, refer to [db.collection.createIndex()](https://www.mongodb.com/docs/v5.0/reference/method/db.collection.createIndex/#mongodb-method-db.collection.createIndex).

   * If you set a shard key for a newly created collection (i.e., an empty collection), you can directly perform sharding through the [sh.shardCollection()](https://www.mongodb.com/docs/v7.0/reference/method/sh.shardCollection/) command. The system will automatically create an index on the shard key without any additional settings.

   * You can use the [db.collection.getIndexes()](https://www.mongodb.com/docs/v5.0/reference/method/db.collection.getIndexes/) command to query the index details of a specified collection.

   * If a compound index is used, the shard key must be a prefix of the index. Otherwise, an error related to `Uniqueness can't be maintained unless shard key is a prefix` may occur when setting the shard key.

   * When modifying sharded data, if the shard key field is not included in the filter of the update request and the options `upsert:true` or `multi:false` are set, the update request will return the error `An upsert on a sharded collection must contain the shard key and have the simple collation`. To avoid affecting online services, it is recommended to perform the modification during the off\-peak business hours.

   * After enabling sharding for an existing collection (i.e., a collection with existing data), the shards will be relocated immediately. Therefore, during the period from enabling sharding to the complete balance of data, the load of the [primary shard](https://www.mongodb.com/docs/manual/core/sharded-cluster-shards/#primary-shard) may increase. To avoid affecting online services, it is recommended to perform the sharding operation during off\-peak business hours.

      If your business is sensitive to latency, you can use relevant parameters such as `migrateCloneInsertionBatchDelayMS` to limit the data migration and cleanup speed of the instance. For more details, refer to [Why does instance experience performance jitter (such as increased business access latency) when adding shards](https://docs.byteplus.com/en/docs/mongodb/change-instance-config-faq#43y5spqX).

* For MongoDB 4.0 and 4.2 version instances, when sharding is enabled for an existing collection (i.e., a collection with existing data), there will be a short\-term table\-locking and write\-prohibition. During this period, the collection written without a Shard key cannot be queried by Mongos, but you can connect to the specific Shard for querying.

* It is highly recommended to closely monitor the table data volume of the MongoDB instance and enable sharding for the instance in advance.


<span id=".5YiG54mH6ZuG576k5L2_55So5bu66K6u"></span>
## Suggestions for sharding cluster use

<span id=".6K6-572u5ZCI6YCC55qELXNoYXJk44CBbW9uZ29zLeaVsOmHjw=="></span>
### Setting proper number of shards and Mongos nodes

Shards and Mongos nodes are important components of a MongoDB sharding cluster instance. You can use the following methods to determine the number of Shards and Mongos nodes based on your business needs:


* The sharding cluster is only used as a solution for storing high volumes of data that are not frequently accessed.

   For example, if the maximum storage amount of a shard is A and the total storage amount required is B. You can calculate the number of shards and Mongos nodes required by your business using the following formula:

   * Number of Shards = B ➗ A ➗ 0.75 (assuming that the capacity threshold is 75%)

   * Number of Mongos nodes: At least two Mongos nodes for high availability

* The sharding cluster is used as a solution for highly concurrent data write (or read), with a small data volume. In other words, shards and Mongos nodes must meet the read\-write performance requirements.

   For example, if the maximum QPS of a shard is C, the maximum QPS of a Mongos node is D, and the total QPS required is Q. You can calculate the number of shards and Mongos nodes required by your business using the following formulas:

   * Number of Shards = Q ➗ C ➗ 0.75 (assuming that the load threshold is 75%)

   * Number of Mongos nodes = Q ➗ D ➗ 0.75


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the sharding cluster must solve both issues, the higher requirements prevail for the evaluation.</div>


* <div data-tips="true" data-tips-type="tip">The prerequisite for the above calculation methods is that data and requests are evenly distributed in the sharding cluster, which is hard to implement in real\-world scenarios. To evenly distribute the system load, you must select a proper shard key. For more information, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/ug-for-sharding-cluster#X5MWXlDL">Setting a proper shard key</a>.</div>


* <div data-tips="true" data-tips-type="tip">The service capabilities of Shard and Mongos must be measured based on your business characteristics.</div>



<span id="X5MWXlDL"></span>
### Setting proper shard key

Collection is the basic unit of data shards in the sharding cluster, and data in a collection is divided into multiple parts by the shard key. A shard key is a proper field selected from a collection to evenly distribute data in this collection to all the shards in it. Improper shard key may deteriorate the cluster performance and lead to stuck during the execution of a sharding statement.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Starting from MongoDB 5.0, you can run the <code>reshardCollection</code> command to modify the shard key for data resharding. For detailed steps on modifying the shard key, refer to <a href="https://www.mongodb.com/docs/v5.0/core/sharding-reshard-a-collection/#reshard-a-collection">Reshard collection</a>.</div>


* <div data-tips="true" data-tips-type="tip">Starting from MongoDB 4.4, the shard key for sharding documents in a collection may be missing. For more information, refer to <a href="https://www.mongodb.com/docs/manual/core/sharding-set-missing-shard-key-fields/#set-missing-shard-key-fields">Set missing shard key fields</a>.</div>


* **Sharding policies**

   The MongoDB sharding cluster supports two sharding policies.

   
   |Sharding policy |Description |Precautions |
   |---|---|---|
   |Ranged sharding<br><br>（[Ranged Sharding](https://www.mongodb.com/docs/manual/sharding/#ranged-sharding)） |Performs query based on the range of shard keys. |When ranged sharding or hashed sharding is used, the sharding effect or performance will be affected in the following scenarios:<br><br><br>* The value range of a shard key is too small. For example, if the data center is used as the shard key, the sharding effect is not good because the number of data centers is small.<br><br>* If a shard key contains many documents with the specified value, a single chunk (that is jumbo chunk) is especially large, affecting chunk migration and load balancing.<br><br>* Query and update operations based on non\-shard key will change to scatter\-gather query, affecting the efficiency. |
   |Hashed sharding<br><br>（[Hashed Sharding](https://www.mongodb.com/docs/manual/sharding/#hashed-sharding)） |Evenly distributes written data to multiple shards. ||
   

* **Characteristics of ideal shard key**

   * Sufficient cardinality of the key

   * Evenly distributed write

   * Targeted read to prevent scatter\-gather query

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the selected shard key does not possess the preceding characteristics, the read\-write scalability of the cluster will be affected. For example, if a frequently updated or queried field is used as the shard key, data sharding may be uneven and some shards have too many reads and writes, highly limiting the sharding advantages. We recommend you adjust your shard key based on the data sharding situation of your business, common queries, and the written data.   </div>
   

* **Factors to consider when setting shard key**

   You can determine whether the set shard key meets your business needs based on the following information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information, refer to <a href="https://www.mongodb.com/docs/v5.0/core/sharding-choose-a-shard-key/">Choose shard key</a>.   </div>
   

   
   |**Factor** |**Description** |
   |---|---|
   |Cardinality of the shard key |* The cardinality of the shard key determines the number of chunks to be divided. Every unique shard key value can only be stored in a single chuck at any given time. Therefore, when conditions permit, it is recommended to choose a shard key with higher cardinality.<br><br>* If the cardinality is too small, most data could be centralized in a few shards, leading to unbalanced sharding and even affecting the database performance.<br><br>   For example, using the user ID as the shard key provides a larger cardinality than using gender as the shard key, offering more even data distribution.<br><br>* A shard key with large or low cardinality itself cannot guarantee even data distribution in the sharding cluster. The occurrence frequency of the shard key and the potential monotonic change (increment or decrement) of the shard key value also affect the data distribution. |
   |Sharding Query Mode |* A proper shard key can evenly distribute data to the sharding cluster. The shard key also needs to cover common queries. If most queries are performed based on a field, using this field as the shard key can improve the query performance.<br><br>* If queries contain the shard key in the sharding cluster, Mongos will route the queries only to the shards containing relevant data. If queries do not contain the shard key, queries will be broadcast to all shards for evaluation. This will lower the query efficiency and cluster scalability. |
   |Limit of shard key |Some databases have specific limits (maximum length or data type) on the shard key. You must consider these limits when selecting a shard key. |
   


<span id=".Y2h1bmstc2l6ZS3kuI4tanVtYm8tY2h1bms="></span>
### Chunk size and jumbo chunk


* **Chunk size**

   In MongoDB 5.0 and earlier versions, the default chunk size is 64 MB. You can modify the chunk size based on your business data amount and the application scenario of the shard. The value range of the chunk size is 1 MB to 1024 MB. Pay attention to the following points when you modify the chunk size:

   * Automatic chunk splitting occurs during data insert or update only.

   * A small chunk size value will make data distribution more even but will result in more frequent migrations, leading to higher query route costs. If you decrease the chunk size value, it takes some time for MongoDB to split data from the original chunk to a new chunk. This operation is non\-reversible.

   * A large chunk size value means few migrations and low query route and network load. However, it may lead to uneven data distribution, limiting sharding advantages. If you increase the chunk size value, an existing chunk can be expanded to the new size only after an insert or update operation.

   For more information, refer to [Modify Chunk Size in a Sharding Cluster](https://www.mongodb.com/docs/v5.0/tutorial/modify-chunk-size-in-sharded-cluster/).

* **Jumbo chunk**

   When data is written to a chunk persistently to exceed the chunk size value and the chunk cannot be split due to some causes (for example, a chunk is a single shard key value), the chunk will be marked as a jumbo chunk. A jumbo chunk cannot be migrated by a balancer, which may lead to load unbalancing and affect the database performance.

   After a chunk is marked as a jumbo chunk, you can handle the issue as follows:

   * If the chunk can be split, you can run the `sh.splitAt()` or `sh.splitFind()` command to split it. After the chunk is split, MongoDB automatically clears the jumbo flag of the chunk. For more information, refer to [sh.splitAt()](https://www.mongodb.com/docs/v5.0/reference/method/sh.splitAt/#mongodb-method-sh.splitAt) and [sh.splitFind()](https://www.mongodb.com/docs/v5.0/reference/method/sh.splitFind/#mongodb-method-sh.splitFind).

   * If the chunk cannot be split, you can run the `clearJumboFlag` command to manually clear the jumbo flag of the chunk. For more information, refer to [clearJumboFlag](https://www.mongodb.com/docs/v5.0/reference/command/clearJumboFlag/#mongodb-dbcommand-dbcmd.clearJumboFlag).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">We recommend you back up the Config database before clearing to avoid damage to the database by misoperation. For more information, refer to <a href="https://www.mongodb.com/docs/v5.0/tutorial/clear-jumbo-flag/">Clear jumbo Flag</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can increase the chunk size. The jumbo flag will be cleared when the chunk does not exceed the chunk size. The jumbo chunk appears again when more data is written to the chunk. The fundamental solution is to set a proper shard key. For more information, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/ug-for-sharding-cluster#X5MWXlDL">Setting a proper shard key</a>.      </div>
      


<span id=".6LSf6L295Z2H6KGh"></span>
### Load balancing

The MongoDB balancer periodically checks whether the shards have a balanced number of chunks. If the difference in chunk quantity of the shards reaches the specified migration threshold, the balancer automatically migrates data among the shards to implement even data distribution to all the shards.

The MongoDB balancer is enabled by default. You can run the `sh.stopBalancer()` command to manually disable the balancer. For more details, refer to [Disable balance](https://www.mongodb.com/docs/v5.0/tutorial/manage-sharded-cluster-balancer/#disable-the-balancer).

The MongoDB balancer supports online data migration, but data migration has a huge impact on the cluster load. We recommend you set the migration time of the balancer to off\-peak hours. You can set the active time window of the balancer through the `activeWindow` parameter in the following commands:

```Bash
# Switch to config database
use config

# Set the active time window of the balancer
db.settings.updateOne(
   { _id: "balancer" },
   { $set: { activeWindow : { start : "<start-time>", stop : "<stop-time>" } } },
   { upsert: true }
)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Change <code><start-time></code> and <code><stop-time></code> in the preceding code to the specified time, for example, <code>{ start : "01:30", stop : "04:30" }</code>, based on your business scenario. For more information, refer to <a href="https://www.mongodb.com/docs/v5.0/tutorial/manage-sharded-cluster-balancer/#modify-the-balancer-s-window">Modify balancer's window</a>.</div>


* <div data-tips="true" data-tips-type="tip">The above time is subject to the time zone of the region where the MongoDB sharding cluster instance is located, among which:</div>


   * <div data-tips="true" data-tips-type="tip">Mainland China region: The time zone used is UTC +8.</div>


   * <div data-tips="true" data-tips-type="tip">China (Hong Kong) and overseas regions: The time zone used is UTC.</div>



<span id=".5YiG54mH6ZuG576k5pWw5o2u5YiG54mH6K6-572u5a6e5pON"></span>
## Configuring data sharding for sharding cluster

<span id=".5L2_55So5Zy65pmv"></span>
### Usage scenario

An automobile self\-driving application wants to use the MongoDB sharding cluster to store self\-driving logs of mass vehicles. Assume that there are millions of vehicles and the vehicles upload logs to the MongoDB database every 10 seconds. The logs contain the vehicle ID and timestamp information. The application wants to query the log information of a specific vehicle within the specified period.

<span id=".c2hhcmQta2V5Leiuvue9ruaWueahiA=="></span>
### Shard key setting solutions

You can select a shard key setting solution from the following table based on the usage scenario and query requirements.


|Optional solution |Description |
|---|---|
|Solution 1 (recommended):<br><br>This solution adopts ranged sharding by using the combination of vehicle ID and timestamp as the shard key. |* This solution evenly writes data to multiple shards.<br><br>* Data of a vehicle ID is further distributed to multiple chunks based on the timestamp.<br><br>* The complex index (vehicle ID and timestamp) can be used to query data within the specified period based on the vehicle ID. |
|Solution 2:<br><br>This solution adopts ranged sharding by using the timestamp as the shard key. |* This solution writes new requests with continuous timestamps to the same shard, resulting in uneven data distribution.<br><br>* Vehicle ID\-based queries are distributed to all the shards, resulting in low efficiency. |
|Solution 3:<br><br>This solution adopts hashed sharding by using the timestamp as the shard key. |* This solution evenly writes data to multiple shards.<br><br>* Vehicle ID\-based queries are distributed to all the shards, resulting in low efficiency. |
|Solution 4:<br><br>This solution adopts hashed sharding by using the vehicle ID as the shard key.<br><br>Ranged sharding can be used if there are no obvious rules concerning the vehicle ID. |* This solution evenly writes data to multiple shards.<br><br>* Data of a vehicle ID cannot be further split and can only be distributed to the same chunk, resulting in a jumbo chunk.<br><br>* Vehicle ID\-based queries are routed to a single shard. After the queries reach the shard, full table scan and sorting are performed based on the range of the timestamp. |


<span id=".c2hhcmQta2V5Leiuvue9ruatpemqpA=="></span>
### Setting shard key

Based on the usage scenarios and query requirements, this topic uses the recommended solution 1 (ranged sharding by using the combination of the vehicle ID and timestamp as the shard key) as an example to describe how to set a shard key for the MongoDB sharding cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following steps use the <code>IoV</code> database, the <code>AutonomousCar</code> collection, and the <code>VehicleId</code> and <code>Timestamp</code> fields as an example.</div>



1. Log in to the target sharding cluster instance via the Mongo shell tool. For more information, refer to [Connect to instance via Mongo shell tool](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

2. Run the `use <database name>` command to access the target database.

   Example is as follows.

   ```Bash
   use IoV
   ```
   

3. Run the following commands to check whether the target collection is sharded.

   ```Bash
   db.<collection>.getShardDistribution()
   ```
   

   If the response is `Collection <collection> is not sharded`, the current collection is not sharded. For more information, refer to [db.collection.getShardDistribution()](https://www.mongodb.com/docs/v5.0/reference/method/db.collection.getShardDistribution/).

   The command example is as follows:

   ```Bash
   db.AutonomousCar.getShardDistribution()
   ```
   

4. Enable the sharding feature on the database to which the collection belongs.

   You can use either of the following methods to enable the sharding feature on the target database.

   
   <Tabs>
   <Tab zoneid="X4aTlCZdJK" title="Method 1">
   <TabTitle>Method 1</TabTitle>
   
   Log in to the target sharding cluster instance via the Mongo shell tool and then run the following commands:
   
   ```Bash
   sh.enableSharding("<database>")
   ```
   
   
   Example is as follows.
   
   ```Bash
   sh.enableSharding("IoV")
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="Pjjq5C2rOG" title="Method 2">
   <TabTitle>Method 2</TabTitle>
   
   Log in to the target sharding cluster instance via the Mongo shell tool. First, run the `use admin` command to enter the admin database, then execute the following command:
   
   ```Bash
   db.runCommand({enablesharding:"<database>"})
   ```
   
   
   Example is as follows.
   
   ```Bash
   db.runCommand({enablesharding:"IoV"})
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

   Run the following commands to check whether the MongoDB balancer is enabled:

   ```Bash
   sh.getBalancerState()
   ```
   

   If the response is `true`, the balancer is enabled. If the difference in chunk quantity of the shards reaches the specified migration threshold, the balancer automatically migrates data among the shards to implement even data distribution to all the shards. For more details, refer to [Check balancer state](https://www.mongodb.com/docs/v5.0/tutorial/manage-sharded-cluster-balancer/#check-the-balancer-state).

   If the response is `false`, the balancer is disabled. You can run the `sh.startBalancer()` command to enable the balancer. For more information, refer to [Enable balancer](https://www.mongodb.com/docs/v5.0/tutorial/manage-sharded-cluster-balancer/#enable-the-balancer).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Starting from MongoDB 4.2, when you turn on the balancer using the <code>sh.startBalancer()</code> command, the sharding cluster's auto\-splitting feature is enabled by default. For more details, refer to <a href="https://www.mongodb.com/docs/v5.0/reference/method/sh.enableAutoSplit/#mongodb-method-sh.enableAutoSplit">sh.enableAutoSplit</a>.   </div>
   

6. Shard the collection.

   You can use either of the following methods to shard the target collection.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This example uses the combination of the <code>VehicleId</code> and <code>Timestamp</code> fields as the shard key. You must create a complex index by using the two fields. For the specific method of creating an index, refer to <a href="https://www.mongodb.com/docs/v5.0/reference/method/db.collection.createIndex/#mongodb-method-db.collection.createIndex">db.collection.createIndex()</a>.   </div>
   

   
   <Tabs>
   <Tab zoneid="mj96UkD8u8" title="Method 1">
   <TabTitle>Method 1</TabTitle>
   
   Log in to the target sharding cluster instance via the Mongo shell tool and then run the following commands.
   
   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="0">tip</div>
   
   
   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">For more information on the <code>sh.shardCollection</code> command, refer to <a href="https://www.mongodb.com/docs/v7.0/reference/method/sh.shardCollection/">sh.shardCollection()</a>.</div>
   
   
   ```Bash
   sh.shardCollection("<database>.<collection>",{"<keyname>":<value> })
   ```
   
   
   Example is as follows.
   
   ```Bash
   sh.shardCollection("IoV.AutonomousCar",{"VehicleId":1,"Timestamp":1})
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="t0sJaTw5KB" title="Method 2">
   <TabTitle>Method 2</TabTitle>
   
   Log in to the target sharding cluster instance via the Mongo shell tool. First, run the `use admin` command to enter the admin database, then execute the following command.
   
   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="0">tip</div>
   
   
   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">For more information on the <code>shardcollection</code> command, refer to <a href="https://www.mongodb.com/docs/v7.0/reference/command/shardCollection/#mongodb-dbcommand-dbcmd.shardCollection">shardCollection</a>.</div>
   
   
   ```Bash
   db.runCommand({shardcollection:"<database>.<collection>",key:{"keyname":<value> }})
   ```
   
   
   Example is as follows.
   
   ```Bash
   db.runCommand({shardcollection:"IoV.AutonomousCar",key:{"VehicleId":1,"Timestamp":1}})
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

   The descriptions of the relevant parameters in the command are shown in the following table.

   
   |Parameter |Description |
   |---|---|
   |`<database>` |Name of the target database. |
   |`<collection>` |Name of the target collection. |
   |`<keyname>` |Shard key. The cluster instance shards the data based on the shard key value. Select a proper shard key for the collection based on your business needs. For more information, refer to [Setting a proper shard key](https://docs.byteplus.com/en/docs/mongodb/ug-for-sharding-cluster#X5MWXlDL). |
   |`<value>` |Sharding policy based on the shard key. The value range is as follows:<br><br><br>* `1`: Ranged sharding is used.<br><br>* `hashed`: Hashed sharding is used.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information on the sharding policy, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/ug-for-sharding-cluster#X5MWXlDL">Sharding Policies</a>.</div><br> |
   |`numInitialChunks` |The minimum number of shards specified during initial creation when hashed sharding is used to shard a null collection. For more information on `numInitialChunks`, refer to [sh.shardCollection()_option](https://www.mongodb.com/docs/manual/reference/method/sh.shardCollection/#definition) or [shardCollection_command-fields](https://www.mongodb.com/docs/v6.0/reference/command/shardCollection/#command-fields). |
   

7. On the target database, run the following commands to view data storage on each shard node.

   ```Bash
   sh.status()
   ```
   

   For more information, refer to [sh.status()](https://www.mongodb.com/docs/v5.0/reference/method/sh.status/).
