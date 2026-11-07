---
title: "Terms"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/terms"
---

This topic introduces the terms that are used in Message Queue for Kafka to help you better understand and use Message Queue for Kafka.

<span id="Apache Kafka"></span>
### Apache Kafka

An open source platform for processing distributed data streams. This platform allows you to publish, subscribe to, store, and process data streams in real time. For more information on Apache Kafka, refer to [Apache Kafka](https://kafka.apache.org/).

<span id="实例"></span>
### instance

Also referred to as a Kafka instance. An instance is an independent resource entity in Message Queue for Kafka, which corresponds to a Kafka cluster.

<span id="接入点"></span>
### endpoint

An address that is used by producers and consumers to connect to a Kafka instance for sending and receiving messages.

<span id="消息"></span>
### message

A carrier for delivering information in Message Queue for Kafka. In Message Queue for Kafka, a message is a byte array.

<span id="生产者"></span>
### producer

An application that sends messages to Message Queue for Kafka.

<span id="消费者"></span>
### consumer

An application that receives messages from Message Queue for Kafka.

<span id="消费组"></span>
### consumer group

A group of consumers that have the same group ID. If messages in a topic are consumed by multiple consumers in the same consumer group, each message is delivered to only one of the consumers. This balances the load among consumers. Consumer groups allow messages in a topic to be concurrently consumed.

<span id="Topic"></span>
### topic

A message topic that is used to classify messages.

<span id="分区"></span>
### partition

A message partition that is used to store messages. A topic consists of multiple partitions. Messages in each partition are stored on one or more brokers.

<span id="消息保留时长"></span>
### message retention period

The maximum period of time during which messages can be retained on a Kafka instance when the disk capacity is sufficient.

<span id="最大消息大小"></span>
### maximum message size

The maximum size of a message that can be received and sent on brokers in Message Queue for Kafka.

<span id="订阅关系"></span>
### subscription relationship

The subscription status of consumer groups to topics. Message Queue for Kafka allows you to view consumer groups that subscribe to a specific topic.
