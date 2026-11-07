---
title: "API overview"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/API-overview-2"
---

<span id="10fde559"></span>
## **Resource check**


|**API** |**Description** |
|---|---|
|[DescribeRegions](https://docs.byteplus.com/en/docs/kafka/DescribeRegions-v2) |Call the DescribeRegions interface to view the Region list. |
|[DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/kafka/DescribeAvailabilityZones-v2) |Call DescribeAvailabilityZones interface to view the list of available zones. |


<span id="2c0506e6"></span>
## **Instance management**


|**API** |**Description** |
|---|---|
|[CreateInstance](https://docs.byteplus.com/en/docs/kafka/CreateInstance-v2) |Call CreateInstance to create a message queue Kafka Edition instance. |
|[ModifyInstanceParameters](https://docs.byteplus.com/en/docs/kafka/ModifyInstanceParameters-v2) |Call ModifyInstanceParameters interface to modify the parameter configuration of the corresponding instance. |
|[ModifyInstanceAttributes](https://docs.byteplus.com/en/docs/kafka/ModifyInstanceAttributes-v2) |Call ModifyInstanceAttributes interface to modify the corresponding instance name, description and other instance information. |
|[ModifyInstanceSpec](https://docs.byteplus.com/en/docs/kafka/ModifyInstanceSpec-v2) |Call the ModifyInstanceSpec interface to modify the calculation specifications, storage specifications, and number of additional partitions of the instance. |
|[ModifyInstanceChargeType](https://docs.byteplus.com/en/docs/kafka/ModifyInstanceChargeType-v2) |Call ModifyInstanceChargeType interface to change the billing type of the instance. |
|[DescribeInstances](https://docs.byteplus.com/en/docs/kafka/DescribeInstances-v2) |Call the DescribeInstances interface to get the list of instances under the current account. |
|[DescribeInstanceDetail](https://docs.byteplus.com/en/docs/kafka/DescribeInstanceDetail-v2) |Call DescribeInstanceDetail interface to view the details of the specified instance. |
|[DeleteInstance](https://docs.byteplus.com/en/docs/kafka/DeleteInstance-v2) |Call the DeleteInstance interface to release the pay\-per\-amount instance. |


<span id="c72aa60c"></span>
## **Network management**


|**API** |**Description** |
|---|---|
|[CreatePublicAddress](https://docs.byteplus.com/en/docs/kafka/CreatePublicAddress-v2) |call CreatePublicAddress Interface Enables public network access for Kafka instances. |
|[DeletePublicAddress](https://docs.byteplus.com/en/docs/kafka/DeletePublicAddress-v2) |call DeletePublicAddress The interface closes the public network access method. |


<span id="d75a6cd6"></span>
## **Topic management**


|**API** |**Description** |
|---|---|
|[CreateTopic](https://docs.byteplus.com/en/docs/kafka/CreateTopic-v2) |Call the CreateTopic interface to create a Kafka Topic. |
|[DeleteTopic](https://docs.byteplus.com/en/docs/kafka/DeleteTopic-v2) |Call the DeleteTopic interface to delete the Kafka Topic. |
|[ModifyTopicAttributes](https://docs.byteplus.com/en/docs/kafka/ModifyTopicAttributes-v2) |call ModifyTopicAttributes The interface modifies the description of the Topic. |
|[ModifyTopicParameters](https://docs.byteplus.com/en/docs/kafka/ModifyTopicParameters-v2) |Call the ModifyTopicParameters interface to modify the parameter configuration of the Topic. |
|[ModifyTopicAccessPolicies](https://docs.byteplus.com/en/docs/kafka/ModifyTopicAccessPolicies-v2) |Call ModifyTopicAccessPolicies interface to change the user permissions of the specified Topic. |
|[DescribeTopics](https://docs.byteplus.com/en/docs/kafka/DescribeTopics-v2) |Call the DescribeTopics interface to view the Topic list. |
|[DescribeTopicParameters](https://docs.byteplus.com/en/docs/kafka/DescribeTopicParameters-v2) |Call DescribeTopicParameters view the parameter configuration for the specified Topic. |
|[DescribeTopicPartitions](https://docs.byteplus.com/en/docs/kafka/DescribeTopicPartitions-v2) |Call the DescribeTopicPartitions interface to get the Partition information of the Topic. |
|[DescribeTopicAccessPolicies](https://docs.byteplus.com/en/docs/kafka/DescribeTopicAccessPolicies-v2) |Call the DescribeTopicAccessPolicies interface to view the permission list of the Topic. |


<span id="dfb20fcb"></span>
## **Group management**


|**API** |**Description** |
|---|---|
|[CreateGroup](https://docs.byteplus.com/en/docs/kafka/CreateGroup-v2) |Call CreateGroup to create a ConsumerGroup. |
|[ModifyGroup](https://docs.byteplus.com/en/docs/kafka/ModifyGroup-v2) |Call ModifyGroup to modify the consumer group description information. |
|[DeleteGroup](https://docs.byteplus.com/en/docs/kafka/DeleteGroup-v2) |Call DeleteGroup to delete the consumption group. |
|[DescribeGroups](https://docs.byteplus.com/en/docs/kafka/DescribeGroups-v2) |Call the DescribeGroups interface to get the list of consumer groups. |
|[DescribeConsumedTopics](https://docs.byteplus.com/en/docs/kafka/DescribeConsumedTopics-v2) |Call DescribeConsumedTopics interface to view the topic information of the consumption group subscription. |
|[DescribeConsumedPartitions](https://docs.byteplus.com/en/docs/kafka/DescribeConsumedPartitions-v2) |Call DescribeConsumedPartitions interface to view the partition information for the specified Topic that the consumer group subscribes to. |
|[ResetConsumedOffsets](https://docs.byteplus.com/en/docs/kafka/ResetConsumedOffsets-v2) |Call ResetConsumedOffsets reset the consumption check point of the consumer group. |


<span id="7518913b"></span>
## Message query


|**API** |**Description** |
|---|---|
|[QueryMessageByTimestamp](https://docs.byteplus.com/en/docs/kafka/QueryMessageByTimestamp-v2) |Call QueryMessageByTimestamp to query message metadata of a partition during a specified time period. |


<span id="4cb172ef"></span>
## SASL user management


|**API** |**Description** |
|---|---|
|[CreateUser](https://docs.byteplus.com/en/docs/kafka/CreateUser-v2) |Call the CreateUser interface to create a Kafka SASL user. |
|[DeleteUser](https://docs.byteplus.com/en/docs/kafka/DeleteUser-v2) |Call the DeleteUser interface to delete the Kafka SASL user. |
|[ModifyUserAuthority](https://docs.byteplus.com/en/docs/kafka/ModifyUserAuthority-v2) |Call the ModifyUserAuthority interface to change the default permissions of the specified SASL user for all users. |
|[DescribeUsers](https://docs.byteplus.com/en/docs/kafka/DescribeUsers-v2) |Call the DescribeUsers interface to get a list of Kafka SASL users. |


<span id="8d211cc7"></span>
## ACL policy management


|**API** |**Description** |
|---|---|
|[CreateAcl](https://docs.byteplus.com/en/docs/kafka/CreateAcl-v2) |Call the CreateAcl interface to create an ACL policy. |
|[DescribeAcls](https://docs.byteplus.com/en/docs/kafka/DescribeAcls-v2) |Call the DescribeAcls interface to query the created ACL rule policy. |
|[DeleteAcl](https://docs.byteplus.com/en/docs/kafka/DeleteAcl-v2) |Call the DeleteAcl interface to remove the ACL policy. |


<span id="4b54f591"></span>
## Tag management


|**API** |**Description** |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/en/docs/kafka/AddTagsToResource-v2) |Call the AddTagsToResource interface to bind the label for the specified instance. |
|[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/kafka/RemoveTagsFromResource-v2) |Call RemoveTagsFromResource interface to untie labels for one or more instances. |
|[DescribeTagsByResource](https://docs.byteplus.com/en/docs/kafka/DescribeTagsByResource-v2) |call DescribeTagsByResource The interface queries for tagged resources. |


<span id="fe113a29"></span>
## Allowlist management


|**API** |**Description** |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/kafka/CreateAllowList-v2) |Call the CreateAllowList interface to create a new IP whitelist rule. |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/kafka/ModifyAllowList-v2) |Call ModifyAllowList to modify an already created whitelist rule. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/kafka/DeleteAllowList-v2) |Call DeleteAllowList to delete an already created whitelist rule. |
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/kafka/DescribeAllowLists-v2) |Call DescribeAllowLists to query the whitelist list. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/kafka/DescribeAllowListDetail-v2) |Call DescribeAllowListDetail query the details of the specified whitelist. |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/kafka/AssociateAllowList-v2) |Call AssociateAllowList to bind the instance to the whitelist. |
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/kafka/DisassociateAllowList-v2) |Call DisassociateAllowList unbind instance with whitelist. |
