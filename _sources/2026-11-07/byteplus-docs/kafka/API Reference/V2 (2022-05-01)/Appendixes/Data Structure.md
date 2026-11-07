---
title: "Data Structure"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2"
---

<span id="cb5455aa"></span>
## **AccessPolicyObject**

List of SASL user permissions.

Referred to by the following interface:


* CreateTopic

* ModifyTopicAccessPolices

* DescribeTopicAccessPolicies



|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|UserName |String |Yes |Test |SASL user name. |
|AccessPolicy |String |Yes |Sub |The SASL user's access to the current Topic.<br><br><br>* PubSub: Has publish and subscribe permissions.<br><br>* Pub: Has permission to publish.<br><br>* Sub: Has subscription rights. |


<span id="346d5ef7"></span>
## AclObject

ACL details.

Referred to by the following interface:


* DescribeAcls



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|UserName |String |Test |The username of the rule binding. |
|Ip |String |192.168.0.1/18 |The IP address or network segment specified by the rule. |
|ResourceType |String |Topic |The resource type of the rule configuration. |
|PatternType |String |Literal |The resource match type for rule configuration. |
|Resources |String |Test |The Topic or Group name or prefix of the rule configuration. |
|AccessPolicy |String |Read |Access policy for rule configuration. |


<span id="f2ed3110"></span>
## AllowListInfo

Whitelist details.

Referred to by the following interface:


* DescribeAllowLists



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowListId |String |acl\-fda2ed6365b94c909e44198fbbf48\*\*\*\* |Whitelist ID. |
|AllowListName |String |Test |Whitelist name. |
|AllowListDesc |String |Test whitelist |Whitelist description. |
|AllowListIpNum |Integer |2 |The number of IP addresses or IP segments specified in the whitelist. |
|AssociatedInstanceNum |Integer |3 |Number of instances of whitelist bindings. |


<span id="659b367e"></span>
## AssociatedInstanceInfo

Whitelist binding instance information.

Referred to by the following interface:


* DescribeAllowListDetail



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |kafka\-cnitzqgnk0g4\*\*\*\* |The instance ID of the whitelist binding. |
|InstanceName |String |Test example |The instance name of the whitelist binding. |


<span id="57963f15"></span>
## BasicGroupInfo

The basic information of the instance, including the instance name, ID and other information.

Referred to by the following interface:


* DescribeGroups



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|GroupId |String |Testgroup |Consumer group ID. |
|State |String |Empty |Consumer group status.<br><br><br>* PreparingRebalance: Consumption preparation<br><br>* CompletingRebalance:<br><br><br>in the allocated partition<br><br><br>* Stable: Consuming<br><br>* Empty: not consumed |
|Description |String |News |Consumption group description information. |
|ProtocolType |String |Consumer |The type of consumer agreement specified by the consumer group.<br><br><br>* If using the standard Kafka consumer protocol, it is displayed as consumer.<br><br>* If other protocol types are used, the corresponding protocol name is displayed, for example, when Kafka\-Connector is connected, it is displayed as the connect type.<br><br>* This field may be empty if a custom partition is consumed. |
|BalanceAlgorithm |String |Range |The algorithm for assigning the consumed partition to the consumer is specified by the consuming client side. This field may be empty if the consumption method of a custom partition is used. |


<span id="757b6ad8"></span>
## **BasicInstanceInfoObject**

The basic information of the instance, including the instance name, ID and other information.

Referred to by the following interface:


* DescribeInstances

* DescribeInstanceDetail



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AccountId |String |200000 \*\*\* |The Byteplus Engine master account ID for creating the instance. |
|ChargeDetail |ChargeDetailObject |/ |Billing information such as the billing method of the instance. For detailed instructions, please refer to ChargeDetailObject. |
|ComputeSpec |String |Kafka.60xrate.hw |Calculation specifications for Kafka instances. |
|CreateTime |String |2022\-07\-18T07:48:58Z |The creation time of the instance. The time display format is YYYY\-MM\-DD T'HH: MM: SS'Z '. |
|EipId |String |eip\-mjhulvqza6805smt1bnc\*\*\*\* |The ID of the EIP.<br><br>This parameter is not returned if the instance does not have public access enabled. |
|InstanceDescription |String |This is a test example |A brief description of the instance. |
|InstanceId |String |kafka\-cnngqkfgdudt\*\*\*\* |Kafka instance ID. |
|InstanceName |String |Kafkainstance |Kafka instance name. |
|InstanceStatus |String |Running |Instance state. |
|PrivateDomainOnPublic |Boolean |False |Whether the public network parsing function has been turned on.<br><br><br>* True: turned on<br><br>* False: closed |
|ProjectName |String |NewProject |The IAM project to which the instance belongs. This parameter is not returned if the instance does not belong to any IAM project. |
|RegionId |String |ap\-southeast\-1 |The region ID of the instance. |
|StorageSpace |Integer |200 |Total instance storage. The unit is GiB. |
|StorageType |String |ESSD_PL0 |Type of cloud disk for Kafka instance data storage. That is ESSD_FlexPL or ESSD_PL0. |
|SubnetId |String |subnet\-min6uy01kuf45smt1a2i\*\*\*\* |The subnet ID of the VPC. |
|Tags |Map < String, String \> |{<br><br>"Mode": "http",<br><br>"Tag\-wzx": "11"<br><br>} |Bound tag. |
|UsablePartitionNumber |Integer |20 |The number of available partitions remaining for the current instance. |
|UsableGroupNumber |Integer |100 |The number of remaining available consumer groups for the current instance. |
|UsedGroupNumber |Integer |20 |The number of consumer groups that the current instance has created. |
|UsedPartitionNumber |Integer |120 |The number of partitions already in use by the current instance. |
|UsedStorageSpace |Integer |100 |The instance has used storage space. The unit is GiB. |
|UsedTopicNumber |Integer |20 |The number of Topics created by the current instance. |
|Version |String |2.2.2 |Supported Kafka versions. Currently supported versions include:<br><br><br>* 2.2.2: Kafka 2.2.2 version.<br><br>* 2.8.2: Kafka 2.8.2 version. |
|VpcId |String |vpc\-13fo9gkz6j6683n6nu5ec\*\*\*\* |Private Network (VPC) ID. |
|ZoneId |String |ap\-southeast\-1a |The Availability Zone ID where the instance is located. For highly available instances across AZ, multiple Availability Zone IDs are returned here. |


<span id="5a771da6"></span>
## BasicPartitionInfo

Basic information of Topic partition, including partition number, Leader number and other information.

Referred to by the following interface:


* DescribeTopicPartitions



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|PartitionId |Integer |0 |Partition number. |
|Leader |Integer |2 |Section Leader number. |
|Replicas |Array of Integer |[2, 0, 1] |List of copies of the partition. |
|InsyncReplicas |Array of Integer |[2, 0, 1] |List of synchronized replicas of the partition. |
|UnderInsyncReplicas |Array of Integer |[] |List of unsynchronized replicas. |
|StartOffset |Integer |7758654122 |The offset of the current earliest message of the Partition Leader. |
|EndOffset |Integer |7774940552 |The offset of the next message from the Partition Leader, the position of the current latest message is EndOffset \- 1. |
|MessageCount |Integer |16286430 |The current number of messages in the Partition Leader. Where MessageCount=EndOffset\-StartOffset. |


<span id="6a23ad38"></span>
## BasicTopicInfoObject

List of Topics that meet the query criteria.

Referred to by the following interface:


* DescribeTopics



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CreateTime |String |2023\-03\-06T12:47:44Z |The creation time of the Topic. |
|Description |String |Newtopic |Topic description. |
|PartitionNumber |Integer |12 |The number of partitions of the Topic. |
|ReplicaNumber |Integer |3 |Number of copies of Topic. |
|Status |String |Running |Status of Topic. |
|TopicName |String |my_topic |The name of the Topic. |


<span id="0e5082f9"></span>
## BasicMessageInfoObject

List of messages that meet the query criteria.

Referred to by the following interface:


* QueryMessageByTimestamp



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TopicName |String |test\-topic |Topic name |
|PartitionId |Integer |0 |The partition where the message resides. |
|MessageOffset |Integer |0 |Message offset |
|MessageSize |Integer |1024 |The size of message measured by byte. |
|CreateTime |Integer |1717415105339 |The written time of the message. |
|Key |String |test\-key |The Key field of the message. |
|Message |String |test\-value |The Body field of the message. |


<span id="2f2b0798"></span>
## BasicUserInfoObject

List of Kafka SASL users who meet the filter criteria.

Referred to by the following interface:


* DescribeUsers



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllAuthority |Boolean |True |Whether the user has read and write permissions for all topics by default.<br><br><br>* True: This user has read and write permissions for all topics.<br><br>* False: This user does not have read and write permissions for all topics. |
|CreateTime |String |2022\-07\-18T07:48:58Z |SASL user creation time. |
|Description |String |PHP\-sdk |SASL user description. |
|PasswordType |String |Scram |SASL user type. The following types are currently supported:<br><br><br>* Plain<br><br>* Scram<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The user type corresponds to different SASL authentication mechanisms, please refer to the detailed description <a href="https://docs.byteplus.com/en/docs/kafka/viewing-endpoints">Viewing endpoints</a>.</div><br> |
|UserName |String |PHP\-SDK |SASL user name. |


<span id="373c2766"></span>
## **ChargeDetailObject**

The billing information of the instance, including billing methods and other information.

Referred to by the following interface:


* DescribeInstances

* DescribeInstanceDetail



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ChargeType |String |PostPaid |The billing type of the instance. Supported types include:<br><br><br>* PostPaid: pay according to the quantity<br><br>* PrePaid: annual package monthly |
|ChargeStatus |String |Normal |The billing status of the instance. Includes:<br><br><br>* Normal: normal<br><br>* Overdue: Billing by volume Arrears<br><br>* Expired: Annual subscription expires |
|AutoRenew |Boolean |True |Whether the annual subscription will be automatically renewed after the monthly instance expires.<br><br><br>* True: Automatic renewal.<br><br>* False: does not automatically renew. Manual renewal is required after expiration, otherwise the instance will be shut down. |
|ChargeStartTime |String |2022\-07\-18T07:48:58Z |The start billing time of the instance. The time display format is YYYY\-MM\-DD T'HH: MM: SS'Z '. |
|ChargeExpireTime |String |2022\-07\-18T07:48:58Z |The expiration time of the package year\-month instance. The time display format is YYYY\-MM\-DD'T'HH: MM: SS'Z '.<br><br>This parameter is returned only by the annual package\-month instance. |
|OverdueTime |String |2022\-07\-18T07:48:58Z |The default shutdown time of the instance. The time display format is YYYY\-MM\-DD'T'HH: MM: SS'Z '. |
|OverdueReclaimTime |String |2022\-07\-18T07:48:58Z |Estimated release time after instance default shutdown. The time display format is YYYY\-MM\-DD T'HH: MM: SS'Z '. |
|PeriodUnit |String |Month |The unit of lifetime of the monthly subscription type instance, which specifies purchases in months or years. Where:<br><br><br>* Month: (default) subscription month<br><br>* Year: package year |


<span id="88478770"></span>
## **ChargeInfoObject**

Billing information such as the billing type of the Kafka instance.

Referred to by the following interface:


* CreateInstance

* ModifyInstanceChargeType



|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|ChargeType |String |Yes |PostPaid |The billing type of the instance. Supported types include:<br><br><br>* PostPaid: pay according to the quantity<br><br>* PrePaid: annual package monthly |
|AutoRenew |Boolean |No |True |Whether the annual subscription will be automatically renewed after the monthly instance expires.<br><br><br>* True: Automatic renewal.<br><br>* False: (default) does not renew automatically. Manual renewal is required after expiration, otherwise the instance will be shut down. |
|PeriodUnit |String |No |Month |The unit of lifetime of the subscription type instance, which specifies purchases in months or years. Supported settings are:<br><br><br>* Month: monthly subscription<br><br>* Year: package year<br><br><br>Only instances of the package year\-month type need to be specified, that is, ChargeType is required when specified as PrePaid. |
|Period |Integer |No |1 |The purchase duration of the monthly subscription type instance.<br><br><br>* When PeriodUnit is specified as Month, the range of values is 1 to 9.<br><br>* When PeriodUnit is specified as Year, the range of values is 1 to 3.<br><br><br>Only instances of the package year\-month type need to be specified, that is, ChargeType is required when specified as PrePaid. |


<span id="d85c4d3c"></span>
## ConsumedPartitionInfoObject

List of partitions for the specified Topic.

Referred to by the following interface:


* DescribeConsumedPartitions



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Accumulation |Integer |15219375 |The amount of message accumulation for the consumption group on the partition. |
|ConsumedClient |String |Consumer\-1/192.168.xxx.Xx |The information for the partition consumer, specified by the client side when consuming, may be empty here. |
|ConsumedOffset |Integer |2662697877 |Division consumption progress. |
|EndOffset |Integer |2677917252 |The offset to partition the next message. |
|PartitionId |Integer |0 |Topic partition number. |
|StartOffset |Integer |2661451497 |The earliest message offset for the partition. |


<span id="bd2caa7d"></span>
## ConsumedTopicInfoObject

Specifies the list of Topics subscribed by the consumer group.

Referred to by the following interface:


* DescribeConsumedTopics



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TopicName |String |Test |Topic name. |
|Accumulation |Integer |1804832 |The total amount of messages piled up by the consumer group in this Topic. |


<span id="7de6de42"></span>
## EndpointObject

List of access points for the instance.

Referred to by the following interface:


* DescribeInstanceDetail



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|EndpointType |String |PLAINTEXT |The access point type of the instance. For a detailed description of access points, please refer to [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).<br><br>The types of access points provided by Kafka instances include:<br><br><br>* PLAINTEXT: Default access point.<br><br>* SASL_PLAINTEXT: SASL_PLAINTEXT access point.<br><br>* SASL_SSL: SASL_SSL access point. |
|NetworkType |String |PrivateNetwork |The network type of the access point. Unified as PrivateNetwork. |
|InternalEndpoint |String |kafka\-ap\-1dd\*\*\*.kafka.ibytepluses.com:9093 |Instance private network access domain name. |
|PublicEndpoint |String |kafka\-ap\-1ddx\*\*\*.kafka.bytepluses.com:9492 |Instance public network access domain name. When the instance does not open public network access, the public network access domain name is not provided. |


<span id="5266c461"></span>
## RegionObject

Referred to by the following interface:


* DescribeRegions



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|RegionId |String |ap\-southeast\-1 |Region ID. |
|RegionName |String |ap\-southeast\-1 |Area name. |
|Description |String |ap\-southeast\-1 |Region name. |
|Status |String |Available |Regional status.<br><br><br>* Available: Enabled. Users can view, create new resources and other actions in this region<br><br>* Unavailable: deactivated.<br><br><br>You cannot open a new service in the disabled region, but you cannot buy new products in this region. The opened service will still be supported until the service expires. |


<span id="9557927d"></span>
## ResetOffsetInfoObject

Consumption check point information that needs to be reset.

Referred to by the following interface.


* ResetConsumedOffsets



|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|TopicName |String |Yes |my_topic |Topic name.<br><br>When the parameter value is specified as "\*", it means to reset all partitions consumed by the Group. |
|PartitionId |Integer |No |3 |The partition number of the consumption check point needs to be reset.<br><br><br>* When no PartitionId is specified, resets all partitions under the specified Topic.<br><br>* Setting PartitionId is not supported when TopicName is specified as "\*". |
|ResetType |String |No |Offset |The way to reset the consumption check point, the default is Offset. Can be set to:<br><br><br>* Offset: (Default) Reset the consumption check point according to the specified offset, that is, the Group starts to consume from the specified check point in the current partition. At this time, the default is reset to the latest Offset, and the Offset can also be specified through the parameter ResetOffset.<br><br>* Timestamp: Reset the consumption check point according to the specified time, that is, select a time point from a specified time period in the past to start consumption. At this time, you need to set the time point through the parameter ResetTimestamp. |
|ResetOffset |Integer |No |\-2 |Reset the consumption point to the specified Offset. Only needs to be set when the ResetType is Offset. If this parameter is not specified, it means reset to the latest message location.<br><br>Value range:<br><br><br>* \-1: (Default) Resets the consumption check point to the latest message.<br><br>* \-2: Reset the consumption check point to the earliest message.<br><br>* Other integer values: Specifies to reset the consumption point to a specific Offset position in the specified partition of the specified Topic, and the value range is between the minimum Offset and the maximum Offset of the partition, that is, [StartOffset, EndOffset].<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">ResetOffset can be specified as other integer values only when specifying TopicName and PartitionId.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can view StartOffset and EndOffset by DescribeTopicPartitions.</div><br> |
|ResetTimestamp |Integer |No |1677502758825 |Resets the consumption point to the specified timepoint. timestamp format, in milliseconds. Only needs to be set if the ResetType is Timestamp.<br><br><br>* The consumption timestamp is the time the message is stored on the server.<br><br>* The resettable time range is determined by the message retention time of the Topic, that is, the value range of this parameter is [Current Time \- Instance Message Retention Time, Current Time].<br><br>* If no message exists at the specified time, it will be reset to the nearest message location. |


<span id="6ebad017"></span>
## TagFilterObject

Tag details, used to filter instances that contain this tag.

Referred to by the following interface:


* DescribeTagsByResource



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Key |String |Owner |The key of the label. |
|Value |String |Zhangsan |The value of the label. |


<span id="30605bc3"></span>
## TagObject

Tag details.

Referred to by the following interface:


* AddTagsToResource



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Key |String |Owner |The key of the label. |
|Value |String |Zhangsan |The value of the label. |


<span id="e509fd51"></span>
## TagResourceObject

Tag details.

Referred to by the following interface:


* DescribeTagsByResource



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |rocketmq\-cnai1f0c29ca\*\*\*\* |Instance ID. |
|Key |String |Key |The key of the instance tag. |
|Value |String |Value |The value of the instance tag. |


<span id="30e32a75"></span>
## ZoneObject

Referred to by the following interface:


* DescribeAvailabilityZones



|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ZoneId |String |ap\-southeast\-1a |Availability zone ID. |
|ZoneName |String |ap\-southeast\-1a |Availability zone name. |
|Description |String |Availability Zone A |The Chinese name of the regional availability zone. |
|Status |String |Normal |The state of the Availability Zone, including the following states:<br><br><br>* Normal: On sale.<br><br>* Soldout: sold out.<br><br>* Unavailable: deactivated.<br><br><br>You cannot start a new service in a deactivated availability area, but you cannot buy new products in this availability area. Opened services are still supported until the service expires. |
