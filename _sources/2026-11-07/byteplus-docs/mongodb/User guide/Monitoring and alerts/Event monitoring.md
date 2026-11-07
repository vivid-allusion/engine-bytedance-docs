---
title: "Event monitoring"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/event-monitoring"
---

Document Database for MongoDB supports managing instance event monitoring information through the Cloud Monitoring event center, including viewing event details, creating and editing event rules, etc., helping you promptly discover, locate, and resolve issues. This topic introduces the events that MongoDB supports monitoring and the operation steps related to event management.

<span id=".5pSv5oyB55uR5o6n55qE5LqL5Lu2"></span>
## Supported monitoring events

MongoDB allows you to monitor exceptional events (Exception) and expected system maintenance events (Maintenance). The following table describes the events of each type.


<Tabs>
<Tab zoneid="ckXgbIRSv2" title="Sharding cluster instance">
<TabTitle>Sharding cluster instance</TabTitle>


|Event type |Event name |Event code |Description |
|---|---|---|---|
|Exception |Sharding cluster instance status abnormal |ShardInstanceStatusAbnormal |When the instance status is abnormal, an event will be triggered. |
||Sharding cluster instance backup failure |ShardInstanceBackupFailure |When instance backup (including manual and automatic full backups, incremental backups, and logical backups) fails, an event will be triggered. |
||Shard cluster instance primary\-secondary failover (due to faults) |ShardInstanceFailover |This event is triggered when an instance encounters a failover (failover). |
||The oplog window of sharding cluster instance is insufficient |ShardOplogWindowInsufficient |When the oplog window of an instance is insufficient, an event will be triggered. |
|Maintenance |Sharding cluster instance primary\-secondary failover (task switching) |ShardInstanceSwitchover |When there is a primary\-secondary failover (task switching) of an instance, an event will be triggered. |





</Tab>
<Tab zoneid="B63Pc1OcJP" title="Replica set instance">
<TabTitle>Replica set instance</TabTitle>


|Event type |Event name |Event code |Description |
|---|---|---|---|
|Exception |Replica set instance status abnormal |ReplicaInstanceStatusAbnormal |When the instance status is abnormal, an event will be triggered. |
||Replica set instance backup failure |ReplicaInstanceBackupFailure |When instance backup (including manual and automatic full backups, incremental backups, and logical backups) fails, an event will be triggered. |
||Replica set instance primary\-secondary failover (due to faults) |ReplicaInstanceFailover |This event is triggered when an instance encounters a failover (failover). |
||The oplog window of replica set instance is insufficient |ReplicaOplogWindowInsufficient |When the oplog window of an instance is insufficient, an event will be triggered. |
|Maintenance |Replica set instance primary\-secondary failover (task switching) |ReplicaInstanceSwitchover |This event is triggered when an instance encounters a failover (task switchover). |





</Tab>
</Tabs>


<span id=".5p-l55yL5LqL5Lu255uR5o6n"></span>
## Viewing event monitoring

You can view events related to MongoDB by using the event center in Vitality Cloud Monitor, including the event occurrence time, event source, event name, and event details.

For more information about how to view event monitoring, refer to [Viewing cloud service events](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-cloud-service-events).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To view monitoring event information on the <strong>Cloud service event</strong> page, set the product name to<strong> Document Database for MongoDB \- Replica set</strong> or <strong>Document Database for MongoDB \- Sharding cluster</strong>.</div>


* <div data-tips="true" data-tips-type="tip">On the event list page, you can locate the target time and click <strong>Details</strong> in the <strong>Actions</strong> column to view details of the event so that you can locate the reason for event triggering. To further locate the fault, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical support.</div>



<span id=".5Yib5bu65LqL5Lu26KeE5YiZ"></span>
## Creating event rules

You can configure alarming rules for events for specified cloud services. When an event that meets the corresponding rule occurs, you will receive alarm notifications at the earliest opportunity, which helps you quickly locate faulty cloud service resources. For specific procedures, refer to [Creating event rule](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When configuring <strong>Event rule</strong> on the <strong>Create event rule</strong> page, you need to select <strong>Resource type</strong> as <strong>Document Database for MongoDB \- Replica set</strong> or <strong>Document Database for MongoDB \- Sharding cluster</strong>.</div>


* <div data-tips="true" data-tips-type="tip">After the event rule is successfully created, you can manage it in the event rule list of Cloud Monitor, including modifying the event rule, or disabling, enabling, or deleting it. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Managing-an-event-rule">Managing event rules</a>.</div>



<span id=".55u45YWz5paH5qGj"></span>
## Relevant documents


* [What should be done after receiving an event monitoring alarm for the oplog window being insufficient?](https://docs.byteplus.com/en/docs/mongodb/instance-management-faq#.5pS25Yiw5a6e5L6LLW9wbG9nLeS_neeVmeeql-i_h-Wwj-eahOS6i-S7tuebkeaOp-WRiuitpuWQjuivpeWmguS9leWkhOeQhu-8nw==)

* [How does Document Database for MongoDB address node failures?](https://docs.byteplus.com/en/docs/mongodb/feature-faq#.5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5aaC5L2V5aSE55CG6IqC54K55pWF6Zqc77yf)
