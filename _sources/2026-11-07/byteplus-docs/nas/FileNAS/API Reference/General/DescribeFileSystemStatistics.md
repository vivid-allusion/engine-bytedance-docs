---
title: "DescribeFileSystemStatistics"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/DescribeFileSystemStatistics"
---

Call DescribeFileSystemStatistics interface to enumerate file system statistics.

<span id="request-parameters"></span>
## Request parameters

Empty.

<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|TotalCount |Integer |2 |Total number of file systems. |
|Statistics |Array of [Statistic](https://docs.byteplus.com/en/docs/91/24982#statistic) |See the return example for details |File system statistics. |


<span id="statistic"></span>
### Statistic


|Name |Type |Example |Description |
|---|---|---|---|
|ZoneId |String |ap\-southeast\-1a |Availability zone ID. |
|RegionId |String |ap\-southeast\-1 |Region ID. |
|CommonCapacity |Object of [Capacity](https://docs.byteplus.com/en/docs/91/24982#capacity) |{<br><br>"Total": 100,<br><br>"Used": 135<br><br>} |Generic file system capacity information. |
|ExtremeCapacity |Object of [Capacity](https://docs.byteplus.com/en/docs/91/24982#capacity) |{<br><br>"Total": 100,<br><br>"Used": 135<br><br>} |Extremely fast file system capacity information. |
|CommonFileSystemCount |Integer |0 |Number of general\-purpose file systems. |
|ExtremeFileSystemCount |Integer |1 |Number of extremely fast file systems. |


<span id="capacity"></span>
### Capacity


|Name |Type |Example |Description |
|---|---|---|---|
|Used |Long |135 |The file system has used capacity in MiB. |
|Total |Long |100 |Total available file system capacity in GiB. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeFileSystemStatistics&Version=2022-01-01 HTTP/1.1
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
        "Action": "DescribeFileSystemStatistics",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "TotalCount": 1,
        "Statistics": [
            {
                "ZoneId": "ap-southeast-1",
                "RegionId": "ap-southeast-1",
                "CommonCapacity": {
                    "Used": 135,
                    "Total": 100
                },
                "ExtremeCapacity": {
                    "Used": 135,
                    "Total": 100
                },
                "CommonFileSystemCount": 0,
                "ExtremeFileSystemCount": 1
            }
        ]
    }
}
```
