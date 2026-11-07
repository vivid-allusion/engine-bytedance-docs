---
title: "DescribeConsumedPartitions"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeConsumedPartitions-v2"
---

Call DescribeConsumedPartitions interface to view the partition information for the specified Topic that the consumer group subscribes to.

<span id="835a4d29"></span>
## **Instructions for use**

This interface is used to view the basic information of each partition in the specified Topic of the consumption group subscription, including the partition number, consumer, consumption progress, etc.

<span id="1070dd32"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\*x |Instance ID. |
|GroupId |String |Yes |my_group |Consumer group ID. |
|TopicName |String |Yes |my_topic |Topic name. |
|PageNumber |Integer |Yes |1 |The page number of the list, with a minimum value of 1. |
|PageSize |Integer |Yes |10 |The number of entries per page in the list, ranging from 1 to 100. |


<span id="06876a1d"></span>
## **response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|Total |Integer |12 |The total number of partitions corresponding to the Topic consumed by the consumption group. |
|ConsumedPartitionsInfo |Array of ConsumedPartitionInfoObject |/ |List of partitions for the specified Topic. For detailed instructions, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) ConsumedPartition in. |


<span id="91bef760"></span>
## **example**

<span id="128eae20"></span>
### **Request example**

```JSON
POST /?Action=DescribeConsumedPartitions&Version=2022-05-01 HTTP/1.1
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


<span id="ba0abba0"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230321113657C9E60632E1D4F61E5BC5",
        "Action": "DescribeConsumedPartitions",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "ConsumedPartitionsInfo": [
            {
                "Accumulation": 14733811,
                "ConsumedClient": "consumer-1/192.168.xxx.xx",
                "ConsumedOffset": 5384592589,
                "EndOffset": 5399326400,
                "PartitionId": 0,
                "StartOffset": 5383336144
            },
            {
                "Accumulation": 15163307,
                "ConsumedClient": "consumer-1/192.168.xxx.xx",
                "ConsumedOffset": 5384167585,
                "EndOffset": 5399330892,
                "PartitionId": 1,
                "StartOffset": 5382017470
            },
            {
                "Accumulation": 14945858,
                "ConsumedClient": "consumer-1/192.168.xxx.xx",
                "ConsumedOffset": 5384386022,
                "EndOffset": 5399331880,
                "PartitionId": 2,
                "StartOffset": 5383799213
            },
            {
                "Accumulation": 14752456,
                "ConsumedClient": "consumer-1/192.168.xxx.xx",
                "ConsumedOffset": 5384573944,
                "EndOffset": 5399326400,
                "PartitionId": 3,
                "StartOffset": 5382346474
            },
            {
                "Accumulation": 15178847,
                "ConsumedClient": "consumer-1/192.168.xxx.xx",
                "ConsumedOffset": 5384152047,
                "EndOffset": 5399330894,
                "PartitionId": 4,
                "StartOffset": 5382000957
            },
            {
                "Accumulation": 14911104,
                "ConsumedClient": "consumer-1/192.168.xxx.xx",
                "ConsumedOffset": 5384420776,
                "EndOffset": 5399331880,
                "PartitionId": 5,
                "StartOffset": 5383833998
            },
            {
                "Accumulation": 14781616,
                "ConsumedClient": "consumer-1/192.168.xxx.xx",
                "ConsumedOffset": 5384544785,
                "EndOffset": 5399326401,
                "PartitionId": 6,
                "StartOffset": 5382317345
            },
            {
                "Accumulation": 15144197,
                "ConsumedClient": "consumer-1/192.168.xxx.xx",
                "ConsumedOffset": 5384186697,
                "EndOffset": 5399330894,
                "PartitionId": 7,
                "StartOffset": 5382036612
            },
            {
                "Accumulation": 14878307,
                "ConsumedClient": "consumer-1/192.168.xxx.xx",
                "ConsumedOffset": 5384453542,
                "EndOffset": 5399331849,
                "PartitionId": 8,
                "StartOffset": 5383866727
            },
            {
                "Accumulation": 14735190,
                "ConsumedClient": "consumer-1/192.168.xxx.xx",
                "ConsumedOffset": 5384591180,
                "EndOffset": 5399326370,
                "PartitionId": 9,
                "StartOffset": 5382361670
            },
            {
                "Accumulation": 15142067,
                "ConsumedClient": "consumer-1/192.168.xxx.xx",
                "ConsumedOffset": 5384188794,
                "EndOffset": 5399330861,
                "PartitionId": 10,
                "StartOffset": 5382038679
            },
            {
                "Accumulation": 14840853,
                "ConsumedClient": "consumer-1/192.168.xxx.xx",
                "ConsumedOffset": 5384490996,
                "EndOffset": 5399331849,
                "PartitionId": 11,
                "StartOffset": 5383905142
            }
        ],
        "Total": 12
    }
}
```
