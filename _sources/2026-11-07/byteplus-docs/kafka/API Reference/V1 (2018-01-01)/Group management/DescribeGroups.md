---
title: "DescribeGroups"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeGroups-v1"
---

Call the DescribeGroups interface to get the list of consumer groups.

<span id="3ea53867"></span>
## Instructions for use


* Version of this API is `2018-01-01`.

* The calling frequency of this interface is limited to 100 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="e8a9efe8"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\* x |Instance ID. |
|PageNumber |Integer |Required |1 |Query the page number of the consumer group. Not less than 1. |
|PageSize |Integer |Required |10 |Query the number of consumer group single pages. |
|FieldName |String |optional |GroupId |The sorted field of the query result currently only supports GroupId. |
|SortOrder |String |Optional |Asc |Sort by:<br><br><br>* Desc: Descending<br><br>* Asc: ascending |
|Search |String |optional |group\-test |Filter according to the Group name specified by this parameter to support fuzzy matching. |


<span id="5d671f1a"></span>
## Response parameter


|**parameter** |**parameter type** |**explain** |
|---|---|---|
|Total |Integer |Total number of consumer groups. |
|Groups |List |Query the result list of the consumption group. For detailed instructions, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |


<span id="c25007fa"></span>
## Example

<span id="a7c6884b"></span>
### Request example

```json
POST /?Action=DescribeGroups&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "PageNumber": 1,
  "PageSize": 10,
  "InstanceId": "kafka-****x"
}
```


<span id="c9d65a51"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DescribeGroups",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Total": 0,
    "Groups": [
      {
        "GroupId": "",
        "InstanceId": "",
        "State": ""
      }
    ]
  }
}
```
