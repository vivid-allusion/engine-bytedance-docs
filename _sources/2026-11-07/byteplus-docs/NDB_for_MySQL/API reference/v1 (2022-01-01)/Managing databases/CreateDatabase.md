---
title: "CreateDatabase"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDatabase"
---

Call the CreateDatabase to create the database.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDatabase&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-r3xq0zdl\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|DBName |String |Yes |testdb1 |Database name. Naming rules:<br><br><br>* The database name is unique under the current instance.<br><br>* 2 to 64 characters in length. The name must start with a letter and ends with a letter or a digit.<br><br>* Consists of letters, digits, underscores (_) and hyphens (\-).<br><br>* Database names cannot use certain reserved words, see [List of forbidden keywords](https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_forbidden_keywords). |
|CharacterSetName |String |No |utf8mb4 |Database character set:<br><br><br>* `utf8mb4` (default)<br><br>* `utf8`<br><br>* `latin1`<br><br>* `ascii` |
|DBDesc |String |No |This is a database description. |Fill in the description information of the database, with a length of 0 to 256 characters. It can contain numbers, Chinese characters, English characters, underscores (_) and hyphens (\-). |
|DatabasesPrivileges |Array of [DatabasesPrivilegeObject](https://docs.byteplus.com/en/docs/265/57365#databasesprivilegeobject) |No |See the request example. |Database permission information. |


<span id="databasesprivilegeobject"></span>
### DatabasesPrivilegeObject


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AccountName |String |Yes |user1 |The name of the account to be authorized. |
|AccountPrivilege |String |Yes |ReadWrite |Authorized database permission type:<br><br><br>* `ReadWrite`: Read/Write privilege.<br><br>* `ReadOnly`: Read\-only privilege.<br><br>* `DDLOnly`: DDL only privilege.<br><br>* `DMLOnly`: DML only privilege.<br><br>* `Custom`: Custom privilege. |
|AccountPrivilegeDetail |String |No |INSERT,UPDATE,DELETE,CREATE |The specific SQL operation permissions included in the permission type, with multiple strings separated by a comma (,).<br><br><br>* When used as a request parameter in the [CreateDatabase](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDatabase) interface, this parameter is required when `AccountPrivilege` is set to `Custom`. Range of values ​​(multiple selections allowed): `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `CREATE`, `DROP`, `REFERENCES`, `INDEX`, `ALTER`, `CREATE TEMPORARY TABLES`, `LOCK TABLES`, `EXECUTE`, `CREATE VIEW`, `SHOW VIEW`, `CREATE ROUTINE`, `ALTER ROUTINE`, `EVENT`, `TRIGGER`.<br><br>* When this parameter is returned in the [DescribeDatabases](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDatabases) API, it shows the SQL operation permission details for the permission type, regardless of the `AccountPrivilege` value. For the specific SQL operation permissions included in each permission type, see the [Account permission list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Account_permission_description#.6LSm5Y-35p2D6ZmQ5YiX6KGo). |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=CreateDatabase&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "DBName": "testdb1",
    "InstanceId": "vedbm-omvt44tgm5u3",
    "CharacterSetName": "utf8mb4",
    "DBDesc": "这是一段数据库的描述信息",
    "DatabasesPrivileges": [
        {
            "AccountName": "test1",
            "AccountPrivilege": "Custom",
            "AccountPrivilegeDetail": "SELECT,UPDATE,INSERT"
        },
        {
            "AccountName": "test2",
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
        "RequestId": "202204102319080102121361532552D8E0",
        "Action": "CreateDatabase",
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
