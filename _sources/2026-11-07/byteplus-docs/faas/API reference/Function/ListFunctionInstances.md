---
title: "ListFunctionInstances"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/ListFunctionInstances"
---

Query a list of function instances.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=ListFunctionInstances&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListFunctionInstances |Interface name. The current API is called `ListFunctionInstances`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |nw\*\*\*\*\*\* |Function ID. |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=ListFunctionInstances&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "nw******"
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [FunctionInstance](https://docs.byteplus.com/en/docs/faas/ListFunctionInstances#functioninstance) | |A detailed list of function instances. |
|Total |Integer |1 |The total amount of the data in the response list. |


<span id="functioninstance"></span>
### FunctionInstance


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |nw\*\*\*\*\*\* |Function ID. |
|CreationTime |String |2024\-06\-25 11:17:11.492301904 +0800 CST |Function instance creation time. |
|InstanceName |String |nw\*\*\*\*\*\*\-vd9qztck6t\-74b9cf8975\-bkd99 |Function instance name. |
|InstanceStatus |String |Starting |Function instance status:<br><br><br>* Starting: Starting<br><br>* Ready: Ready<br><br>* Failed: Failed<br><br>* Terminating: Terminating<br><br>* Unknown: Unknown state |
|RevisionNumber |Integer |1 |Function instance version number. |
|UserVpcIP |String |192.168.1.4 |User function binding ENI IPv4 address used by VPC |
|UserVpcIPv6 |String |fdbd:dc01:ff:30a:f323:xxx:xxx:xxx |User function binding ENI IPv6 address used by VPC |
|InstanceType |String | |Instance type (elastic / frozen / activated / reserved) |
|AvailabilityZone |String |ap\-southeast\-1a |Function instance is abbreviated in the AZ name |


<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListFunctionInstances",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Items": [
            {
                "Id": "nw******",
                "CreationTime": "2024-06-25 11:17:11.492301904 +0800 CST",
                "InstanceName": "nw******-vd9qztck6t-74b9cf8975-bkd99",
                "InstanceStatus": "Starting",
                "RevisionNumber": 1
            }
        ],
        "Total": 1
    }
}
```


<span id="错误码"></span>
## Error code 

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
