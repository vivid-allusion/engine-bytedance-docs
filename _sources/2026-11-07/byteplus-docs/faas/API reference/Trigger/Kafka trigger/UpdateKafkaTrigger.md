---
title: "UpdateKafkaTrigger"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/UpdateKafkaTrigger"
---

Update the specified Kafka Trigger.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=UpdateKafkaTrigger&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateKafkaTrigger |Interface name. The current API is called `UpdateKafkaTrigger`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |wrw\*\*\*\*\*\* |Function ID. You can call the [ListFunctions](https://docs.byteplus.com/en/docs/faas/ListFunctions) interface to obtain function ID (`Items.Id`). |
|Id |String |Yes |nw\*\*\*\*\*\* |Kafka Trigger ID. You can call the [ListTriggers](https://docs.byteplus.com/en/docs/faas/ListTriggers) interface to obtain the Trigger ID. |
|Enabled |Boolean |No |true |Whether to enable the Trigger while creating it. Value:<br><br><br>* **true**: Enable.<br><br>* **false**: Turn off.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only Trigger enabled will work properly.</div><br> |
|MaximumRetryAttempts |Integer |No |100 |The maximum number of retries when a function has run errors, including user code errors and runtime errors. A positive integer with values ranging from 0 to 100. |
|Description |String |No |Example Kafka Trigger |Kafka Trigger description. The length is limited to 200 characters. |
|BatchSize |Integer |No |10 |The number of messages per batch consumed by the Trigger in bulk. The recommended value should not exceed 1,000. |
|BatchFlushDurationMilliseconds |Integer |No |1,000 |Maximum waiting time for bulk consumption by Trigger. The unit is millisecond (ms), and the value range is 1,000 to 60,000 ms. The default value is 1,000 ms.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter only takes effect when the <strong>BatchSize</strong> parameter has been configured.</div><br> |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=UpdateKafkaTrigger&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "wrw******",
    "Id": "nw******",
    "Enabled": true,
    "MaximumRetryAttempts": 100,
    "Description": "Sample kafka Trigger"
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|FunctionId |String |wrw\*\*\*\*\*\* |Function ID. |
|Name |String |reviews\-consumer |Kafka Trigger name. |
|Description |String |Example Kafka Trigger |Kafka Trigger description. |
|Enabled |Boolean |true |Whether to enable Kafka Trigger. Parameter value description:<br><br><br>* **true**: Enabled<br><br>* **false**: Turned off |
|MqInstanceId |String |kafka\-cnngl4if\*\*\*\*\*\* |Message queue Kafka instance ID. |
|TopicName |String |reviews\-topic |Topic name of the message queue Kafka instance. |
|StartingPosition |String |Latest |Start consuming the message located in the Topic. Parameter value description:<br><br><br>* **Latest**: Only consume messages generated after subscribing to the Topic.<br><br>* **Earliest**: Start consuming from the first message produced in the Topic. |
|MaximumRetryAttempts |Integer |100 |The maximum number of retries when a function runs incorrectly. |
|Id |String |18lt\*\*\*\* |Kafka Trigger ID. |
|ConsumerGroup |String |reviews\-topic_18lt\*\*\*\* |The consumer group of message queue Kafka instance. |
|Status |String |pending |Kafka Trigger status. Parameter value description:<br><br><br>* **ready**: Running<br><br>* **failed**: Failed<br><br>* **pending**: Starting |
|CreationTime |String |2025\-02\-03 06:47:41.423691239 +0000 UTC |The creation time for Kafka Trigger. UTC + 0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|LastUpdateTime |String |2025\-02\-03 06:47:41.423691239 +0000 UTC |The latest update time for Kafka Trigger. UTC + 0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
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
        "Action": "UpdateKafkaTrigger",
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
