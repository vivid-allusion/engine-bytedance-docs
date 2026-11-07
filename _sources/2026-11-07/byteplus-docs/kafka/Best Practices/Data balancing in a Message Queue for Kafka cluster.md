---
title: "Data balancing in a Message Queue for Kafka cluster"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/best-practices-for-data-balancing"
---

&nbsp;

All message Queue for Kafka instances are deployed in clusters, and each instance consists of multiple brokers. This topic introduces how to ensure data balancing among brokers in a Kafka cluster.

&nbsp;

<span id="7ec90b32"></span>
## Data balancing

Each Kafka instance consists of multiple brokers. The instance exhibits its best performance when the data traffic and disk usage are consistent among brokers. In some scenarios, the data traffic may not be evenly distributed across brokers. For example, the number of partitions varies greatly among brokers. Higher data traffic and disk usage occur in those brokers with more partitions. This results in a higher disk skew rate. The specification of a Kafka instance is based on the maximum broker performance. In scenarios with uneven data distribution, rate limiting can be triggered if a broker reaches the performance threshold of the selected instance specification. This results in the waste of resources in other brokers.

<span id="36acd608"></span>
## Ensuring data balancing in a Message Queue for Kafka cluster

We recommend that you ensure data balancing in a Message Queue for Kafka cluster using the following methods.

<span id="1ce73137"></span>
### Creating resources as needed

Each topic of a Kafka instance can be divided into multiple partitions, each of which is an ordered message queue. The number of partitions affects the traffic processing capabilities of a topic. You must specify the number of partitions when creating a topic. Your Kafka instance evenly distributes the specified partitions to brokers. Each broker processes and stores part of the data in the Kafka cluster.

To ensure relatively balanced data storage and processing in each broker, comply with the following rules for setting parameters such as the number of partitions when you create a topic.


|Scenario |Parameter setting rule |
|---|---|
|Balanced data storage |(Number of partitions × Number of replicas) % Number of brokers = 0 |
|Balanced data processing |Number of partitions % Number of brokers = 0 |


<span id="cfb7810e"></span>
### Standardizing a data write method

In addition to creating resources as needed, message production behavior must be standardized to ensure data balancing to the greatest extent. It is advisable for each partition to be fairly selected when messages are sent from the producer client. For example, the round robin method can be used for partition selection.

This topic describes the impacts of partition selection on data balancing, using the official Confluent client as an example.

If the partition number for writing data and the message key are not specified for the sent message, the round robin method is used for partition selection. This method ensures that data processing and storage remain relatively balanced when messages are written.

If a partition is specified, messages are written to the specified partition. In this case, the balancing of data processing and storage depends on the partition specification policy you use.

If no partition is specified but a message key is specified, the partition selected for writing data is determined by the hash result of the message key. In this case, the balancing of data processing and storage depends on whether the hash result of the message key is balanced.

&nbsp;
