---
title: "DescribeFileSystemOverview"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/DescribeFileSystemOverview"
---

Call DescribeFileSystemOverview interface to enumerate file system overview information.

<span id="request-parameters"></span>
## Request parameters

Empty.

<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|Overview |Object of [Overview](https://docs.byteplus.com/en/docs/91/24981#overview) |See the return example for details |File system overview information. |


<span id="overview"></span>
### Overview


|Name |Type |Example |Description |
|---|---|---|---|
|RegionId |String |ap\-southeast\-1 |Region ID. |
|ErrorCount |Integer |0 |The number of incorrect file systems. |
|OtherCount |Integer |1 |The number of file systems in addition to running and error states. |
|TotalCount |Integer |2 |Total number of file systems. |
|RunningCount |Integer |1 |The number of file systems running. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeFileSystemOverview&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeFileSystemOverview",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Overview": {
            "RegionId": "ap-southeast-1",
            "ErrorCount": 0,
            "OtherCount": 1,
            "TotalCount": 2,
            "RunningCount": 1
        }
    }
}
```
