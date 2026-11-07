---
title: "DescribeFileSystems"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/DescribeFileSystems"
---

Call the DescribeFileSystems interface to query the file system.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|PageSize |Integer |No |10 |Number of records per page, the default is 10. |
|PageNumber |Integer |No |1 |The page number of the list, up to the maximum value of the Integer data type, starting at 1. |
|OrderBy |String |No |CreateTimeDesc |File system sort type, defaults to descending order by creation time. the value selection description is as follows:<br><br><br>* `CreateTimeDesc`: in descending order according to the creation time of the file system.<br><br>* `CreateTimeAsc`: In ascending order according to the creation time of the file system of the file system.<br><br>* `CapacityDesc`: in descending order according to the total capacity of the file system.<br><br>* `CapacityAsc`: in ascending order according to the total capacity of the file system.<br><br>* `IdDesc`: in descending order by file system ID.<br><br>* `IdAsc`: In ascending order by file system ID. |
|Filters |Array of [FileSystemFilter](https://docs.byteplus.com/en/docs/92/25008#filesystemfilter) |No |See the request example for details |File system filter information, filter eligible file system information. |
|Project |String |No |default |Filter by project name. |
|FileSystemIds |String |No |vepfs\-apse1dfff3e96\*\*\*\* |Filter by instance ID, with multiple IDs separated by a comma (,). |


<span id="filesystemfilter"></span>
### FileSystemFilter


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |Yes |FileSystemName |Filters instances of the specified feature based on the feature. The parameters that support filtering are as follows:<br><br><br>* `ChargeType`: Precise filtering according to billing type, multiple selection is not supported.<br><br>* `FileSystemType`: Precise filtering by file system type, multiple selection is not supported.<br><br>* `StoreType`: Precise filtering according to storage specifications, multiple selection is not supported.<br><br>* `FileSystemName`: Fuzzy filtering based on filesystem name, multiple selection is not supported.<br><br>* `Status`: Precise filtering according to file system status, supports multiple selection, and is separated by English commas (,).<br><br>* `ZoneId`: Precise filtering based on the filesystem availability zone, multiple selection is not supported.<br><br>* `Protocol`: Accurate filtering according to the file system protocol, multiple selection is not supported.<br><br>* `AccountId`: Precise filtering according to the account ID to which the file system belongs, multiple selection is not supported. |
|Value |String |Yes |aaa |Filter the value of the item. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|TotalCount |Integer |1 |Number of file systems. |
|PageSize |Integer |10 |Number of file systems per page. |
|PageNumber |Integer |1 |The pagination page number of the file system list. |
|FileSystems |Array of [FileSystem](https://docs.byteplus.com/en/docs/92/25008#filesystem) |See the return example for details |File system details. |


<span id="filesystem"></span>
### FileSystem


|Name |Type |Example |Description |
|---|---|---|---|
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/92/25008#tag) |See the return example for details |The label information of the file system is returned when adding labels while creating the file system. |
|Status |String |Running |File system status. value selection description is as follows:<br><br><br>* `Running`: The instance is running.<br><br>* `Creating`: Instance is being created.<br><br>* `CreateError`: Instance creation failed.<br><br>* `Updating`: The instance is being updated.<br><br>* `UpdateError`: Instance update failed.<br><br>* `Expanding`: Instance expansion in progress.<br><br>* `ExpandError`: Instance scaling failed.<br><br>* `Deleting`: Instance deleting.<br><br>* `DeleteError`: Instance deletion failed.<br><br>* `Stopped`: The instance has been shut down.<br><br>* `Error`: The instance is in an error state. |
|ZoneId |String |ap\-southeast\-1a |Availability zone ID. |
|Project |String |vepfs\-test |The project to which the file system belongs. |
|Version |String |5.1.2.4 |File system version. |
|FreeTime |String |2022\-12\-22 T00:00:00 + 08:00 |File system release time. |
|RegionId |String |ap\-southeast\-1 |Area ID. |
|AccountId |String |210004\*\*\*\* |Account ID. |
|Bandwidth |Integer |600 |vePFS file system throughput cap. |
|StoreType |String |Advance_100 |File system specification, value selection description is as follows:<br><br><br>* Advance_100: 100MB/s/TiB |
|ChargeType |String |PayAsYouGo |Billing type. The value selection description is as follows:<br><br>`PayAsYouGo`: Billed by volume. |
|CreateTime |String |2022\-09\-15 T18:17:09 + 08:00 |File system creation time. |
|ExpireTime |String |2022\-12\-15 T23:59:59 + 08:00 |File system expiration time. |
|Description |String |test |File system description information. |
|CapacityInfo |Object of [CapacityInfo](https://docs.byteplus.com/en/docs/92/25008#capacityinfo) | |Capacity information. |
|ChargeStatus |String |Normal |Billing status, the default is`Normal`, which means normal billing. |
|FileSystemId |String |vepfs\-sw07b082188a\*\*\*\* |File system ID. |
|ProtocolType |String |VePFS |File system protocol type. |
|FileSystemName |String |test |File system name. |
|FileSystemType |String |VePFS |File system type, defaults to`VePFS`. |
|LastModifyTime |String |2022\-09\-15 T18:25:22 + 08:00 |File system update time. |
|StopServiceTime |String |2022\-12\-16 T12:00:00 + 08:00 |File system shutdown time. |


<span id="tag"></span>
### Tag


|Name |Type |Example |Description |
|---|---|---|---|
|Key |String |tag_00 |Label key. |
|Type |String |Custom |The label type is described as follows:<br><br><br>* `Custom`: user\-defined labels.<br><br>* `System`: System label. |
|Value |String |tag_value00 |Label value. |


<span id="capacityinfo"></span>
### CapacityInfo


|Name |Type |Example |Description |
|---|---|---|---|
|UsedGiB |Integer |117 |The file system uses capacity in gibs. |
|TotalTiB |Integer |28 |Total file system capacity in TiB. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeFileSystems&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "PageSize": 10,
    "PageNumber": 1,
    "OrderBy": "CreateTimeDesc",
    "Filters": [
        {
            "Key": "FileSystemName",
            "Value": "aaa"
        }
    ],
    "Project": "default",
    "FileSystemIds": "vepfs-apse1dfff3e96****"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeFileSystems",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
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
                        "Key": "tag_00",
                        "Type": "Custom",
                        "Value": "tag_value00"
                    }
                ],
                "Status": "Running",
                "ZoneId": "ap-southeast-1a",
                "Project": "vepfs-test",
                "Version": "5.1.2.4",
                "FreeTime": "2022-12-22T00:00:00+08:00",
                "RegionId": "ap-southeast-1",
                "AccountId": "210004****",
                "Bandwidth": 600,
                "StoreType": "Advance_100",
                "ChargeType": "PayAsYouGo",
                "CreateTime": "2022-09-15T18:17:09+08:00",
                "ExpireTime": "2022-12-15T23:59:59+08:00",
                "Description": "test",
                "CapacityInfo": "{ \"TotalTiB\": 6, \"UsedGiB\"：20 }",
                "ChargeStatus": "Normal",
                "FileSystemId": "vepfs-sw07b082188a****",
                "ProtocolType": "VePFS",
                "FileSystemName": "test",
                "FileSystemType": "VePFS",
                "LastModifyTime": "2022-09-15T18:25:22+08:00",
                "StopServiceTime": "2022-12-16T12:00:00+08:00"
            }
        ]
    }
}
```
