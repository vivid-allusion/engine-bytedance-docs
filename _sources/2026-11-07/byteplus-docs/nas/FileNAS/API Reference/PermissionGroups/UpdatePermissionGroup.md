---
title: "UpdatePermissionGroup"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/UpdatePermissionGroup"
---

Call UpdatePermissionGroup update permission group information.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemType |String |Yes |Extreme |File system type. The value selection description is as follows:<br><br><br>* `Extreme`: NAS Extreme Speed. |
|PermissionGroupId |String |Yes |pgroup\-6dn7\*\*\*\* |Permission group ID. |
|PermissionGroupName |String |No |test |Permission group name. The naming convention is as follows:<br><br><br>* Cannot start with a number or a dash (\-).<br><br>* Can only contain Chinese, letters, numbers, underscores (_) or underscores (\-).<br><br>   The length is from 1 to 128 characters. |
|Description |String |No |Just\-for\-test |Permission group description information, with a length of 0 to 120 characters. |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=UpdatePermissionGroup&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemType": "Extreme",
    "PermissionGroupId": "pgroup-6dn7****",
    "PermissionGroupName": "test",
    "Description": "Just-for-test"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdatePermissionGroup",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```
