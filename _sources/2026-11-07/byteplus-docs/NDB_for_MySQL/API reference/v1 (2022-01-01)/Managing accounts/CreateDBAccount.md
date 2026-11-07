---
title: "CreateDBAccount"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBAccount"
---

Call the CreateDBAccount to create a database account.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDBAccount&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-r3xq0zdl\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|AccountName |String |Yes |testuser1 |Database account name. The account name must meet the following requirements:<br><br><br>* The name must be unique and 2 to 32 characters in length.<br><br>* It must consist of letters, numbers, underscores (_) and hyphens (\-).<br><br>* The name must start with a letter and ends with a letter or a digit.<br><br>* The name cannot contain any forbidden keywords. For more details, refer to [List of forbidden keywords](https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_forbidden_keywords). Can not use some reserved words, including root and admin. |
|AccountPassword |String |Yes |Test@123 |The password of the database account. The account password must meet the following requirements:<br><br><br>* Can only contain uppercase and lowercase letters, digits and the following special characters `~!@#$%^&*_-+=`\|\(){}[]:;'<>,.?/`.<br><br>* The length must be between 8 and 32 characters.<br><br>* Must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and specific special characters. |
|AccountType |String |Yes |Normal |The database account type. Valid values:<br><br><br>* `Super`: Super account. An instance can only create one super account, and has all the permissions of all databases under the instance, and can manage all normal accounts and databases.<br><br>* `Normal`: Normal account. An instance can create multiple normal accounts, and it is necessary to manually grant the permissions of a specific database to the normal account. |
|AccountDesc |String |No |This is a description of the account |The description information of the account, with a length of 0 to 256 characters. It can contain numbers, Chinese characters, English characters, underscores (_) and hyphens (\-). |
|AccountPrivileges |Array of [AccountPrivilegeObject](https://docs.byteplus.com/en/docs/265/57369#accountprivilegeobject) |No |See the request example. |Database permission information.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is not required when <code>AccountType</code> is set to <code>Super</code>. The super account has all permissions for all databases in the instance by default.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>AccountType</code> is set to <code>Normal</code>, it is recommended to specify this parameter to grant the normal account permissions on specific databases. If this is not set, the account has no permissions for any database.</div><br> |


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
POST /?Action=CreateDBAccount&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-r3xq0zdl****",
    "AccountName": "test3",
    "AccountPassword": "Root****",
    "AccountType": "Normal",
    "AccountDesc": "这是一段账号的描述信息",
    "AccountPrivileges": [
        {
            "DBName": "db3",
            "AccountPrivilege": "Custom",
            "AccountPrivilegeDetail": "SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,REFERENCES"
        },
        {
            "DBName": "db2",
            "AccountPrivilege": "ReadOnly"
        },
        {
            "DBName": "db1",
            "AccountPrivilege": "ReadWrite"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "d78bbf4e-63a5-4937-ac3c-3767e7eddfbe",
        "Action": "CreateDBAccount",
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
