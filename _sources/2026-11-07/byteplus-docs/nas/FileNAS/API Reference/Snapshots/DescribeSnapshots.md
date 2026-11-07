---
title: "DescribeSnapshots"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/DescribeSnapshots"
---

Call the DescribeSnapshots interface to query the snapshot of the specified file system.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemId |String |No |extreme\-22f\*\*\*\* |Specifies the file system ID. |
|SnapshotIds |String |No |snap\-472a716f\*\*\*\* |Snapshot ID. |
|SnapshotName |String |No |FinanceJoshua |Snapshot name. |
|SnapshotType |String |No |Manual |Snapshot type, value selection description is as follows:<br><br><br>* `Manual`: Manual snapshots. |
|PageSize |Integer |No |10 |The number of rows per page to set when paging a query. |
|PageNumber |Integer |No |1 |The page number of the snapshot list. |
|Status |String |No |all |Snapshot status. The value selection description is as follows:<br><br><br>* `Progressing`: The snapshot being created.<br><br>* `Accomplished`: Create a successful snapshot.<br><br>* `Failed`: Create a failed snapshot.<br><br>* `all` (default): All snapshot states. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|TotalCount |Integer |36 |Total number of snapshots. |
|PageSize |Integer |10 |The number of rows per page to set when paging a query. |
|PageNumber |Integer |1 |The page number of the snapshot list. |
|Snapshots |Array of [Snapshot](https://docs.byteplus.com/en/docs/91/25000#snapshot) |See the return example for details |Snapshot details. |


<span id="snapshot"></span>
### Snapshot


|Name |Type |Example |Description |
|---|---|---|---|
|Status |String |Progressing |Snapshot status. Description as follows:<br><br><br>* `Progressing`: Creating.<br><br>* `Accomplished`: Created successfully.<br><br>* `Failed`: Failed to create |
|ZoneId |String |ap\-southeast\-1a |Availability zone ID. |
|Progress |String |100 |Snapshot creation progress. |
|IsEncrypt |Boolean |false |Whether to encrypt, currently only`false`is supported, that is, no encryption. |
|CreateTime |String |2022\-11\-16 T11:18:02 + 08:00 |Snapshot creation time. |
|SnapshotId |String |snap\-472a716f\*\*\*\* |Snapshot ID. |
|SourceSize |Integer |100 |File system capacity, in GiB. |
|Description |String |test |Snapshot description information. |
|FileSystemId |String |enas\-apse1a03854ca4a\*\*\*\* |File system ID. |
|SnapshotName |String |testcreate |Snapshot name. |
|SnapshotType |String |Manual |Snapshot type, the default is`Manual`, that is, manual snapshot. |
|RetentionDays |Integer |2147483647 |Snapshot retention time, the default is`2147483647`, which is permanent retention. |
|SourceVersion |String |1.1.10.7 |File system version. |
|FileSystemName |String |doctest |File system name. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeSnapshots&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
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
        "Action": "DescribeSnapshots",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "TotalCount": 36,
        "PageSize": 10,
        "PageNumber": 1,
        "Snapshots": [
            {
                "Status": "Progressing",
                "ZoneId": "ap-southeast-1a",
                "Progress": "100",
                "IsEncrypt": true,
                "CreateTime": "2022-11-16T11:18:02+08:00",
                "SnapshotId": "snap-472a716f****",
                "SourceSize": 100,
                "Description": "test",
                "FileSystemId": "enas-c789dca****",
                "SnapshotName": "testcreate",
                "SnapshotType": "Manual",
                "RetentionDays": 2147483647,
                "SourceVersion": "1.1.10.7",
                "FileSystemName": "doctest"
            }
        ]
    }
}
```
