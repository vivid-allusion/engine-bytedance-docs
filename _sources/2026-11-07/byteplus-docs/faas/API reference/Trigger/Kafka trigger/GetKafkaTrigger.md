---
title: "GetKafkaTrigger"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GetKafkaTrigger"
---

Obtain detailed information about Kafka Trigger.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=GetKafkaTrigger&Version=2024\-06\-06


<span id="请求参数"></span>
## Ruquest parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetKafkaTrigger |Interface name. The current API is called `GetKafkaTrigger`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|Id |String |Yes |nw\*\*\*\*\*\* |Kafka Trigger ID. You can call the [ListTriggers](https://docs.byteplus.com/en/docs/faas/ListTriggers) interface to obtain the Trigger ID. |
|FunctionId |String |Yes |wrw\*\*\*\*\*\* |Function ID. You can call the [ListFunctions](https://docs.byteplus.com/en/docs/faas/ListFunctions) interface to obtain Function ID (`Items.Id`). |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=GetKafkaTrigger&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "Id": "nw******",
    "FunctionId": "wrw******"
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|FunctionId |String |wrw\*\*\*\*\*\* |Function ID. |
|Name |String |reviews\-consumer |Kafka Trigger name. |
|Description |String |Example Kafka Trigger |Kafka Trigger description. |
|Enabled |Boolean |true |Whether to enable Kafka Trigger. Parameter value description:<br><br><br>* **true**: Enable<br><br>* **false**: Turn off |
|MqInstanceId |String |kafka\-cnngl4if\*\*\*\*\*\* |Message queue Kafka instance ID. |
|TopicName |String |reviews\-topic |Topic name of the message queue Kafka instance. |
|StartingPosition |String |Latest |Start consuming the location of the message in the Topic. Parameter value description:<br><br><br>* **Latest**: Only consume messages generated after subscribing to the Topic.<br><br>* **Earliest**: Start consuming from the first message produced in the Topic. |
|MaximumRetryAttempts |Integer |100 |The maximum number of retries when a function runs incorrectly. |
|Id |String |18lt\*\*\*\* |Kafka Trigger ID. |
|ConsumerGroup |String |reviews\-topic_18lt\*\*\*\* |The consumer group of message queue Kafka instance. |
|Status |String |pending |Kafka Trigger status. Parameter value description:<br><br><br>* **ready**: Running<br><br>* **failed**: Failed<br><br>* **pending**: Starting |
|CreationTime |String |2025\-02\-03 06:47:41.423691239 +0000 UTC |The creation time for the Kafka Trigger. UTC + 0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|LastUpdateTime |String |2025\-02\-03 06:47:41.423691239 +0000 UTC |The latest update time of Kafka Trigger. UTC + 0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|BatchSize |Integer |10 |The number of messages per batch consumed by the Trigger in bulk. |
|BatchFlushDurationMilliseconds |Integer |1,000 |Maximum waiting time for bulk consumption by Trigger. The unit is millisecond. |


<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetKafkaTrigger",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "FunctionId": "wrw******",
        "Name": "reviews-consumer",
        "Description": "Sample kafka Trigger",
        "Enabled": true,
        "MqInstanceId": "kafka-cnngl4if******",
        "TopicName": "reviews-topic",
        "StartingPosition": "Latest",
        "MaximumRetryAttempts": 100,
        "Id": "18lt****",
        "ConsumerGroup": "reviews-topic_18lt****",
        "Status": "pending",
        "CreationTime": "2025-02-03 06:47:41.423691239 +0000 UTC",
        "LastUpdateTime": "2025-02-03 06:47:41.423691239 +0000 UTC"
    }
}
```


<span id="错误码"></span>
## Error code 

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
