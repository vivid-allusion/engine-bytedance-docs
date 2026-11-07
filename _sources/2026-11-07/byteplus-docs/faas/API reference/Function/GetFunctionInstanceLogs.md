---
title: "GetFunctionInstanceLogs"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GetFunctionInstanceLogs"
---

Query function instance logs information.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=GetFunctionInstanceLogs&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetFunctionInstanceLogs |Interface name. The name of the current API is `GetFunctionInstanceLogs`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The version of the current API is `2024-06-06`. |
|FunctionId |String |Yes |nw\*\*\*\*\*\* |Function ID. |
|Name |String |Yes |nw\*\*\*\*\*\*\-vd9qztck6t\-74b9cf8975\-bkd99 |Function instance name. |
|Limit |Long |No |500 |Set the maximum number of rows for the returned logs, with a value greater than 0.<br><br><br>* Without settings, the logs starting from the container creation are displayed.<br><br>* If the settings are N, the latest N\-line logs will be displayed. |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=GetFunctionInstanceLogs&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "nw******",
    "Name": "nw******-vd9qztck6t-74b9cf8975-bkd99",
    "Limit": 500
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample Value |Description |
|---|---|---|---|
|Logs |String |2024\-06\-25T11:18:25.136415053+08:00 Model loaded in 11.1s (load weights from disk: 3.7s, create model: 0.6s, apply weights to model: 5.5s, load textual inversion embeddings: 0.2s, calculate empty prompt: 1.0s).\n |Function instance logs data. |


<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetFunctionInstanceLogs",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Logs": "2024-06-25T11:18:25.136415053+08:00 Model loaded in 11.1s (load weights from disk: 3.7s, create model: 0.6s, apply weights to model: 5.5s, load textual inversion embeddings: 0.2s, calculate empty prompt: 1.0s).\\n"
    }
}
```


<span id="错误码"></span>
## Error code 

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to [Public error code ](https://docs.byteplus.com/en/docs/faas/Public_error_code)to troubleshoot.
