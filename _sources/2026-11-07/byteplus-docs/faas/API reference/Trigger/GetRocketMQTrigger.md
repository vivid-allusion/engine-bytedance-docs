---
title: "GetRocketMQTrigger"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GetRocketMQTrigger"
---

Query RocketMQ Trigger details.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=GetRocketMQTrigger&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetRocketMQTrigger |Interface name. The current API is called `GetRocketMQTrigger`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|Id |String |Yes |kh\*\*\*\*\*\* |RocketMQ Trigger ID. |
|FunctionId |String |Yes |aj\*\*\*\*\*\* |Function ID. |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=GetRocketMQTrigger&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "Id": "kh******",
    "FunctionId": "aj******"
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|FunctionId |String |aj\*\*\*\*\*\* |Function ID. |
|Name |String |rmq1 |RocketMQ Trigger name. |
|Description |String |Lightweight official website |RocketMQ Trigger description. |
|Enabled |Boolean |true |Trigger enabled or not:<br><br><br>* true: Enabled<br><br>* false: Not enabled |
|MqInstanceId |String |rocketmq\-cno\*\*\*\*\*\* |RocketMQ instance ID. |
|TopicName |String |test |The RocketMQ Topic consumed. |
|StartingPosition |String |Latest |Initial starting position (latest or earliest). |
|MaximumRetryAttempts |Integer |100 |Maximum number of retries. |
|Id |String |khq\*\*\*\*\*\* |RocketMQ Trigger ID. |
|ConsumerGroup |String |GID_test |RocketMQ consumer group name. |
|Status |String |ready |RocketMQ Trigger Status:<br><br><br>* pending: Suspended<br><br>* ready: Ready<br><br>* failed: Failed |
|Orderly |Boolean |false |Do RocketMQ consumers consume in order:<br><br><br>* true: In order<br><br>* false: Out of order. |
|QPSLimit |Integer |0 |The maximum QPS that all the RocketMQ consumer instances send to the function. |
|CreationTime |String |2024\-02\-13 02:36:23.033 +0000 UTC |RocketMQ Trigger creation time. |
|LastUpdateTime |String |2024\-02\-13 02:36:23.033 +0000 UTC |The last update time for RocketMQ Trigger. |
|Endpoint |String |http://rocketmq\-cnoeaf7\*\*\*\*\*\*.rocketmq.byteplus.com:9876 |RocketMQ access endpoints. |


<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetRocketMQTrigger",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "FunctionId": "aj******",
        "Name": "rmq1",
        "Description": "Lightweight official website",
        "Enabled": true,
        "MqInstanceId": "rocketmq-cnoe******",
        "TopicName": "test",
        "StartingPosition": "Latest",
        "MaximumRetryAttempts": 100,
        "Id": "kh******",
        "ConsumerGroup": "GID_test",
        "Status": "ready",
        "Orderly": true,
        "QPSLimit": 0,
        "CreationTime": "2024-02-13 02:36:23.033 +0000 UTC",
        "LastUpdateTime": "2024-02-13 02:36:23.033 +0000 UTC",
        "Endpoint": "http://rocketmq-cnoeaf70cd8b1234.rocketmq.byteplus.com:9876"
    }
}
```


<span id="错误码"></span>
## Error code 

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
