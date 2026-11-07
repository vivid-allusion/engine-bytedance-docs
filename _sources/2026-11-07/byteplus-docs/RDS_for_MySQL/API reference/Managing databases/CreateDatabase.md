---
title: "CreateDatabase"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdatabase1"
---

Call the CreateDatabase API to create a database.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDatabase&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-r3xq0zdl\*\*\*\* |Instance ID. |
|DBName |String |Yes |testdb1 |Database name. Naming rules are as follows:<br><br><br>* The name must be unique.<br><br>* 2 to 64 characters in length.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of letters, digits, underscores (_), or hyphens (\-).<br><br>* It cannot contain certain reserved words, including root and admin. Refer to the [List of forbidden keywords](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_forbidden_keywords) for forbidden reserved words. |
|CharacterSetName |String |No |utf8 |Database character set. Supported character sets include: utf8, utf8mb4 (default), latin1, and ascii. |
|DatabasePrivileges |Array of [DatabasePrivilegeObject](https://docs.byteplus.com/en/docs/40/15466#databaseprivilegeobject) |No |[<br><br>{<br><br>"AccountName": "user1",<br><br>"Host":"%",<br><br>"AccountPrivilege":"ReadWrite"<br><br>}<br><br>] |Database authorization information. |
|DBDesc |String |No |This is a database description. |The description of the database cannot exceed 256 characters. This field is optional. If this field is not set, or if the description length is 0, the description is empty. |


<span id="databaseprivilegeobject"></span>
### DatabasePrivilegeObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|AccountName |String |Yes |testdb1 |The name of the account to be authorized first. |
|Host |String |No |% |The Internet protocol address from which the specified database account can access the database. The default value is %.<br><br><br>* If the host is specified as `%`, allow the account to access the database from any IP address.<br><br>* If the host is set to `192.10.10.%`, the account can access the database from any IP address in the range of `192.10.10.0` to `192.10.10.255`.<br><br>* The specified host needs to be added to the allowlist associated with the instance. |
|AccountPrivilege |String |Yes |ReadWrite |Type of privilege granted to the account. Valid values:<br><br><br>* `ReadWrite`: Read/Write privilege.<br><br>* `ReadOnly`: read\-only privilege.<br><br>* `DDLOnly`: only DDL privilege.<br><br>* `DMLOnly`: only DML privilege.<br><br>* `Custom`: custom privilege.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Select only one privilege type. An error occurs if multiple privileges are passed.</div><br> |
|AccountPrivilegeDetail |String |No |SELECT,INSERT,UPDATE |Database privilege string.<br><br>This parameter is required when AccountPrivilege is `Custom`. Valid values:<br><br><br>* `SELECT`<br><br>* `INSERT`<br><br>* `UPDATE`<br><br>* `DELETE`<br><br>* `CREATE`<br><br>* `DROP`<br><br>* `REFERENCES`<br><br>* `INDEX`<br><br>* `ALTER`<br><br>* `CREATE TEMPORARY TABLES`<br><br>* `LOCK TABLES`<br><br>* `EXECUTE`<br><br>* `CREATE VIEW`<br><br>* `SHOW VIEW`<br><br>* `CREATE ROUTINE`<br><br>* `ALTER ROUTINE`<br><br>* `EVENT`<br><br>* `TRIGGER`<br><br>   When returned as a result, the detailed privileges for AccountPrivilege are displayed regardless of whether its value is `Custom`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Multiple strings are separated by a comma (,).</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CreateDatabase&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-4674157d****",
    "DBName": "test",
    "DBDesc": "这是一段数据库 testdb 的描述信息。"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202301102106150EF6F410713D7FE58AAE",
        "Action": "CreateDatabase",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
