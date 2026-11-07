---
title: "CreateGroup"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/CreateGroup-v2"
---

Call CreateGroup to create a ConsumerGroup.

**Instructions for use**

This interface is used to create a Kafka consumption group under the specified instance, which you can use for subscriptions.

**request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |Instance ID. |
|GroupId |String |Yes |my_group |The consumer group ID to be created.<br><br><br>* The length is 3 to 128 characters.<br><br>* Contains only uppercase and lowercase letters, numbers, hyphens (\-), special characters (@), and underscores (_).<br><br>* Contains at least one letter or number. |
|Description |String |No |Test |Consumer group description information. Length should not exceed 128 characters. |


**response parameter**

None

**example**

**Request example**

```JSON
POST /?Action=CreateGroup&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "InstanceId": "kafka-cnngbnntswg1****",
    "GroupId": "my_group",
    "Description": "test"
}
```


**Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023022719194098F0DF73611FD95FA1A2",
        "Action": "CreateGroup",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
