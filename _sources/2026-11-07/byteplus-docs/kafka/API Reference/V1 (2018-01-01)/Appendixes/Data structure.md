---
title: "Data structure"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Data-structure-v1"
---

<span id="5aa1922a"></span>
## Authority

User permissions.

Referred to by the following interface.


* CreateTopic

* DescribeTopicAuthorities

* ModifyTopicAuthorities



|**parameter** |**parameter type** |**Required** |**sample value** |**explain** |
|---|---|---|---|---|
|Name |String |Required |Test |User name. |
|Permission |String |Required |Read |The user's access rights to the current Topic.<br><br><br>* Read: read only.<br><br>* Write: write only.<br><br>* ReadWrite: read and write. |
|Operator |String |Optional |Remove |Add or remove ACL configurations.<br><br><br>* Set: Add ACL permission configuration.<br><br>* Remove: Delete the ACL permission configuration.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is not required in the CreateTopic interface.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">ModifyTopicAuthorities interface, this parameter is required.</div><br> |


<span id="9626a934"></span>
## BasicChargeInfo

Billing information for the instance.

Referred to by the following interface.


* DescribeInstanceDetail



|**parameter** |**parameter type** |**sample value** |**explain** |
|---|---|---|---|
|ChargeType |String |PrePaid |The billing type of the instance.<br><br><br>* PostPaid: Billed by volume. |
|ChargeSubType |String |Monthly |The unit of time specified at the time of purchase of the monthly subscription instance.<br><br><br>* Monthly: Purchased on a monthly basis.<br><br>* Yearly: Purchased annually. |
|OverdueTime |Integer |0 |Package year Package month Instance expiration time. Unix timestamp, in seconds. |
|CreatedTime |Integer |0 |Instance creation time. Unix timestamp in seconds. |
|ChargeStatus |String |Normal |Instance order status.<br><br><br>* Normal: normal charge<br><br>* Unpaid: Pending payment<br><br>* Overdue: expired<br><br>* Expired: released<br><br>* Reclaimed: Reclaimed |
|StopTime |Integer |0 |Instance shutdown time. Unix timestamp in seconds. |
|RecycleTime |Integer |0 |Instance expiration recovery time. Unix timestamp, in seconds. |
|AutoReNew |Bool |True |Whether to renew automatically.<br><br><br>* True: auto\-renewal<br><br>* False: Manual renewal is required before expiration |
|OrderId |String |Order\-xxxxxxx |Instance Order ID. |


<span id="39bfa643"></span>
## CreateChargeInfo

Billing information for the instance.

Referred to by the following interface.


* CreateKafkaInstance



|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|ChargeType |String |Required |PostPaid |The billing type of the instance. Supported settings are:<br><br><br>* PostPaid: Billed by volume. |
|ChargeSubType |String |Required |1 |The unit of time for the subscription month instance purchase. Support settings are:<br><br><br>* Monthly: Purchased on a monthly basis.<br><br>* Yearly: Purchased annually. |
|ChargeUnitNum |Integer |Required |1 |The number of hours purchased. Valid only when the billing type is annual and monthly, i.e. ChargeType is specified as `PrePaid`. |
|AutoReNew |Bool |Required |10 |Whether it is automatically renewed, it must be passed on every year and every month. |
|PartitionOfBuy |Integer |Optional |900 |The number of partitions for Kafka instances, please set the number of partitions reasonably according to business needs.<br><br>Different specifications provide different numbers of free partition credits, and the part exceeding the free quota will be charged an additional partition fee. Please refer to the range of the number of partitions that can be created in each specification [Specifications](https://docs.byteplus.com/en/docs/kafka/specifications) please refer to the billing method of the partition [Billing items](https://docs.byteplus.com/en/docs/kafka/billable-items). |


<span id="58ac6bfa"></span>
## ConsumedPartition

Consumed partition information.

Referred to by the following interface.


* DescribeConsumedPartitions



|**parameter** |**parameter type** |**explain** |
|---|---|---|
|PartitionNumber |Integer |Topic partition number. |
|ConsumedClient |String |The information for the partition consumer, specified by the client side when consuming, may be empty here. |
|ConsumedOffset |Integer |Division consumption progress. |
|StartOffset |Integer |The earliest message offset for the partition. |
|EndOffset |Integer |Partitioning the offset of the next message. |
|Accumulation |Integer |The amount of message accumulation for the consumption group on the partition. |


<span id="ccef3949"></span>
## ConsumedTopic

List of Topics Consumed.

Referred to by the following interface.


* DescribeConsumedTopics



|**parameter** |**parameter type** |**explain** |
|---|---|---|
|TopicName |String |Topic name. |
|Accumulation |Integer |The total amount of messages piled up by the consumption group in this Topic. |


<span id="97db8152"></span>
## DataItem

Availability zone information.

Referred to by the following interface.


* ListKafkaConf



|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|ID |String |Required |ap\-southeast\-1a |Availability zone ID. |
|Value |String |Required |ap\-southeast\-1a |Availability zone name. |
|Desc |String |Required |Availability Zone A:ap\-southeast\-1a |Availability zone description information. |
|IsSoldOut |Bool |optional |False |Whether the resources in the current Availability Zone have been sold out. |


<span id="0c9a2674"></span>
## EndpointInfo

List of Kafka access points.

Referred to by the following interface.


* DescribeInstanceDetail



|**parameter** |**parameter type** |**explain** |
|---|---|---|
|EndpointType |String |The connection type accessed by the instance.<br><br><br>* Private: Private network VPC access.<br><br>* Internet: Public network access. |
|EndpointProtocol |String |The protocol types accessed by the instance, including:<br><br><br>* PLAINTEXT: Default access point.<br><br>* SASL_PLAINTEXT: SASL access point. |
|AccessAddress |String |The access point for the Kafka instance. |


<span id="ef05e84d"></span>
## InstanceBasicInfo

List of instance basic information.

Referred to by the following interface.


* DescribeInstancesSummary



|**parameter** |**parameter type** |**sample value** |**explain** |
|---|---|---|---|
|InstanceId |String |Kafka\- \*\*\*\* |Instance ID. |
|InstanceName |String |Kafka\-test |Instance name. |
|Status |String |Running |Instance state. |
|AvaliableZones |List |*  |Availability zone information to which the instance belongs. |
|UsedTopicNumber |Integer |20 |The number of Topics created by the current instance. |
|UsedGroupNumber |Integer |20 |The number of consumer groups that the current instance has created. |
|AccountId |Integer |0 |The user account ID to which the instance belongs. |
|CreateTime |String |2021\-12\-14 18:26:56 |Instance creation time. The format is "YYYY\-MM\-DDTHH: mm: ss + 08:00". |
|KafkaSpecifications |String |Kafka.n3.x2. small |The specification name of the instance purchase. |
|Description |String |Here's a test case. |Instance description information. |
|VpcInfo |VpcInfo |*  |Network access information for the instance. |
|ProjectName |String |Test |The name of the project to which the user belongs. Empty if there is no project. |
|KafkaChargeInfo |BasicChargeInfo |*  |Billing information for the instance. |


<span id="9ab353a2"></span>
## InstanceSpec

Specification details for Kafka instances.

Referred to by the following interface.


* ListKafkaConf



|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|PartitionNum |Integer |Required |300 |Number of partitions. |
|DiskIncStep |Integer |Required |100 |Disk growth step, in GiB. |
|DiskMinSize |Integer |Required |1500 |Minimum disk capacity in gigabytes. |
|DiskMaxSize |Integer |Required |30000 |Maximum disk capacity in GiB. |
|SpecName |String |Required |Kafka.n3.x2. small |Specification name. |
|IsSoldOut |Map < String, Bool \> |optional | |The rule specifies whether the availability zone has been sold out. |
|ElasticIpNumber |Integer |optional |3 |The number of Elastic IPs (EIPs) required for this specification if public access is enabled. |


<span id="e08123af"></span>
## KafkaParam

Parameters related to the Kafka instance.

Referred to by the following interface.


* DescribeInstanceDetail



|**parameter** |**parameter type** |**sample value** |**explain** |
|---|---|---|---|
|Name |String |max_message_length |Parameter name. |
|DefaultValue |String |10 |Default values for parameters. |
|RunningValue |String |5 |Parameter run value. |
|Description |String |Maximum message length that a Kafka instance can write to |Parameter description. |
|Restart |Bool |True |Modifying the parameter state requires restarting the instance. |
|ParamType |String |int |The data type of the parameter. |
|ValueRange |String |0\-10 |The value range of the parameter, the parameter of type string does not support displaying the value range for the time being. |
|Unit |String |MB |The unit of measure for the parameter. |


<span id="11732ee2"></span>
## KafkaMessage

The content of the message found.

Referred to by the following interface.


* QueryMessageByMessageId



|**parameter** |**parameter type** |**sample value** |**explain** |
|---|---|---|---|
|InstanceId |String |Kafka\- \*\*\*\* |Instance ID. |
|TopicName |String |Test |Topic name. |
|Partition |Integer |0 |The partition number. |
|MessageOffset |Integer |0 |The number (offset) of the message in the partition. |
|MessageSize |Integer |1024 |Message size, in bytes. |
|CreateTime |Integer |*  |Message write time. |
|Key |String |*  |Message Key field. |
|Body |String |*  |Message content. In order to avoid the influence of special characters, the message content will be returned in Base64 encoding, which needs to be decoded by Base64 before viewing. |


<span id="5216d563"></span>
## Param

Parameter configuration items open by Kafka instances.

Referred to by the following interface.


* ListKafkaConf



|**parameter** |**parameter type** |**sample value** |**explain** |
|---|---|---|---|
|Name |String |max_message_length |Parameter name. |
|DefaultValue |String |10 |Default values for parameters. |
|RunningValue |String |5 |Parameter run value. |
|Description |String |Maximum message length that a Kafka instance can write to |Parameter description. |
|Restart |Bool |True |Modifying the parameter state requires restarting the instance. |
|PType |String |int |The data type of the parameter. |
|ValueRange |String |0\-10 |The value range of the parameter, the parameter of type string does not support displaying the value range for the time being. |
|Unit |String |MB |The unit of measure for the parameter. |


<span id="6f1bd553"></span>
## ResetOffset

Consumption check point information that needs to be reset.

Referred to by the following interface.


* ResetConsumedOffsets



|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|TopicName |String |Required |my_topic |Topic name.<br><br>When the field value is specified as "\*", it resets all partitions consumed by the Group. |
|PartitionNumber |Integer |Optional |3 |The partition number of the consumption check point needs to be reset.<br><br>Setting PartitionNumber is not supported when TopicName is specified as "\*". Resets all partitions under the specified TePic when PartitionNumber is not specified. |
|ResetType |String |Optional |Offset |The way to reset the consumption check point can be set to:<br><br><br>* Offset: Specify the check point for consumption reset. When not specified, this is the default method.<br><br>* Timestamp: Specify the time for consumption reset. |
|ResetValue |Integer |Optional |\-2 |The location where the consumption check point is reset.<br><br><br>* When this parameter is not specified, it means reset to the latest message location.<br><br>* If ResetType is set to Offset, ResetValue is used to specify the consumption check point, which can be set to:<br><br>   * \-2: Reset the consumption check point to the earliest message.<br><br>   * \-1: Reset the consumption check point to the latest message.<br><br>   * Custom location: The value cannot be greater than the partition EndOffset, and cannot be less than the partition's StartOffset. Custom Offset is only supported if both TopicName and PartitionNumber are specified.<br><br>* If ResetType is set to Timestamp, ResetValue is used to specify the consumption timestamp in the format of Unix timestamp, accurate to the second.<br><br>   * The consumption timestamp is the time the message is stored on the server.<br><br>   * The minimum value is the current time \- the retention time of the instance message, and the maximum time is the current time<br><br>   * If no message exists at the specified time, it will be reset to the nearest message location. |


<span id="75252527"></span>
## StandardGroupInfo

Group basic information.

Referred to by the following interface.


* DescribeGroups



|**parameter** |**parameter type** |**explain** |
|---|---|---|
|GroupId |String |Consumer group ID. |
|InstanceId |String |Instance ID. |
|State |String |Consumer group status.<br><br><br>* PreparingRebalance: Consumption preparation<br><br>* CompletingRebalance:<br><br><br>in the allocated partition<br><br><br>* Stable: Consuming<br><br>* Empty: not consumed<br><br>* Dead: expired |


<span id="6e4fbff5"></span>
## StandardSaslUserInfo

Group basic information.

Referred to by the following interface.


* DescribeSaslUsers



|**parameter** |**parameter type** |**explain** |
|---|---|---|
|UserName |String |SASL user name. |
|CreateTime |String |The creation time of the SASL user. |
|Description |String |SASL user description information. |
|AllAuthority |Bool |Does this user have read and write permissions for all topics?<br><br><br>* True: have.<br><br>* False: not available. |
|PasswordType |String |Password type.<br><br><br>* Plain: Plain type.<br><br>* Scram: Scram type. |


<span id="7ae23fc5"></span>
## StandardTopicInfo

List of Topics that meet the query criteria.

Referred to by the following interface.


* DescribeTopics



|**parameter** |**parameter type** |**explain** |
|---|---|---|
|Name |String |Topic name. |
|Description |String |Topic Description. |
|InstanceId |String |Instance ID. |
|CreateTime |String |Topic creation time. |
|UpdateTime |String |Topic update time. |
|PartitionNumber |Integer |Number of partitions. |
|Status |String |Topic status.<br><br><br>* Fault: exception<br><br>* Downgrade: downgrade<br><br>* ExpandPartition: Partition expansion<br><br>* ExpandReplica: replica expansion in progress<br><br>* Sync: Synchronizing<br><br>* Running: Running normally<br><br>* Creating: Creating |
|ReplicaNumber |Integer |Number of Topic Copies. |
|MinInsyncReplicaNumber |Integer |Topic Minimum number of synchronous replicas. |
|RetentionHour |Integer |The amount of time the message is retained. The unit is hours. |
|MaxMessageMegabyte |Integer |Maximum message size. The unit is MB. |
|Region |String |Topic area.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter to be offline, please ensure that there is no business logic dependent on this parameter in the relevant business.</div><br> |


<span id="b7096db1"></span>
## StandardPartitionInfo

List of partitions that meet the query criteria.

Referred to by the following interface.


* DescribeTopicPartitions



|**parameter** |**parameter type** |**explain** |
|---|---|---|
|PartitionNumber |Integer |The partition number. |
|Leader |Integer |Division Leader Number. |
|Replicas |List |List of replicas of the partition. |
|InsyncReplicas |List |List of synchronized replicas of the partition. |
|UnderInsyncReplicas |List |List of unsynchronized replicas. |
|StartOffset |Integer |The offset of the current earliest message for the partition Leader. |
|EndOffset |Integer |The offset of the next message from the Partition Leader.<br><br>This parameter is defined as the offset of the next message, then the position of the current latest message is EndOffset \- 1. |
|MessageCount |Integer |The current number of messages in the partition Leader.<br><br>EndOffset is the offset of the next message, so MessageCount=EndOffset\-StartOffset. |


<span id="3374e0d4"></span>
## SupportZoneInfo

Details of supported Availability Zones.

Referred to by the following interface.


* ListKafkaConf



|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|Zone |JSON Array |Required |*  |Availability zone information. Please refer to DataItem for details. |


<span id="c4101c17"></span>
## UpdateInstanceParamItem

Parameters related to the Kafka instance.

Referred to by the following interface.


* CreateKafkaInstance

* ModifyInstanceParams



|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|Name |String |Required |max_byte |Parameter name. For detailed parameter meaning and description, please refer to [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter) parameters that support setting include:<br><br><br>* MessageMaxByte: Maximum message size.<br><br>* LogRetentionHours: Message retention duration.<br><br>* OffsetRetentionMinutes: Spend check point retention time.<br><br>* LogAutoDeletion: Automatically delete old messages. |
|RunningValue |String |Required |1 |Parameter values. Different parameters have different value ranges:<br><br><br>* MessageMaxByte: The unit is MB, and the value range is 1 to 12.<br><br>* LogRetentionHours: The unit is hours, and the value range is 0~ 2160, that is, the message is retained for a maximum of 90 days.<br><br>* OffsetRetentionMinutes: The unit is minutes, and the value range is 1~ 10080, that is, the consumption check point is retained for a maximum of 7 days.<br><br>* LogAutoDeletion: 0 means off, 1 means on. |


<span id="0d2fb1b2"></span>
## VPCInfo

Network access information for the instance.

Referred to by the following interface.


* CreateKafkaInstance

* DescribeInstanceDetail



|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|ID |String |Required |vpc\-testtesttest |VPC ID. |
|Name |String |Required |Kafka\-test |VPC name. |
|SubnetId |String |Required |Subnet\-xxxxxxxxxx |VPC subnet ID. |
|EipIds |List < String \> |Optional |[Eip \- ** *, Eip \-* ** ]\* n |Elastic network interface card ID, i.e. EIP ID.<br><br>When calling the interface CreateKafkaInstance to create an instance, the parameter EipIds is not supported for the time being. If you need to enable public network access, please call the interface EnableInternetAccess after creating the instance. |


<span id="e09d7954"></span>
## Zone

Availability zone information where the Kafka instance is located.

Referred to by the following interface.


* DescribeInstanceDetail



|**parameter** |**parameter type** |**sample value** |**explain** |
|---|---|---|---|
|ZoneId |String |ap\-southeast\-1a |Availability zone ID. |
|ZoneIdInChinese |String |Availability Zone A:ap\-southeast\-1a |The Chinese name of the Availability Zone. |
