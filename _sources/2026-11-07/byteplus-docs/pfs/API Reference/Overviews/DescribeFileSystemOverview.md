---
title: "DescribeFileSystemOverview"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/DescribeFileSystemOverview"
---

Call DescribeFileSystemOverview interface to enumerate overview information about the file system.

<span id="request-parameters"></span>
## Request parameters

Empty.

<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|OverView |Object of [FileSystemOverView](https://docs.byteplus.com/en/docs/92/25014#filesystemoverview) |See the return example for details |File system overview information. |


<span id="filesystemoverview"></span>
### FileSystemOverView


|Name |Type |Example |Description |
|---|---|---|---|
|RegionId |String |ap\-southeast\-1 |Area ID. |
|AccountId |String |210004\*\*\*\* |Account ID. |
|ErrorCount |Integer |0 |Number of instances running incorrectly. |
|OtherCount |Integer |0 |The number of instances other than running and running error states. |
|TotalCount |Integer |2 |Total number of instances. |
|RunningCount |Integer |2 |The number of running instances. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeFileSystemOverview&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
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
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "OverView": {
               "AccountId": "210004****",
               "ErrorCount": 0,
               "OtherCount": 0,
               "RegionId": "ap-southeast-1",
               "RunningCount": 2,
               "TotalCount": 2
          }
    }
}
```
