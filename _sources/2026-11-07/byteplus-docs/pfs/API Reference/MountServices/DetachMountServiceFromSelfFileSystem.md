---
title: "DetachMountServiceFromSelfFileSystem"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/DetachMountServiceFromSelfFileSystem"
---

Call DetachMountServiceFromSelfFileSystem unbind the vePFS instance from the mount service.

<span id="note"></span>
## Note

After unbinding, the client side business associated with the mount service will all be interrupted, please proceed with caution.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|MountServiceId |String |Yes |mount\-75a6\*\*\*\* |Mount service ID. |
|FileSystemId |String |Yes |vepfs\-apse1dfff3e96\*\*\*\* |The file system ID to unbind. |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DetachMountServiceFromSelfFileSystem&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "MountServiceId": "mount-75a6****",
    "FileSystemId": "vepfs-apse1dfff3e96****"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DetachMountServiceFromSelfFileSystem",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```
