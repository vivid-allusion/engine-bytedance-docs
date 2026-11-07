---
title: "Solution 1 for migrating to Message Queue for Kafka"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/solution1-migrating-to-Kafka"
---

This topic describes how to migrate business data from an open source Apache Kafka cluster to a Message Queue for Kafka cluster by using Solution 1.

<span id="注意事项"></span>
## Precautions


* Business migration only involves the migration of message production, consumption links, and business traffic. No message data in the original Apache Kafka cluster is migrated.

* To avoid migration failures due to access exceptions, confirm whether the Kafka instance is accessible before creating migration message sending and receiving links. You can verify the network connectivity by viewing the endpoints on the details page of the Kafka instance.

* Confirm that the proper migration solution has been selected as needed before business data migration. For more information on the comparison between migration solutions, refer to [Migration overview](https://docs.byteplus.com/en/docs/kafka/migration-overview).


<span id="1 环境准备"></span>
## 1 Setting up the environment

Before migration, evaluate the required resources based on your business volume, and create a Kafka instance and the related resources accordingly.

<span id="1.1 迁移评估"></span>
### 1.1 Evaluation before migration

Evaluate the required Message Queue for Kafka resources based on your current business and message volumes, such as the maximum read traffic, maximum write traffic, disk capacity, and number of partitions. Different specifications of Kafka instances vary in computing capacity and storage space. Evaluate the required resources based on your business volume.

<span id="1.2 准备相关资源"></span>
### 1.2 Preparing related resources

Preparing the related resources after confirming the resource requirements, such as the virtual private cloud (VPC), subnet, Elastic Compute Service (ECS) instance, and Kafka instance.


1. Set up an environment.

   Create a VPC and a subnet and buy an ECS instance. After migration, the Kafka instance can be accessed only when it is deployed in the same Region and VPC as the ECS instance. For more information, refer to [Setting up the development environment](https://docs.byteplus.com/en/docs/kafka/setting-up-environment).

2. Buy a Kafka instance.

   To ensure sufficient resources, select the instance type and storage specification for the Kafka instance based on the evaluation result of your business volume. For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance).


<span id="2 迁移元数据"></span>
## 2 Migrating metadata

The migration of metadata mainly involves creating and specifying the same topic and group configurations in the new Kafka instance as those in the original Kafka cluster. These configurations include the topic name, number of partitions, number of replicas, and message retention period. To migrate group configurations, create a group in the Message Queue for Kafka console or using the SDK as needed.


1. Collect the basic information about topics and groups from the original Kafka cluster.

   The core configurations are described as follows:

   
   |**Parameter** |**Description** |
   |---|---|
   |Topic name |The name of a topic. |
   |No. of Partitions |The number of partitions in the topic. The larger the number of partitions, the higher the concurrency of message consumption. |
   |No. of replicas |The number of replicas in a partition. Replicas ensure the high availability of the partition. The data availability can be guaranteed when a broker fails. The higher the number of replicas, the greater the data reliability. |
   |Group ID |The ID of a group, namely, the ID of the consumer group specified during message production and consumption. |
   

2. Create topics with identical quantities and configurations in the Message Queue for Kafka console.

   You can manually create topics, or batch create topics by uploading a configuration file, depending on your needs. For more information, refer to[Creating a topic](https://docs.byteplus.com/25c43zbc/72040)or[Batch importing topics](https://docs.byteplus.com/25c43zbc/2zch6o5u).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Core configurations of topics, such as the topic name and the number of partitions, must be identical to those in the original Kafka cluster. Other parameters, such as the message retention period, can be specified as needed.   </div>
   

3. Create groups with identical quantities and configurations.

   In Message Queue for Kafka, the supported group creation methods for Kafka instances are controlled by the flexible group creation feature. This feature is enabled by default. You can choose whether to enable this feature as needed to create groups with identical quantities and IDs to those of the migration source address.

   * If this feature is enabled, you can not only create groups in the console but also get, parse, and display the group information using the consumer SDK. For more information on how to create groups using the consumer SDK as needed, refer to [Setting a group by using the SDK](https://docs.byteplus.com/en/docs/kafka/creating-group).

   * If this feature is disabled, you can only create groups in the console. For more information on how to create groups in the console, refer to [Creating a group in the console](https://docs.byteplus.com/en/docs/kafka/creating-group).


<span id="3 迁移消息服务"></span>
## 3 Migrating message services

In Solution 1, start new producer and consumer clients first to keep normal message production and consumption in the new cluster. Then, stop the original producer client. Next, wait until the messages in the original cluster are consumed by original consumers. Finally, stop the original consumer client to complete the migration process. This solution ensures the business availability and facilitates smoother data migration. It is suitable for scenarios requiring higher business continuity and availability. However, message consumption is synchronously processed in cloud\-based and on\-premises Kafka clusters. This cannot ensure ordered message consumption.

The migration procedure is as follows:


1. Start new consumers and producers.

   Start new consumers and producers for the new Message Queue for Kafka instance that you create. Set up new message production and consumption processes in the cloud, and start message production and consumption.

   If internet\-facing access is enabled for your Kafka instance, you can directly modify the endpoints in the code of producer and consumer clients. This means that the endpoint of a self\-managed Kafka cluster can be changed to the public endpoint of a Message Queue for Kafka instance.

2. Verify whether the new Kafka instance runs normally.

   You can verify whether your Message Queue for Kafka instance runs normally by determining the healthiness of current services based on your business logic. Alternatively, refer to [Viewing migration progress and results](https://docs.byteplus.com/en/docs/kafka/viewing-migration-progress-results) to verify whether messages are produced and consumed normally in the instance based on the monitoring data provided by Vitality Cloud Monitor (VCM).

   After confirming that your instance runs normally, stop the original cluster.

3. Stop producers in the self\-managed Kafka cluster but retain the original consumers.

   In this case, the original consumers still consume existing historical messages. That is to say, two consumer clients are consuming different messages at the same time. Stopping message production first can avoid the continuous writing of production traffic. Continuous writing of traffic leads to the constant processing of new data by consumers and the failure in stopping message consumption.

4. After all messages in the original Kafka cluster are consumed by the original consumers, stop the original consumers and the original Kafka cluster.

   When the production is stopped, you can observe the processing progress in the consumer group. For more information, refer to [Viewing migration progress and results](https://docs.byteplus.com/en/docs/kafka/viewing-migration-progress-results). After the processing progress in the consumer group ends, stop the original consumers and the original Kafka cluster.

   Once the self\-managed Kafka cluster is stopped, your business data has been migrated from an open source Apache Kafka cluster to a Message Queue for Kafka cluster.
