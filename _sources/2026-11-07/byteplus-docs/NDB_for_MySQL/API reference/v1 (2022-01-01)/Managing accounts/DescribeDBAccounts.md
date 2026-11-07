---
title: "DescribeDBAccounts"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBAccounts"
---

Call the DescribeDBAccounts to query the account information of the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBAccounts&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-r3xq0zdl\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1,000, with a default of 10. |
|PageNumber |Integer |No |1 |Page number. The value is greater than or equal to 1, but does not exceed the maximum value of Integer. The default value is 1. |
|AccountName |String |No |testuser1 |Database account name. Fuzzy search is supported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Accounts created through SQL that do not comply with naming conventions can be modified and deleted via the API, but cannot be precisely queried by specifying this parameter.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of accounts. |
|Accounts |Array of [AccountObject](https://docs.byteplus.com/en/docs/265/57371#accountobject) |Refer to the return example. |Account list. |


<span id="accountobject"></span>
### AccountObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AccountName |String |testuser |Account name. |
|AccountType |String |Normal |Account type:<br><br><br>* `Super`: Super account.<br><br>* `Normal`: Normal account. |
|AccountDesc |String |This is a description of the account |Account description. |
|AccountPrivileges |Array of [AccountPrivilegeObject](https://docs.byteplus.com/en/docs/265/57371#accountprivilegeobject) |Refer to the return example. |The privilege information of the account. |


<span id="accountprivilegeobject"></span>
### AccountPrivilegeObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DBName |String |db1 |Name of the database to be authorized. |
|AccountPrivilege |String |ReadWrite |Authorized database permission type:<br><br><br>* `ReadWrite`: Read/Write privilege.<br><br>* `ReadOnly`: Read\-only privilege.<br><br>* `DDLOnly`: DDL only privilege.<br><br>* `DMLOnly`: DML only privilege.<br><br>* `Custom`: Custom privilege. |
|AccountPrivilegeDetail |String |INSERT,UPDATE,DELETE,CREATE |The specific SQL operation permissions included in the permission type, with multiple strings separated by a comma (,).<br><br><br>* When used as a request parameter in the [CreateDBAccount](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBAccount) and [GrantDBAccountPrivilege](https://docs.byteplus.com/en/docs/NDB_for_MySQL/GrantDBAccountPrivilege) interface, this parameter is required when `AccountPrivilege` is set to `Custom`. Range of values ​​(multiple selections allowed): `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `CREATE`, `DROP`, `REFERENCES`, `INDEX`, `ALTER`, `CREATE TEMPORARY TABLES`, `LOCK TABLES`, `EXECUTE`, `CREATE VIEW`, `SHOW VIEW`, `CREATE ROUTINE`, `ALTER ROUTINE`, `EVENT`, `TRIGGER`.<br><br>* When this parameter is returned in the [DescribeDBAccounts](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBAccounts) API, it shows the SQL operation permission details for the permission type, regardless of the `AccountPrivilege` value. For the specific SQL operation permissions included in each permission type, see the [Account permission list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Account_permission_description#.6LSm5Y-35p2D6ZmQ5YiX6KGo). |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeDBAccounts&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-ca12cbqv****",
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202406261717167860DC3556BF29132202-461255",
        "Action": "DescribeDBAccounts",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "Accounts": [
            {
                "AccountDesc": "这是一段账号的描述信息",
                "AccountName": "test_user",
                "AccountPrivileges": [],
                "AccountType": "Super"
            },
            {
                "AccountDesc": "这是一段账号的描述信息",
                "AccountName": "test3",
                "AccountPrivileges": [
                    {
                        "AccountPrivilege": "ReadWrite",
                        "AccountPrivilegeDetail": "SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,REFERENCES,INDEX,ALTER,CREATE TEMPORARY TABLES,LOCK TABLES,CREATE VIEW,SHOW VIEW,CREATE ROUTINE,ALTER ROUTINE,EXECUTE,EVENT,TRIGGER",
                        "DBName": "db1"
                    },
                    {
                        "AccountPrivilege": "ReadOnly",
                        "AccountPrivilegeDetail": "SELECT,LOCK TABLES,SHOW VIEW",
                        "DBName": "db2"
                    },
                    {
                        "AccountPrivilege": "Custom",
                        "AccountPrivilegeDetail": "SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,REFERENCES",
                        "DBName": "db3"
                    }
                ],
                "AccountType": "Normal"
            },
        ],
        "Total": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
