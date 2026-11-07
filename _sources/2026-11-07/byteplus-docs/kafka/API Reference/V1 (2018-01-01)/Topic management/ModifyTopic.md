---
title: "ModifyTopic"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyTopic-v1"
---

Call the ModifyTopic interface to modify the configuration of the Topic.

<span id="e724279f"></span>
## Instructions for use

This interface is used to adjust the configuration of Topic partitions, minimum number of synchronization replicas, etc., and can also modify parameter configurations such as message retention time.


* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="724a2d18"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\*\* |The instance ID of the Topic. |
|TopicName |String |Required |my_topic |The name of the Topic. Modifying the TopicName is not supported after the Topic is created. |
|PartitionNumber |Integer |Optional |12 |The number of partitions of the Topic.<br><br>When modifying the number of partitions, only increasing the number of partitions is supported, not reducing the number of partitions. |
|MinInsyncReplicaNumber |Integer |Optional |2 |The minimum number of simultaneous replicas of the Topic.<br><br>Minimum 1 and maximum \-1 replicas. |
|RetentionHour |Integer |optional |144 |The retention time of the message, the value range is 0 to 2160, and the unit is hours. |
|MaxMessageMegabyte |Integer |optional |1 |Maximum message size, values range from 1 to 12, in MiB. |
|Description |String |optional |new\-describe |Description of the Topic. |


<span id="f83b39d0"></span>
## Response parameter

null

<span id="2fcd4359"></span>
## Example

<span id="b9daf718"></span>
### Request example

```json
POST /?Action=ModifyTopic&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-****",
  "TopicName": "my_topic",
  "PartitionNumber": 12,
  "MinInsyncReplicaNumber": 2,
  "RetentionHour": 144,
  "MaxMessageMegabyte": 1,
  "Description": "new-describe"
}
```


<span id="6e94b673"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "ModifyTopic",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
