---
title: "UpdatePermissionRule"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/UpdatePermissionRule"
---

Call UpdatePermissionRule interface to update rule information for permission groups.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemType |String |Yes |Extreme |File system type. The value selection description is as follows:<br><br>`Extreme`: NAS Extreme Speed. |
|PermissionGroupId |String |Yes |pgroup\-33251455\*\*\*\* |Permission group ID. |
|PermissionRules |Array of [PermissionRule](https://docs.byteplus.com/en/docs/nas/UpdatePermissionRule?lang=en#permissionrule) |Yes |See the request example for details |Authority rule information. |


<span id="permissionrule"></span>
### PermissionRule


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|CidrIp |String |Yes |192.168.0.0 |The client side IP address that allows access. |
|RwMode |String |Yes |RW |Permission group read and write rules. The value selection description is as follows:<br><br><br>* `RW`: allows reading and writing.<br><br>* `RO`: read\-only mode. |
|UserMode |String |Yes |No_root_squash |Permission group user permissions. The value selection description is as follows:<br><br>All_squash: All visiting users are mapped to anonymous users or user groups.<br><br><br>* `No_all_squash`: The visiting user is first matched with the native user, and then mapped to an anonymous user or user group after the match fails.<br><br>* Root_squash: Maps Root users to anonymous users or user groups.<br><br>* `No_root_squash`: Root users maintain Root account permissions. |
|PermissionRuleId |String |Yes |prule\-059a3343\*\*\*\* |Permission rule ID, the console interface will not be displayed directly.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When referenced by the <a href="https://docs.byteplus.com/en/docs/nas/UpdatePermissionRule">UpdatePermissionRule</a> interface as a request parameter, this parameter does not need to be specified.</div><br> |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=UpdatePermissionRule&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemType": "Extreme",
    "PermissionGroupId": "pgroup-33251455****",
    "PermissionRules": [
        {
            "CidrIp": "192.168.0.0",
            "RwMode": "RW",
            "UserMode": "No_root_squash",
            "PermissionRuleId": "prule-059a3343****"
        }
    ]
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdatePermissionRule",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```
