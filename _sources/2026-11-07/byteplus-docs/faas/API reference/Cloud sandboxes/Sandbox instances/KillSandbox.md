---
title: "KillSandbox"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/KillSandbox"
---

Delete the cloud sandbox instance.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=KillSandbox&Version=2024\-06\-06


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |KillSandbox |Interface name. The name of the current API is `KillSandbox`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|FunctionId |String |Yes |e8m6\*\*\*\* |The ID of the sandbox application to which the sandbox instance belongs.<br><br>To obtain sandbox application IDs, you can go to [Function Service Console](https://console.byteplus.com/vefaas) \> **Cloud sandbox** \> **Sandbox application** page. |
|SandboxId |String |Yes |vefaas\-e8m6xarn\-p2zamuv2fr\-\*\*\*\* |Sandbox instance ID/name.<br><br>To obtain sandbox instance IDs, you can go to [BytePlus Function Service (FaaS) console](https://console.byteplus.com/vefaas) \> **Cloud sandbox** \> **Sandbox application** page, click the target sandbox application, and switch to **Sandbox example** tab. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=KillSandbox&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "e8m6****",
    "SandboxId": "vefaas-e8m6xarn-p2zamuv2fr-****"
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
        "Action": "KillSandbox",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
