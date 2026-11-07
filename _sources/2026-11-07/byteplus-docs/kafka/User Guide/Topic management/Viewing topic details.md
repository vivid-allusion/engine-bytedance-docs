---
title: "Viewing topic details"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/viewing-topic-details"
---

Once a topic is created, you can view detailed information about the topic and its partitions at any time in the console, including topic details, partition information, and consumer connection information.

<span id="前提条件"></span>
## Before you begin

Create a Message Queue for Kafka instance. For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance).

<span id="操作步骤"></span>
## Viewing topic details

To view the details of a topic:


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. Click the **Topic Management** tab.

5. Locate the target topic to view its basic information.

   For numerous topics, we recommend that you search by topic name on the upper\-right corner. The topic list displays the topic name, current status, partition count, replica count, message retention period, description, and creation time.

6. Click the topic name to see detailed information about all partitions in the topic.


<span id="db8894c3"></span>
## Data description

<span id="9615eeb4"></span>
### Topic details

The **Topic Details** tab displays basic information and parameter configurations for the topic. To modify the parameter configurations of the topic, click **Modify** in the **Parameter configuration** pane.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The actual effective <strong>Message Retention Period</strong> and other configurations are determined by the parameter configurations of each topic. Instance\-level parameter configurations determine the default parameter values of the instance. This means that topics created after instance configuration modification use these default values.</div>



|Pane |Item |**Description** |
|---|---|---|
|Basic information |Topic name |The name of a topic. |
||Describe |A brief description of the topic. |
||Create Time |The time when the topic is created. |
|Parameter configuration |No. of Partitions |The number of partitions in the topic. |
||No. of replicas |The number of replicas for a topic partition. Data is backed up on the specified number of replicas. |
||Minimum number of synchronous replicas |The minimum number of in\-sync replicas for the topic. A larger value improves data reliability but reduces availability. |
||Message Retention Period |The maximum retention period of messages in the topic. Consumers must consume messages before this time ends. Otherwise, messages are deleted. Deleted messages cannot be consumed. |
||Maximum Message Size |The maximum message size in this topic. |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26a938fe4ba74ca288ee23499ad9f4f2~tplv-goo7wpa0wc-image.image) </span>

<span id="7e1c1177"></span>
### Partition information

The **Partition information** tab displays detailed information about all partitions of this topic. You can search for a partition by partition number.


|Item |Description |
|---|---|
|Partition number |The partition number. |
|Leader |The leader handles all read and write requests for the partition, and followers regularly replicate data from the leader. |
|Replica |The list of replicas. |
|ISR |The in\-sync replica that has the latest messages. |
|Unsynchronized replicas |The number of non\-in\-sync replicas. You can filter partitions with non\-in\-sync replicas. |
|Start offset |The start position where messages are written. |
|End offset |The end position where messages are written. |
|No. of stored messages |The number of messages stored in this partition. |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef030fff8b9542ddb252bf9b3672ed1c~tplv-goo7wpa0wc-image.image) </span>

<span id="71cdfb23"></span>
### Consumer connection information

The **Consumer connection information** tab displays connection information about all groups that consume the current topic. You can filter groups by group ID.


|Item |Description |
|---|---|
|Group ID |The ID of the group that consumes this topic. |
|State |The status of this group. For more information on status description, refer to [Viewing consumption status in a group](https://docs.byteplus.com/en/docs/kafka/Viewing-consumption-status). |
|Protocol Type |The consumption protocol type specified for the consumer group.<br><br><br>* If the standard Kafka consumption protocol is used, it appears as consumer.<br><br>* For other protocol types, the respective protocol name is displayed, for example, connect for Kafka\-Connector access.<br><br>* If a custom partition consumption method is used, this field may be empty. |
|Equalization algorithm |The algorithm for distributing partitions among consumers, as specified by the consumer client. If a custom partition consumption method is used, this field may be empty. |
