---
title: "Recommendations for using topics"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/recommendations-for-using-topics"
---

Topics are basic resources of a BytePlus Kafka instance. Messages are written to topics during production and read out from topics during consumption. Selecting suitable parameter configurations when creating a topic can ensure the optimal balance between internal data and business traffic of a Kafka instance. This way, the capabilities of the instance can be utilized to the maximum extent.

<span id="5121ff93"></span>
## Number of partitions

Partitions are the basic units for storing data in a topic. Partitions of each topic are distributed within a Kafka instance. Actually, messages are written to and read from partitions.

The number of partitions in a topic must be set to an integer multiple of the number of brokers when the topic is created. This ensures the even distribution of partitions in a cluster. The number of brokers in a Kafka instance is related to the instance type. The larger the instance type, the more the number of brokers. For example, the number of brokers is 3 for the instance type kafka.20.xrate.hw. For such an instance, the number of partitions in each topic must be an integer multiple of 3, such as 3, 6, and 9. Additionally, the number of brokers is 18 for the instance type kafka.1500.xrate.hw. For such an instance, the number of partitions in each topic must be an integer multiple of 18, for example, 18, 36, and 54. After creating an instance, you can view the broker list and the number of brokers corresponding to the instance type on the broker page of the instance. For more information, refer to [Viewing node information](https://docs.byteplus.com/en/docs/kafka/viewing-broker-information).

In addition, it is not advisable to have too many partitions in a topic, as this can easily trigger the rebalancing for the consumer client. We recommend that you keep the number of partitions in a topic less than 100.

<span id="66c5a2f1"></span>
## Number of replicas

The number of replicas represents the message redundancy in a topic. The higher the number of replicas, the better the data reliability and availability, but more storage space is needed.

At present, you can create a topic with 1 to 3 replicas in a BytePlus Kafka instance. We recommend that you create a topic with 3 replicas, which offers the greatest data reliability and availability. In scenarios with less data reliability, a topic with 2 replicas can be created to ensure higher disk usage while reducing some data reliability and availability. Creating a topic with 1 replica is not recommended for message production, as the data reliability and availability cannot be guaranteed. It is recommended for use only in the initial feature testing phase.

<span id="78456b62"></span>
## Minimum number of in\-sync replicas

The minimum number of in\-sync replicas means the minimum number of replicas required for writing consumption messages. At least one in\-sync replica is required, and the maximum number of in\-sync replicas cannot exceed the number of replicas. We recommend that you keep the default value when creating a topic. Namely, set the minimum number of in\-sync replicas to 1 in the case of 1 or 2 replicas, and to 2 in the case of 3 replicas.
