---
title: "Viewing monitoring data"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/viewing-monitoring-data"
---

Message Queue for Kafka is integrated with Cloud Monitor. During the daily operation of instances, you can view various metrics in the Message Queue for Kafka console or the VCM console, facilitating real\-time analysis of instance statuses. This topic introduces how to view Message Queue for Kafka monitoring data and describes metrics.

<span id="前提条件"></span>
## Prerequisites

Before viewing monitoring data, create a Message Queue for Kafka instance.

<span id="通过 Kafka 控制台查看监控数据"></span>
## Viewing monitoring data in the Kafka console


1. Log into [BytePlus Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Project and Region where the desired instance resides.

3. On the **Instances** page, locate the desired instance and click its name.

4. On the **Vitality Cloud Monitor** tab, view the monitoring data.

   The **Vitality Cloud Monitor** tab displays monitoring data within the last day up to the current moment by default. You can specify a time period to view the data. Additionally, you can enable **chart linkage** to view the data values for all metrics at a specific moment.

   The page displays metrics such as the message production traffic rate, message consumption traffic rate, and disk utilization of the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Make sure that producers and consumers are working properly. Otherwise, data such as consumer count and message count are displayed as 0.   </div>
   

<span id="通过云监控控制台查看监控数据"></span>
## Viewing monitoring data in the Cloud Monitor console

You can also view monitoring data in the CloudMonitor console. The metrics are the same as those in the Kafka console.


1. Log into [BytePlus Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left\-side navigation pane, click **Cloud Service Monitor**, find the **Middleware** pane, and select **Message Queue for Kafka**.

   The page displays the current alarm overview, resource quantity distribution, and an instance list. The instance list displays the status, topic count, consumer group count, message production traffic rate, and message consumption traffic rate of each instance.

3. Click the desired instance name to go to the **Monitor** page of the instance.


<span id="监控指标说明"></span>
## Monitoring metrics

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">All units in the metric tables are basic units. Specific units for metrics in the console prevail. Units displayed in the console are flexibly adjusted based on metric values and certain conversion standards. For example, the basic unit of the message production traffic rate is Byte/s, but if the value reaches KiB, MiB, or GiB per second, the console displays the unit as KiB/s, MiB/s, or GiB/s, respectively.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Data dump</strong> and <strong>data dump \- task</strong> metrics are used to monitor Kafka Connector; <strong>data sync</strong> metric is used to monitor Kafka synchronization function. The above three metrics are currently in beta status, and you can contact our technical support to request allowlist permission as needed.</div>



<span id="实例"></span>
### Instance

Message Queue for Kafka supports the following instance metrics.


|**Metric ID** |**Metric Name** |**Unit** |**Description** |
|---|---|---|---|
|CpuUtil |CpuUtil |% |The maximum CPU utilization among all brokers in the instance. |
|MemUtil |MemUtil |% |The maximum memory utilization among all brokers in the instance. |
|CapUtil |disk cap usage |% |The overall disk utilization of the instance. |
|MaxDiskUtil |max disk usage |% |The maximum disk utilization among all brokers in the instance at the current moment. |
|DiskSkewness |DiskSkewness |% |The uneven distribution of data across disks. The calculation method is (MaxBrokerCap \- MinBrokerCap) / MaxBrokerCap. |
|TopicDataSizeTop10 |TopicDataSizeTop10 |Count |Top 10 topics by disk usage in the instance. |
|MsgProductionRate |message producer rate |Bytes/s |The volume of data written to the instance per second. |
|MsgConsumptionRate |message consumer rate |Bytes/s |The volume of data read from the instance per second. |
|ConnectionsPerIP |IPConnectionsTop5 |Count |The top 5 client IP addresses by connection count in the instance. |
|ProductionRatePercent |ProductionRatePercent |% |The network bandwidth utilization rate for message production in the instance. The calculation method is ProduceRate / SpecBandwidth. |
|ConsumptionRatePercent |ConsumptionRatePercent |% |The network bandwidth utilization rate for message consumption in the instance. The calculation method is ConsumeRate / SpecBandwidth. |
|ReqProductionCount |ReqProductionCount |Count |The number of message production requests in the instance. |
|MsgProductionCount |MsgProdcutionCount |Count |The total number of messages produced in the instance. |
|ReqConsumptionCount |ReqProductionCount |Count |The number of message consumption requests in the instance. |
|ProductionRequestMeanTime |ProductionRequestMeanTime |μs |The average duration of message production requests in the instance. |
|ConsumptionRequestMeanTime |ConsumptionRequestMeanTime |μs |The average duration of message consumption requests in the instance. |
|ProductionRequestP99Time |ProductionRequestP99Time |μs |The P99 duration of message production requests in the instance. |
|ConsumptionRequestP99Time |ConsumptionRequestP99Time |μs |The P99 duration of message consumption requests in the instance. |
|ConnectionsCount |ConnectionsCount |Count |The total number of TCP connections between clients and the Kafka instance. |
|BrokerOnlineRate |BrokerOnlineRate |% |The percentage of brokers in normal status in the instance. |


<span id="9b2a0ee5"></span>
### Broker

Message Queue for Kafka supports the following broker metrics.


|**Metric ID** |**Metric Name** |**Unit** |**Description** |
|---|---|---|---|
|CpuUtil |CpuUtil |% |The CPU utilization of the broker. |
|MemUtil |MemUtil |% |The memory utilization of the broker. |
|DiskUtil |DiskUtil |% |The disk utilization of the broker. |
|MsgProductionRate |MsgProductionRate |Bytes/s |The volume of data written to the broker per second. |
|MsgConsumptionRate |MsgConsumptionRate |Bytes/s |The volume of data read from the broker per second. |
|ProductionRequestMeanTime |ProduceRequestMeanTime |μs |The average duration of message production requests in the broker. |
|ConsumptionRequestMeanTime |ConsumptionRequestMeanTime |μs |The average duration of message consumption requests in the broker. |
|ProductionRequestP99Time |ProductionRequestP99Time |μs |The P99 duration of message production requests in the broker. |
|ConsumptionRequestP99Time |ConsumptionRequestP99Time |μs |The P99 duration of message consumption requests in the broker. |
|ConnectionsCount |ConnectionsCount |Count |The number of TCP connections between clients and a specific broker. |


<span id="主题"></span>
### Topic

Message Queue for Kafka supports the following topic metrics.


|**Metric ID** |**Metric Name** |**Unit** |**Description** |
|---|---|---|---|
|MsgProductionRate |message producer rate |Byte/s |The message production traffic in the topic. |
|MsgConsumptionRate |message consumer rate |Byte/s |The message consumption traffic in the topic. |
|ReqProductionCount |ReqProductionCount |Count |The number of message production requests in the topic. |
|MsgProductionCount |MsgProductionCount |Count |The total number of messages produced in the topic. |
|ReqConsumptionCount |ReqConsumptionCount |Count |The number of message consumption requests in the topic, including replica synchronization requests. |
|TopicDataSize |TopicDataSize |Bytes |The size of data in the topic, including all replicas. |


<span id="消费组"></span>
### Consumer group

Message Queue for Kafka supports the following monitoring metrics for consumer group.


|**Metric ID** |**Metric Name** |**Unit** |**Description** |
|---|---|---|---|
|GroupConsumptionRate |Group consumption rate |Count |The number of messages consumed by the consumer group per minute. |
|GroupMsgAccum |Group message accumulation |Count |The total number of messages that haven't been consumed by the specified consumer group. If the message accumulation becomes too large, messages may be lost. |
|GroupRebalanceCount |Number of group rebalancing |Count |The number of group rebalancing per minute. |


<span id="消费组主题"></span>
### Consumer group \- topic

Message Queue for Kafka supports the following monitoring metrics for consumer group topic.


|**Metric ID** |**Metric Name** |**Unit** |**Description** |
|---|---|---|---|
|TopicConsumptionRate |Topic consumption rate |Count |The number of messages in each subscribed topic consumed by a specified consumer group per minute. |
|TopicMsgAccum |Topic message accumulation |Count |The number of messages in each subscribed topic that haven't been consumed by a specified consumer group per minute.<br><br>This metric is only for visualization use. If you want to set alarms based on this metric, we recommend that you use the **Partition Message Accumulation** metric of **Partition Accumulation** instead. |


<span id="7cb77a2d"></span>
### Data dump

Message Queue for Kafka supports the following monitoring metrics for data dumping.


|**Metric ID** |**Metric Name** |**Unit** |**Description** |
|---|---|---|---|
|TotalTaskCount |Total number of dump tasks |Count |Total number of Connector tasks created. |
|TotalSubTaskCount |Total number of dump subtasks |Count |Total number of Connector subtasks created. |


<span id="432bd994"></span>
### Data dump \- task

Message Queue for Kafka supports the following monitoring metrics for data dump task.


|**Metric ID** |**Metric Name** |**Unit** |**Description** |
|---|---|---|---|
|ConnectorTaskStatus |Task status |Count |Status of the specified Connector task.<br><br><br>* 1: Running<br><br>* 2: Paused<br><br>* 3: Error |
|ConnectorSubTaskStatus |Subtask status |Count |Status of each subtask in the specified Connector task.<br><br><br>* 1: Running<br><br>* 2: Paused<br><br>* 3: Error |
|MsgReadRate |Read rate |Count/s |Rate at which each Connector subtask reads messages from the data source. |
|MsgWriteRate |Write rate |Count/s |Rate at which each Connector subtask sends messages to the destination. |
|MsgAccumCount |Number of retained messages |Count |Number of messages that have been read by each Connector subtask but haven't yet been sent. |


<span id="10dc6c5e"></span>
### Data synchronization

Message Queue for Kafka supports the following monitoring metrics for data synchronization.


|**Metric ID** |**Metric Name** |**Unit** |**Description** |
|---|---|---|---|
|DataSyncTaskStatus |Task status |Count |Status of the specified data sync task.<br><br><br>* 1: Running<br><br>* 2: Paused<br><br>* 3: Error |
|DataSyncSubTaskStatus |Subtask status |Count |Status of each subtask in the specified data sync task.<br><br><br>* 1: Running<br><br>* 2: Paused<br><br>* 3: Error |
|DataSyncMsgReadRate |Read rate |Count/s |Rate at which each data sync subtask reads messages from the data source. |
|DataSyncMsgWriteRate |Write rate |Count/s |Rate at which each data sync subtask sends messages to the destination. |
|DataSyncMsgAccumCount |Number of retained messages |Count |Number of messages that have been read by each data sync subtask but haven't yet been sent. |


<span id="f6a346f2"></span>
### Topic \- TopN

It displays TopN information for traffic and storage at topic level, including message production rate, number of messages produced, number of production events, and topic data size.


* Different time periods can be specified to view corresponding TopN information for that period.

* The top 20 topics are displayed by default, and ascending and descending order based on different metrics are supported.


<span id="dcc4dece"></span>
### Consumer group \- TopN

It displays TopN information for message accumulation at consumer group level.


* Different time periods can be specified to view corresponding TopN information for that period.

* The top 20 topics are displayed by default, and ascending and descending order based on different metrics are supported.
