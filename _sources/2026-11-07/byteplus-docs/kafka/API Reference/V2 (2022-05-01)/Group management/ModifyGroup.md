---
title: "ModifyGroup"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyGroup-v2"
---

Call ModifyGroup to modify the consumer group description information.

**Instructions for use**

After creating a consumption group, you can call this interface to adjust the description information of the consumption group.

**request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |Instance ID. |
|GroupId |String |Yes |my_group |The consumer group ID described to be modified. |
|Description |String |Yes |Modify test |Modify the description of the consumption group to no more than 128 characters in length. |


**response parameter**

None

**example**

**Request example**

```JSON
POST /?Action=ModifyGroup&Version=2022-05-01 HTTP/1.1
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
        "Action": "ModifyGroup",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
