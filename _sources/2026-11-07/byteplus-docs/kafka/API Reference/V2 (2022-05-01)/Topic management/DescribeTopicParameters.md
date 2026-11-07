---
title: "DescribeTopicParameters"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeTopicParameters-v2"
---

Call DescribeTopicParameters view the parameter configuration for the specified Topic.

<span id="d2b714bd"></span>
## **Instructions for use**

This interface is used to view the parameter configuration information of the specified Topic, including the minimum number of synchronization replicas, the maximum message size, etc.

<span id="925ce818"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |Instance ID. |
|TopicName |String |Yes |Name |Topic name. |


<span id="8037df0e"></span>
## **response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|Parameters |String | |Topic\-level parameter configuration. The description is as follows:<br><br><br>* LogAutoDeletion: Whether to automatically delete old messages.<br><br>* MessageMaxByte: Maximum message size. The unit is MB.<br><br>* MinInsyncReplicaNumber: The minimum number of synchronous replicas of a Topic.<br><br><br>You can also go through the documentation. [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter) View the details of each parameter. |


<span id="ea1b74bb"></span>
## **example**

<span id="2a7d7212"></span>
### **Request example**

```JSON
POST /?Action=DescribeTopicParameters&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnngbnntswg1****",
  "TopicName": "my_topic"
}
```


<span id="32793a27"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230227195620C7B6D308FCE70D6B1BD1",
        "Action": "DescribeTopicParameters",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Parameters": "{\"LogRetentionHours\":\"72\",\"MessageMaxByte\":\"10\",\"MinInsyncReplicaNumber\":\"2\"}"
    }
}
```
