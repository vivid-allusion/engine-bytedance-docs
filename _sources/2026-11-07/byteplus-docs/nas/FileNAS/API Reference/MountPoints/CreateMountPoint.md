---
title: "CreateMountPoint"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/CreateMountPoint"
---

Call CreateMountPoint to create a mount point.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemId |String |Yes |enas\-apse1a03854ca4a\*\*\*\* |File system ID. |
|VpcId |String |Yes |vpc\-30uexwepls3cw7r2qr2h2\*\*\*\* |Private network ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeVpcs">DescribeVpcs</a> interface to query the private network ID.</div><br> |
|SubnetId |String |Yes |subnet\-3jhaxpk3qwrgg3pncme77\*\*\*\* |Subnet ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeSubnets">DescribeSubnets</a> interface to query all subnet IDs in the specified Availability Zone.</div><br> |
|PermissionGroupId |String |Yes |pgroup\-77afc370\*\*\*\* |Permission group ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/nas/DescribePermissionGroup">DescribePermissionGroups</a> interface to query all available permission group IDs.</div><br> |
|MountPointName |String |Yes |MountPoint2 |Mount point name. The naming convention is as follows:<br><br><br>* Cannot start with a number or a dash (\-).<br><br>* Can only contain Chinese, letters, numbers, underscores (_) and underscores (\-).<br><br>   The length should be between 1 and 128 characters. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|MountPointId |String |mount\-n7db\*\*\*\* |Mount Point ID. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=CreateMountPoint&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemId": "enas-apse1a03854ca4a****",
    "VpcId": "vpc-30uexwepls3cw7r2qr2h2****",
    "SubnetId": "subnet-3jhaxpk3qwrgg3pncme77****",
    "PermissionGroupId": "pgroup-77afc370****",
    "MountPointName": "MountPoint2"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateMountPoint",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "MountPointId": "mount-n7db****"
    }
}
```
