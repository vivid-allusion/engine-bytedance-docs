---
title: "Note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/pulsar_note"
---

<span id="_1-pulsar-简介"></span>
## 1 Pulsar Introduction

Apache Pulsar (hereinafter referred to as Pulsar) is an open\-source, high\-performance messaging and streaming platform based on the **publish/subscribe model**, supporting multi\-tenancy, distributed architecture, and cloud\-native deployment. It provides **messaging queue and computation** services, addressing the challenges of message transmission and queuing between servers.

Pulsar combines the advantages of traditional messaging systems (such as RabbitMQ) and publish\-subscribe\-based messaging systems (such as Kafka), making it suitable for real\-time message delivery between services, big data use cases, and many others. Pulsar enables seamless dynamic scaling, offering greater elasticity and helping reduce hardware costs.

Pulsar adopts an advanced cloud\-native architecture, separating stateful storage and stateless computation into different architectural layers, making it highly suitable for deployment, usage, and operation in cloud\-based infrastructure. The architecture features of separating storage and computation, as well as distributed data storage, significantly reduce the cost and risk of scaling computing or storage capacity. In particular, scaling does not require heavy data migration, and this greatly benefits system availability, stability, maintainability, and operational cost optimization.

Pulsar has been widely adopted in the industry, with common use cases including high\-performance data pipelines, microservices, instant messaging, data integration, real\-time data warehouses, and many others.

Pulsar offers the following key features:


|Features |Note |
|---|---|
|**Cloud native** |Multi\-layer architecture with separation of compute and storage, convenient horizontal scaling of compute and storage, supports cloud storage, and is easy to deploy in the cloud and on Kubernetes. |
|**Serverless functions** |Write serverless functions using easy\-to\-use APIs. When Pulsar receives data, it can natively process the data, simplifying real\-time data pipelines without the need for additional streaming data processing engines. |
|**Horizontal scalability** |Supports seamless scaling of large cluster nodes, allowing independent scaling of compute and storage nodes. Scaling operations are lightweight and low\-cost, and do not involve data migration during the process. Supports massive amounts of topic data. |
|**High stability, low latency** |Low latency and high stability for large\-scale message production, with low end\-to\-end latency. |
|**Cross\-region replication** |Data replicas can be configured across multiple regional data centers. |
|**Multi\-tenancy** |Native multi\-tenant system, supports tenant isolation, authentication, user authorization, and quota management. |
|**Persistent storage** |Persistent message storage based on Apache BookKeeper, stable and reliable, supports separation of read and write operations at the IO level.<br><br>Supports hot and cold tiered storage of data, allowing historical data to be transferred to lower\-cost storage systems. |
|**Client libraries** |* Supports Java, Go, Python, C++, Node.js, WebSocket, C#, and other languages, offering flexible message models and high\-level APIs.<br><br>* Supports multiple subscription modes. |
|**Maintainability** |Provides RESTful APIs for deployment, management, tools, and monitoring. Supports flexible and diverse deployment modes, such as bare metal, on ECS, on Kubernetes, and more. |


<span id="_2-pulsar-的应用场景"></span>
## 2 Pulsar Use cases

Pulsar supports a variety of use cases for messaging queues, such as:


* Online scenarios: asynchronous communication between services, message buffering, system decoupling, broadcast notifications, and many others.

* Offline scenarios: In the big data domain, Pulsar serves as a crucial component of offline and real\-time data pipelines, handling log reporting, aggregating client\-side event logs, database binlogs, service monitoring, and many others. It also supports storage, computation, and service of intermediate result data for real\-time data warehouses.


<span id="_3-pulsar-的基本概念"></span>
## 3 Pulsar Basic concepts

<span id="_3-1-概览"></span>
### 3.1 Overview

Pulsar is built on the **publish/subscribe model** (**publish\-subscribe pattern**, also known as **pub\-sub**).

In this model:


* Producers publish messages to topics;

* Consumers subscribe to these topics, process the received messages, and send acknowledgements to the Broker when message processing is complete.


After a subscription is created, Pulsar retains messages (even if consumers disconnect from Pulsar). Retained messages can only be discarded after consumers acknowledge that all messages have been successfully processed.

To re\-consume a message after a consumption failure, a negative acknowledgement can be sent to the Broker, or an acknowledgement timeout mechanism can be enabled for unacknowledged messages to trigger automatic message redelivery.

<span id="_3-2-消息"></span>
### 3.2 Messages

Messages are the basic processing unit in Pulsar and consist of the following parts:


|Components |Description |
|---|---|
|Value / Data payload |The data content carried by the message. The message content is in the form of raw bytes and also supports the corresponding schema. |
|Key |Messages can be tagged with a key (optional), which is useful in scenarios such as topic compaction. |
|Properties |A collection of user\-defined key\-value attribute pairs (optional). |
|Producer name |The name of the producer that produces the message. If the producer name is not specified, the default name will be used. |
|Sequence ID |Each message belongs to an ordered sequence within its topic. The sequence ID of the message is its number in this sequence. |
|Publish time |A timestamp automatically added by the producer when the message is published. |
|Event time |An optional timestamp attached to the message by the business application. For example, the application attaches a timestamp when the message is processed. If the event time is not set, its value is 0. |
|TypedMessageBuilder |Used to construct a message. You can use `TypedMessageBuilder` to set message attributes, such as the key or value of the message.<br><br>When configuring `TypedMessageBuilder`, set the key to a string. If the key is set to another type (for example, an AVRO object), the key will be sent as binary bytes, making it difficult for the consumer to deserialize the AVRO object when consuming the message. |


<span id="_3-3-主题"></span>
### 3.3 Topics

Topics, similar to other Pub\-Sub systems, are the pipeline through which messages are delivered from producers to consumers and serve as the carrier of messages in Pulsar. Each topic has its own name, which is structured as a URL:

```Plain
{persistent|non-persistent}://tenant/namespace/topic
```


The specific meaning is as follows:


|Components |Description |
|---|---|
|`persistent` / `non-persistent` |Identifier for the topic type.<br><br>Pulsar supports two topic types: **persistent** and **non\-persistent**. The default topic type is persistent. If the topic type is not specified, the topic is persistent. All messages in a persistent topic are stored on disk (if there is more than one broker, messages are stored on multiple disks), while data in a non\-persistent topic is not stored on disk. |
|`tenant` |The topic corresponds to a **tenant** in the Pulsar instance. A tenant is a key concept in Pulsar's multi\-tenancy feature and can span Pulsar clusters. |
|`namespace` |**Namespace** (**namespace**) is the management unit for topics and provides a grouping mechanism for related topics. Most topic configuration items take effect at the namespace level. Each tenant has one or more namespaces. |
|`topic` |The topic name can be named as needed. |


Topics are automatically created during production and consumption. There is no need to explicitly create topics.

Pulsar supports **partitioned topics** (**partitioned topic**). A partitioned topic can be handled by multiple brokers, thereby increasing the overall throughput of the topic. The creation of partitioned topics requires explicit operations.

<span id="_3-4-订阅"></span>
### 3.4 Subscriptions

Subscriptions are named configuration rules that determine how messages are delivered to consumers.

Pulsar supports four subscription modes: exclusive, failover, shared, and key\-shared, which are described as follows:


* **Exclusive** (**exclusive**): Only one consumer is allowed to be associated with the subscription. This is the default subscription mode.

* **Failover** (**failover**): Multiple consumers can be associated with the same subscription. For each non\-partitioned topic or each partition of a partitioned topic, a primary consumer is selected to receive messages. When the primary consumer is unavailable, all unacknowledged and subsequent messages will be sent to the next consumer in line.

* **Shared** (**shared**): Multiple consumers can be associated with the same subscription. Messages are delivered to each consumer in a round robin manner, and each message is sent to only one consumer. If a consumer becomes unavailable, all messages sent to that consumer that have not been acknowledged will be rescheduled and sent to the remaining consumers.

* **Key\-shared** (**key_shared**): Multiple consumers can be associated with the same subscription. Messages are sent to different consumers, but messages with the same key are sent to the same consumer.


<span id="_4-pulsar-的架构"></span>
## 4 Pulsar architecture

A Pulsar cluster consists of the following modules:


* **Broker**: One or more brokers, responsible for the following tasks:

   * Processing (and load balancing) messages received from producers;

   * Delivering messages to consumers;

   * Communicating with Pulsar's configuration store to handle various coordination tasks;

   * Storing messages in BookKeeper nodes (that is, bookies);

   * Performing specific tasks based on the cluster's corresponding ZooKeeper.

* **BookKeeper**: One or more bookie nodes, responsible for persistent storage of messages.

* **ZooKeeper**: Handles distributed coordination tasks for the cluster.


<span id="_5-火山引擎-e-mapreduce（emr）-中的-pulsar"></span>
## 5 Pulsar in Volcano Engine E\-MapReduce (EMR)

Volcano Engine EMR has provided the Pulsar cluster type in the On ECS deployment mode since version 1.3.0. The currently integrated Pulsar version is 2.9.1. For details, see [版本概述](https://docs.byteplus.com/docs/undefined/68da347242e561058e056938).

The Pulsar cluster type includes three services: ZooKeeper, Pulsar, and BookKeeper.


* The ZooKeeper service includes two components: ZooKeeper Server and ZooKeeper Client:

   * ZooKeeper Server is deployed on Master nodes and some Core nodes (a total of three nodes), providing metadata related to Broker and Bookie;

   * ZooKeeper Client is deployed on all nodes, providing the client program for accessing ZooKeeper.

* The Pulsar service includes two components: Pulsar Broker and Pulsar Client.

   * Pulsar Broker: Deployed on Master, Core, and Task nodes, responsible for providing read and write services as well as Pulsar's computation logic;

   * Pulsar Client: Deployed on Master, Core, and Task nodes, providing the client program for accessing Pulsar.

* The BookKeeper service includes the Bookie component.

   * Bookie: As a BookKeeper node, deployed on Master and Core nodes, responsible for persistent storage of message data.


Both Pulsar and BookKeeper services depend on the ZooKeeper service. In addition, the Pulsar service depends on the BookKeeper service.

<span id="_6-参考文献"></span>
## 6 References


* Apache Pulsar official website: [https://pulsar.apache.org/](https://pulsar.apache.org/)

* Jack Vanlightly: [Understanding How Apache Pulsar Works](https://jack-vanlightly.com/blog/2018/10/2/understanding-how-apache-pulsar-works)
