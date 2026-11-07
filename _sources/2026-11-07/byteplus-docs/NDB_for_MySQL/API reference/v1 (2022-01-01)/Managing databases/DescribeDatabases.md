---
title: "DescribeDatabases"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDatabases"
---

Call the DescribeDatabases to query the database list.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDatabases&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-r3xq0zdl\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|PageNumber |Integer |No |1 |The page number, which must be greater than or equal to 1 and not exceed the maximum value of an Integer. The default is 1. |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1,000, with a default of 10. |
|DBName |String |No |testdb1 |Database name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you perform a fuzzy search, the underscore (_) is not used as a wildcard character. It matches the underscore (_) itself.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |2 |Total number of databases. |
|Databases |Array of [DatabaseObject](https://docs.byteplus.com/en/docs/265/57366#databaseobject) |Refer to the return example. |Database list information. |


<span id="databaseobject"></span>
### DatabaseObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DBName |String |testdb |Database name. |
|CharacterSetName |String |utf8 |Database character set:<br><br><br>* `utf8mb4`<br><br>* `utf8`<br><br>* `latin1`<br><br>* `ascii` |
|DBDesc |String |This is a database description. |The description of the database. |
|DatabasesPrivileges |Array of [DatabasesPrivilegeObject](https://docs.byteplus.com/en/docs/265/57366#databasesprivilegeobject) |Refer to the return example. |Database permission information. |


<span id="databasesprivilegeobject"></span>
### DatabasesPrivilegeObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AccountName |String |user1 |The name of the account to be authorized. |
|AccountPrivilege |String |ReadWrite |Authorized database permission type:<br><br><br>* `ReadWrite`: Read/Write privilege.<br><br>* `ReadOnly`: Read\-only privilege.<br><br>* `DDLOnly`: DDL only privilege.<br><br>* `DMLOnly`: DML only privilege.<br><br>* `Custom`: Custom privilege. |
|AccountPrivilegeDetail |String |INSERT,UPDATE,DELETE,CREATE |The specific SQL operation permissions included in the permission type, with multiple strings separated by a comma (,).<br><br><br>* When used as a request parameter in the [CreateDatabase](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDatabase) interface, this parameter is required when `AccountPrivilege` is set to `Custom`. Range of values ​​(multiple selections allowed): `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `CREATE`, `DROP`, `REFERENCES`, `INDEX`, `ALTER`, `CREATE TEMPORARY TABLES`, `LOCK TABLES`, `EXECUTE`, `CREATE VIEW`, `SHOW VIEW`, `CREATE ROUTINE`, `ALTER ROUTINE`, `EVENT`, `TRIGGER`.<br><br>* When this parameter is returned in the [DescribeDatabases](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDatabases) API, it shows the SQL operation permission details for the permission type, regardless of the `AccountPrivilege` value. For the specific SQL operation permissions included in each permission type, see the [Account permission list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Account_permission_description#.6LSm5Y-35p2D6ZmQ5YiX6KGo). |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeDatabases&Version=2022-01-01 HTTP/1.1
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
        "RequestId": "20240626181457AE8FEFE71A65F50CF16C-44a261",
        "Action": "DescribeDatabases",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "Databases": [
            {
                "CharacterSetName": "utf8mb4",
                "DBDesc": "这是一段数据库的描述信息",
                "DBName": "db1",
                "DatabasesPrivileges": [
                    {
                        "AccountName": "test1",
                        "AccountPrivilege": "DDLOnly",
                        "AccountPrivilegeDetail": "CREATE,DROP,INDEX,ALTER,CREATE TEMPORARY TABLES,LOCK TABLES,CREATE VIEW,SHOW VIEW,CREATE ROUTINE,ALTER ROUTINE"
                    },
                    {
                        "AccountName": "test2",
                        "AccountPrivilege": "Custom",
                        "AccountPrivilegeDetail": "INSERT,UPDATE,DELETE,CREATE"
                    },
                    {
                        "AccountName": "test3",
                        "AccountPrivilege": "ReadWrite",
                        "AccountPrivilegeDetail": "SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,REFERENCES,INDEX,ALTER,CREATE TEMPORARY TABLES,LOCK TABLES,CREATE VIEW,SHOW VIEW,CREATE ROUTINE,ALTER ROUTINE,EXECUTE,EVENT,TRIGGER"
                    }
                ]
            }
        ],
        "Total": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
