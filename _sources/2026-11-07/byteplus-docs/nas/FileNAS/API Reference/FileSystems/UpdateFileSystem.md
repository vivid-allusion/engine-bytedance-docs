---
title: "UpdateFileSystem"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/UpdateFileSystem"
---

Call the UpdateFileSystem interface to update file system information.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemId |String |Yes |enas\-apse1a03854ca4a\*\*\*\* |File system ID. |
|FileSystemName |String |No |test |File system name. The naming convention is as follows:<br><br><br>* Cannot start with a number or a dash (\-).<br><br>* Can only contain Chinese, letters, numbers, underscores (_) and underscores (\-).<br><br>   The length should be between 1 and 128 characters. |
|Description |String |No |Just\-for\-test |File system description information. |
|ProjectName |String |No |default |The project to which the file system belongs. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/91/24985#tag) |No |See the request example for details |Label information to be added. |


<span id="tag"></span>
### Tag


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |Yes |tagkey |Label key. |
|Type |String |Yes |Custom |The label type is described as follows:<br><br><br>* `Custom`: user\-defined labels.<br><br>* `System`: System label. |
|Value |String |Yes |tagvalue |Label value. |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=UpdateFileSystem&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemId": "enas-a8cecb87****",
    "FileSystemName": "test",
    "Description": "Just-for-test",
    "ProjectName": "default",
    "Tags": [
        {
            "Key": "tagkey",
            "Type": "Custom",
            "Value": "tagvalue"
        }
    ]
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateFileSystem",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```
