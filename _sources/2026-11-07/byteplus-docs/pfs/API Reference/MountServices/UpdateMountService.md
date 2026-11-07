---
title: "UpdateMountService"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/UpdateMountService"
---

Call the UpdateMountService interface to modify the mount service information.

<span id="note"></span>
## Note

Currently only modifying the mount service name is supported.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|MountServiceId |String |Yes |mount\-75a6\*\*\*\* |The mount service ID that needs to be modified. |
|MountServiceName |String |No |mountservice |The name of the mount service that needs to be modified. The value selection description is as follows:<br><br><br>* Cannot start with numbers, dashes (\-) and underscores (_).<br><br>* Can only contain Chinese, letters, numbers, underscores (_) and dashes (\-).<br><br>   The length should be between 1 and 128 characters.<br><br>* The mount service name under each account in each region is unique and cannot be repeated. |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=UpdateMountService&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "MountServiceId": "mount-75a6****",
    "MountServiceName": "mountservice"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateMountService",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```
