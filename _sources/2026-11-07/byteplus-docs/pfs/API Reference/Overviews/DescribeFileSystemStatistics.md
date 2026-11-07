---
title: "DescribeFileSystemStatistics"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/DescribeFileSystemStatistics"
---

Call DescribeFileSystemStatistics interface to enumerate file system statistics.

<span id="request-parameters"></span>
## Request parameters

Empty.

<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|Statistics |Array of [FileSystemStatistics](https://docs.byteplus.com/en/docs/92/25015#filesystemstatistics) |See the return example for details |File system statistics. |


<span id="filesystemstatistics"></span>
### FileSystemStatistics


|Name |Type |Example |Description |
|---|---|---|---|
|RegionId |String |ap\-southeast\-1 |Area ID. |
|AccountId |String |210004\*\*\*\* |Account ID. |
|StoreType |String |Advance_100 |File system specification, value selection description is as follows:<br><br><br>* `Advance_100`: 100MB/s/TiB. |
|TotalCount |Integer |2 |Total number of file systems. |
|CapacityInfo |Object of [CapacityInfo](https://docs.byteplus.com/en/docs/92/25015#capacityinfo) |See the return example for details |Capacity information. |
|FileSystemType |String |VePFS |File system type, defaults to`VePFS`. |


<span id="capacityinfo"></span>
### CapacityInfo


|Name |Type |Example |Description |
|---|---|---|---|
|UsedGiB |Integer |117 |The file system uses capacity in gibs. |
|TotalTiB |Integer |28 |Total file system capacity in TiB. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeFileSystemStatistics&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeFileSystemStatistics",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Statistics": [
            {
                "RegionId": "ap-southeast-1",
                "AccountId": "210004****",
                "StoreType": "Advance_100",
                "TotalCount": 2,
                "CapacityInfo": {
                    "TotalTiB": 0,
                    "UsedGiB": 0
                },
                "FileSystemType": "VePFS"
            }
        ]
    }
}
```
