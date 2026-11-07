---
title: "DescribeTopics"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeTopics-v1"
---

Call the DescribeTopics interface to view the Topic list.

<span id="47248f02"></span>
## Instructions for use


* Version of this API is `2018-01-01`.

* The calling frequency of this interface is limited to 100 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="3c2dc8d3"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\*\* |Instance ID. |
|PageNumber |Integer |Required |1 |The page number of the list, with a value not less than 1. |
|PageSize |Integer |Required |10 |The number of instances of a single\-page query, with values ranging from 1 to 50. |
|FiledName |String |optional |Name |Sorting fields used, currently only sorting by Name is supported. |
|SortOrder |String |Optional |Asc |Sort by. Supported settings are:<br><br><br>* Asc: in ascending order.<br><br>* Desc: in descending order. |
|Search |String |optional |my_topic |Match accurately according to Topic name. |
|Filters |`List<Filter>` |Optional |Please refer to DescribeTopics |Filter conditions. These include:<br><br><br>* Name: The name of the filter. Currently only setting to "Name" is supported, that is, filtering according to the Topic name.<br><br>* Values: Filtered values,`List<String>` Type.<br><br><br>For details, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |


<span id="764a0d26"></span>
## Response parameter


|**parameter** |**parameter type** |**explain** |
|---|---|---|
|Total |Integer |The total number of topics that meet the query criteria. |
|Topics |List |List of Topics that meet the query criteria. For details, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |


<span id="924ce602"></span>
## Example

<span id="4c5534c8"></span>
### Request example

```json
POST /?Action=DescribeTopics&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "PageNumber": 1,
  "PageSize": 10,
  "InstanceId": "kafka-****",
  "FiledName": "Name",
  "SortOrder": "Asc",
  "Search": "my_topic",
  "Filters": [
    {
      "Name": "Name",
      "Values": [
        ""
      ]
    }
  ]
}
```


<span id="9dc6a199"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DescribeTopics",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": {
        "Topics": [
            {
                "CreateTime": "2022-04-07T21:13:34+08:00",
                "Description": "",
                "InstanceId": "kafka-******",
                "MaxMessageMegabyte": 10,
                "MinInsyncReplicaNumber": 2,
                "Name": "test-plb",
                "PartitionNumber": 12,
                "Region": "ap-southeast-1",
                "ReplicaNumber": 3,
                "RetentionHour": 72,
                "Status": "Running",
                "UpdateTime": "2022-04-07T21:13:35+08:00"
            }
        ],
        "Total": 1
    }
}
```
