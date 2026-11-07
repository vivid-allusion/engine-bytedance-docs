---
title: "TerminateAsyncTask"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/TerminateAsyncTask"
---

Terminate the asynchronous task.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=TerminateAsyncTask&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |TerminateAsyncTask |Interface name. The current API is called `TerminateAsyncTask`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |wrw\*\*\*\*\*\* |Function ID. You can call the [ListFunctions](https://docs.byteplus.com/en/docs/faas/ListFunctions) interface to obtain function ID (`Items.Id`). |
|RequestId |String |Yes |634f6fbf\-e7fa\-4d87\-85e3\-8b085944a71b |The RequestId of the asynchronous task that needs to be terminated. |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=TerminateAsyncTask&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "wrw******",
    "RequestId": "634f6fbf-e7fa-4d87-85e3-8b085944a71b"
}
```


<span id="返回参数"></span>
## Response parameter 

This interface has no specific response parameters. For public response parameters, refer to [Response result](https://docs.byteplus.com/en/docs/faas/Response_result).

<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TerminateAsyncTask",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    }
}
```


<span id="错误码"></span>
## Error code 

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
