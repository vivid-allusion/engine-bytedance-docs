---
title: "DescribeConsumedTopics"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeConsumedTopics-v1"
---

Call DescribeConsumedTopics interface to see the Topic name of the consumer group subscription.

<span id="ff17366d"></span>
## Instructions for use


* Version of this API is `2018-01-01`.

* The calling frequency of this interface is limited to 100 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="1f069f23"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\* x |Query the instance ID to which the consumer group belongs. |
|GroupId |String |Required |test_grooup |The consumer group ID to query. |
|PageNumber |Integer |Required |1 |Query the page number of the consumer group. Not less than 1. |
|PageSize |Integer |Required |10 |Query the number of consumer group single pages. |
|FiledName |String |Optional |test_grooup |Fields used for sorting.<br><br><br>* PartitionNumber: (Default) Sort by partition number.<br><br>* Accumulation: Sorted by consumption accumulation. |
|SortOrder |String |Optional |Asc |Sort by:<br><br><br>* Desc: Descending<br><br>* Asc: ascending |
|Search |String |Optional |test_topic |Filter according to the Topic name specified by this parameter to support fuzzy matching. |


<span id="6b2c2560"></span>
## Response parameter


|**parameter** |**parameter type** |**explain** |
|---|---|---|
|Total |Integer |Specifies the total number of Topics consumed by the consumption group. |
|Accumulation |Integer |Specifies the total number of messages piled up by the consumption group. |
|Topics |List |List of Topics that meet the query criteria. For detailed instructions, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |


<span id="9dab6910"></span>
## Example

<span id="e2f2ed36"></span>
### Request example

```json
POST /?Action=DescribeConsumedTopics&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "PageNumber": 1,
  "PageSize": 10,
  "InstanceId": "kafka-****x",
  "GroupId": "my_grooup",
  "FiledName": "my_grooup",
  "SortOrder": "Asc",
  "Search": "my_topic"
}
```


<span id="8da1aff5"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DescribeConsumedTopics",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Total": 0,
    "Accumulation": 0,
    "Topics": [
      {
        "TopicName": "",
        "Accumulation": 0
      }
    ]
  }
}
```
