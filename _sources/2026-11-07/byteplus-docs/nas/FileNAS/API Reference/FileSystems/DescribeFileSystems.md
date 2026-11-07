---
title: "DescribeFileSystems"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/DescribeFileSystems"
---

Call the DescribeFileSystems interface to enumerate the file system.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|PageSize |Integer |No |10 |When the query results are displayed in pages, this parameter is used to represent the amount of data per page. The range of values is 1 to 100. |
|PageNumber |Integer |No |1 |This parameter is used to represent the page number when the query results are displayed in pages. The minimum supported value is 1. |
|FileSystemIds |String |No |enas\-apse1a03854ca4a\*\*\*\* |The file system ID that needs to be enumerated, supports multiple selection, and is separated by English commas (,). |
|ProjectName |String |No |default |Project name. |
|FileSystemType |String |No |Extreme |File system type. The value selection description is as follows:<br><br><br>* `Extreme`: NAS Extreme Speed. |
|SortOrderType |String |No |Desc |Sort by, the value selection description is as follows:<br><br><br>* `Desc`: Descending order.<br><br>* `Asc`: ascending order. |
|SortByType |String |No |CreateTime |Sorting type, value selection description is as follows:<br><br><br>* `CreateTime`: Sort by creation time.<br><br>* `Capacity`: sorted by total capacity. |
|Filters |Array of [FileSystemFilter](https://docs.byteplus.com/en/docs/91/24979#filesystemfilter) |No |See sample values for details |Filter for eligible file system information. |
|TagFilters |Array of [TagFilter](https://docs.byteplus.com/en/docs/91/24979#tagfilter) |No |See sample values for details |Filter file system information that meets the label criteria. |


<span id="filesystemfilter"></span>
### FileSystemFilter


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |Yes |Status |Filters instances of the specified feature based on the feature. The parameters that support filtering are as follows:<br><br><br>* `Status`: Precise filtering according to file system status, supports multiple selection, and is separated by English commas (,).<br><br>* `FileSystemName`: Fuzzy filtering based on filesystem name, multiple selection is not supported.<br><br>* `ZoneId`: Precise filtering based on availability zone ID, multiple selection is not supported.<br><br>* `ProtocolType`: Precise filtering according to file system protocol, multiple selection is not supported.<br><br>* `StorageType`: Precise filtering according to storage specifications, multiple selection is not supported.<br><br>* `ChargeType`: Precise filtering according to billing type, multiple selection is not supported.<br><br>* `PermissionGroupId`: Precise filtering based on permission group ID, multiple selection is not supported.<br><br>* `MountPointId`: Precise filtering based on mount point ID, multiple selection is not supported. |
|Value |String |Yes |Running |Filter the value of the item. |


<span id="tagfilter"></span>
### TagFilter


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |Yes |tagkey |Label key. |
|Value |String |No |tagvalue |Label value. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|TotalCount |Integer |1 |Total number of file systems. |
|PageSize |Integer |10 |When the query results are displayed in pages, it indicates the amount of data per page. |
|PageNumber |Integer |1 |When the query results are displayed in pages, it indicates the page number. |
|FileSystems |Array of [FileSystem](https://docs.byteplus.com/en/docs/91/24979#filesystem) |See the return example for details |File system information. |


<span id="filesystem"></span>
### FileSystem


|Name |Type |Example |Description |
|---|---|---|---|
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/91/24979#tag) |See the return example for details |Tag information for the file system. |
|ZoneId |String |ap\-southeast\-1a |Availability zone ID. |
|Version |String |1.1.7.0 |Version number. |
|Capacity |Object of [Capacity](https://docs.byteplus.com/en/docs/91/24979#capacity) |{<br><br>"Total": 102400,<br><br>"Used": 135<br><br>} |Capacity information. |
|RegionId |String |ap\-southeast\-1 |Area ID. |
|ZoneName |String |Asia Pacific (Johor) A |Availability zone name. |
|ChargeType |String |PayAsYouGo |Billing status, value selection description is as follows:<br><br><br>* `PayAsYouGo`: Billing by volume. |
|CreateTime |String |2022\-08\-14 T13:15:39 + 08:00 |File system creation time. |
|UpdateTime |String |2023\-04\-21 T15:26:14 + 08:00 |File system update time. |
|Description |String |test |File system description information. |
|ProjectName |String |default |The project to which the file system belongs. |
|StorageType |String |Standard |File system storage type. The value selection description is as follows:<br><br><br>* `Standard`: Extreme speed standard type. |
|FileSystemId |String |enas\-2b4f43b\*\*\*\* |File system ID. |
|ProtocolType |String |NFS |File system protocol type. The value selection description is as follows:<br><br><br>* `NFS`: NFS protocol, often used Linux client side. |
|SnapshotCount |Integer |1 |Number of snapshots. |
|FileSystemName |String |lytest |File system name. |
|FileSystemType |String |Extreme |File system type. The value selection description is as follows:<br><br><br>* `Extreme`: NAS Extreme Speed. |


<span id="tag"></span>
### Tag


|Name |Type |Example |Description |
|---|---|---|---|
|Key |String |tagkey |Label key. |
|Type |String |Custom |The label type is described as follows:<br><br><br>* `Custom`: user\-defined labels.<br><br>* `System`: System label. |
|Value |String |tagvalue |Label value. |


<span id="capacity"></span>
### Capacity


|Name |Type |Example |Description |
|---|---|---|---|
|Used |Long |135 |The file system has used capacity in MiB. |
|Total |Long |100 |Total available file system capacity in GiB. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeFileSystems&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "PageSize": 10,
    "PageNumber": 1,
    "FileSystemIds": "enas-1234****",
    "ProjectName": "default",
    "Filters": [
        {
            "Key": "Status",
            "Value": "Running"
        }
    ],
    "TagFilters": [
        {
            "Key": "tagkey",
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
        "Action": "DescribeFileSystems",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "TotalCount": 1,
        "PageSize": 10,
        "PageNumber": 1,
        "FileSystems": [
            {
                "Tags": [
                    {
                        "Key": "tagkey",
                        "Type": "Custom",
                        "Value": "tagvalue"
                    }
                ],
                "Status": "Running",
                "ZoneId": "ap-southeast-1a",
                "Version": "1.1.7.0",
                "Capacity": {
                    "Used": 135,
                    "Total": 100
                },
                "RegionId": "ap-southeast-1",
                "ChargeType": "PayAsYouGo",
                "CreateTime": "2022-08-14T13:15:39+08:00",
                "UpdateTime": "2023-04-21T15:26:14+08:00",
                "Description": "test",
                "ProjectName": "default",
                "StorageType": "Standard",
                "FileSystemId": "enas-d2b4f43b****",
                "ProtocolType": "NFS",
                "SnapshotCount": 1,
                "FileSystemName": "lytest",
                "FileSystemType": "Extreme"
            }
        ]
    }
}
```
