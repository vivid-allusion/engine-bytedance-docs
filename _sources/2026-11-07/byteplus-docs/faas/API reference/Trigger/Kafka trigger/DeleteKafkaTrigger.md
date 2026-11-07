---
title: "DeleteKafkaTrigger"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/DeleteKafkaTrigger"
---

Delete the specified Kafka Trigger.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=DeleteKafkaTrigger&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteKafkaTrigger |Interface name. The current API is called `DeleteKafkaTrigger`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|Id |String |Yes |nw\*\*\*\*\*\* |Kafka Trigger ID. You can call the [ListTriggers](https://docs.byteplus.com/en/docs/faas/ListTriggers) interface to obtain the Trigger ID. |
|FunctionId |String |Yes |wrw\*\*\*\*\*\* |Function ID. You can call the [ListFunctions](https://docs.byteplus.com/en/docs/faas/ListFunctions) interface to obtain function ID (`Items.Id`). |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=DeleteKafkaTrigger&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "Id": "nw******",
    "FunctionId": "wrw******"
}
```


<span id="返回参数"></span>
## Response parameter 

This interface has no specific response parameter. For public response parameters, refer to [Response results](https://docs.byteplus.com/en/docs/faas/Response_result).

<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteKafkaTrigger",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    }
}
```


<span id="错误码"></span>
## Error code 

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
