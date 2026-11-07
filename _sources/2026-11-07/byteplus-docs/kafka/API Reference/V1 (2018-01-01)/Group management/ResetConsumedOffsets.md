---
title: "ResetConsumedOffsets"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ResetConsumedOffsets-v1"
---

Call ResetConsumedOffsets reset the Offset consumed by the consumer group.

<span id="c890fda6"></span>
## Instructions


* ResetConsumedOffsets interface is used to reset the consumption Offset of the consumer group in a partition. Resetting the offset may cause repeated consumption. Please be careful.

* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="2bb4532c"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Yes |Kafka\- \*\*\* x |The instance ID of the consumption check point needs to be reset. |
|GroupId |String |Yes |my_group |The consumption group ID of the consumption check point needs to be reset. |
|Offsets |List |Yes |my_group |Consumption check point information that needs to be reset. For details, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |


<span id="ce76b1a5"></span>
## Response parameter

None

<span id="c1152226"></span>
## Example

<span id="53967357"></span>
### Request example

```json
POST /?Action=ResetConsumedOffsets&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-****x",
  "GroupId": "my_group",
  "Offsets": [
    {
      "TopicName": "my_topic",
      "PartitionNumber": 3,
      "ResetType": "Timestamp",
      "ResetValue": 1628782942
    }
  ]
}
```


<span id="f0493585"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "ResetConsumedOffsets",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
