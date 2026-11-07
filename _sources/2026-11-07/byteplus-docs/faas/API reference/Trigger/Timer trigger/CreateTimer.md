---
title: "CreateTimer"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/CreateTimer"
---

Call the CreateTimer interface to create a Timer Trigger in the specified function.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=CreateTimer&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateTimer |Interface name. The current API is called `CreateTimer`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |qtqzj\*\*\* |Specify a function ID, and create a Timer Trigger in this function. |
|Name |String |Yes |doc\-timer |Custom settings for the name of the Timer Trigger.<br><br><br>* Supports uppercase and lowercase letters, numbers, and dashes (\-), and can only start with letters.<br><br>* The length is between 4 and 64 characters. |
|Description |String |No |Timer Trigger |The remarks information for the Timer Trigger. |
|Enabled |Boolean |No |true |Whether the Timer Trigger is enabled or not.<br><br><br>* true: Default, enabled<br><br>* false: Turned off |
|Crontab |String |Yes |`*/5 * * * *` |Set the timed triggering time for Timer Triggers. The time format is a crontab expression. You can access [crontab guru](https://crontab.guru/) to view the meanings of the crontab expression. |
|Payload |String |No |`{"body": "create event payload"}` |The Timer Trigger sends the requested content payload, which is the trigger message. The length should not exceed 1,000 unicode characters. |
|EnableConcurrency |Boolean |No |false |Whether the Timer Trigger allows concurrency.<br><br><br>* true: Concurrency is allowed. After turning on, when the specific trigger has not finished the last request, it will not wait until the last request is finished and directly processes the next request in concurrency.<br><br>* false: Default, prohibits concurrency. |
|Retries |Integer |No |0 |The number of retries for the Timer Trigger. |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=CreateTimer&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "qtqzj**",
    "Name": "doc-timer",
    "Description": "Timer Trigger",
    "Enabled": true,
    "Crontab": "*/5 * * * *",
    "EnableConcurrency": false
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|FunctionId |String |qt\*\*\*\* |Function ID. |
|Id |String |v02\*\*\*\* |Timer Trigger ID. |
|Name |String |doc\-timer |Timer Trigger name. |
|Description |String |Timer Trigger |The remarks information for the Timer Trigger. |
|Enabled |Boolean |true |Timer Trigger whether enabled or not, `true` means enabled. |
|Crontab |String |`*/5 * * * *` |The triggering time of the Timer Trigger in the format of a crontab expression. |
|Payload |String |`{"body": "update event payload"}` |The Timer Trigger sends the requested payload, which is the trigger message. |
|CreationTime |String |2024\-06\-14 15:31:07.143863441 +0800 CST m=+88714.902440864 |Timer Trigger creation time. |
|LastUpdateTime |String |2024\-06\-14 15:31:07.143863441 +0800 CST m=+88714.902440864 |Timer Trigger update time. |
|EnableConcurrency |Boolean |true |Whether the Timer Trigger allows concurrency, `true` means concurrency is allowed. |
|Retries |Integer |0 |The number of retries for the Timer Trigger. |


<span id="返回示例"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202411291616311B603AD90**",
        "Action": "CreateTimer",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "FunctionId": "qtqzj**",
        "Id": "ing3qa2**",
        "Name": "doc-timer",
        "Description": "Timer Trigger",
        "Enabled": true,
        "Crontab": "*/5 * * * *",
        "Payload": "",
        "CreationTime": "2024-11-29 16:16:31.540584873 +0800 CST m=+65768.359252459",
        "LastUpdateTime": "2024-11-29 16:16:31.540584953 +0800 CST m=+65768.359252522",
        "EnableConcurrency": false,
        "Retries": 0
    }
}
```


<span id="错误码"></span>
## Error code

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
