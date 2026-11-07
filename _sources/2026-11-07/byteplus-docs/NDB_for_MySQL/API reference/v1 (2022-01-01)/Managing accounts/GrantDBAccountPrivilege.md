---
title: "GrantDBAccountPrivilege"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/GrantDBAccountPrivilege"
---

Calling the GrantDBAccountPrivilege gives the account permissions on the specified database.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* This API only supports granting permissions to normal database accounts. **Super accounts** have permissions on all databases, so it is unnecessary to grant them permissions.

* The instance account type is **Normal account**. This means that when you call the [DescribeDBAccounts](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBAccounts) API to view the instance account information, `AccountType` is `Normal`.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=GrantDBAccountPrivilege&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-r3xq0zdl\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|AccountName |String |Yes |testuser |Name of the normal database account. |
|AccountPrivileges |Array of [AccountPrivilegeObject](https://docs.byteplus.com/en/docs/265/57374#accountprivilegeobject) |Yes |See the request example. |Reset account authorization information. |


<span id="accountprivilegeobject"></span>
### AccountPrivilegeObject


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|DBName |String |Yes |db1 |Name of the database to be authorized. |
|AccountPrivilege |String |Yes |ReadWrite |Authorized database permission type:<br><br><br>* `ReadWrite`: Read/Write privilege.<br><br>* `ReadOnly`: Read\-only privilege.<br><br>* `DDLOnly`: DDL only privilege.<br><br>* `DMLOnly`: DML only privilege.<br><br>* `Custom`: Custom privilege. |
|AccountPrivilegeDetail |String |No |INSERT,UPDATE,DELETE,CREATE |The specific SQL operation permissions included in the permission type, with multiple strings separated by a comma (,).<br><br><br>* When used as a request parameter in the [CreateDBAccount](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBAccount) and [GrantDBAccountPrivilege](https://docs.byteplus.com/en/docs/NDB_for_MySQL/GrantDBAccountPrivilege) interface, this parameter is required when `AccountPrivilege` is set to `Custom`. Range of values ​​(multiple selections allowed): `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `CREATE`, `DROP`, `REFERENCES`, `INDEX`, `ALTER`, `CREATE TEMPORARY TABLES`, `LOCK TABLES`, `EXECUTE`, `CREATE VIEW`, `SHOW VIEW`, `CREATE ROUTINE`, `ALTER ROUTINE`, `EVENT`, `TRIGGER`.<br><br>* When this parameter is returned in the [DescribeDBAccounts](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBAccounts) API, it shows the SQL operation permission details for the permission type, regardless of the `AccountPrivilege` value. For the specific SQL operation permissions included in each permission type, see the [Account permission list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Account_permission_description#.6LSm5Y-35p2D6ZmQ5YiX6KGo). |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=GrantDBAccountPrivilege&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-r3xq0zdl****",
    "AccountName": "test1",
    "AccountPrivileges": [
        {
            "DBName": "db1",
            "AccountPrivilege": "DDLOnly"
        },
        {
            "DBName": "db2",
            "AccountPrivilege": "DDLOnly"
        },
        {
            "DBName": "db3",
            "AccountPrivilege": "Custom",
            "AccountPrivilegeDetail": "TRIGGER,EVENT,ALTER ROUTINE,CREATE ROUTINE"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202204102315470102120720961D4F4997",
        "Action": "ResetDBAccount",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
