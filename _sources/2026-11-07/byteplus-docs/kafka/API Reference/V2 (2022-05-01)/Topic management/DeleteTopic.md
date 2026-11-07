---
title: "DeleteTopic"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DeleteTopic-v2"
---

Call the DeleteTopic interface to delete the Kafka Topic.

<span id="55152ae4"></span>
## **Instructions for use**

This interface will delete the related resources of the Topic under the instance. After the Topic is deleted, it cannot be restored. Please call carefully.

<span id="822b39f9"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\*x |The instance ID to which the Topic belongs to be deleted. |
|TopicName |String |Yes |my_topic |The name of the Topic to be deleted. |


<span id="3ca72a78"></span>
## **response parameter**

None

<span id="2dfdc4bb"></span>
## **example**

<span id="774ba8d9"></span>
### **Request example**

```JSON
POST /?Action=DeleteTopic&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnngbnntswg1****",
  "TopicName":"123"
}
```


<span id="0a859387"></span>
## **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202302271945402D353B4989FAFE7476F1",
        "Action": "DeleteTopic",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
