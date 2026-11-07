---
title: "CreateKafkaTrigger"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/CreateKafkaTrigger"
---

Create Kafka Trigger.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=CreateKafkaTrigger&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateKafkaTrigger |Interface name. The current API is called `CreateKafkaTrigger`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |wrw\*\*\*\*\*\* |Function ID. You can call the [ListFunctions](https://docs.byteplus.com/en/docs/faas/ListFunctions) interface to obtain function ID (`Items.Id`). |
|Name |String |Yes |reviews\-consumer |Kafka Trigger name.<br><br><br>* Trigger names cannot be repeated under the same function.<br><br>* Contains only uppercase and lowercase letters, numbers, and underscores (_), and starts with a letter, with a length limit of 4 to 63 characters. |
|Description |String |No |Example Kafka Trigger |Kafka Trigger description. The length is limited to 200 characters. |
|MqInstanceId |String |Yes |kafka\-cnngl4ifv\*\*\*\*\*\* |Message queue Kafka instance ID. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/kafka/DescribeInstances-v2) interface to obtain Kafka instance ID. |
|TopicName |String |Yes |reviews\-topic |Topic name of the message queue Kafka instance. You can call the [DescribeTopics](https://docs.byteplus.com/en/docs/kafka/DescribeTopics-v2) interface to obtain the Topic name of the Kafka instance. |
|Enabled |Boolean |No |true |Whether to enable Trigger while creating Trigger. Value:<br><br><br>* **true ** : Enable.<br><br>* **false**: Turn off.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only the Trigger enabled can work properly.</div><br> |
|StartingPosition |String |No |Latest |Specify the location of the message when starting consuming messages in the Topic. Value:<br><br><br>* **Latest**: Only consume messages generated after subscribing to the Topic.<br><br>* **Earliest**: Start consuming from the first message produced in the Topic. |
|MaximumRetryAttempts |Integer |No |100 |The maximum number of retries when a function has running errors (including user code errors and Runtime errors). A positive integer with values ranging from 0 to 100. |
|KafkaCredentials |Object of [KafkaCredentials](https://docs.byteplus.com/en/docs/faas/CreateKafkaTrigger#kafkacredentials) |Yes | |Kafka identity authentication. Function Service authenticates message consumption for both PLAIN and SCRAM\-SHA\-256 types of SASL users through the Kafka ACL permission policy. |
|BatchSize |Integer |No |10 |The number of messages per batch for batch consumption of Trigger. It is recommended that the value does not exceed 1,000. |
|BatchFlushDurationMilliseconds |Integer |No |1,000 |The maximum waiting time for batch consumption of Trigger. The unit is millisecond (ms), and the value range is 1,000\-60,000 ms. The default value is 1,000 ms.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter only takes effect when the <strong>BatchSize</strong> parameter has been already configured.</div><br> |


<span id="kafkacredentials"></span>
### KafkaCredentials


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Password |String |Yes |xxxxxxxxxx |The SASL/PLAIN user password set when creating Kafka instances. You can call the [DescribeUsers](https://docs.byteplus.com/en/docs/kafka/DescribeUsers-v2) interface to obtain Kafka instances SASL/PLAIN user password. |
|Username |String |Yes |demo\-name |The SASL/PLAIN user name set when creating the Kafka instance. You can call the [DescribeUsers](https://docs.byteplus.com/en/docs/kafka/DescribeUsers-v2) interface to obtain the Kafka instance SASL/PLAIN user name. |
|Mechanism |String |Yes |PLAIN |Kafka authentication mechanism. Value:<br><br><br>* PLAIN<br><br>* SCRAM\-SHA\-256<br><br>   For a detailed description, refer to [Message queue Kafka document](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints). |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=CreateKafkaTrigger&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "wrw******",
    "Name": "reviews-consumer",
    "Description": "Sample kafka trigger",
    "MqInstanceId": "kafka-cnngl4ifv******",
    "TopicName": "reviews-topic",
    "Enabled": true,
    "StartingPosition": "Latest",
    "MaximumRetryAttempts": 100,
    "KafkaCredentials": {
        "Mechanism": "PLAIN",
        "Username": "demo-name",
        "Password": "xxxxxxxxxx"
    }
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|FunctionId |String |wrw\*\*\*\*\*\* |Function ID. |
|Name |String |reviews\-consumer |Kafka Trigger name. |
|Description |String |Example Kafka trigger |Kafka Trigger description. |
|Enabled |Boolean |true |Whether to enable Kafka Trigger. Parameter value description:<br><br><br>* **true**: Enable<br><br>* **false**: Turn off |
|MqInstanceId |String |kafka\-cnngl4if\*\*\*\*\*\* |Message queue Kafka instance ID. |
|TopicName |String |reviews\-topic |Topic name of the message queue Kafka instance. |
|StartingPosition |String |Latest |Start consuming the location of the message in the Topic. Parameter value description:<br><br><br>* **Latest**: Only consume messages generated after subscribing to the Topic.<br><br>* **Earliest**: Start consuming from the first message produced in the Topic. |
|MaximumRetryAttempts |Integer |100 |The maximum number of retries when a function has running errors. |
|Id |String |18lt\*\*\*\* |Kafka Trigger ID. |
|ConsumerGroup |String |reviews\-topic_18lt\*\*\*\* |The consumption group name of message queue Kafka instance. |
|Status |String |pending |Kafka Trigger status. Parameter value description:<br><br><br>* **ready**: Running<br><br>* **failed**: Failed<br><br>* **pending**: Starting |
|CreationTime |String |2025\-02\-03 06:47:41.423691239 +0000 UTC |The creation time for Kafka Trigger. <br><br>UTC + 0 time in standard [RFC3339 ](https://tools.ietf.org/html/rfc3339)format. |
|LastUpdateTime |String |2025\-02\-03 06:47:41.423691239 +0000 UTC |The latest update time for Kafka Trigger. UTC + 0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|BatchSize |Integer |10 |The number of messages per batch for batch consumption of Trigger. |
|BatchFlushDurationMilliseconds |Integer |1000 |The maximum waiting time for batch consumption of Trigger. The unit is millisecond. |


<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateKafkaTrigger",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "FunctionId": "wrw******",
        "Name": "reviews-consumer",
        "Description": "Sample kafka trigger",
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

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
