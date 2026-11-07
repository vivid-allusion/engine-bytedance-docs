---
title: "QueryMessageByMessageId"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/QueryMessageByMessageId-v1"
---

Calling QueryMessageByMessageId can query the message content of the specified Offset in the partition.

<span id="ef5f3e69"></span>
## Instructions for use


* Version of this API is `2018-01-01`.

* The calling frequency of this interface is limited to 100 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="e1efe407"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\*\* |Instance ID. |
|Topic |String |Required |query_topic |Topic name. |
|Partition |Integer |Required |0 |The partition number. |
|MessageOffset |Integer |Required |0 |Message offset. |
|NeedMessageBody |Bool |Required |False |Whether you need to query the message content.<br><br><br>* True: need to return the message content<br><br>* False: No need to return message content |


<span id="1a2a769f"></span>
## Response parameter


|**parameter** |**parameter type** |**explain** | |
|---|---|---|---|
|IsExist |Bool |False |Whether the message is still retained at the server level.<br><br><br>* True: The message exists.<br><br>* False: The message does not exist. |
|Message |JSON Array |*  |The content of the message found. Please refer to the detailed description [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |


<span id="072ca275"></span>
## Example

<span id="d18cfbd4"></span>
### Request example

```json
POST /?Action=QueryMessageByMessageId&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-****",
  "Topic": "query_topic",
  "Partition": 0,
  "MessageOffset": 0,
  "NeedMessageBody": false
}
```


<span id="86fe7510"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "QueryMessageByMessageId",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "IsExist": false,
    "Message": {
      "InstanceId": "kafka-*****",
      "TopicName": "topic",
      "Partition": 0,
      "MessageOffset": 0,
      "MessageSize": 1023,
      "CreateTime": 0,
      "Key": "name",
      "Body": "hello"
    }
  }
}
```
