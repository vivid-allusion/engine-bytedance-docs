---
title: "DescribeTopicPartitions"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeTopicPartitions-v1"
---

Call the DescribeTopicPartitions interface to get the Partition information of the Topic.

<span id="98e50116"></span>
## Instructions for Use


* DescribeTopicPartitions interface provides a paged query function for you to view information such as the number of partitions of a specified topic, the status of the partition ISR, and so on.

* Version of this API is `2018-01-01`.

* The calling frequency of this interface is limited to 100 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="2d8135f7"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|PageNumber |Integer |Required |1 |The page number of the list. |
|PageSize |Integer |Required |1 |The number of entries per page in the list. |
|InstanceId |String |Required |Kafka\- \*\*\*\* |Instance ID. |
|TopicName |String |Required |my_topic |Topic name. |
|PartitionNumbers |List |optional |[1, 2] |Partition number, if not specified, all partitions are queried. |
|UnderInsyncOnly |Bool |Optional |True |Whether to query only the partition list with unsynchronized replicas, the default value is false.<br><br><br>* True: only query the partition list with unsynchronized replicas.<br><br>* False: Query the full partition list. |


<span id="deb636ee"></span>
## Response parameter


|**parameter** |**parameter type** |**explain** |
|---|---|---|
|Total |Integer |The total number of partitions that meet the query criteria. |
|Partitions |List |List of partitions that meet the query criteria. For details, please refer to [StandardPartitionInfo]. |


<span id="a33e2320"></span>
## Example

<span id="980eb4e2"></span>
### Request example

```json
POST /?Action=DescribeTopicPartitions&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "PageNumber": 1,
  "PageSize": 1,
  "InstanceId": "kafka-****",
  "TopicName": "my_topic",
  "PartitionNumbers": [
    0
  ],
  "UnderInsyncOnly": true
}
```


<span id="6530bcf5"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DescribeTopicPartitions",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": {
        "Partitions": [
            {
                "EndOffset": 0,
                "InsyncReplicas": [
                    0,
                    1,
                    2
                ],
                "Leader": 0,
                "MessageCount": 0,
                "PartitionNumber": 0,
                "Replicas": [
                    0,
                    1,
                    2
                ],
                "StartOffset": 0,
                "UnderInsyncReplicas": []
            }
        ],
        "Total": 12
    }
}
```
