---
title: "Solution 2 for migrating to Message Queue for Kafka"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Solution2-migrating-to-Kafka"
---

This topic describes how to migrate business data from an open source Apache Kafka cluster to a Message Queue for Kafka cluster by using Solution 2.

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

   You can manually create topics, or batch create topics by uploading a configuration file, depending on your needs. For more information, refer to [Creating a topic](https://docs.byteplus.com/en/docs/kafka/creating-topic) or [Batch importing topics](https://docs.byteplus.com/en/docs/kafka/batch-importing-topics).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Core configurations of topics, such as the topic name and the number of partitions, must be identical to those in the original Kafka cluster. Other parameters, such as the message retention period, can be specified as needed.   </div>
   

3. Create groups with identical quantities and configurations.

   In Message Queue for Kafka, the supported group creation methods for Kafka instances are controlled by the flexible group creation feature. This feature is enabled by default. You can choose whether to enable this feature as needed to create groups with identical quantities and IDs to those of the migration source address.

   * If this feature is enabled, you can not only create groups in the console but also get, parse, and display the group information using the consumer SDK. For more information on how to create groups using the consumer SDK as needed, refer to [2 Specifying a group during message consumption](https://docs.byteplus.com/en/docs/kafka/creating-group).

   * If this feature is disabled, you can only create groups in the console. For more information on how to create groups in the console, refer to [Creating a group in the console](https://docs.byteplus.com/en/docs/kafka/creating-group).


<span id="bb3a80bd"></span>
## 3 Migrating message services

Solution 2: Migrate the message data of the new producer client without message consumption. Wait until all subscribed messages are consumed by the original consumers, then start new consumers for message consumption. This solution is suitable for scenarios that are sensitive to the message consumption order or dependent on ordered messages.

The migration procedure is as follows:


1. Migrate the producer client to the Message Queue for Kafka instance.

   After stopping the producer client in the original cluster, start a new producer client in the new cluster. The new cluster contains no consumers, so new messages produced are not consumed.

2. After all historical messages in the original cluster are consumed by the original consumers, stop the original consumers and the original Kafka cluster.

   When the production in the original Kafka cluster is stopped, the original consumers still consume existing historical messages. For more information on how to observe the processing progress in a consumer group, refer to [Viewing migration progress and results](https://docs.byteplus.com/en/docs/kafka/viewing-migration-progress-results). After the processing progress in the consumer group ends, proceed with subsequent steps.

3. Start the new consumer client in your Message Queue for Kafka instance to begin message consumption.

   Once the production in the new cluster is started, message production and consumption links are established in the cloud through Message Queue for Kafka. You can verify whether your Kafka instance runs normally by determining the healthiness of current services based on your business logic. Alternatively, refer to [Viewing migration progress and results](https://docs.byteplus.com/en/docs/kafka/viewing-migration-progress-results) to verify whether messages are produced and consumed normally in the instance based on the monitoring data provided by Vitality Cloud Monitor (VCM).
