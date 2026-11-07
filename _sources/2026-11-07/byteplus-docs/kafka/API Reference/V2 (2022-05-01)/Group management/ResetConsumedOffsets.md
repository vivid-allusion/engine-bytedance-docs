---
title: "ResetConsumedOffsets"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ResetConsumedOffsets-v2"
---

Call ResetConsumedOffsets reset the consumption check point of the consumer group.

<span id="04399484"></span>
## **Instructions for use**

This interface is used to reset the consumption check point of the specified consumption group, change the current consumption position of the subscriber, that is, directly from a specified time point, the latest offset check point or the specified offset check point to consume messages.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Message queue Kafka version does not support online resetting of consumption check points. Before resetting consumption check points, all consumer client sides in the Consumer Group must be stopped to ensure that the status of the Group is Empty.</div>


* <div data-tips="true" data-tips-type="tip">After stopping the consumer client side, the server level needs to pass the specified timeout time before it considers the Consumer to be truly offline. The timeout time is <code>ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG</code> Configured time, default 10000ms.</div>



<span id="c1b7aca9"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\*x |The instance ID of the consumption check point needs to be reset. |
|GroupId |String |Yes |my_group |The consumption group ID of the consumption check point needs to be reset. |
|ResetOffsetsInfo |Array of ResetOffsetInfoObject |Yes |/ |Consumption check point information that needs to be reset. For details, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) ResetOffsetInfoObject part in. |


<span id="d79947cb"></span>
## **response parameter**

None

<span id="2fb0f3b6"></span>
## **example**

<span id="ef4c0561"></span>
### **Request example**

```JSON
POST /?Action=ResetConsumedOffsets&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnng1si21igu****",
  "GroupId":"Group",
  "ResetOffsetsInfo": {
      "TopicName": "test",
      "PartitionId":0,
      "ResetType": "Offset",
      "ResetOffset": -1
  }
}
```


<span id="e62180f9"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230227211906E9F948120F87D27F1AEE",
        "Action": "ResetConsumedOffsets",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
