---
title: "DescribeTopics"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeTopics-v2"
---

Call the DescribeTopics interface to view the Topic list.

<span id="6e24d770"></span>
## **Instructions for use**

This interface is used to view the list of topics of the specified instance, and can also be used to view the basic information of a topic.

<span id="4f1c7c25"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |Instance ID. |
|PageNumber |Integer |Yes |1 |The page number of the list, with a minimum value of 1. |
|PageSize |Integer |Yes |10 |The number of entries per page in the list, ranging from 1 to 100. |
|TopicName |String |No |Name |Topic name, setting this parameter means filtering according to the specified Topic name, and supports fuzzy matching. |
|PartitionNumber |Integer |No |10 |Number of partitions. Set this parameter to filter the Topic list according to the specified number of partitions. |
|ReplicaNumber |Integer |No |2 |Number of Topic replicas. Set this parameter to filter the Topic list according to the specified number of replicas. |


<span id="6d409e77"></span>
## **response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|InstanceId |String |kafka\-cnngbnntswg1\*\*\*\* |Instance ID. |
|Total |Integer |1 |The total number of topics that meet the query criteria. |
|TopicsInfo |Array of BasicTopicInfoObject |/ |List of Topics that meet the query criteria. For details, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) BasicTopicInfoObject part in. |


<span id="a0ce136b"></span>
## **example**

<span id="7cebb8cd"></span>
### **Request example**

```JSON
POST /?Action=DescribeTopics&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnngbnntswg1****",
  "PageNumber": 1,
  "PageSize": 12
}
```


<span id="9e7bd906"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230320225232367C4DA3A071871773BB",
        "Action": "DescribeTopics",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "kafka-cnou4r7qnu4r4ghd",
        "TopicsInfo": [
            {
                "CreateTime": "2023-03-06T12:47:44Z",
                "Description": "",
                "PartitionNumber": 12,
                "ReplicaNumber": 3,
                "Status": "Running",
                "TopicName": "test"
            },
            {
                "CreateTime": "2023-03-08T13:23:53Z",
                "Description": "",
                "PartitionNumber": 12,
                "ReplicaNumber": 3,
                "Status": "Running",
                "TopicName": "my_topic3w"
            }
        ],
        "Total": 2
    }
}
```
