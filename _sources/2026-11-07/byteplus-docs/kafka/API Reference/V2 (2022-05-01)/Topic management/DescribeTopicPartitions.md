---
title: "DescribeTopicPartitions"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeTopicPartitions-v2"
---

Call the DescribeTopicPartitions interface to get the Partition information of the Topic.

<span id="05d7edd2"></span>
## **Instructions for use**

DescribeTopicPartitions interface provides a paged query function for you to view the number of partitions, partition ISR status, and other information for a specified topic.

<span id="01687971"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |Instance ID. |
|TopicName |String |Yes |my_topic |Topic name. |
|PageNumber |Integer |Yes |1 |The page number of the list, with a minimum value of 1. |
|PageSize |Integer |Yes |10 |The number of entries per page in the list, ranging from 1 to 100. |
|PartitionIds |Array of Integer |No |[1, 2] |Partition number. If not specified, returns information for all partitions. |
|UnderInsyncOnly |Boolean |No |True |Whether to query only the partition list with unsynchronized replicas, the default value is false.<br><br><br>* True: only query the partition list with unsynchronized replicas.<br><br>* False: Query the full partition list. |


**response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|Total |Integer |2 |The total number of partitions that meet the query criteria. |
|PartitionsInfo |Array of BasicPartitionInfo |/ |List of partitions that meet the query criteria. For details, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) BasicPartitionInfo in. |


<span id="ec973bdc"></span>
## **example**

<span id="627d99d9"></span>
### **Request example**

```JSON
POST /?Action=DescribeTopicPartitions&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnngbnntswg1****",
  "TopicName": "my_topic",
  "PageNumber": 1,
  "PageSize": 1
}
```


<span id="6c5654a3"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023022720063227B3DCC115F59769D448",
        "Action": "DescribeTopicPartitions",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "PartitionsInfo": [
            {
                "EndOffset": 7774940552,
                "InsyncReplicas": [
                    2,
                    1,
                    0
                ],
                "Leader": 2,
                "MessageCount": 16286430,
                "PartitionId": 0,
                "Replicas": [
                    2,
                    1,
                    0
                ],
                "StartOffset": 7758654122,
                "UnderInsyncReplicas": []
            }
        ],
        "Total": 2
    }
}
```
