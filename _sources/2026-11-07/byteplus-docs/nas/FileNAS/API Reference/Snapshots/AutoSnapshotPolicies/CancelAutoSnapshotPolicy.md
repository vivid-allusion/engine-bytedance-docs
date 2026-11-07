---
title: "CancelAutoSnapshotPolicy"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/CancelAutoSnapshotPolicy"
---

Call CancelAutoSnapshotPolicy interface to unbind the automatic snapshot policy for the file storage instance.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemIds |String |Yes |enas\-18bcb923\*\*\*\* |The file system ID that needs to be untied for the automatic snapshot policy. Multiple IDs are supported, separated by English commas (,). |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=CancelAutoSnapshotPolicy&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemIds": "enas-18bcb923****"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CancelAutoSnapshotPolicy",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```
