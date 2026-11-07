---
title: "Migration overview"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Migration_overview"
---

This topic describes migration solutions and processes for moving open\-source RabbitMQ clusters or stand alone instances to Message Queue for RabbitMQ.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information 

Message Queue for RabbitMQ provides all native RabbitMQ message processing features, is fully compatible with the open\-source RabbitMQ community and the Queue, Exchange, and Vhost components, and supports stand alone or cluster deployments in the cloud. Migrate from self\-hosted RabbitMQ to Message Queue for RabbitMQ, with no deployment or maintenance required, offering higher stability and security. No changes to business code are needed, enabling effortless cloud migration.

<span id=".6L-B56e75pa55qGI"></span>
## Migration plan

Message Queue for RabbitMQ offers the following two migration solutions for you to choose from. Please select a migration solution carefully based on the specific characteristics of your business.


|Solution |DescriptionDescription |Applicable scenarios |
|---|---|---|
|Option 1 |First, establish a new message production and consumption workflow, while the old Cluster continues to consume the existing old messages until consumption is complete. |This solution cannot guarantee message consumption order and is suitable for business scenarios where the order of message consumption is not important or there is no reliance on ordered messages, such as order submission in high\-concurrency scenarios. |
|Option 2 |Migrate to the new producer endpoint, but do not start consuming messages yet. Wait until all old messages have been consumed by the old consumer endpoint, then start the new consumer endpoint to begin consumption. |Applicable to business scenarios that are sensitive to the order of message consumption or rely on ordered messages, such as MySQL binlog consumption. |


<span id=".6L-B56e75rWB56iL"></span>
## Migration process


1. Environment preparations.

   Before migration, you need to reasonably assess resource requirements based on business volume and create the RabbitMQ instance and related dependent resources.

2. Migrate metadata.

   Migrate the configuration information of Vhost, Exchange, Queue, and other configuration information from open\-source RabbitMQ to Message Queue for RabbitMQ. All configuration information, including the number of queues and permissions, must be migrated.

3. Migrate the message service.

   * Plan 1: First, take the old production end offline, and then start the new consumer end and production end so that production and consumption in the new Cluster are Running normally. After the messages in the old cluster have been fully consumed by the old consumer, shut down the old consumer endpoint to complete the migration to the cloud.

   * Option 2: Migrate all message producers to the new cluster. After messages in the old cluster have been fully consumed by the old consumers, migrate the consumers to the new cluster to complete the cloud migration.
