---
title: "SetSandboxTimeout"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/SetSandboxTimeout"
---

Modify the lifetime of sandbox instances.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=SetSandboxTimeout&Version=2024\-06\-06


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |SetSandboxTimeout |Interface name. The name of the current API is `SetSandboxTimeout`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|FunctionId |String |Yes |e8m6\*\*\*\* |The ID of the sandbox application to which sandbox instances belong.<br><br>To obtain sandbox application IDs, you can go to [Function Service Console](https://console.byteplus.com/vefaas) \> **Cloud sandbox** \> **Sandbox application** page. |
|SandboxId |String |Yes |vefaas\-e8m6xarn\-p2zamuv2fr\-\*\*\*\* |Sandbox instance ID/name.<br><br>To obtain sandbox instance IDs, you can go to [BytePlus Function Service (FaaS) console](https://console.byteplus.com/vefaas) \> **Cloud sandbox** \> **Sandbox application** page, click the target sandbox application, and switch to **Sandbox example** tab. |
|Timeout |Integer |Yes |60 |Sandbox instance lifetime:<br><br><br>* Unit: minutes<br><br>* Value range: 3 to 1440<br><br>* Default value: 60 |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=SetSandboxTimeout&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "e8m6****",
    "SandboxId": "vefaas-e8m6xarn-p2zamuv2fr-****",
    "Timeout": 60
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|FunctionId |String |e8m6\*\*\*\* |Sandbox application ID. |
|SandboxId |String |vefaas\-e8m6xarn\-p2zamuv2fr\-\*\*\*\* |Sandbox instance ID/name. |
|ExpireAt |String |2025\-04\-25 11:31:29.376 +0000 UTC |Sandbox instance lifetime. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "SetSandboxTimeout",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "FunctionId": "e8m6****",
        "SandboxId": "vefaas-e8m6xarn-p2zamuv2fr-****",
        "ExpireAt": "2025-04-25 11:31:29.376 +0000 UTC"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
