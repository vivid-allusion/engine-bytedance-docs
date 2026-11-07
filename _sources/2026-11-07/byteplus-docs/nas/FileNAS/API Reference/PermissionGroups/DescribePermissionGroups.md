---
title: "DescribePermissionGroups"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/DescribePermissionGroups"
---

Call DescribePermissionGroups interface to view permission group information.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemType |String |Yes |Extreme |File system type. The value selection description is as follows:<br><br><br>* `Extreme`：NAS Extreme Speed. |
|PageSize |Integer |No |10 |The pagination page number of the file system list. |
|PageNumber |Integer |No |1 |Number of file systems per page. |
|Filters |Array of [PermissionGroupFilter](https://docs.byteplus.com/en/docs/91/24991#permissiongroupfilter) |No |See the request example for details |Filters the permission group for the specified feature. |


<span id="permissiongroupfilter"></span>
### PermissionGroupFilter


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |Yes |PermissionGroupName |Filter the permission group for the specified feature based on the feature. The parameters that support filtering are as follows:<br><br><br>* `PermissionGroupName`: Fuzzy filtering based on permission group name, multiple selection is not supported.<br><br>* `PermissionGroupId`: Precise filtering based on permission group ID, multiple selection is not supported. |
|Value |String |Yes |test |Filter the value of the item. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|TotalCount |Integer |1 |Number of permission groups. |
|PageSize |Integer |10 |The pagination page number of the file system list. |
|PageNumber |Integer |1 |The number of file systems per page. |
|PermissionGroups |Array of [PermissionGroup](https://docs.byteplus.com/en/docs/91/24991#permissiongroup) |See the return example for details |Permission group information does not contain valid permission rule information. |


<span id="permissiongroup"></span>
### PermissionGroup


|Name |Type |Example |Description |
|---|---|---|---|
|CreateTime |String |2022\-05\-26 T20:09:00 + 08:00 |Permission group creation time. |
|Description |String |test |Permission group description information. |
|MountPoints |Array of [BasicMountPoint](https://docs.byteplus.com/en/docs/91/24991#basicmountpoint) |See the return example for details |Use the mount point information for this permission group. |
|FileSystemType |String |Extreme |File system type. The value selection description is as follows:<br><br><br>* `Extreme`: NAS Extreme Speed. |
|FileSystemCount |Integer |1 |Number of file systems associated with this permission group. |
|PermissionGroupId |String |test |Permission group ID. |
|PermissionGroupName |String |test |Permission group name. |
|PermissionRuleCount |Integer |1 |Number of permission rules. |


<span id="basicmountpoint"></span>
### BasicMountPoint


|Name |Type |Example |Description |
|---|---|---|---|
|FileSystemId |String |eenas\-1c789dca\*\*\*\* |File system ID. |
|MountPointId |String |mount\-a6ee\*\*\*\* |Mount Point ID. |
|MountPointName |String |MountPoint |Mount point name. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribePermissionGroups&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "PageSize": 10,
    "PageNumber": 1,
    "Filters": [
        {
            "Key": "PermissionGroupName",
            "Value": "test"
        }
    ]
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribePermissionGroups",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "TotalCount": 1,
        "PageSize": 10,
        "PageNumber": 1,
        "PermissionGroups": [
            {
                "CreateTime": "2022-05-26T20:09:00+08:00",
                "Description": "test",
                "MountPoints": [
                    {
                        "FileSystemId": "eenas-1c789dca****t",
                        "MountPointId": "mount-a6ee****",
                        "MountPointName": "MountPoint"
                    }
                ],
                "FileSystemType": "Extreme",
                "FileSystemCount": 1,
                "PermissionGroupId": "test",
                "PermissionGroupName": "test",
                "PermissionRuleCount": 1
            }
        ]
    }
}
```
