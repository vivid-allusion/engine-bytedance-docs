---
title: "ModifyTopicAttributes"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyTopicAttributes-v2"
---

Call the ModifyTopic interface to modify the description of the Topic.

<span id="5c1f8ab6"></span>
## **Instructions for use**

After creating an instance, you can call this interface to adjust the description information of the Topic.

<span id="4e61a2e0"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |The instance ID of the Topic. |
|TopicName |String |Yes |my_topic |The name of the Topic. Modifying the TopicName is not supported after the Topic is created. |
|Description |String |No |New\-describe |Modify the description of the Topic. |


<span id="f175358f"></span>
## **response parameter**

None

<span id="d8a6e246"></span>
## **example**

<span id="7700f208"></span>
### **Request example**

```JSON
POST /?Action=ModifyTopicAttributes&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnngbnntswg1****",
  "TopicName":"httptopic",
  "Description":"topic for http module"
}
```


<span id="69218d97"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230227194819ABF4BF3AE0C5F76CECDD",
        "Action": "ModifyTopicAttributes",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
