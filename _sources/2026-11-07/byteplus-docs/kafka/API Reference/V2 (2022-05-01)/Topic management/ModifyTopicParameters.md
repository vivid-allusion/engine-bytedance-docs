---
title: "ModifyTopicParameters"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyTopicParameters-v2"
---

Call the ModifyTopicParameters interface to modify the parameter configuration of the Topic.

<span id="9915177d"></span>
## **Instructions for use**

This interface is used to adjust the configuration of the specified Topic, such as the number of partitions and the minimum number of synchronous replicas.

<span id="2035a656"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |The instance ID of the Topic. |
|TopicName |String |Yes |my_topic |The name of the Topic. Modifying the TopicName is not supported after the Topic is created. |
|Parameters |String |Yes | |Kafka parameter configuration at the Topic level.<br><br>For the current list of supported parameters and their default values, please refer to [CreateTopic](https://docs.byteplus.com/en/docs/kafka/CreateTopic-v2) You can also go through the documentation [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter) View the details of each parameter.<br><br>When calling the API through Mail carrier, etc., you should pay attention to escaping, such as`{\"LogRetentionHours\":\"72\",\"MessageMaxByte\":\"10\",\"MinInsyncReplicaNumber\":\"2\"}`. |
|PartitionNumber |Integer |No |12 |Number of partitions for this Topic. The higher the number of partitions, the higher the concurrency consumed.<br><br>This parameter can only be adjusted larger and not smaller. The maximum can be set to 300 and cannot exceed the remaining available partitions of the Kakfa instance. |
|ReplicaNumber |Integer |No |3 |The number of replicas of the partition indicates that the data is backed up on the corresponding number of replicas. Data availability can still be guaranteed when one of the brokers fails. The larger the number of replicas, the higher the reliability.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Increasing the number of replicas will consume the instance disk capacity, please ensure sufficient capacity. Increasing replicas will consume instance bandwidth resources, and it is recommended to operate during low business peaks.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Reducing the number of replicas will reduce data availability, so proceed with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">1 Replica Topic cannot guarantee data reliability and cannot read and write during instance upgrade. It is recommended to choose 2 replicas or 3 replicas.</div><br> |


<span id="f4dabb15"></span>
## **response parameter**

None

<span id="5d87c487"></span>
## **example**

<span id="653489c6"></span>
### **Request example**

```JSON
POST /?Action=ModifyTopicParameters&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "InstanceId": "kafka-cnngbnntswg1****",
    "TopicName": "123",
    "Parameters": "{\"LogRetentionHours\":\"72\",\"MessageMaxByte\":\"10\",\"MinInsyncReplicaNumber\":\"2\"}",
    "PartitionNumber": 22
}
```


<span id="fccb487e"></span>
## **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023022720003326EC39DC5C89026AD3E1",
        "Action": "ModifyTopicParameters",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
