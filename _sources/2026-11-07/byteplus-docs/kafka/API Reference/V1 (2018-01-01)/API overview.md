---
title: "API overview"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/API-overview-v1"
---

Message queue Kafka Edition provides the following related API interfaces.

<span id="b962a598"></span>
## Instance management


|**API** |**explain** |
|---|---|
|[ListKafkaConf](https://docs.byteplus.com/en/docs/kafka/ListKafkaConf-v1) |Call the ListKafkaConf interface to obtain the relevant configuration supported by the message queue Kafka version. |
|[CreateKafkaInstance](https://docs.byteplus.com/en/docs/kafka/CreateKafkaInstance-v1) |Call the CreateKafkaInstance interface to create a Kafka instance. |
|[DeleteKafkaInstance](https://docs.byteplus.com/en/docs/kafka/DeleteKafkaInstance-v1) |Call the DeleteKafkaInstance interface to delete the Kafka instance. |
|[DescribeInstanceDetail](https://docs.byteplus.com/en/docs/kafka/DescribeInstanceDetail-v1) |Call DescribeInstanceDetail interface to get the details of the specified Kafka instance. |
|[DescribeInstancesSummary](https://docs.byteplus.com/en/docs/kafka/DescribeInstancesSummary-v1) |Call DescribeInstancesSummary interface to get an overview list of instances under the current account. |
|[ModifyInstanceDescription](https://docs.byteplus.com/en/docs/kafka/ModifyInstanceDescription-v1) |Invoke ModifyInstanceDescription interface to modify instance description information. |
|[ModifyInstanceName](https://docs.byteplus.com/en/docs/kafka/ModifyInstanceName-v1) |Call the ModifyInstanceName interface to modify the Kafka instance name. |
|[ModifyInstanceParams](https://docs.byteplus.com/en/docs/kafka/ModifyInstanceParams-v1) |Call ModifyInstanceParams interface to modify the configuration parameters of a Kafka instance. |
|[ScaleKafkaInstance](https://docs.byteplus.com/en/docs/kafka/ScaleKafkaInstance-v1) |Call the ScaleKafkaInstance interface to change the Kafka instance specification. |
|[ModifyChargeToPrepaid](https://docs.byteplus.com/en/docs/kafka/ModifyChargeToPrepaid-v1) |Call the ModifyChargeToPrepaid interface to convert the pay\-as\-you\-go instance into a package year\-per\-month instance. |
|[EnableInternetAccess](https://docs.byteplus.com/en/docs/kafka/EnableInternetAccess-v1) |Call EnableInternetAccess interface to enable public network access. |
|[DisableInternetAccess](https://docs.byteplus.com/en/docs/kafka/DisableInternetAccess-v1) |Call DisableInternetAccess interface to close public network access. |


<span id="fd1e42cd"></span>
## Topic Management


|**API** |**explain** |
|---|---|
|[CreateTopic](https://docs.byteplus.com/en/docs/kafka/CreateTopic-v1) |Call the CreateTopic interface to create a Topic. |
|[DeleteTopic](https://docs.byteplus.com/en/docs/kafka/DeleteTopic-v1) |Call the DeleteTopic interface to delete the Topic. |
|[DescribeTopicAuthorities](https://docs.byteplus.com/en/docs/kafka/DescribeTopicAuthorities-v1) |Call DescribeTopicAuthorities interface to get permission information of Topic. |
|[DescribeTopicPartitions](https://docs.byteplus.com/en/docs/kafka/DescribeTopicPartitions-v1) |Call DescribeTopicPartitions interface to get the Partition information of the Topic. |
|[DescribeTopics](https://docs.byteplus.com/en/docs/kafka/DescribeTopics-v1) |Call the DescribeTopics interface to get the Topic list. |
|[ModifyTopic](https://docs.byteplus.com/en/docs/kafka/ModifyTopic-v1) |Call the ModifyTopic interface to modify the configuration of the Topic. |
|[ModifyTopicAuthorities](https://docs.byteplus.com/en/docs/kafka/ModifyTopicAuthorities-v1) |Call ModifyTopicAuthorities interface to change the permissions of the corresponding Topic. |
|[QueryMessageByMessageId](https://docs.byteplus.com/en/docs/kafka/QueryMessageByMessageId-v1) |The calling QueryMessageByMessageId can query messages for the specified Offset in Partition. |


<span id="25999422"></span>
## Group management


|**API** |**explain** |
|---|---|
|[DeleteGroup](https://docs.byteplus.com/en/docs/kafka/DeleteGroup-v1) |Call the DeleteGroup interface to delete the ConsumerGroup. |
|[DescribeConsumedPartitions](https://docs.byteplus.com/en/docs/kafka/DescribeConsumedPartitions-v1) |Call DescribeConsumedPartitions interface to get the Partition information of ConsumerGroup subscription. |
|[DescribeConsumedTopics](https://docs.byteplus.com/en/docs/kafka/DescribeConsumedTopics-v1) |Call DescribeConsumedTopics interface to get the Topic name of the ConsumerGroup subscription. |
|[DescribeGroups](https://docs.byteplus.com/en/docs/kafka/DescribeGroups-v1) |Call the DescribeGroups interface to get the list of ConsumerGroups. |
|[ResetConsumedOffsets](https://docs.byteplus.com/en/docs/kafka/ResetConsumedOffsets-v1) |Call ResetConsumedOffsets interface to reset the Offset consumed by the consumer group. |


<span id="4e4e7fdb"></span>
## User management


|**API** |**explain** |
|---|---|
|[CreateSaslUser](https://docs.byteplus.com/en/docs/kafka/CreateSaslUser-v1) |Call the CreateSaslUser interface to delete the SASL user. |
|[DeleteSaslUser](https://docs.byteplus.com/en/docs/kafka/DeleteSaslUser-v1) |Call the DeleteSaslUser interface to delete a SASL user with a password type of SCRAM. |
|[DescribeSaslUsers](https://docs.byteplus.com/en/docs/kafka/DescribeSaslUsers-v1) |Call the DescribeSaslUsers interface to get a list of Kafka users. |
|[ModifySaslPassword](https://docs.byteplus.com/en/docs/kafka/ModifySaslPassword-v1) |Call the ModifySaslPassword interface to reset the SCRAM user password. |
|[ModifyUserAuthority](https://docs.byteplus.com/en/docs/kafka/ModifyUserAuthority-v1) |Call the ModifyUserAuthority interface to change the default permissions for SASL users. |
