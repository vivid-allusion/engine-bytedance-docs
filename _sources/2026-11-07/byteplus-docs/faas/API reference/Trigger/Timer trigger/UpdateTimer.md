---
title: "UpdateTimer"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/UpdateTimer"
---

Call the UpdateTimer interface to update the configuration of Timer Trigger.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=UpdateTimer&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateTimer |Interface name. The current API is called `UpdateTimer`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |wr\*\*\*\*\*\* |The ID of the function to which the Timer Trigger belongs. |
|Id |String |Yes |nw\*\*\*\*\*\* |Timer Trigger ID. |
|Description |String |No |Timer trigger |The remarks information for the Timer Trigger. |
|Enabled |Boolean |No |true |Whether the Timer Trigger is enabled or not.<br><br><br>* true: Enabled<br><br>* false: Turned off. |
|Crontab |String |No |\*/5 \* \* \* \* |Timer Trigger trigger time. The time format is crontab expression, and you can access [crontab.guru](https://crontab.guru/) to view the meanings of crontab expression. |
|Payload |String |No | |The Timer Trigger sends requested payload, that is, a trigger message. |
|EnableConcurrency |Boolean |No |false |Whether the Timer Trigger allows concurrency.<br><br><br>* true: allows concurrency<br><br>* false: concurrency is prohibited. |
|Retries |Integer |No |0 |The number of retries for the Timer Trigger. |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=UpdateTimer&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
"FunctionId": "qt******",
"Id": "in******",
"Description": "Timer Trigger",
"Enabled": false,
"Crontab": "*/5 * * * *",
"EnableConcurrency": true
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|FunctionId |String |wr\*\*\*\*\*\* |Function ID. |
|Id |String |nw\*\*\*\*\*\* |Timer trigger ID. |
|Name |String |doc\-timer |Timer trigger name. |
|Description |String |Timer Trigger |The remarks information for the Timer trigger. |
|Enabled |Boolean |true |Whether the Timer trigger has been turned on. `true` indicates it is turned on. |
|Crontab |String |\*/5 \* \* \* \* |The execution time of Trimer trigger, in the format crontab expression. |
|Payload |String | |The Timer trigger sends requested payload, that is, a trigger message. |
|CreationTime |String |2024\-06\-14 15:31:07.143863441 +0800 CST m=+88714.902440864 |Timer trigger creation time. |
|LastUpdateTime |String |2024\-06\-14 15:31:07.143863441 +0800 CST m=+88714.902440864 |Timer trigger update time. |
|EnableConcurrency |Boolean |true |Whether the Timer trigger allows concurrency. `true` indicates it allows concurrency. |
|Retries |Integer |0 |The number of retries for the Timer trigger. |


<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202411291622408A1DCA972BE**",
        "Action": "UpdateTimer",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "FunctionId": "qt******",
        "Id": "in******",
        "Name": "doc-timer",
        "Description": "Timer-Trigger",
        "Enabled": false,
        "Crontab": "*/5 * * * *",
        "Payload": "",
        "CreationTime": "2024-11-29 08:16:31.54 +0000 UTC",
        "LastUpdateTime": "2024-11-29 16:22:40.412373364 +0800 CST m=+66137.231040950",
        "EnableConcurrency": true,
        "Retries": 0
    }
}
```


<span id="错误码"></span>
## Error code 

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
