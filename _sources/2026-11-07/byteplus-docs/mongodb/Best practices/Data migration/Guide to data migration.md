---
title: "Guide to data migration"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/data-migration-guide"
---

Document Database for MongoDB supports multiple data migration solutions provided by Database Transmission Service (DTS) to meet the needs of MongoDB data migration in different business scenarios. This topic introduces the MongoDB data migration solutions supported by DTS, basic principles, and relevant suggestions on migration speed limits.

<span id=".6L-B56e75bel5YW35LuL57uN"></span>
## Introduction to migration tools

Database Transmission Service (DTS) is a data stream service that integrates data migration, synchronization, and subscription. It supports data interaction between relational databases, non\-relational databases, and other data sources, reducing the complexity of data flow between databases. DTS helps you easily migrate databases to the cloud without interrupting business operations, effortlessly build high\-availability database disaster recovery architectures through real\-time synchronization channels, and freely consume real\-time incremental data provided by cloud databases according to your own needs. For more information on DTS, refer to [About DTS](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service).

<span id=".6L-B56e75pa55qGI5qaC6KeI"></span>
## Overview of migration plans


|Source database access method |Source database version |Migration type |Operation guide |
|---|---|---|---|
|BytePlus Document Database for MongoDB |* MongoDB 4.0<br><br>* MongoDB 4.2<br><br>* MongoDB 4.4<br><br>* MongoDB 4.0<br><br>* MongoDB 6.0<br><br>* MongoDB 7.0 |* Schema migration<br><br>* Schema migration<br><br>* Schema migration |[Migrating data from BytePlus MongoDB to BytePlus MongoDB](https://docs.byteplus.com/en/docs/mongodb/bp-mongodb-to-bp-mongodb) |
|Self\-managed MongoDB (public network) |* MongoDB 3.4<br><br>* MongoDB 3.6<br><br>* MongoDB 4.0<br><br>* MongoDB 4.2<br><br>* MongoDB 4.4<br><br>* MongoDB 5.0<br><br>* MongoDB 6.0<br><br>* MongoDB 7.0 ||[Migrating data from self-managed MongoDB (public network) to BytePlus MongoDB](https://docs.byteplus.com/en/docs/mongodb/self-managed-public-network-mongodb-to-bp-mongodb) |
|Self\-managed MongoDB (express network) |||[Migrate data from self-managed MongoDB (express network) to BytePlus MongoDB](https://docs.byteplus.com/en/docs/mongodb/self-managed-express-network-mongodb-to-bp-mongodb) |


<span id=".6L-B56e75Z-65pys5Y6f5YiZ"></span>
## Basic principles for migration


* Before formal migration, it is strongly recommended to conduct drills in a test scenario that simulates real business to evaluate the impact of data migration on the performance of MongoDB (with a focus on read/write I/O, primary\-secondary replication delay, etc.).

* It is strongly recommended to perform data migration operations during off\-peak business hours to avoid or reduce the impact on online business.

* When the Document Database for MongoDB is used as the source database, it is recommended to read data from the secondary node or read\-only node of MongoDB first. Moreover, during the data migration process, focus on the impact of data **reading operations** on business.

* When the Document Database for MongoDB is used as the target database, it is recommended to focus on monitoring indicators such as data **write operations** and **replication lag** in MongoDB during the data migration process. Avoid excessive delay on secondary nodes, which may cause the secondary nodes to enter an abnormal state and cannot be recovered, thereby affecting the overall availability and data reliability of the instance. For more explanations on the MongoDB replication lag monitoring indicator, refer to [Monitoring metrics](https://docs.byteplus.com/en/docs/mongodb/monitoring-metric).

* Appropriately limit the concurrency and batch size of the data migration tool to control the impact of data writing within an acceptable range and avoid excessive migration speed leading to excessive replication lag on the instance and affecting business. **It is strongly recommended to first set a lower migration rate according to the instance specifications, and then gradually increase the rate according to the read and write pressure of the source and target databases**. For more instructions, refer to S[peed limit suggestions for migration tools](https://docs.byteplus.com/en/docs/mongodb/data-migration-guide#.6L-B56e75bel5YW36ZmQ6YCf5bu66K6u).


<span id=".6L-B56e75bel5YW36ZmQ6YCf5bu66K6u"></span>
## Speed limit suggestions for migration tools

The Database Transmission Service (DTS) of BytePlus provides rate configuration parameters for full migration when migrating MongoDB data to prevent excessive migration rate from affecting database performance. You can appropriately adjust relevant parameters according to the read and write pressure of the source and target databases. The specific parameter descriptions are shown in the following table.


|Parameter name |Parameter description |
|---|---|
|Concurrency of migration tasks |Set the concurrency of migration tasks as needed. The default value is 8, and the value range is 8\-64. |
|Rows migrated per second |Enable and set the number of rows migrated per second as needed. The default value is 100,000, and the value range is 1\-100,000. |
|Data migrated per second |Enable and set the amount of data migrated per second as needed. The default value is 25,000, and the value range is 1\-25,000, unit: KB. |


Combined with the above speed limit configuration parameters, MongoDB provides the following migration speed limit suggestions for your reference.


|Database type |Migration speed limit suggestion |
|---|---|
|Source database |* The impact of data reading on the source database is relatively controllable. It is recommended to use the default migration task concurrency of DTS (i.e., 8) in the migration drill scenario and record the impact of data migration on the read/write I/O, CPU, memory, etc. of the source MongoDB instance under this concurrency.<br><br>* When officially performing data migration in the production environment, combine the instance specifications of the source database and the remaining performance resources of the business to appropriately increase or decrease the concurrency.<br><br>   For example, when the specification of the source MongoDB instance is relatively small or the resource utilization rate of the source MongoDB is relatively high, migration can be started with a concurrency of 2 or 4 first.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the migration speed allowed by the current specification of the instance cannot meet your migration requirements, you can try to upgrade the specification configuration of the source MongoDB instance. For the specific operation steps of instance configuration change, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-replica-set-instance-spec">Modifying replica set instance specification</a> and <a href="https://docs.byteplus.com/en/docs/mongodb/change-sharding-cluster-config">Changing sharding cluster instance configuration</a>.   </div><br>    |
|Target database |* If no data has been written in the target MongoDB instance and it is only used for data migration, then according to the reference values of the test results in [MongoDB migration performance reference](https://docs.byteplus.com/en/docs/mongodb/data-migration-guide#.bW9uZ29kYi3ov4Hnp7vmgKfog73lj4LogIM=), you can configure reasonable full migration rate parameters for the DTS migration task, including the number of rows migrated per second and the amount of data migrated per second.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The migration performance reference values provided in <a href="https://docs.byteplus.com/en/docs/mongodb/data-migration-guide#.bW9uZ29kYi3ov4Hnp7vmgKfog73lj4LogIM=">MongoDB migration performance reference</a> are obtained through tests without any other business loads. When configuring full migration rate parameters in actual business, you need to set them comprehensively considering the actual read and write load of the business.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can estimate the general situation of the current read\-write load of the business according to the monitoring metric values of <strong>Network input rate</strong> and <strong>Network output rate</strong> of the instance. For more details about Network input rate and Network output rate, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/monitoring-metric">Monitoring metrics</a>.   </div><br>   <br><br>* It is recommended to set a relatively low migration rate first according to the instance specification, and then gradually increase the rate according to the read and write pressure of the source and target databases. For specific procedure, refer to [Adjusting full migration rate](https://docs.byteplus.com/en/docs/DTS/adjusting_full_migration_rate).<br><br>* It is recommended to closely monitor the **Replication lag** monitoring indicator in the target MongoDB instance during the migration process. For more explanations on the MongoDB replication lag monitoring indicator, refer to [Monitoring metrics](https://docs.byteplus.com/en/docs/mongodb/monitoring-metric).<br><br>* The migration process is likely to generate a large amount of oplog in a short period of time. If you have configured the oplog minimum retention period parameter (i.e., `oplogMinRetentionHours`) for the target MongoDB, it is recommended that you closely monitor the monitoring indicator of **Total disk usage** of the instance to avoid the risk of decreased instance performance due to excessive disk space occupied by oplog when the oplog generation speed is relatively fast. For more details, refer to [Guide to setting oplog-related parameters](https://docs.byteplus.com/en/docs/mongodb/guide-to-set-oplog-related-parameters). |


<span id=".bW9uZ29kYi3ov4Hnp7vmgKfog73lj4LogIM="></span>
## MongoDB migration performance reference

<span id=".5oCn6IO95rWL6K-V5pa55rOV"></span>
### Performance testing methods

Details of the test methods used in this topic when testing the reference values of MongoDB migration performance, refer to [Test environment](https://docs.byteplus.com/en/docs/mongodb/performance-whitepaper#.5rWL6K-V546v5aKD), [Test tool](https://docs.byteplus.com/en/docs/mongodb/performance-whitepaper#.5rWL6K-V5bel5YW3) and [Test commands](https://docs.byteplus.com/en/docs/mongodb/performance-whitepaper#.5rWL6K-V5ZG95Luk).

<span id=".5oCn6IO95rWL6K-V57uT5p6c"></span>
### Performance test results

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The test results of different specification instances in this topic are all average results obtained after executing the same stress test command three times.</div>


* <div data-tips="true" data-tips-type="tip">The measurement indicators in the performance test result table are explained as follows:</div>


   * <div data-tips="true" data-tips-type="tip">Read rate: That is, the amount of data read from MongoDB by the client per second, unit: MB/s.</div>


   * <div data-tips="true" data-tips-type="tip">Write rate: That is, the amount of data written to MongoDB by the client per second, unit: MB/s.</div>


* <div data-tips="true" data-tips-type="tip">The migration performance reference value provided in this topic is obtained through testing without any other business load. When you configure the full migration rate parameter in actual business, you need to set it comprehensively considering the actual read and write load situation of the business.</div>


* <div data-tips="true" data-tips-type="tip">You can estimate the general situation of the current read\-write load of the business according to the monitoring metric values of <strong>Network input rate</strong> and <strong>Network output rate</strong> of the instance. For more details about Network input rate and Network output rate, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/monitoring-metric">Monitoring metrics</a>.</div>




<Tabs>
<Tab zoneid="pup0uIJBwc" title="Replica set instance">
<TabTitle>Replica set instance</TabTitle>


|Specifications |Test result reference value ||
|---|---|---|
||Read rate(MB/s) |Write rate(MB/s) |
|2 cores 4 GiB |25 |6 |
|4 cores 8 GiB |50 |10 |
|4 cores 16 GiB |55 |10 |
|4 cores 32 GiB |55 |10 |
|8 cores 16 GiB |60 |15 |
|8 cores 32 GiB |60 |15 |
|8 cores 64 GiB |60 |15 |
|16 cores 32 GiB |65 |18 |
|16 cores 64 GiB |65 |18 |
|16 cores 128 GiB |65 |18 |
|32 cores 64 GiB |65 |18 |
|32 cores 128 GiB |85 |18 |
|32 cores 256 GiB |85 |18 |



</Tab>
<Tab zoneid="NbKIqWfUwL" title="Sharding cluster instance">
<TabTitle>Sharding cluster instance</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MongoDB sharding cluster instances provide a variety combinations of node specifications and quantities for Mongos, as well as specifications and quantities for shards. Different combinations may have different impacts on data migration performance.</div>


<div data-tips="true" data-tips-type="tip">For easy comparison, when testing sharding cluster instances of various specifications in this topic, 3 Mongos nodes and 2 shards are used, and the specifications of Mongos and Shard nodes used in each instance are the same. For example, if the specification of the Mongos node used during testing is 2 cores 4 GiB, then the specification of the Shard node in this test instance is also 2 cores 4 GiB.</div>



|Specifications |Test result reference value ||
|---|---|---|
||Read rate(MB/s) |Write rate(MB/s) |
|2 cores 4 GiB |25 x Number of shards |6 |
|4 cores 8 GiB |50 x Number of shards |10 |
|4 cores 16 GiB |55 x Number of shards |15 |
|4 cores 32 GiB |60 x Number of shards |15 |
|8 cores 16 GiB |60 x Number of shards |30 |
|8 cores 32 GiB |60 x Number of shards |30 |
|8 cores 64 GiB |60 x Number of shards |30 |
|16 cores 32 GiB |65 x Number of shards |40 |
|16 cores 64 GiB |65 x Number of shards |40 |
|16 cores 128 GiB |65 x Number of shards |40 |
|32 cores 64 GiB |65 x Number of shards |40 |
|32 cores 128 GiB |85 x Number of shards |40 |
|32 cores 256 GiB |85 x Number of shards |40 |



</Tab>
</Tabs>
