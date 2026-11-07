---
title: "DeleteTopic"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DeleteTopic-v1"
---

Call the DeleteTopic interface to delete the Kafka Topic.

<span id="6bb6dd55"></span>
## Instructions for use

This interface will delete the related resources of the Topic under the instance. After the Topic is deleted, it cannot be restored. Please call carefully.


* Version of this API is`2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="fba92419"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|TopicName |String |Required |my_topic |The name of the topic to be deleted. |
|InstanceId |String |Required |Kafka\- \*\*\* x |The instance ID to which the Topic belongs to be deleted. |


<span id="2a292362"></span>
## Response parameter

null

<span id="2ecb4be1"></span>
## Example

<span id="c1f85e05"></span>
### Request example

```json
POST /?Action=DeleteTopic&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "TopicName": "test-plb1",
  "InstanceId": "kafka-****x"
}
```


<span id="569e813a"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DeleteTopic",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
