---
title: "DescribeConsumedPartitions"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeConsumedPartitions-v1"
---

Call DescribeConsumedPartitions interface to view partition information for consumer group subscriptions.

<span id="512e03f0"></span>
## Instructions for use


* Version of this API is `2018-01-01`.

* The calling frequency of this interface is limited to 100 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="815f1273"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\* x |Instance ID. |
|GroupId |String |Required |my_group |Consumer group ID. |
|TopicName |String |Required |my_topic |Topic name. |
|PageNumber |Integer |Required |1 |Query the page number of the consumer group. Not less than 1. |
|PageSize |Integer |Required |10 |The number of single\-page queries, with a value of not less than 1. |
|FiledName |String |Optional |PartitionNumber |Fields used for sorting.<br><br><br>* PartitionNumber: (Default) Sort by partition number.<br><br>* Accumulation: Sorted by consumption accumulation. |
|SortOrder |String |Optional |Asc |Sort by:<br><br><br>* Desc: Descending<br><br>* Asc: ascending |


<span id="6eece580"></span>
## Response parameter


|**parameter** |**parameter type** |**explain** |
|---|---|---|
|Total |Integer |The total number of partitions that the consumption group consumes corresponding to the Topic. |
|Partitions |List |List of Partitions that meet the query criteria. For detailed instructions, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |


<span id="0321dfca"></span>
## Example

<span id="a11aa19f"></span>
### Request example

```json
POST /?Action=DescribeConsumedPartitions&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "PageNumber": 1,
  "PageSize": 10,
  "InstanceId": "kafka-****x",
  "GroupId": "my_group",
  "TopicName": "my_topic",
  "FiledName": "PartitionNumber",
  "SortOrder": "Asc"
}
```


<span id="62bc6a62"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DescribeConsumedPartitions",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Total": 0,
    "Partitions": [
      {
        "PartitionNumber": 0,
        "ConsumedClient": "",
        "ConsumedOffset": 0,
        "StartOffset": 0,
        "EndOffset": 0,
        "Accumulation": 0
      }
    ]
  }
}
```
