---
title: "Kafka overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Kafka_overview"
---

<span id="_1-kafka-是什么"></span>
## 1 What is Kafka

Kafka was originally developed by LinkedIn and is a distributed messaging system that supports partitions and multiple replicas, coordinated by ZooKeeper. According to the latest official definition, Kafka is a distributed streaming platform.

For more information about Kafka, refer to the official website: [https://kafka.apache.org/](https://kafka.apache.org/)

<span id="_2-kafka-的设计目标"></span>
## 2 Kafka design goals


|Design objectives |Description |
|---|---|
|High throughput, low latency |Kafka can process hundreds of thousands of messages per second, with latency as low as a few milliseconds. |
|Scalability |The Kafka cluster supports dynamic scaling. |
|Persistence, reliability |Messages are persisted to the local disk, and data backup is supported to prevent data loss. |
|High concurrency |Supports thousands of clients reading and writing simultaneously. |
|Fault tolerance |Allows node failures within the cluster (if the number of replicas is n, then n\-1 node failures are allowed). |


<span id="_3-kafka-的架构"></span>
## 3 Kafka architecture

<span id="_3-1-kafka-的专用术语"></span>
### 3.1 Kafka terminology


|Terminology |Note |
|---|---|
|Broker |The Kafka cluster consists of one or more servers responsible for message storage and services. These servers are called brokers. |
|Topic |Each message published to the Kafka cluster has a category, which is called a topic. Messages from different topics are stored separately. |
|Partition |Partition is a physical concept. Each topic contains one or more partitions. |
|Record |Produce and consume a message or a record. Each record contains a key, a value, and a timestamp. |
|Offset |Each record published to the broker is assigned an offset. The offset increases sequentially within a single partition. |
|Producer |Responsible for publishing messages to the Kafka broker. |
|Consumer |Message consumer: A client that reads messages from the Kafka broker. |
|Consumer Group |Manage a group of consumer instances, each consumer belonging to a specific consumer group. |


<span id="_3-2-kafka-的架构拓扑"></span>
### 3.2 Kafka architecture topology

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_afbf506c5c86bc9839bb902d81a44df6.png) </span>

A typical Kafka cluster contains several producers, several brokers, and several consumer groups.

Kafka provides four core APIs, with the two most commonly used being:


* Producer API: Publish messages to one or more Kafka topics

* Consumer API: Subscribe to one or more Kafka topics and process data


<span id="_3-3-topic-和-partition"></span>
### 3.3 Topic and partition

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_537a73fe4bb8591f3ea1cb844fef49a6.png) </span>


* Topic: Logically, a topic can be considered a queue. Each message must specify its topic. Simply put, you must specify which queue to place the message in.

* Partition: Physically, a topic is divided into one or more partitions. Each partition corresponds to a folder on a physical machine, and this folder stores all messages and index files for the partition. If a topic corresponds to a single file, the I/O of the machine where the file resides will become the performance bottleneck for that topic. With partitions, different messages can be written in parallel to different partitions on different brokers, greatly improving concurrency and throughput.

* Offset: Each message has a unique 64\-bit offset within its current partition. This indicates the position of the message.


Choosing the number of partitions: The number of partitions is determined by two factors: throughput and concurrency. Having too many or too few partitions will lead to corresponding issues:


* If there are too many partitions:

   The cluster will have a large amount of metadata, and metadata synchronization will be slow. When machines are restarted or replaced due to failure, the switchover time is long, affecting cluster stability. Data storage becomes fragmented, leading to more random reads and writes.

* If there are too few partitions:

   Concurrency is low, and throughput is low. If a single partition holds too much data, it puts excessive pressure on a single disk, affecting other partitions and thereby impacting the throughput and latency of the entire cluster.

* Recommended partition count:

   The peak load for a single partition should not exceed 5M. Recommended management strategies: Apply for a topic with a small reserved buffer. If the number of partitions is insufficient, apply for expansion. Shrinking partitions is not supported. The cluster supports rate limiting per partition. If a single partition has a large volume, it will be rate limited.


<span id="_3-4-可靠性"></span>
### 3.4 Reliability

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7288efcd0c394653525b925bf274bcd8.png) </span>


* Replication: To ensure data reliability and prevent data loss caused by single\-node failures, each partition can have multiple replicas distributed across different brokers, as shown in the diagram above. For example, you can configure 2 replicas or 3 replicas.

* Leader election: Each partition selects a leader from among multiple replicas. Clients read and write data through the leader partition. The other replicas act as followers and are responsible for synchronizing data from the leader.

* Data synchronization: Kafka's data synchronization falls between strong and weak synchronization, controlled by two parameters: min.insync.replica and acknowledgment acks. The broker must maintain at least the minimum number of replicas in sync and ensure that writing to 0, 1, or all synchronized replicas is successful.


For example:


* replica = 2, min.insync.replica = 1, acks = 1: At least one replica remains in sync. One replica (the leader) writes successfully, and the write is acknowledged as successful; otherwise, the write fails.

* replica = 3, min.insync.replica = 2, acks = all: At least two replicas remain in sync. All in\-sync replicas write successfully, and the write is acknowledged as successful; otherwise, the write fails. This configuration can be considered for workloads with high reliability requirements. It is necessary to consider the trade\-offs: high reliability equals low availability, high latency, and low throughput.
