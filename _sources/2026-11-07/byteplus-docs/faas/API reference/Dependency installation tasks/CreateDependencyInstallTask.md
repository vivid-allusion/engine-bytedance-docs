---
title: "CreateDependencyInstallTask"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/CreateDependencyInstallTask"
---

Creating dependency installation tasks.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: http://open.volcengineapi.com/?Action=CreateDependencyInstallTask&Version=2024\-06\-06


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDependencyInstallTask&serviceCode=vefaas&version=2024-06-06&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateDependencyInstallTask |Interface name. The name of the current API is `CreateDependencyInstallTask`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|FunctionId |String |Yes |wrwsk\*\*\*\* |Function ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://open.volcengineapi.com/?Action=CreateDependencyInstallTask&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "wrwsk****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

There are no dedicated response parameters for this API. For common response parameters, see [Responses](https://docs.byteplus.com/en/docs/faas/Response_result).

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateDependencyInstallTask",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
