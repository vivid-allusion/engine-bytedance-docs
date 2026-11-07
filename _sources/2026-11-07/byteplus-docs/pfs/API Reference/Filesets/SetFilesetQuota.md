---
title: "SetFilesetQuota"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/SetFilesetQuota"
---

Call the SetFilesetQuota interface to set the Quota information of the Fileset.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemId |String |Yes |vepfs\-apse1dfff3e96\*\*\*\* |File system ID. |
|FilesetId |String |Yes |fset\-719d\*\*\*\* |The Fileset ID that needs to be set. |
|FileLimit |Long |No |3000 |Fileset file count quota limit.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">The number of files quota cannot exceed the Inode limit, you can call the <a href="https://docs.byteplus.com/en/docs/pfs/DescribeFilesets">DescribeFilesets</a> interface to check the Inode limit.</div><br> |
|CapacityLimit |Integer |No |3000 |Fileset capacity quota limit in gibs. |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=SetFilesetQuota&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemId": "vepfs-apse1dfff3e96****",
    "FilesetId": "fset-719d**** ",
    "FileLimit": 3000,
    "CapacityLimit": 3000
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "SetFilesetQuota",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```
