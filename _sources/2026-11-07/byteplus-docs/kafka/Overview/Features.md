---
title: "Features"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/features"
---

<span id="实例管理"></span>
## Instance management


|**Feature** |**Description** |
|---|---|
|Instance management |* You can manage resources at the instance level. This means that you can create, view, and delete instances. For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance) and [Viewing instance details](https://docs.byteplus.com/en/docs/kafka/viewing-instance-details).<br><br>* You can select from multiple instance types and upgrade your instance at any time. When you upgrade an instance, you can customize the time for executing a rebalance to avoid traffic peaks. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications). |
|Internal access and [Enabling internet-facing access](https://docs.byteplus.com/en/docs/kafka/enabling-internet-facing) |* Kafka instances can be accessed over the internet or virtual private clouds (VPCs) to meet access requirements in diversified scenarios.<br><br>* Message Queue for Kafka offers various endpoints for use, depending on the access method. |
|[Parameter management](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter) |Message Queue for Kafka allows you to perform online, visual configurations of some parameters at the instance and topic levels. You can specify various message policies for different scenarios. For example, you can use the **Message Retention Period** parameter to configure a [Message deletion policy upon expiration](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter) and the **Disk cleanup level** parameters to configure a [Disk capacity threshold policy](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter). |
|[Managing background tasks](https://docs.byteplus.com/en/docs/kafka/managing-background-tasks) |Message Queue for Kafka offers execution records of background tasks such as instance specification changes and restarts. Each record contains the execution status, details, start time, and end time. |
|[IP allowlist](https://docs.byteplus.com/en/docs/kafka/creating-allowlist) |You can manage IP allowlists for your instances. If you associate an IP allowlist with an instance, only the IP addresses in the allowlist can access the instance. |


<span id="Group和Topic管理"></span>
## Group and topic management


|**Feature** |**Description** |
|---|---|
|[Topic management](https://docs.byteplus.com/en/docs/kafka/creating-topic) |You can manage resources at the topic level. This means that you can create, view, and delete topics. |
|[Group management](https://docs.byteplus.com/en/docs/kafka/creating-group) |You can manage resources at the group level and create groups using SDKs. You can also view details such as consumer group status, subscribed topics, and consumer offsets in the console. |


<span id="消息管理"></span>
## Message management


|**Feature** |**Description** |
|---|---|
|[Resetting consumer offsets](https://docs.byteplus.com/en/docs/kafka/Resetting-consume-offsets) |You can reset consumer offsets and change the current consumption positions of consumers in the Message Queue for Kafka console. This feature allows you to consume messages directly from a specified point in time, the latest offset, or a specified offset. |
|[Message query](https://docs.byteplus.com/en/docs/kafka/message-query) |You can filter and query messages by message ID or time range. You can download messages and view message details online. |


<span id="监控告警"></span>
## Monitoring and alarming


|**Feature** |**Description** |
|---|---|
|Real\-time data monitoring |Message Queue for Kafka is integrated with Vitality Cloud Monitor (VCM) to achieve real\-time data monitoring. VCM monitors various data of instances around the clock, including the instance status, resource usage, and the amount of time used for sending and receiving messages. |
|Custom alarm configurations |Message Queue for Kafka supports a wide range of data metrics and custom alarm policies. This enables alarm notifications through different notification methods in various scenarios. |


<span id="权限管理"></span>
## Permission management


|**Feature** |**Description** |
|---|---|
|Permission management provided by Apache Kafka |Message Queue for Kafka supports permission management based on access control lists (ACLs) and is fully compatible with all built\-in permission policies provided by Apache Kafka. |
|[User management](https://docs.byteplus.com/en/docs/kafka/creating-SASLuser) |Message Queue for Kafka allows you to manage users in the console. You can create and manage PLAIN and SCRAM users to implement secure permission management. |
|[IAM-based access control](https://docs.byteplus.com/en/docs/kafka/IAM--permission-management) |Message Queue for Kafka is fully integrated with Identity and Access Management (IAM). You can attach different instance access policies to different IAM roles. This way, you can achieve fine\-grained permission management in various scenarios. |


<span id="开发者工具"></span>
## Developer tools


|**Feature** |**Description** |
|---|---|
|[OpenAPI](https://docs.byteplus.com/en/docs/kafka/API-release-notes) |Message Queue for Kafka offers a remote procedure call (RPC) API, with which you can experience all the features of the service. |
|[Multi-language SDKs](https://docs.byteplus.com/en/docs/kafka/SDK-overview) |Message Queue for Kafka is compatible with Apache Kafka SDKs for multiple programming languages. This ensures easy and secure connection to the service. |
