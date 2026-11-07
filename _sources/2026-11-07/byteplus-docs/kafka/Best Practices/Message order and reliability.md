---
title: "Message order and reliability"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/message-order-reliability"
---

It is necessary to focus on the order and reliability of messages when they are sent to and received by a Message Queue for Kafka instance. This topic introduces the recommended methods for achieving the message order and ensuring message reliability.

<span id="1d5917ce"></span>
## Message order

As for a Message Queue for Kafka instance, messages stored in a single partition follow the First\-In\-First\-Out (FIFO) principle. That is, if message A is written before message B to the same partition, the client always reads message A before message B. However, ordered messages within a partition of the instance only guarantee the order of messages sent by the same producer. For messages sent by different producers, their arrival order at the Kafka instance is not confirmed, so the message sending and receiving order cannot be guaranteed.

Messages are ordered in a partition of a Message Queue for Kafka instance. To ensure that messages are globally ordered, the following methods are recommended.


|Method |Description |
|---|---|
|Globally ordered messages |A topic with only one partition is created. In this case, the Kafka instance receives messages strictly in the order in which they are sent from the producer client.<br><br>A single topic with only one partition underutilizes the capabilities of a Kafka cluster during message writing and reading. To fully utilize the capabilities, multiple topics, each with one partition, must be used together. |
|Ordered messages in a partition |Messages are ordered in each partition of a Message Queue for Kafka instance. You can also ensure the message order by writing messages to the same partition in the desired order. This method is suitable for scenarios in which not all messages must be sent and received in order.<br><br><br>* The order in which messages are read can be guaranteed by specifying the same serial number of a partition to which messages are sent.<br><br>* For an official Confluent producer client, messages can be sent to the same partition by specifying the same message key for them. However, the partition number calculated from the message key also varies in scenarios with changing partitions of a topic, such as partition scale\-out. |


<span id="6f2f62a8"></span>
## Message reliability

Message reliability is affected by both client and Kafka instance configurations. To guarantee the security, reliability, and no loss of messages, the client and Kafka instance configurations must match each other.

<span id="b5728d79"></span>
### Configurations of a Kafka instance

Message Queue for Kafka allows you to improve the data storage reliability by specifying the following parameters.


|Parameter |Description |
|---|---|
|replicas |The number of replicas for storing messages written to the topic. Both 2 replicas and 3 replicas are supported. The latter is more reliable but consumes additional storage resources. |
|Minimum number of synchronous replicas |Message writing is allowed only when the specified number of replicas is available in the topic. The specified value of this parameter must be less than or equal to the number of replicas in the topic. The minimum number of in\-sync replicas must be 2 if the topic contains 3 replicas. A writing success response is returned to the client only when messages are written to at least 2 replicas. This reduces the availability to some extent while improving the data reliability. |


<span id="1343f041"></span>
### Kafka producer client

Message Queue for Kafka is fully compatible with an Apache Kafka client for message sending. The following are data reliability parameters supported by an Apache Kafka producer client of version 2.2 or later.


|Parameter |Description |
|---|---|
|acks |The stringency for message writing success. This parameter can be set to 0, 1, \-1, or all. The semantics represented by \-1 and all are the same.<br><br><br>* The value `0` indicates that the client requires no writing response from the Kafka instance. This configuration exhibits high performance and high risks of data loss.<br><br>* The value `1` indicates that a writing success is deemed when the messages are written to the primary replica. In this case, the Kafka instance returns a writing success response to the client. This configuration exhibits common performance and certain risks of data loss when the primary node fails.<br><br>* The value `-1` or all indicates that a writing success is deemed when the messages are written to all in\-sync replicas. In this case, the Kafka instance returns a writing success response to the client. If the messages fail to be written to any in\-sync replica, the Kafka instance returns a writing failure response to the client. This configuration exhibits poor performance but has low risks of data security. Data loss occurs only when the primary and secondary nodes fail at the same time. |
|max.in.flight.requests.per.connection |The maximum number of requests sent at the same time. This parameter can be set to 1 or more. If a value greater than 1 is set, messages cannot be sent in order even if they are from the same producer because message sending retries usually occur after sending failures. |
|retries |The number of retries after a message sending failure. This parameter can be set to 0, 1, or more. By default, unlimited retries are allowed for an Apache Kafka Java client. |
|enable.idempotence |The message idempotency. If this feature is enabled, the message idempotency is guaranteed by the producer client. |


<span id="4f142b1f"></span>
### Kafka consumer client

By specifying the preceding Kafka instance and client parameters, you can ensure the data reliability during message sending and storage to the maximum extent. As for the consumer client, the client must correctly process the messages that are read. For this purpose, you can specify the following parameters for the consumer client as needed.


|Parameter |Description |
|---|---|
|enable.auto.commit |Whether to enable the automatic commit feature. We recommend that you disable this feature to ensure that consumer offsets are committed after message processing. |
|auto.offset.reset |The policy for initializing the consumer offset if no valid consumption records are available in a consumer group. By default, this parameter is set to **latest**. The following options are supported:<br><br><br>* **earliest**: reads from the earliest message in a topic.<br><br>* **latest**: reads form the latest message in a topic.<br><br>* **none**: throws an error. |
