---
title: "View monitoring data"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/View_monitoring_data"
---

The message queue for RabbitMQ is integrated with cloud monitoring. During daily instance operation, you can directly view various monitoring metrics on the RabbitMQ console or the cloud monitor console to analyze running status of the instance in real time. This section shows you how to view monitoring data and the key monitoring metrics for message queue for RabbitMQ.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before viewing monitoring data, please create message queue for RabbitMQ instance in advance.

<span id="52a2c5b1"></span>
## Notes

After creating an instance, the message service for RabbitMQ automatically adds a RabbitMQ user for you to collect and report monitoring metrics data of the instance. To ensure monitoring data accuracy, please do not modify or delete this user.

The basic information of this user is as follows. You can log in to the RabbitMQ Web UI and check the user under the **Admin** tab. You can refer to [Connect to the RabbitMQ management address](https://docs.byteplus.com/en/docs/rabbitmq/Connect_to_the_RabbitMQ_management_address) or login methods.

<span id=".5pON5L2c5q2l6aqk"></span>
## Operation steps

<span id=".6YCa6L-HIFJhYmJpdE1RIOaOp-WItuWPsOafpeeci-ebkeaOp-aVsOaNrg=="></span>
### View monitoring data through the RabbitMQ console


1. Log in to the [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq).

2. Select the region where the instance is located in the top menu bar.

3. Find the specified instance on the **Instances** page and click the instance name.

4. View monitoring data on the **Cloud Monitor** tab.

   The **Cloud Monitor** tab displays monitoring data for the past 24 hours up to the current moment by default. You can also specify a time range to view data. You can enable **Chart linkage** to view all monitored metric values at a specific moment.

   The displayed monitoring metrics include connection count, channel count, queue count, consumer count, ready message count, speed of published messages, count of delivered messages (manual), UnackDeliveryRate, storage watermark, memory watermark, and so on.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please confirm that producers and consumers are successfully connected. Otherwise, data such as consumer count and message count will show as 0.   </div>
   

<span id=".6YCa6L-H5LqR55uR5o6n5o6n5Yi25Y-w5p-l55yL55uR5o6n5pWw5o2u"></span>
### View monitoring data through the Cloud Monitor console

You can also view monitoring data through the Cloud Monitor console. The monitoring items are exactly the same as those in the RabbitMQ console.


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor).

2. Click **Cloud Service Monitor** in the left navigation bar, and select **RabbitMQ** in the **Middleware**.

   The page displays the current alarm overview, distribution of resources, and instance list. The instance list shows each instance name, status, instance message delivery, and total production consumption rate.

3. Click the instance name to enter the monitoring data page of that instance.


<span id=".55uR5o6n5oyH5qCH6K-05piO"></span>
## Monitoring metrics description

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The units in the monitoring metrics table are all base units. Please refer to the console for the specific units of each metric. The units displayed on the console adjust flexibly according to the monitoring values using a certain conversion standard. For example, the base unit of message production rate is Count/s. If the rate reaches thousands, millions, or billions per second, the console may adjust the unit to KCount/s, MCount/s, or BCount/s.</div>


<span id="9ab04a34"></span>
### Instance

Message queue for RabbitMQ supports the following monitoring metrics at the instance level.


|**Monitoring item ID** |**Monitoring item name** |**Unit** |**Description** |
|---|---|---|---|
|TotalConns |Number of connections |Count |Calculate the total number of connections in the RabbitMQ instance. |
|TotalChannels |Number of channels |Count |Count the total number of channels in the RabbitMQ instance. |
|TotalQueues |Queue count |Count |Total number of queues in the RabbitMQ instance. |
|TotalConsumers |Number of consumers |Count |Count the total number of consumers in the RabbitMQ instance. |
|TotalReadyMsgy |Number of consumable messages |Count |Total number of consumable messages in the RabbitMQ instance. |
|MsgPublishingRateh |Message production rate |Count/s |Calculate the real\-time message production rate in the RabbitMQ instance. |
|AckDeliveryRater |Message consumption rate (manual) |Count/s |Real\-time message consumption rate (manual confirmation) in the RabbitMQ instance. |
|UnackDeliveryRatek |Message consumption rate (automatic) |Count/s |Count the real\-time message consumption rate (automatic acknowledgment) in the RabbitMQ instance. |
|TotalProductionConsumptionRate |Instance production and consumption rate |Count/s |Total number of messages received and consumed per second by the instance. |
|ConnectionUsedRate |Connection usage rate |% |Usage rate of instance connections. |
|InstanceTotalPublish |Total number of messages produced |Count |The total number of messages produced by the instance. |
|InstanceTotalConsume |Total number of consumed messages |Count |Total messages consumed by the instance (auto\-ack + manual\-ack). |
|CpuUtils |Instance CPU usage |% |Average CPU usage of each instance node. |
|MemUtile |Memory usage rate |% |Calculate the maximum memory usage rate among nodes in the instance. |
|CapUtile |Disk usage rate |% |Max disk usage rate across nodes in the instance. |
|BrokerOnlineRate |Node online rate |% |The ratio of online instance nodes, calculated as `number of online instance nodes / total number of instance nodes`. |
|UnroutableMessageRate |Unroutable message rate |Count/s |Unroutable message rate, sum of Unroutable (return) and Unroutable (drop). |
|messages_in_ram_bytes |Size of messages stored in memory |Bytes |Message size stored in memory. |
|InstanceMessageUnacked |Unacknowledged message count |Count |The number of unacknowledged messages in the instance. |
|RunningStateConnection |Number of connections in running state |Count |Number of running connections in the instance. |
|FlowStateConnection |Flow status connection count |Count |The number of flow state connections in the instance. |
|BlockedStateConnection |Number of connections in Blocked state |Count |Number of connections in blocked status in the instance. |
|CloseStateConnection |Number of closed connections |Count |Number of connections in the Close state in the instance. |
|RunningStateChannel |Number of channels in the Running state |Count |The number of running state channels in the instance. |
|FlowStateChannel |Flow status channel count |Count |Number of Flow status channels in the instance. |
|BlockedStateChannel |Number of blocked state channels |Count |The number of blocked state channels in the instance. |


<span id="82f67501"></span>
### Queue

Message queue for RabbitMQ supports the following monitoring metrics at the queue level.


|**Monitoring item ID** |**Monitoring item name** |**Unit** |**Description** |
|---|---|---|---|
|QueueTPSIn |Message production rate |Count/s |The message production rate of this queue, i.e. the total messages written per second. |
|QueueTPSOut |Message consumption rate |Count/s |The message consumption rate for this queue, i.e. the number of messages consumed per second. |
|Consumers |Number of consumers |Count |Total consumers subscribed to this queue. |
|QueueTPSInAndOut |Message production and consumption rate |Count |The total rate of message production and consumption for this queue, i.e. number of messages written and consumed per second. |
|MessageReady |Number of message backlogs |Count/s |The number of messages currently available for consumption in the queue, i.e. the message backlog. |
|QueueMessageUnacked |Unacknowledged message count |Count |The number of unacknowledged messages in the queue. |
|QueueRedeliverRate |Message retransmission rate |Count/s |Message retransmission rate for this queue. |


<span id="ccf58d57"></span>
### Node

Message queue for RabbitMQ supports the following monitoring metrics at the node level.


|**Monitoring item ID** |**Monitoring item name** |**Unit** |**Description** |
|---|---|---|---|
|NodeCpuUtils |CPU usage |% |The CPU usage rate of each node is calculated as the currently used memory capacity of the node divided by the total CPU capacity of that node. |
|CapUtil |disk usage rate |% |Disk usage rate of each node, calculated as `disk space currently used by the node / total disk capacity of the node`. |
|MemUtil |Memory usage rate |% |Memory usage rate per node, calculated as `current used memory / node memory limit`. |
|NodeMemHighWater |memory high watermark |Count |Whether each node's memory has reached the high watermark. 0 indicates the high watermark is not reached; 1 indicates it is reached. |
|NodeDiskHighWater |Disk high water level |Count |Whether each node's memory has reached the high watermark. 0 indicates the high watermark is not reached; 1 indicates it is reached. |
|NodeTPSIn |Node message production rate |Count/s |The message production rate of each node, i.e. the total number of messages written per second. |
|NodeTPSOut |Node message consumption rate |Count/s |The message consumption rate of each node, i.e. the total number of messages consumed per second. |
|UsedFileDescriptors |Number of file descriptors used |Count |The number of file descriptors used by each node. |
|UsedSockets |Number of connections |Count |Number of connections per node. |
|NodeQueues |Queue count |Count |Number of queues per node. |
|NodeMessageReady |Accumulated message volume |Count |The current number of consumable messages at each node. |
|NodeMessageUnacked |Unacknowledged message count |Count |Number of unacknowledged messages on each node. |
|NodeMessageBytesInRam |Message size in memory |Bytes |Message size in each node's memory. |
|DiskReadCostTime |Average disk read time |ms |Average disk read operation time across nodes. |
|DiskWriteCostTime |Average disk write time |ms |Average disk write time per node. |


<span id="7c31c382"></span>
### Vhost

Message queue for RabbitMQ supports the following monitoring metrics at the Vhost level.


|**Monitoring item ID** |**Monitoring item name** |**Unit** |**Description** |
|---|---|---|---|
|VhostTPSIn |Vhost message production rate |Count/s |The message production rate of each Vhost, i.e. the total number of messages written per second. |
|VhostTPSOut |Vhost message consumption rate |Count/s |Message consumption rate per Vhost, i.e. the total number of messages consumed per second. |
|InstanceVhostConsumers |Vhost consumer count |Count |Number of consumers for each Vhost. |
|VhostTotalPublish |Total number of messages produced |Count |Total number of produced messages for each Vhost. |
|VhostTotalConsume |Total number of consumed messages |Count |Total number of consumed messages for each Vhost. |
