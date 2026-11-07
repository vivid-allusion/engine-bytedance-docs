---
title: "GetTimer"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GetTimer"
---

Call the GetTimer interface to obtain Timer Trigger details.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=GetTimer&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetTimer |Interface name. The current API is called `GetTimer`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |wr\*\*\*\*\*\* |The ID of the function to which the Timer Trigger belongs. |
|Id |String |Yes |nw\*\*\*\* |Timer Trigger ID. |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=GetTimer&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "wr******",
    "Id": "nw****"
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|FunctionId |String |wr\*\*\*\* |Function ID. |
|Id |String |nw\*\*\*\* |Timer trigger ID. |
|Name |String |doc\-timer |Timer trigger name. |
|Description |String |Timer trigger |The remarks information for the Timer trigger. |
|Enabled |Boolean |true |Whether the Timer trigger has been turned on. `true` indicates it is turned on.  |
|Crontab |String |\*/5 \* \* \* \* |The trigger time of Timer trigger, in the format crontab expression. |
|Payload |String | |The Timer trigger sends the requested payload, which is the trigger message. |
|CreationTime |String |2024\-06\-14 15:31:07.143863441 +0800 CST m=+88714.902440864 |Timer trigger creation time. |
|LastUpdateTime |String |2024\-06\-14 15:31:07.143863441 +0800 CST m=+88714.902440864 |Timer trigger update time. |
|EnableConcurrency |Boolean |true |Whether the Timer trigger allows concurrency. `true` indicates it allows concurrency. |
|Retries |Integer |0 |The number of retries for the Timer trigger. |


<span id="返回示例"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "2024112916192814CC1E0FD73**",
        "Action": "GetTimer",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "FunctionId": "qt******",
        "Id": "in******",
        "Name": "doc-timer",
        "Description": "Timer Trigger",
        "Enabled": true,
        "Crontab": "*/5 * * * *",
        "Payload": "",
        "CreationTime": "2024-11-29 08:16:31.54 +0000 UTC",
        "LastUpdateTime": "2024-11-29 08:16:31.54 +0000 UTC",
        "EnableConcurrency": false,
        "Retries": 0
    }
}
```


<span id="错误码"></span>
## Error code 

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troublehshoot.
