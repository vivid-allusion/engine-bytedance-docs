---
title: "Best practices for producers"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/best-practices-for-producers"
---

This topic uses the official Confluent SDK for Java as an example to introduce suggestions for using Kafka producers and consumers. We recommend that you read the following suggestions before using a Message Queue for Kafka instance for message production and consumption. These suggestions help improve the access efficiency and service stability.

<span id="b4610999"></span>
## Message order

In a BytePlus Kafka instance, messages stored in a single partition follow the First\-In\-First\-Out (FIFO) principle. That is, if message A is written before message B to the same partition, the client always reads message A before message B. Note that only the order of messages sent by the same producer can be guaranteed. For messages sent by different producers, their arrival order at the Kafka instance is not confirmed so that the message sending and receiving order cannot be guaranteed.

Based on these characteristics, you can use one of the following methods to guarantee the message order.


* **Globally ordered messages:**  A topic with only one partition is created. In this case, messages are received strictly in the order in which they are sent from the producer client. However, a single topic with only one partition underutilizes the capabilities of a Kafka cluster during message writing and reading. To fully utilize the capabilities, multiple topics, each with one partition, must be used together.

* **Ordered messages in a partition:**  Messages are ordered in each partition of a Message Queue for Kafka instance. You can also ensure the message order by writing messages to the same partition in the desired order. This method is suitable for scenarios in which not all messages or the specific type of messages must be in order.


The message production and consumption performance is greatly restricted in a topic with one partition. We recommend that you select ordered messages in a partition to implement the business logic in practice. This way, messages that must be ordered can be written to the same partition to ensure the ordering of messages of the same type.

<span id="6894cd84"></span>
## Message reliability

The acks parameter defines the acknowledgement method for written messages. The following three configurations are supported:


* `acks=0`: The message writing result is not concerned. The Kafka instance returns no result regardless of whether a message is successfully written.

* `acks=1`: The Kafka instance returns the writing result to the producer client immediately after a message is written to the primary replica.

* `acks=-1` or `acks=all`: The Kafka instance returns the writing result to the producer client only after a message is written to both the primary and secondary replicas.


The three configurations for the acks parameter exhibit descending message sending performance and ascending data reliability from top down. We recommend that you select the configuration with the highest data reliability.

For distributed systems, message sending failures may occur occasionally due to issues related to the network or switching of the primary node. You can specify the number of retries after a writing failure using the `retries` parameter. The default number of retries is set to the maximum value of a long integer. You can also specify a retry interval using the `retry.backoff.ms` parameter. The default retry interval is 100 ms. The recommend configurations are 3 for the number of retries and 1,000 ms for the retry interval.

<span id="01159483"></span>
## Partition selection

When writing messages, a destination partition in a topic is selected. The partition selection logic is described below:


* If a message key is specified, the partition is selected based on the hash result of the message key. Messages with identical message keys are assigned with the same partition number. Therefore, if the same message key is specified for a batch of messages, they can be ordered in the partition. However, note that the partition number selected by the message key may change if partitions are added to the corresponding topic.

* For a Kafka client earlier than version 2.4, if no message key is specified, messages are written to each partition using the round robin method. This method can lead to an unsatisfactory message aggregation effect on the client and affect the message sending performance.

* For a Kafka client of version 2.4 or later, if no message key is specified, messages are written to partitions using the sticky partition selection method. This method mainly resolves the issue of unsatisfactory message aggregation effect. In terms of partition selection, messages are written to the last partition in priority. Message writing continues until the upper limit of message aggregation, namely the specified value of the batch.size parameter, for that partition is reached on the client. In the long run, this achieves message writing balance among partitions while ensuring the message aggregation effect.

* In addition to the default logic mentioned above, you can customize the partition selection logic.


We recommend that you use the default one. If no message key is used, the default logic itself ensures the balance of messages among partitions. If a message key is used, messages can be effectively distributed by reducing the hash conflict of the message key. This avoids too much traffic and too many messages in some partitions. For custom partition selection, the balance among the selected partitions must also be ensured as far as possible to avoid excessive concentration of traffic and messages in some partitions.

<span id="d70c4d35"></span>
## Message sending result

Currently, the asynchronous message sending logic is used for producers. That is, when messages are written using the send() method, they are actually written to the local cache and not sent to the Kafka instance. These messages are aggregated in the local cache based on partitions. Then, aggregated messages are scanned by an asynchronous sending thread and sent to the Kafka instance.


* Using the send() method aims at writing messages to the cache and does not mean a message writing success. To get the actual message writing result, you can use the following methods:

* Associate a callback function with each message when using the send() method.

* Specify the `interceptor.classes` parameter for the producer to inject a custom interceptor for implementing the `ProducerInterceptor` API action. This interceptor transmits the message writing result or exception by using the `onAcknowledgement` method.

* A `Future` object is returned when the send() method is used. You can directly call the `get` method for this object to block and wait for the writing result of messages.


We recommend that you use any of the first two methods. Actually, the third one is a pseudo\-synchronization method that seriously affects the message production performance of the client. This method is not recommended.

<span id="cdbc6b20"></span>
## Message production performance

The producer aggregates messages in the memory cache to reduce network requests to the Kafka instance. As a result, the throughput is greatly improved. For the message aggregation capabilities of the producer client, you can customize the following parameters:


* The batch.size parameter defines the maximum message size for a single aggregation. The default value is 16 KB. Small values are not recommended. An excessively high production request rate of the Kafka instance can result in high CPU usage of the Kafka instance. In this case, increase the value of this parameter appropriately to improve the message aggregation capabilities and reduce CPU usage.

* The linger.ms parameter defines the minimum period for a single aggregation. The default value is 0 ms, meaning that messages are sent as soon as possible. Appropriate adjustments to this parameter can improve the message aggregation effect. but relatively prolong the latency in sending messages. In the case of poor message aggregation and dramatic growth in producer requests, you can increase this parameter appropriately. This way, proper balance can be reached between the message aggregation effect and the acceptable latency in sending messages.

* The send.buffer.bytes parameter defines the size of the TCP send buffer. The default value is 128 KB. This parameter must be adjusted if the size of a single message sent from the client is large or the batch.size parameter has been adjusted to a larger value. The recommended value for this parameter is between 128 KB and 1,024 KB.


<span id="3ca8db17"></span>
## Message timestamp

Message timestamps can be populated using two methods, depending on the configurations of Kafka instance clusters. For more information, refer to [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter).


* LogAppendTime: The time when a message is written to the Kafka instance is used as the message timestamp.

* CreateTime: The time when a message is created by the producer, namely the built\-in timestamp for message writing. This method is used by default.


Message timestamps are used to calculate and determine the expiration, aging, and other statuses of messages. Messages sent from the client must have proper timestamps. Any population error of message timestamps can lead to the failure in deleting aged messages as scheduled. Once a message is written, its timestamp can be verified by querying the consumer offset. Generally, the issue of no message timestamp is found in APIs of earlier versions. Use the recommended client versions.

If no message timestamp is specified for a default Confluent SDK, the local time at the producer location is populated. If you want to specify a timestamp, fill it in the correct format to avoid affecting the aging of messages in the Kafka instance.

<span id="31b3975b"></span>
## Use of multiple threads

Producers are thread\-safe. Therefore, the use of a producer pool is recommended for clients. In this mode, producers are used in diversified multiple threads, avoiding the creation of a separate producer for each message production task.

<span id="eae4f2fa"></span>
## Graceful exit

The asynchronous sending mode is used for producers. We recommend that you call the `flush` method to push the cached messages to the Kafka instance, then call the `close` method to close the producer client before the scheduled close. Otherwise, some cached messages may not be released before the close, resulting in message loss.

<span id="1b519b56"></span>
## Domain name resolution (DNS)

BytePlus Kafka instances are deployed in distributed clusters. The initial endpoint is offered using a domain name. When a client uses a domain name for access, we recommend that you set the DNS of the client to all IP address resolution, namely `client.dns.lookup = use_all_dns_ips`. This ensures that the client can still be used normally when a back\-end node changes in the distributed cluster.
