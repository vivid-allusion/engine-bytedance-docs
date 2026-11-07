---
title: "ListTriggers"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/ListTriggers"
---

Obtain all Triggers in bulk.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=ListTriggers&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListTriggers |Interface name. The current API is called `ListTriggers`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |pq\*\*\*\*\*\* |Function ID. |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=ListTriggers&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "pq******"
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [Trigger](https://docs.byteplus.com/en/docs/faas/ListTriggers#trigger) |\- |Trigger list. |
|Total |Integer |1 |Total number of Triggers. |


<span id="trigger"></span>
### Trigger


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |kh\*\*\*\*\*\* |Trigger ID. |
|Name |String |apig\-sales |Trigger name. |
|Type |String |timer |Trigger type:<br><br><br>* timer: Timing Trigger<br><br>* kafka: Consuming Kafka message queue<br><br>* bmq: Consuming BMQ message queue<br><br>* rocketmq: Consuming RocketMQ message queue<br><br>* apig: Trigger function via APIG gateway<br><br>* tos: Trigger function via TOS events<br><br>* tls: Consume TLS logs and trigger function |
|Enabled |Boolean |true |Trigger enabled or not:<br><br><br>* true: Enabled<br><br>* false: Not enabled |
|AccountID |String |210\*\*\*\*\*\* |BytePlus root user ID. |
|FunctionID |String |wr\*\*\*\*\*\* |Function ID. |
|Description |String |apig sales Trigger |Description. |
|CreationTime |String |2024\-02\-13 02:36:23.033 +0000 UTC |Creation time. |
|ImageVersion |String |master_613da8e9\*\*\*\*\*\*31be8d0e7e3f5d3d1785b1_20230327163215 |Trigger image version. |
|DetailedConfig |String |{"UpstreamId":"uci4qt01aqt740c03bn80", "GatewayId":"gci4\*\*\*\*\*\*" |Trigger configuration details. Currently only the APIG and TOS Trigger types contain configuration details. |
|LastUpdateTime |String |2024\-02\-13 02:36:23.033 +0000 UTC |Update time. |


<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListTriggers",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Items": [
            {
                "Id": "kh******",
                "Type": "tls",
                "Name": "TLSTrigger3",
                "Description": "",
                "CreationTime": "2024-07-22 07:15:54.522 +0000 UTC",
                "LastUpdateTime": "2024-07-22 07:27:17.739 +0000 UTC",
                "DetailedConfig": "",
                "Enabled": false
            }
        ],
        "Total": 1
    }
}
```


<span id="错误码"></span>
## Error code

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
