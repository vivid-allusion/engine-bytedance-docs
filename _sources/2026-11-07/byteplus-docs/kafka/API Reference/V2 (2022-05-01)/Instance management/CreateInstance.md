---
title: "CreateInstance"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/CreateInstance-v2"
---

Call CreateInstance to create a message queue Kafka instance.

<span id="cf64f3db"></span>
## Instructions for use

The instance is the virtual machine resource of the message queue Kafka Edition service, which is used to manage and store resources such as Topic and Group.

<span id="4bd4c7d6"></span>
## Precautions


* If you are creating a Kafka instance for the first time, you need to complete cross\-service access authorization first. It is recommended to operate through the Byteplus Engine main account. For detailed instructions, please refer to [Cross-service access authorization](https://docs.byteplus.com/en/docs/kafka/cross-service-authorization).

* If you need to access the message queue Kafka Edition instance over a private network, first create the ECS Cloud as a Service, private network, and subnet in the same region. After creating an instance, you cannot change the private network and subnet where the instance is located.

* If you need to access the message queue Kafka version instance through the public network, please apply for the EIP of the same region first.

* By default, you can create 8 Kafka instances in each region, and the total storage capacity of all instances in each region for each account is up to 90 TiB. Otherwise, an error message "**The instance_num/storage_sum has exceeded quota**" will be displayed when creating an instance. If you need to increase the quota, please submit an application in the Quota Center, such as applying to increase the maximum number of instances (InstanceNum) in each region, which can be adjusted up to 16.


<span id="8277e692"></span>
## Request parameters


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|ZoneId |String |Yes |ap\-southeast\-1a |The ID of the Availability Zone where the instance is located.<br><br>Message queue Kafka Edition instances support cross\-AZ deployments. You can specify multiple Availability Zones when viewing which compute specifications are available under Specify Availability Zones. Multiple Availability Zones are separated by comma (,) IDs.<br><br>You can call [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/kafka/DescribeAvailabilityZones-v2) Query the list of availability zones currently served. |
|Version |String |Yes |2.2.2 |Supported Kafka versions. Currently supported versions include:<br><br><br>* 2.2.2: Kafka 2.2.2 version.<br><br>* 2.8.2: Kafka 2.8.2 version. |
|ComputeSpec |String |Yes |Kafka.20xrate.hw |The calculation specification of the instance.<br><br>For the list of calculation specifications provided by the Message Queuing Kafka Edition instance, please refer to [Specifications](https://docs.byteplus.com/en/docs/kafka/specifications). |
|VpcId |String |Yes |vpc\-13fo9gkz6j6683n6nu5ec\*\*\*\* |The VPC ID of the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After the instance is created, the corresponding private network cannot be modified. Please exercise caution when creating an instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the DescribeVpcs interface of the private network (VPC) to query the list of available VPCs and subnets.</div><br> |
|SubnetId |String |Yes |subnet\-min6uy01kuf45smt1a2i\*\*\*\* |The VPC subnet ID of the instance.<br><br>You can call the DescribeVpcs interface of the private network (VPC) to query the list of available VPCs and subnets. |
|ChargeInfo |ChargeInfoObject |Yes |/ |Billing information such as the billing type of the Kafka instance. For details, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) The ChargeInfoObject section of the document. |
|UserName |String |No |Test1 |SASL/PLAIN username. The following requirements should be met:<br><br><br>* Consists of letters, numbers, hyphens (\-), or underscores.<br><br>* The length is 3 to 64 characters.<br><br>* The user name is not supported to be set to admin or monitor, and the user name is unique within the instance. |
|UserPassword |String |No |Test@123456 |The password of the SASL/PLAIN user. The following requirements should be met:<br><br><br>* The length is 8 to 32 characters.<br><br>* It should contain at least any three of uppercase letters, lowercase letters, numbers, and special characters.<br><br>* Special characters supported include`!@#$%^&*()_+-=`. |
|StorageSpace |Integer |No |1000 |The storage space for the instance.<br><br>The unit is GiB and must be specified as a multiple of 100. The range of values depends on the currently specified calculation specification. |
|StorageType |String |No |ESSD_PL0 |The cloud disk type of Kafka instance data storage. Can be set to ESSD_FlexPL or ESSD_PL0, the default is ESSD_FlexPL.<br><br><br>* For specifications with peak traffic exceeding 100MB/s, ESSD_FlexPL should be used.<br><br>* Modifying the storage type is not supported after creating an instance, please choose carefully. |
|PartitionNumber |Integer |No |1000 |Number of partitions. The range of values depends on the currently specified calculation specification.<br><br>Different specifications provide different numbers of free partition credits, and the part exceeding the free quota will be charged an additional partition fee. Please refer to the range of the number of partitions that can be created in each specification [Specifications](https://docs.byteplus.com/en/docs/kafka/specifications) Please refer to the billing method of the partition [Billing items](https://docs.byteplus.com/en/docs/kafka/billable-items). |
|EipId |String |No |eip\-mjhulvqza6805smt1bnc\*\*\*\* |The ID of the EIP.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Specifying EipId means enabling public network access for the instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">EIP provides independent public network IP resources, including public network Internet Protocol Address and public network egress bandwidth service. After specifying this parameter to enable public network access, the public network address will be bound to your Elastic Public Network IP (EIP), and the fee will be charged by EIP.</div><br> |
|InstanceName |String |No |Name123 |The name of the Kafka instance. The following requirements should be met:<br><br><br>* Contains only Chinese, letters, numbers, underscores (_) and hyphens (\-).<br><br>* Cannot start with a number or a hyphen (\-).<br><br>* The length range is 1 to 128 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If no name is specified when the instance is created, the instance ID is used as the instance name by default.</div><br> |
|InstanceDescription |String |No |Instance for testing |A brief description of a Kafka instance. Length ranges from 1 to 128 characters. |
|Parameters |String |No |"{" MessageMaxByte ":" 10 "," LogRetentionHours ":" 72 "," OffsetRetentionMinutes ":" 4320 "}" |Initial parameter configuration for the Kafka instance.<br><br>For the current list of supported parameters and their default values, please refer to the following table Parameters parameter descriptionYou can also pass [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter) View the details of each parameter.<br><br>When calling the API through Mail carrier, etc., you should pay attention to escaping, such as`{\"LogRetentionHours\":\"72\",\"MessageMaxByte\":\"10\",\"MessageTimestampType\":\"CreateTime\",\"OffsetRetentionMinutes\":\"4320\"}`. |
|ProjectName |String |No |NewProject |The IAM project to which the currently created Kafka instance belongs. If no IAM project is specified, the message queue Kafka Edition will add the new instance to the `default` In the IAM project. |
|Tags |Map < String, String \> |No | |Cloud resource tags. Instances can be classified by tags to facilitate instance search and resource aggregation. For detailed instructions, please refer to [Tag overview](https://docs.byteplus.com/en/docs/kafka/tag-overview). |
|IpWhiteList |Array of String |No | |List of whitelisted IDs to which the instance is bound. After binding the whitelist, only the IP addresses and address segments configured in the whitelist can access this instance. If this parameter is not set, the new Kafka instance will be bound to the whitelist `default`The corresponding IP address is 0.0.0.0, indicating that all addresses are allowed to access the Kafka instance. |
|ClientToken |String |No |123e4567\-e89b\-12d3\-a456\-426655440000 |An identifier that guarantees client side request idempotency.<br><br>The identifier is a 1\-64\-bit ASCII string, case\-sensitive, generated by the client side, and should ensure that the identifier is unique between different requests.<br><br>How to use the idempotent flag, please refer to [Request Idempotence](https://docs.byteplus.com/en/docs/kafka/Request-Idempotence-v2). |


Parameters parameter description


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|MessageMaxByte |String |No |12 |Maximum message size.<br><br>The unit is MB, and the value range is 1 to 12. Default is 10. |
|LogRetentionHours |String |No |2160 |Message retention duration.<br><br>The unit is hours, and the value range is 0~ 2160, that is, the message is retained for a maximum of 90 days. The default is 72. |
|OffsetRetentionMinutes |String |No |10080 |Spend check point retention time.<br><br>The unit is minutes, and the value range is 1~ 10080, that is, the consumption check point is retained for a maximum of 7 days. The default is 4320. |
|MessageTimestampType |String |No |LogAppendTime |Message time type, supported setting is:<br><br><br>* LogAppendTime: The time the message was written to the server.<br><br>* CreateTime: (Default) The time the Producer created the message. |
|AutoDeleteGroup |String |No |False |Whether to automatically delete Groups. Defaults to false.<br><br><br>* True: If all consumers in a consumer group are Empty, the backend service will automatically delete the consumer group after the consumption check point retention period is exceeded.<br><br>* False: The automatic deletion of the consumption progress does not affect the status of the consumption group, and the group in the Empty state will not be automatically deleted. |


<span id="6bcf56fb"></span>
## **response**Parameter


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|InstanceId |String |kafka\-cnngqkfgdudt\*\*\*\* |Kafka instance ID. |
|OrderId |String |order\-712089661643355\*\*\*\* |Order ID. |


<span id="ea6eaaa8"></span>
## Example

<span id="a8f2689a"></span>
### Request example

```JSON
POST /?Action=CreateInstance&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "ZoneId": "ap-southeast-1a",
  "Version": "2.2.2",
  "ComputeSpec": "kafka.20xrate.hw",
  "VpcId": "vpc-rs4yccs57e9sv0x57bf****",
  "SubnetId": "subnet-rrps5hvr1bswv0x58fp****",
  "UserName": "kafka2001",
  "UserPassword":"Test@123456",
  "ChargeInfo": {
    "ChargeType": "PrePaid",
    "AutoRenew": true,
    "PeriodUnit": "Month",
    "Period": 1
  }
}
```


<span id="1bf83ac7"></span>
### **response**Example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202302271904532FE25613615E5671AB07",
        "Action": "CreateInstance",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "kafka-cnngbnntswg1****",
        "OrderId": "Order720478931462498****"
    }
}
```
