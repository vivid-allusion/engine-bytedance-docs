---
title: "DeleteGroup"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DeleteGroup-v2"
---

Call DeleteGroup to delete the ConsumerGroup.

<span id="397587d3"></span>
## **Instructions for use**

This interface will delete the consumption group under the instance, and it cannot be restored after deletion. Please call carefully.

<span id="e5616875"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |The instance ID of the consumer group to be deleted. |
|GroupId |String |Yes |my_group |The consumer group ID to be deleted. |


<span id="05445527"></span>
## **response parameter**

None

<span id="248be8b5"></span>
## **example**

<span id="f84c0e1c"></span>
### **Request example**

```JSON
POST /?Action=DeleteGroup&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnngbnntswg1****",
  "GroupId": "Group"
}
```


<span id="9ec76b98"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202302272036532B034FE726F55372A619",
        "Action": "DeleteGroup",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
