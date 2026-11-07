---
title: "Authorizable resources and actions"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/authorizable-resources-actions"
---

With the permissions management feature of Identity and Access Management (IAM), you can authorize certain operations for Message Queue for Kafka instance resources.

<span id="4e7ee0ee"></span>
## Authorizable resources

In APIs that allow you to configure resource\-specific permissions for users, you can manage the data access permissions of IAM users across different resources through resource authorization. The following table describes types of resources that can be authorized through IAM in Message Queue for Kafka.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Variables such as <code>$region</code> and <code>$account</code> must be modified to your actual values.</div>



|Resource Type |Permission Description |Resource Description Method |
|---|---|---|
|Kafka instance |Specifies permissions on a specific instance or all instances. |* Specific instance:<br><br><br>`trn:kafka:{$region}:{$accountid}:instance/{$instanceid}`<br><br><br>* All instances:<br><br><br>`trn:kafka:{$region}:{$accountid}:instance/*` |


<span id="3ef76a97"></span>
## Authorizable operations

The following operations can be authorized for Message Queue for Kafka:


|Category |Action |Description |
|---|---|---|
|Instance management |CreateInstance |Create a Message Queue for Kafka instance. |
||ModifyInstanceParameters |Modify the parameter configurations of an instance. |
||ModifyInstanceAttributes |Modify instance information such as name and description. |
||ModifyInstanceSpec |Modify instance specifications, such as the instance type, storage specification, and the number of added partitions. |
||ModifyInstanceChargeType |Modify the billing method. |
||DescribeInstances |Get the list of instances under the account. |
||DescribeInstanceDetail |View detailed information on a specific instance. |
||DeleteInstance |Release a pay\-as\-you\-go instance. |
||CreatePublicAddress |Enable internet\-facing access for a Kafka instance. |
||DeletePublicAddress |Disable internet\-facing access. |
|Topic management |CreateTopic |Create a Kafka topic. |
||DeleteTopic |Delete a Kafka topic. |
||ModifyTopicAttributes |Modify the description of the topic. |
||ModifyTopicParameters |Modify the topic parameter configurations. |
||ModifyTopicAccessPolicies |Modify user permissions of a specific topic. |
||DescribeTopics |View the list of topics. |
||DescribeTopicParameters |View the parameter configurations of a specific topic. |
||DescribeTopicPartitions |Get the partition information about a topic. |
||DescribeTopicAccessPolicies |View the permissions list of a topic. |
|Group management |CreateGroup |Call CreateGroup to create a consumer group. |
||ModifyGroup |Call ModifyGroup to modify the description information about a consumer group. |
||DeleteGroup |Delete a consumer group. |
||DescribeGroups |Get the list of consumer groups. |
||DescribeConsumedTopics |View information about topics subscribed by a consumer group. |
||DescribeConsumedPartitions |View the partition information about a specific topic subscribed by a consumer group. |
||ResetConsumedOffsets |Reset the consumer offset of a consumer group. |
|Simple Authentication and Security Layer (SASL) user management |CreateUser |Create a Kafka SASL user. |
||DeleteUser |Delete a Kafka SASL user. |
||ModifyUserAuthority |Modify the default permissions of a specific SASL user for all users. |
||DescribeUsers |Get the list of Kafka SASL users. |
|ACL management |CreateAcl |Call CreateAcl to create an access control list (ACL). |
||DescribeAcls |Call DescribeAcls to query the created ACLs. |
||DeleteAcl |Call DeleteAcl to delete an ACL. |
|Tag management |AddTagsToResource |Call AddTagsToResource to associate tags with a specific instance. |
||RemoveTagsFromResource |Call RemoveTagsFromResource to disassociate tags from one or multiple instances. |
||DescribeTagsByResource |Call DescribeTagsByResource to query resources with tags. |
