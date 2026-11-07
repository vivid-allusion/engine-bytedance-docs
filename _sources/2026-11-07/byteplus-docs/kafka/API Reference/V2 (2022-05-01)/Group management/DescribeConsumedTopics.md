---
title: "DescribeConsumedTopics"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeConsumedTopics-v2"
---

Call DescribeConsumedTopics interface to view the topic information of the consumption group subscription.

<span id="83e3867c"></span>
## **Instructions for use**

This interface is used to view the list of topics subscribed by the specified consumption group, including the consumption status of the consumption group in each topic.

<span id="d432f7ec"></span>
### **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\*x |Instance ID. |
|PageNumber |Integer |Yes |1 |The page number of the list, with a minimum value of 1. |
|PageSize |Integer |Yes |10 |The number of entries per page in the list, ranging from 1 to 100. |
|GroupId |String |Yes |Connect\-cluster |Consumer group ID. |
|TopicName |String |No |TestTopic |Filter by Topic name, support fuzzy search. If this parameter is not specified, all Topics subscribed to the specified Group are returned by default. |


<span id="84fef477"></span>
## **response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|Total |Integer |1 |Specifies the total number of Topics consumed by the consumption group. |
|Accumulation |Integer |182238602 |Specifies the total number of messages piled up by the consumption group. |
|ConsumedTopicsInfo |Array of ConsumedTopicInfoObject |/ |The list of topics that meet the filter criteria in the Topics subscribed by the specified consumer group. For detailed instructions, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) ConsumedTopicInfoObject part in. |


<span id="7e6d3f16"></span>
## **example**

<span id="95c0276f"></span>
### **Request example**

```JSON
POST /?Action=DescribeConsumedTopics&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnng1si21igu****",
  "PageNumber": 1,
  "PageSize": 2,
  "GroupId":"Group",
  "TopicName": "test"
}
```


<span id="f34e6ede"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202302272048242247F4CA2CB8745C6DD7",
        "Action": "DescribeConsumedTopics",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Accumulation": 182238602,
        "ConsumedTopicsInfo": [
            {
                "Accumulation": 182238602,
                "TopicName": "test"
            }
        ],
        "Total": 1
    }
}
```
