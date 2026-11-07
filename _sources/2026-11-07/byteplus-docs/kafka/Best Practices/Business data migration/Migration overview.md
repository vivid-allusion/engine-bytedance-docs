---
title: "Migration overview"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/migration-overview"
---

This topic describes the solutions and basic process for migrating business data to a Message Queue for Kafka cluster. This topic helps you smoothly migrate your business data from a self\-managed or cross\-cloud Kafka cluster to a Message Queue for Kafka cluster.

<span id="背景信息"></span>
## Background information

Message Queue for Kafka is a distributed, message\-oriented middleware service based on Apache Kafka. It features high throughput and high scalability. Message Queue for Kafka allows you to publish and subscribe to streaming data and store them in multiple replicas. It is used in a wide range of scenarios such as log compression and collection, streaming data processing, message decoupling, and traffic peak clipping.

During business data migration, only the message production and consumption links and business traffic are migrated. Persistent messages are not migrated to the new Kafka cluster and require manual processing.

<span id="迁移方案"></span>
## Migration solutions

Message Queue for Kafka offers you the following two migration solutions. Select a suitable one with caution based on your business characteristics.


|**Solution** |**Description** |**Scenario** |
|---|---|---|
|Solution 1 |Establish a new message production and consumption process in the cloud, then stop message production in the original Kafka cluster. In addition, stop the consumer client after all historical messages are consumed in the original Kafka cluster.<br><br>This solution allows synchronous business data processing in cloud\-based and on\-premises Kafka clusters, and the original business data is migrated gradually. |This solution can ensure business continuity, and any newly produced messages can be consumed and processed in time. It is suitable for business scenarios that have no special requirements for the message processing order. |
|Solution 2 |Migrate the message data of the new producer client without message consumption. Wait until all subscribed messages are consumed by the original consumers, then start new consumers for message consumption.<br><br>In this solution, only one Kafka cluster processes business data at a time. |Wait until all data is processed by the original Kafka cluster during migration. This solution guarantees the order of message consumption and ensures that the data written earlier can be processed in priority. It is suitable for the businesses that have requirements for the message processing order. |


<span id="迁移流程"></span>
## Migration process


1. Set up an environment.

   Before migration, evaluate the required resources based on your business volume, and create a Kafka instance and the related resources accordingly.

2. Migrate metadata.

   Before migrating your business, migrate the metadata that carries businesses. The metadata in a Message Queue for Kafka instance includes the information about topics, partitions, and replicas that are used for your business.

3. Migrate message services.

   * Solution 1: Start new producer and consumer clients first to keep normal message production and consumption in the new cluster. Then, stop the original producer client. Next, wait until the messages in the original cluster are consumed by original consumers. Finally, stop the original consumer client to complete the migration process.

      For more information, refer to [Solution 1](https://docs.byteplus.com/en/docs/kafka/solution1-migrating-to-Kafka).

   * Solution 2: Migrate all producer clients to the new cluster. Wait until all messages in the original cluster are consumed by the original consumers, then migrate the consumer clients to complete the migration process.

      For more information, refer to [Solution 2](https://docs.byteplus.com/en/docs/kafka/Solution2-migrating-to-Kafka).
