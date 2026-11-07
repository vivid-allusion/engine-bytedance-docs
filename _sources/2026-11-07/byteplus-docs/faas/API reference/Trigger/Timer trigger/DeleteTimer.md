---
title: "DeleteTimer"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/DeleteTimer"
---

Call the DeleteTimer interface and delete the Timer Trigger.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=DeleteTimer&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteTimer |Interface name. The current API is called `DeleteTimer`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |wr\*\*\*\*\*\* |The ID of the function to which the Timer Trigger belongs. |
|Id |String |Yes |nw\*\*\*\*\*\* |Timer Trigger ID. |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=DeleteTimer&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "wr******",
    "Id": "nw******"
}
```


<span id="返回参数"></span>
## Response parameter 

This interface has no specific response parameters.

<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "2024112916240762FADB89F5**",
        "Action": "DeleteTimer",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id="错误码"></span>
## Error code 

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
