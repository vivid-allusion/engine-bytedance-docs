---
title: "ModifyDBAccountPrivilege"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbaccountprivilege"
---

Call the ModifyDBAccountPrivilege API to modify the database account permissions.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-ca7b7019\*\*\*\* |Instance ID. |
|AccountName |String |Yes |testuser |Account name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">only supports modifying the privileges of normal account.</div><br> |
|AccountPrivileges |String |Yes |Inherit,Login,CreateRole,CreateDB |Account privileges information. Values:<br><br><br>* `Login`: login privileges.<br><br>* `Inherit`: inherit privileges.<br><br>* `CreateRole`: role creation privileges.<br><br>* `CreateDB`: create database privileges.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Modifying privileges for the super account is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Multiple privileges can be assigned in a single call.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyDBAccountPrivilege&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "AccountName": "test123",
    "AccountPrivileges": "Inherit,Login,CreateDB"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230802164826CE4FCB7FCAD8FBF66470",
        "Action": "ModifyDBAccountPrivilege",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
