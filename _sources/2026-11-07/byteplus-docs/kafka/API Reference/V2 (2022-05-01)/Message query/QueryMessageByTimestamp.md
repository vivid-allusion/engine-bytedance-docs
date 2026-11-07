---
title: "QueryMessageByTimestamp"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/QueryMessageByTimestamp-v2"
---

QueryMessageByTimestamp is called to query message metadata of a partition during a specified time period.

<span id="cabc205e"></span>
## **Instructions**

This interface is used to query message metadata of a partition during a specified time period.

<span id="d3fef4a8"></span>
## **Request parameters**


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |Instance ID |
|TopicName |String |Yes |query_topic |Topic name |
|PartitionId |Integer |Yes |0 |Partition ID. If value is set as `-1`, it means to query among all partitions. |
|QueryStartTimestamp |String |Yes |1661320625000 |The start time of the specified time period for the query. It follows Unix timestamp format and is measured by milliseconds. |
|QueryEndTimestamp |String |Yes |1661320682000 |The end time of the specified time period for the query. It follows Unix timestamp format and is measured by milliseconds. |
|Refresh |Bool |No |false |Whether to force a refresh. Default value is false.<br><br><br>* false: do not force a cache refresh.<br><br>* true: force a cache refresh.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When new data is being written during the specified time period, the cache needs to be refreshed in order to query the new data.</div><br> |
|PageNumber |Integer |Yes |1 |The page number of the list, with a minimum value of 1. |
|PageSize |Integer |Yes |10 |The number of entries per page in the list, ranging from 1 to 16. |
|SortOrder |String |No |Asc |The sorting order for the query results. Default value is Asc<br><br><br>* Asc: sorted by partition and message offset in ascending order.<br><br>* Desc: sorted by partition and message offset in descending order. |


<span id="4516bc2b"></span>
## **Response parameter**


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|MessageList |Array of [BasicMessageInfoObject](https://docs.byteplus.com/docs/kafka/Data-Structure-v2#0e5082f9) | |List of messages that meet the query criteria. |
|HasMoreMessage |Bool |true |Whether there are more pages of messages.<br><br><br>* true：there are more pages of messages.<br><br>* false：there are no more pages of messages.<br><br><br>If the number of messages in the specified time period exceeds the specified `PageSize`, the response data will be arranged in different pages. This parameter is used to indicate whether the currently returned messages are the collection of all eligible messages. |


<span id="d5f9296f"></span>
## **Example**

<span id="dffc40d8"></span>
### **Sample Request**

```JSON
POST /?Action=QueryMessageByTimestamp&Version=2022-05-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/ap-southeast-1/kafka/request, SignedHeaders=x-date, Signature=********

{
  "InstanceId": "kafka-cnaxxxxx",
  "TopicName": "test-topic",
  "PartitionId": 0,
  "QueryStartTimestamp": 1717415062840,
  "QueryEndTimestamp": 1717415962840,
  "PageNumber": 1,
  "PageSize": 16,
  "Refresh": false
}
```


<span id="a370ffec"></span>
### **Sample Response**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2024060511024265745BEBEC5C4***",
        "Action": "QueryMessageByTimestamp",
        "Version": "2022-05-01",
        "Service": "kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "HasMoreMessage": false,
        "MessageList": [
            {
                "CreateTime": 1717556541777,
                "Key": "doc-key",
                "Message": "test-message1",
                "MessageOffset": 0,
                "MessageSize": 13,
                "PartitionId": 0,
                "TopicName": "test-topic"
            },
            {
                "CreateTime": 1717556557043,
                "Key": "doc-key",
                "Message": "test-message2",
                "MessageOffset": 1,
                "MessageSize": 13,
                "PartitionId": 0,
                "TopicName": "test-topic"
            }
        ]
    }
}
```
