---
title: "CreateTopic"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/CreateTopic-v1"
---

Create a Kafka Topic using the CreateTopic interface.

<span id="091fe8ef"></span>
## Instructions for use

This interface is used to create a Kafka Topic under a specified instance, which users can use to publish and subscribe to messages.


* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="96c35096"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\* x |Instance ID. |
|TopicName |String |Required |my_topic |The name of the Topic to be created. The following naming conventions must be followed:<br><br><br>* The length is 3 to 64 characters.<br><br>* Can only start with English or numbers.<br><br>* Supported characters include English letters, numbers, hyphens (\-), underscores (_), and periods (.). |
|AllAuthority |Bool |Optional |True |Whether the topic to be created has read and write permissions enabled for all users by default.<br><br><br>* True: All users have read and write access to this Topic.<br><br>* False: Not all users have read and write permissions for this topic. By default, the user's permissions for this topic follow the user's default permissions. If the default permissions do not meet the requirements, you can also specify a user's custom permissions for this topic through Authorities. |
|Authorities |List |optional |*  |Custom permission configuration, that is, set custom permissions for this Topic for some users. This is only required when AllAuthority is false. For details, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |
|Description |String |optional |Description information |Description information of the Topic. Length should not exceed 128 characters. |
|PartitionNumber |Integer |Required |12 |Number of Topic partitions. The range of values is 1~ 300, and the default is 12. If other Topics have been created in the instance, the sum of the partitions of all Topics does not exceed the upper limit of the number of partitions of the instance.<br><br>If the number of partitions cannot meet the business needs, you can buy more partitions to increase the upper limit of the number of partitions of the instance. For detailed instructions, please refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications). |
|ReplicaNumber |Integer |optional |3 |Number of Topic replicas. The value range is 2 or 3, the default value is 3. |
|MinInsyncReplicaNumber |Integer |Optional |2 |The minimum number of synchronous replicas of the Topic.<br><br>When the number of synchronous replicas is less than the configuration value, the message will not be written to the corresponding Topic. The larger the configuration value, the data reliability will increase, but the availability will decrease. The default value is \-1 replicas. Considering the availability of Topics, it is recommended to set it to \-1 replicas.<br><br>For details, please refer to [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter). |
|RetentionHour |Integer |Optional |144 |The time the message is retained.<br><br>values range from 0 to 2160, and the parameter unit is hours. The default is 72 hours. For details, please refer to [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter). |
|MaxMessageMegabyte |Integer |optional |3 |The maximum message size that can be received, the value range is 1 to 12, the unit is MiB, and the default value is 10. For details, please refer to [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter). |


<span id="dc0162a5"></span>
## Response parameter

null

<span id="7da4682f"></span>
## Example

<span id="78494290"></span>
### Request example

```json
POST /?Action=CreateTopic&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "TopicName": "test-plb1",
  "AllAuthority": false,
  "Authorities": [
    {
      "Name": "test",
      "Permission": "Read"
    }
  ],
  "ReplicaNumber": 3,
  "MinInsyncReplicaNumber": 2,
  "RetentionHour": 144,
  "MaxMessageMegabyte": 3,
  "InstanceId": "kafka-*****",
  "Description": "test",
  "PartitionNumber": 12
}
```


<span id="526e30c3"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "CreateTopic",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
