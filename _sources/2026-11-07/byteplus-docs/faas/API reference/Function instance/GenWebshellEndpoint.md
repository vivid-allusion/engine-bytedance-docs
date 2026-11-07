---
title: "GenWebshellEndpoint"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GenWebshellEndpoint"
---

Generate function instance Webshell port.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=GenWebshellEndpoint&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |GenWebshellEndpoint |Interface name. The name of the current API is `GenWebshellEndpoint`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |wrw\*\*\*\*\*\* |Function ID. You can call the [ListFunctions ](https://docs.byteplus.com/en/docs/faas/ListFunctions)interface to obtain Function ID (`Items.Id `). |
|InstanceName |String |Yes |wrw\*\*\*\*\*\*\-vd9qztck6t\-74b9cf8975\-bkd99 |Function instance name. You can call the [ListFunctionInstances](https://docs.byteplus.com/en/docs/faas/ListFunctionInstances) interface to obtain the function instance name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The function instance must be in the <code>Ready</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/faas/ListFunctionInstances">ListFunctionInstances</a> interface to obtain the current status of the function instance.</div><br> |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=GenWebshellEndpoint&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "wrw******",
    "InstanceName": "wrw******-vd9qztck6t-74b9cf8975-bkd99"
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Endpoint |String |wss://\*\*\*\*.byteplus.com/ws\-\*\*\*\*/ap\-southeast\-1/webshell?id=wrw\*\*\*\*&instance=wrw\*\*\*\*\-yp9zrxli\-prtfgld2t8\-mxkbw&ticket=253ac5df\-68ae\-461f\-b65a\-\*\*\*\* |Function Webshell end point connection address. |


<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GenWebshellEndpoint",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Endpoint": "wss://****.byteplus.com/ws-****/ap-southeast-1/webshell?id=wrw****&instance=wrw****-yp9zrxli-prtfgld2t8-mxkbw&ticket=253ac5df-68ae-461f-b65a-****"
    }
}
```


<span id="错误码"></span>
## Error code 

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
