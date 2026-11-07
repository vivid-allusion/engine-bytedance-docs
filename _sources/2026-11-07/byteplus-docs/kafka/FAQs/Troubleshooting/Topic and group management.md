---
title: "Topic and group management"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/topic-group-management-FAQ"
---

This topic provides answers to frequently asked questions (FAQs) related to topic and group management in Message Queue for Kafka.

<span id="7cf8b7f2"></span>
## Why are there more groups in the group list than I created?

When you view the group list of a specified instance in the Message Queue for Kafka console or by calling API actions, you find more groups than you created. This indicates that some groups are not created manually. This issue is caused by the following reasons:


* The flexible group creation feature is enabled, so Message Queue for Kafka automatically creates some groups. After this feature is enabled, you can directly specify a group ID that meets the naming rules in the consumer SDK for message consumption. The specified group can be displayed in the group list of your instance.

* A connector is created and started. After the connector is started, Message Queue for Kafka automatically creates a consumer group for the specified instance to consume messages from the specified topic. The name of this group is prefixed with `connect-task` and is displayed in the group list of the corresponding instance.

* You have committed a consumer offset by using the `Assign` method. This also leads to the creation of a corresponding group in the Kafka cluster.


<span id="c3878ab6"></span>
## Why is my group automatically deleted?

Message Queue for Kafka supports the automatic group deletion (**auto.delete.group**) feature. You can specify whether to allow the back\-end service to automatically delete consumer groups that are in the Empty state. After this feature is enabled, if all consumers in a consumer group are in the Empty state, the consumer group is automatically deleted after the consumer offset retention period expires. After this feature is disabled, the automatic deletion of data related to the message consumption progress does not affect the status of consumer groups, and the system does not automatically delete groups in the Empty state.

After a group is automatically deleted, you can view the setting of the **Automatically Delete Groups** parameter in the instance parameter settings to see if the feature is enabled. For more information on how to configure parameters, refer to [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter).

<span id="25bc29df"></span>
## Why am I unable to delete my group?

If no consumers are consuming messages in a consumer group, the group status is displayed as Empty. Only groups in the Empty state can be deleted. Before you delete a group, verify that it is in the Empty state.

<span id="a0e5eb13"></span>
## Why am I unable to view the message accumulation of a group, or why is the number of accumulated messages displayed as 0?

When you view the consumption status of a group, although the current and maximum consumer offsets are inconsistent, no message accumulation data is displayed or the number of accumulated messages is displayed as 0. This issue is caused by the following reasons:


* The client has never committed a consumer offset, or the consumer offset committed by the client has expired.

* The client has committed a consumer offset and it has not expired. However, some messages have been deleted due to expiration. As a result, the current consumer offset is less than or equal to the minimum offset.


<span id="26989730"></span>
## Why is the message storage time displayed as 1970?

When you query messages based on a consumer offset, the storage time of some messages may be displayed as 1970.

This issue is caused by the following reasons:

The client version is outdated. We recommend that you upgrade the client version to version 0.10.2 or later.

Null is passed in by the client as the timestamp (CreateTime). The client must pass in a correct timestamp or choose to use the time when the message was written to the disk of the Kafka instance.

<span id="4b761431"></span>
## Why are messages unevenly distributed among the partitions of a topic?

The number of messages stored in each partition is displayed on the topic details page. When a producer sends messages to a specified topic, messages are unevenly distributed among different partitions of the topic. You may find a large number of messages in some partitions and a small number of messages in others.

This issue is caused by the following reasons:


* A partition is specified for the producer to send messages. In this case, messages are sent only to the specified partition. As a result, messages are not stored in unspecified partitions.

* A message key is specified for the producer to send messages. In this case, messages are stored in the corresponding partition based on the message key.

* An additional partition assignment policy for messages is defined in the message consumption logic. As a result, messages are unevenly distributed among partitions. We recommend that you troubleshoot the relevant message consumption logic.


<span id="c7fd44c8"></span>
## Why is no topic subscription relationship displayed for a group?


* Issue description:

   Consumers in a group have started consuming messages. However, you can neither view the topics subscribed to by that group nor view the corresponding consumption status in the Message Queue for Kafka console. The issue is manifested as follows:

   * In the **Overview Statistics** area of the group details page, 0 is displayed in the **Subscribe to Topics** column.

   * In the **Consumption status** area of the group details page, no data is displayed in the **Topic** column.

* Possible causes:

   * The client configurations are incorrect. We recommend that you verify the Kafka client configurations related to message subscription.

   * A network exception occurs on the client side. As a result, the client fails to connect to the Kafka instance. To determine whether the Kafka instance can be connected, run the ping or telnet command to test its connectivity.

   * The client has not committed a consumer offset. This issue can also be caused if the client is configured by using the `Assign` method to subscribe to messages in specific topic partitions for the consumer but has not committed any consumer offset.
