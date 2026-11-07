---
title: "Guide to setting oplog-related parameters"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/guide-to-set-oplog-related-parameters"
---

The Document Database for MongoDB provides parameters related to oplog size and oplog retention time. If the oplog\-related parameters are set unreasonably, it may lead to the oplog being overwritten, thereby affecting functions such as MongoDB's primary\-secondary replication and data recovery by time point. This topic introduces how to configure reasonable oplog\-related parameters for your reference.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

oplog (Operation log) is a special capped collection in MongoDB. It is the basic mechanism for implementing replication functions in MongoDB. It records all write operations (such as insertions, updates, deletions, etc.) executed on the database in chronological order in the `local.oplog.rs` collection. For more details about oplog, refer to [Replica-set-oplog](https://www.mongodb.com/docs/manual/core/replica-set-oplog/).

<span id=".b3Bsb2ct5aSn5bCP"></span>
### Oplog size

The Document Database for MongoDB provides the `replication.oplogSizeMB` parameter to specify the size of oplog. This parameter supports both dynamic and static values, where:


* Dynamic value: That is `Default`. The system will use 10% of the instance's maximum available storage space for logging oplogs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example, if the maximum available storage for the instance is 20 GiB and <code>replication.oplogSizeMB</code> is set to <code>Default</code>, then the space available for logging oplogs in the current instance is 2 GiB. For more details about this parameter, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/supported-parameter">replication.oplogSizeMB</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you modify the instance configuration in such a way that the maximum available storage space for the instance changes, the actual value of <code>replication.oplogSizeMB</code> will also change. For more details about the instance maximum available storage space, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/view-instance">Viewing instance information</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To ensure instance performance, it is recommended that <strong>the oplog size not exceed 30% of the maximum available storage space of the instance</strong>. If the required oplog size exceeds this value, it is recommended to expand the storage space of the instance. For the specific operation steps of instance configuration change, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-replica-set-instance-spec">Modifying replica set instance specification</a> and <a href="https://docs.byteplus.com/en/docs/mongodb/change-sharding-cluster-config">Changing sharding cluster instance configuration</a>.   </div>
   

* Static value: 2048 ~ 90% of the maximum available storage space for instance. Unit: MiB.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The static range of values for this parameter varies by instance or node specification, and the exact value is based on the console. For example, if the maximum available storage space of the instance is 60 GiB, then the static range of values on the console is 2048~55296.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can adjust the oplog size by configuring the <code>replication.oplogSizeMB</code> parameter. After adjusting this parameter, it takes effect immediately without restarting the instance. For parameter modification methods, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-parameter">Modifying instance parameters</a>.   </div>
   


You can connect to a MongoDB instance through client tools such as mongo shell or mongosh. After connecting, execute the following command to view the oplog size and oplog window.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For the specific procedure of connecting to an instance through mongo shell or mongosh tools, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell">Connecting to instance via mongo shell tool</a>.</div>


* <div data-tips="true" data-tips-type="tip">To view the oplog size of a sharding cluster, use the Shard connection address in the sharding cluster for viewing. For more details about the connection address, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/addresses-introduction">Viewing connection address</a>.</div>



```Bash
rs.printReplicationInfo()
```


The example result is as follows.

```Bash
configured oplog size:   2048MB
log length start to end: 13015382secs (3615.38hrs)
oplog first event time:  Fri Oct 18 2024 19:41:03 GMT+0800 (CST)
oplog last event time:   Tue Mar 18 2025 11:04:05 GMT+0800 (CST)
now:                     Tue Mar 18 2025 11:04:05 GMT+0800 (CST)
```


In the above example, the oplog size is 2048MB, and the oplog window is approximately 3615 hours.

<span id=".b3Bsb2ct5pyA55-t5L-d55WZ5pyf"></span>
### Minimum retention period of oplog

The Document Database for MongoDB provides the oplog minimum retention period parameter `oplogMinRetentionHours`. After setting this parameter, it can be ensured that the minimum oplog retention window of a MongoDB instance will not be less than the value of this parameter.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only MongoDB versions 4.4 and later support this parameter. For more details about this parameter, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/supported-parameter">oplogMinRetentionHours</a>.</div>


* <div data-tips="true" data-tips-type="tip">If you need to adjust the oplog minimum retention period, you can modify the <code>oplogMinRetentionHours</code> parameter on the MongoDB console. After this parameter is adjusted, the instance does not need to be restarted to take effect. For parameter modification methods, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-parameter">Modifying instance parameters</a>.</div>


* <div data-tips="true" data-tips-type="tip">The Document Database for MongoDB supports setting up event alert rules for the oplog retention window. If the available time of the oplog is too short, then the number of oplog records that can be retained is limited. In scenarios such as increased primary\-secondary replication latency and slave database reconstruction, the risk of primary\-secondary replication failure due to the lack of required oplog will increase, thereby affecting instance availability and data reliability. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/event-monitoring">Event monitoring</a>.</div>



The oplog cleanup rules of Document Database for MongoDB instances are controlled by the oplog size and minimum retention period. See the table below for specific cleanup rules.


|Parameter setting scenarios |Oplog cleaning rules |Oplog cleaning example |
|---|---|---|
|The `oplogMinRetentionHours` parameter is not set |The default value of the `oplogMinRetentionHours` parameter is 0, indicating that there is no minimum oplog retention period set. At this time, the cleaning rule for oplog is controlled solely by the `replication.oplogSizeMB` parameter. |For example, after a MongoDB instance is successfully created, the default values of `oplogMinRetentionHours` and `replication.oplogSizeMB` are not manually modified. That is, the minimum oplog retention period is not set, and the storage space of oplog size is 10% of the maximum available storage space of the instance. Then the system will be automatically cleaned up after the oplog size exceeds 10% of the maximum available storage space of the instance. |
|The `oplogMinRetentionHours` parameter has been set. |At this time, the oplog cleaning rule will be controlled by both the oplog size and the minimum retention period parameter. When the following conditions are simultaneously met, MongoDB will start cleaning the oplog:<br><br><br>* The actual size of the oplog collection has exceeded the oplog size configured by the `replication.oplogSizeMB` parameter.<br><br>* The timestamp recorded in the oplog has exceeded the oplog time window configured by the `oplogMinRetentionHours` parameter. |For example, after a MongoDB instance is successfully created, according to business needs, the minimum oplog retention period is set to 40 hours. The oplog size still uses the default dynamic value (that is, 10% of the maximum available storage space of the instance).<br><br>When the instance is initialized and not much data has been written yet, the actual size of the oplog collection has not reached the upper limit configured by the `replication.oplogSizeMB` parameter. And the oplog time window configured by the `oplogMinRetentionHours` parameter is usually much larger than the actually needed oplog time window. Therefore, the size of the oplog collection is controlled only by the `replication.oplogSizeMB` parameter alone.<br><br>As business develops, when the actual size of the oplog collection has exceeded the parameter value of `replication.oplogSizeMB`, the size of the oplog will be limited by the shortest retention period of the oplog. If the oplog generation speed is relatively fast, the actual size of the oplog collection may far exceed the parameter value configured by `replication.oplogSizeMB`. |


<span id=".6K6-572u5oyH5Y2X"></span>
## Setup guide

<span id=".6YCa55So5Zy65pmv6K6-572u5oyH5Y2X"></span>
### General scenario setup guide

You can refer to the following table to appropriately increase or decrease the oplog size according to your own business characteristics.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Under normal circumstances, it is recommended to only modify the <code>replication.oplogSizeMB</code> parameter to ensure there is a sufficient oplog window.</div>


* <div data-tips="true" data-tips-type="tip">In the Document Database MongoDB version, the <code>replication.oplogSizeMB</code> parameter defaults to a dynamic value\-taking method, that is, the system will use 10% of the maximum available storage space of the instance to record oplog. Under normal circumstances, you only need to keep the default value. If you change the instance configuration and cause the maximum available storage space of the instance to change, then the actual value of <code>replication.oplogSizeMB</code> will also change automatically.</div>


* <div data-tips="true" data-tips-type="tip">Whether setting the oplog size of a MongoDB instance or the oplog minimum retention period parameter, <strong>it is recommended to ensure that the oplog window period is more than 24 hours</strong>.</div>




|Oplog size adjustment suggestions |Applicable business characteristics |
|---|---|
|Appropriate increase in oplog size |The business has more operations such as addition, deletion, and modification, such as batch updates, frequent insertions and deletions, or a large number of in\-place updates. |
|Consider reducing oplog size as appropriate |There are fewer addition, deletion, and modification operations in the business, and the MongoDB database is mainly used to store cold data. |


<span id=".54m55q6K5Zy65pmv6K6-572u5oyH5Y2X"></span>
### Special scenarios setup guide

<span id=".5Y-Y6YWN6YeN5ZCv562J5Zy65pmv6ZyA5YWz5rOo55qE55u45YWz6YWN572u"></span>
#### Relevant configurations to pay attention to in scenarios such as scaling and restarting

After adding or restarting a secondary node, it is necessary to rely on the records in the oplog to determine whether these nodes can become nodes that work properly in the replica set. These nodes may experience delays in certain situations (such as network latency, packet loss, interruption, the disk throughput of the secondary node reaching a bottleneck, `writeConcern` using `{w:1}` and a large write load), and cannot find the expected oplog records from the synchronization source. At this time, a `too stale to catch up` error will occur, and the node state will also change to the abnormal state of [RECOVERING](https://www.mongodb.com/docs/manual/reference/replica-states/#mongodb-replstate-replstate.RECOVERING), ultimately leading to the failure of primary\-secondary node replication.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before performing operations such as scaling or restarting, it is strongly recommended to focus on the delay of secondary nodes in the MongoDB instance and whether the oplog window period of the instance can meet the requirements to avoid nodes entering an abnormal state and being unable to recover due to excessive delay of secondary nodes. When the delay of secondary nodes continues to increase, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support for assistance.</div>


You can view the delay of secondary nodes in any of the following methods.


|View method |Procedure |Result example |
|---|---|---|
|Method 1: View through the MongoDB console |After logging in to the [MongoDB console](https://console.byteplus.com/db/mongodb), you can view other node's delay by checking the **Replication lag** filed in the node list, located in the **Node information** area on the **Summary** tab. For specific procedures of viewing instance information, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance). |You can refer to the **Replication lag** field in the following figure to view the node's delay.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1554e0a9e241f42bc2313c33983e69d5.png) </span><br><br>As can be seen from the above screenshot, other nodes in the instance have no delay with the primary node. |
||You can view the node's delay through the **Replication lag** indicator on the **Monitoring** tab of the [MongoDB console](https://console.byteplus.com/db/mongodb). For the method of viewing monitoring indicators, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/mongodb/view-monitoring-data). |You can refer to the **Replication lag** indicator in the following figure to view the node's delay.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_df7189d1919edd263cb3325edd2ab36e.png) </span><br><br>As can be seen from the above screenshot, other nodes in the instance have no delay with the primary node. |
|Method 2: View through client tools |You can connect to the MongoDB instance through client tools such as mongo shell or mongosh. After that, execute the following commands to view the delay situation of secondary nodes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For the specific procedure of connecting to an instance through mongo shell or mongosh tools, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell">Connecting to instance via mongo shell tool</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To view the delay between the primary and secondary nodes of a sharding cluster, use the Shard connection address in the sharding cluster for viewing. For more details about the connection address, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/addresses-introduction">Viewing connection address</a>.</div><br><br><br><br>```Bash```<br>```rs.printSecondaryReplicationInfo()```<br> |You can view the delay situation of secondary nodes according to the `behind the primary` information in the command return result. The example result is as follows.<br><br>```Bash```<br>```source: mongo-replica-****-0.mongons.****:27017```<br>```        syncedTo: Thu Mar 13 2025 15:29:40 GMT+0800 (CST)```<br>```        5 secs (0 hrs) behind the primary```<br>```source: mongo-replica-****-0.mongons.****:27017```<br>```        syncedTo: Thu Mar 13 2025 15:29:45 GMT+0800 (CST)```<br>```        0 secs (0 hrs) behind the primary```<br>```source: readonly-mongo-replica-****-0.mongons.****:27017```<br>```        syncedTo: Thu Mar 13 2025 15:29:45 GMT+0800 (CST)```<br>```        0 secs (0 hrs) behind the primary```<br><br><br>In the above example, the first secondary node has a 5\-second delay (`5 secs (0 hrs) behind the primary`), while the other two secondary nodes have no delay (`0 secs (0 hrs) behind the primary`). |


<span id=".6YG_5YWN5pel5b-X5aSH5Lu956m65rSe55qE55u45YWz6YWN572u5bu66K6u"></span>
#### Configuration suggestions for avoiding log backup gaps

By default, the Document Database for MongoDB enables the automatic backup function. The backup objects include database data and oplog logs. For log backups, the system automatically performs streaming backups of oplog logs at a frequency of once per minute without configuration. For more details, see [Backup and recovery](https://docs.byteplus.com/en/docs/mongodb/backup-overview).

MongoDB supports restoring instance data by time point by replaying oplog in log backup files. However, in some data synchronization, import, or testing scenarios (for example, using DTS, mongoShake, or other tools to synchronize/import a large amount of data, batch inserting or updating a large amount of data in a short period, or performing stress tests on data), the write speed of the instance will be very fast. If the oplog size is set to be small or the shortest retention period of oplog is too short at this time, the oplog may cover old operation records too quickly, and the log backup cannot keep up with the oplog coverage speed, resulting in a log backup gap.

You can estimate the oplog generation speed by oplog size and oplog window. For example, if the oplog size of a MongoDB instance is 1800 GiB and the oplog window is 25 hours (i.e., 1500 minutes), then the oplog generation speed is approximately 1.2 GiB/min. According to the past usage experience of Document Database for MongoDB instances, when the oplog generation speed exceeds 10 GiB/min, the probability of log backup gaps will greatly increase.

To avoid or reduce the occurrence of log backup gaps, you can refer to the following suggestions to optimize the database:


* Appropriately limit the write concurrency and batch size of synchronization or import tools.

* Set `writeConcern` to `{w:"majority"}` instead of `{w:1}`.

* Use sharded cluster instances or increase the number of shards to reduce the oplog generation speed on a single shard by dispersing data to multiple shards.

* Appropriately increase the oplog size or the shortest retention period of oplog according to business characteristics and needs to provide more buffer time for log backups so that log backups have enough time to catch up with the previously lagging oplog records during business low periods.


<span id=".55u45YWz55uR5o6n5ZGK6K2m6YWN572u"></span>
## Related monitoring and alarm configuration

After reasonably configuring oplog\-related parameters according to the above setting guidelines, it is strongly recommended that you also set up the following related monitoring and alarm configurations for MongoDB according to business needs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For details on the monitoring metrics supported by MongoDB, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/monitoring-metric">Monitoring metrics</a>.</div>


* <div data-tips="true" data-tips-type="tip">For the specific procedure to view the monitoring data of MongoDB instances, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/view-monitoring-data">Viewing monitoring data</a>.</div>


* <div data-tips="true" data-tips-type="tip">For the specific procedure to create alert policy for MongoDB instances, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/set-alert">Setting alerts</a>.</div>


* <div data-tips="true" data-tips-type="tip">For details on the event monitoring supported by MongoDB, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/event-monitoring">Event monitoring</a>.</div>




|Monitoring alarm items ||Recommended monitoring alarm rules |
|---|---|---|
|Monitoring indicator alarm |Replication lag |It is recommended to focus on the monitoring indicator of **Replication lag** in MongoDB instances to avoid the node entering an abnormal state and being unable to recover due to excessive delay of the secondary node.<br><br>You can configure a cloud monitoring alarm for the monitoring indicator of **Replication lag**. It is recommended to set the alarm threshold to more than 10 seconds. |
||Total disk usage |After setting the oplog minimum retention period parameter, it is recommended that you closely monitor the **Total disk usage** monitoring indicator of the instance to avoid the risk of decreased instance performance due to excessive disk space occupied by oplog when oplog is generated quickly.<br><br>You can configure a cloud monitoring alarm for the **Total disk usage** indicator. It is recommended to set the alarm threshold to 75%. |
|Event alarm |OplogWindowInsufficient |Document Database for MongoDB supports event monitoring and alarming for the oplog retention window of instances. When the available time of oplog is insufficient, a corresponding alarm will be triggered to help you promptly detect unreasonable oplog\-related settings and prevent problems such as abnormal primary\-secondary synchronization and inability to restore data according to a time point.<br><br>When you receive relevant monitoring alarms, please refer to the optimization suggestions in the document for handling. For more details, refer to [What should be done after receiving event monitoring alarm for oplog window being insufficient](https://docs.byteplus.com/en/docs/mongodb/instance-management-faq#.5pS25Yiw5a6e5L6LLW9wbG9nLeS_neeVmeeql-i_h-Wwj-eahOS6i-S7tuebkeaOp-WRiuitpuWQjuivpeWmguS9leWkhOeQhu-8nw==). |
