---
title: "Best practices for consumers"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/best-practices-for-consumers"
---

This topic describes the best practices for consumers of BytePlus Kafka instances. The official Confluent client SDK for Java is used as an example.

<span id="8f532d39"></span>
## Broadcasting and unicasting

In a consumer group, each message is expected to be consumed only once by a consumer in the group. Therefore, unicast message consumption is achieved among different consumers in the same consumer group.

Among different consumer groups, each message is expected to be consumed once by a consumer in each consumer group. Therefore, broadcast message consumption is achieved among different consumers in different consumer groups.

<span id="922973e8"></span>
## Idempotency

From the Kafka instance's perspective, whether a message is consumed by the client is only related to the consumer offset stored on the Kafka instance. Consumer offsets are recorded on the Kafka instance through relevant API actions called by consumers. Therefore, in the rebalancing process caused by client startup or stop, consumer offsets may not be promptly synchronized to the Kafka instance.

As a result, it cannot ensure that a message is consumed only once even among different consumers in the same consumer group. To realize full idempotency among consumers, you can add an identification field to a message for secondary verification after the message is consumed.

<span id="237519fa"></span>
## Message consumption

A topic can be specified for consumers using the following methods:


* Subscribe: This is the standard method used by consumers. A complete consumer subscription model is encapsulated on the client, including the partition assignment for each consumer and rebalancing when consumers join or leave.

* Assign: The business side specifies the partition information consumed by consumers and coordinates consumption among different consumers.


We recommend that you use the Subscribe method.

<span id="fe2f8510"></span>
## Consumption model

Consumers use a pull model to read messages. Ensure that the pulling threads neither exit unexpectedly nor get blocked. Otherwise, consumption requests cannot be initiated properly.

Almost all consumer requests are sent and responded based on the calls of the `poll` method.

If messages are consumed on the client by using the Subscribe method, the `poll` method must be called within a fixed period during use. At most, this period cannot exceed the value of the `max.poll.interval.ms` parameter, which defaults to 300,000 ms. This parameter defines the maximum time interval between two calls of the `poll` method. Exceeding the maximum time interval causes the Kafka instance to determine a consumer as abnormal and thus remove it from the consumer group. An excessively long time interval also affects the rebalancing of the consumer group, resulting in extended periods of message consumption lagging.

<span id="be1b9a42"></span>
## Rebalancing

When messages are consumed on the client by using the Subscribe method, a consumer group may transition among the following states within its lifecycle.


* PreparingRebalance: The consumer group is reassigning partitions.

* CompletingRebalance: The consumer group completes the computing for partition reassignment and waits for all assignment results to be delivered to the specified consumers.

* Stable: After the assignment results are synchronized to all consumers, the consumer group enters this state and starts consumption.

* Empty: No active consumers and message consumption in progress exists in the consumer group.


Generally, a normal consumer group is expected to maintain in the `Stable` status for normal message consumption.

When new consumers join or existing consumers exit or fail in a subscribed consumer group, a rebalancing action is triggered in the group. The consumer group enters the `PreparingRebalance` state and waits for all current consumers to join the group again. When all rebalancing actions are triggered, the consumer group performs computing again for partition reassignment and enters the `CompletingRebalance` state. When each consumer gets its own partition, the consumer group enters the `Stable` state for normal message consumption.

It can be seen that two interactions with consumers are required in the rebalancing logic. However, the processing of all consumer requests must be triggered by calling the `poll` method. Therefore, blocking the calling of the `poll` method can easily cause extended periods of lagging or even timeout in rebalancing tasks of consumer groups.

We recommend that you guarantee the time interval between two consumer calls of the `poll` method not exceeding 10 seconds. In scenarios where messages are processed slowly on the downstream side, consider increasing the downstream processing rate or using the asynchronous message processing method.

In addition, note that the consumer group always maintains in the `Empty` state if messages are consumed by using the Assign method.

<span id="28f98ee3"></span>
## Consumer offset commit

The default commit mode on the client is periodic automatic commit, depending on the following configurations:


* The enable.auto.commit parameter defines whether to enable automatic commits. The default value is true.

* The auto.commit.interval.ms parameter defines the time interval for automatic commits. The default value is 5,000 ms.


We recommend that you disable automatic commits in practice and allow the business side to commit consumer offsets by calling the `commitAsync` method after message processing. This helps avoid issues with automatic commits that prevent retries in case of message processing failures. In addition, note that the business side cannot call the commit method too frequently. We recommend committing once after a batch of messages is processed, with a commit interval of every 5 seconds.

<span id="0d7ff58e"></span>
## Message consumption performance

The number of consumers that can consume messages concurrently in a consumer group is related to the number of partitions in the consumed topic and cannot exceed the number of partitions. Therefore, when messages are accumulated in a consumer group, you can use one of the following methods:


* If the number of consumers is less than the number of partitions, try to improve the message consumption performance by adding consumers to the consumer group.

* If the number of consumers is equal to the number of partitions, scale out partitions in the topic, then try to add consumers. Note that scaling out partitions may disrupt the original ordered messages in the partitions.

* If the consumer traffic is large, you can also modify the `receive.buffer.bytes` parameter to adjust the size of the TCP receive buffer. The default value is 64 KB. We recommend that you modify it to 1 MB.


<span id="de6393ba"></span>
## Use of multiple threads

Consumers, unlike producers, are not thread\-safe and do not support the calling of the same consumer in multiple threads. Each consumer must be called in a separate thread.

<span id="fe2d9e89"></span>
## Graceful exit

When a consumer exits, we recommend that you call the `close` method actively close the connection with the Kafka instance. If this method is not used, the consumer may fail to send the exit request, blocking the consumer group processing on the Kafka instance. The blocking duration is 10 seconds by default.

Always avoid frequent creation and close of consumers. Each creation or close can cause rebalancing of a consumer group. A consumer group that is rebalancing cannot get messages as expected.

<span id="4fa4c6e5"></span>
## Domain name resolution (DNS)

BytePlus Kafka instances are deployed in distributed clusters. The initial endpoint is offered using a domain name. When a client uses a domain name for access, we recommend that you set the DNS of the client to all IP address resolution, namely `client.dns.lookup = use_all_dns_ips`. This ensures that the client can still be used normally when a back\-end node changes in the distributed cluster.
