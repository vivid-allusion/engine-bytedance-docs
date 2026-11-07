---
title: "DescribeMountPoints"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/DescribeMountPoints"
---

Call the DescribeMountPoints interface to view mount point information.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemId |String |Yes |enas\-18bcb923\*\*\*\* |The file system ID to query. |
|MountPointName |String |No |MountPoint |Mount point name. |
|MountPointId |String |No |mount\-a6ee\*\*\*\* |Mount Point ID. |
|VpcId |String |No |vpc\-30uexwepls3cw7r2qr2h2\*\*\*\* |Private network ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeVpcs">DescribeVpcs</a> interface to query the private network ID.</div><br> |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|TotalCount |Integer |1 |Number of mount points. |
|MountPoints |Array of [MountPoint](https://docs.byteplus.com/en/docs/91/24986#mountpoint) |See the return example for details |Mount point information. |


<span id="mountpoint"></span>
### MountPoint


|Name |Type |Example |Description |
|---|---|---|---|
|Ip |String |192.168. **.**  |Mount point address. |
|VpcId |String |vpc\-30uexwepls3cw7r2qr2h2\*\*\*\* |Private network ID. |
|Domain |String |apse1a03854ca4a\*\*\*\*.vpc\-22qcdcj9zcu0wds3n8bu\*\*\*\*.nas.ibytepluses.com |DNS address. |
|VpcName |String |NAStest |Private network name. |
|SubnetId |String |subnet\-3jhaxpk3qwrgg3pncme77\*\*\*\* |Subnet ID. |
|CreateTime |String |2023\-06\-13 T14:30:10 + 08:00 |Mount point creation time. |
|SubnetName |String |NAStest |Subnet name. |
|UpdateTime |String |2023\-06\-13 T14:30:10 + 08:00 |Mount point update time. |
|MountPointId |String |mount\-a6ee\*\*\*\* |Mount Point ID. |
|MountPointName |String |MountPoint |Mount point name. |
|PermissionGroup |Object of [BasicPermissionGroup](https://docs.byteplus.com/en/docs/91/24986#basicpermissiongroup) |{<br><br>"PermissionGroupId": "pgroup\-default",<br><br>"PermissionGroupName": "Default permission group"<br><br>} |The permission group information for the mount point binding. |


<span id="basicpermissiongroup"></span>
### BasicPermissionGroup


|Name |Type |Example |Description |
|---|---|---|---|
|PermissionGroupId |String |pgroup\-77afc370\*\*\*\* |Permission group ID. |
|PermissionGroupName |String |PGgroup |Permission group name. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeMountPoints&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemId": "enas-18bcb923****"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeMountPoints",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "TotalCount": 1,
        "MountPoints": [
            {
                "Ip": "192.168.**.**",
                "VpcId": "vpc-30uexwepls3cw7r2qr2h2****",
                "Domain": "apse1a03854ca4a****.vpc-22qcdcj9zcu0wds3n8bu****.nas.ibytepluses.com",
                "VpcName": "NAStest",
                "SubnetId": "subnet-3jhaxpk3qwrgg3pncme77****",
                "CreateTime": "2023-06-13T14:30:10+08:00",
                "SubnetName": "NAStest",
                "UpdateTime": "2023-06-13T14:30:10+08:00",
                "MountPointId": "mount-a6ee****",
                "MountPointName": "MountPoint",
                "PermissionGroup": {
                    "PermissionGroupId": "pgroup-77afc370****",
                    "PermissionGroupName": "PGgroup"
                }
            }
        ]
    }
}
```
