---
title: "DescribeDBAccounts"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbaccounts"
---

Call the DescribeDBAccounts API to view the account list.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-r3xq0zdl\*\*\*\* |Instance ID. |
|AccountName |String |No |testuser1 |Database account name. It supports fuzzy queries. |
|PageNumber |Integer |No |1 |Current page number. The minimum value is 1. Default value: 1. |
|PageSize |Integer |No |10 |Number of records per page. The minimum value is 1, and the maximum value cannot exceed 1,000. The default value is 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Accounts |Array of [AccountObject](https://docs.byteplus.com/en/docs/40/15503#accountobject) |Refer to the Sample response. |Account list. |
|Total |Integer |1 |Total number of accounts. |


<span id="accountobject"></span>
### AccountObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AccountDesc |String |This is a description of the account. |Account description.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not returned if the account has no description.</div><br> |
|AccountName |String |test1 |Account name. |
|AccountPrivileges |Array of [AccountPrivilegeObject](https://docs.byteplus.com/en/docs/40/15503#accountprivilegeobject) |null |Account permission information on the specified database.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the account does not have privileges for the specified database, the value returned for this field is<code>null</code>。</div><br> |
|AccountPrivilegesSQL |Array of String |[<br><br>"GRANT PROCESS, REPLICATION SLAVE, REPLICATION CLIENT ON  *.*  TO 'TestAccount'@'%'",<br><br>"GRANT SELECT, SHOW VIEW ON `mysql`.\* TO 'TestAccount'@'%'"<br><br>] |The SQL statement corresponding to the current privilege settings for the account. |
|AccountStatus |String |Available |Account state. The values are:<br><br><br>* `Not available`: not available.<br><br>* `Available`: available. |
|AccountType |String |Normal |Account type, value range:<br><br><br>* `Super`: super account.<br><br>* `Normal`: normal account. |
|AuthenticationType |String |IAM |The authentication type of the database account. Values:<br><br><br>* `MySQLNative`: MySQL native authentication.<br><br>* `IAM`: IAM authentication.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter, the default value is <code>MySQLNative</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The authentication type can only be specified when creating an account and cannot be modified afterward.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Specifying the authentication type for a database account is a feature that requires allowlisting. To apply for this feature, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000178">submit a ticket</a>.</div><br> |
|GlobalAccountPrivileges |Array of String |[<br><br>"PROCESS",<br><br>"REPLICATION SLAVE",<br><br>"REPLICATION CLIENT"<br><br>] |Global privilege of the account. The value range for this field is as follows (multiple selections allowed):<br><br>\- `PROCESS`<br><br>\- `REPLICATION SLAVE`<br><br>\- `REPLICATION CLIENT`<br><br>\- `SELECT`<br><br>\- `INSERT`<br><br>\- `UPDATE`<br><br>\- `DELETE`<br><br>\- `CREATE`<br><br>\- `DROP`<br><br>\- `RELOAD`<br><br>\- `REFERENCES`<br><br>\- `INDEX`<br><br>\- `ALTER`<br><br>\- `LOCK TABLES`<br><br>\- `EXECUTE`<br><br>\- `CREATE VIEW`<br><br>\- `SHOW VIEW`<br><br>\- `CREATE ROUTINE`<br><br>\- `ALTER ROUTINE`<br><br>\- `CREATE USER`<br><br>\- `EVENT`<br><br>\- `TRIGGER`<br><br>\- `SHOW DATABASES`<br><br>\- `CREATE TEMPORARY TABLES` |
|HasTableColumnPrivilegeDBNames |Array of String |["db1","db2"] |The database to which the account's table and column privileges belong.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is not returned if the account has no table or column privileges.</div><br> |
|Host |String |% |The Internet protocol address from which the specified database account can access the database. |


<span id="accountprivilegeobject"></span>
### AccountPrivilegeObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AccountPrivilege |String |ReadWrite |Database privilege type. Range:<br><br><br>* `ReadWrite`: read/write privilege.<br><br>* `ReadOnly`: read\-only privilege.<br><br>* `DDLOnly`: only DDL privilege.<br><br>* `DMLOnly`: only DML privilege.<br><br>* `Custom`: custom privilege.<br><br>* `Global`: global privilege.<br><br>* `None`: clear account privileges.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Note the following when this parameter is used as a request parameter:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter, the only allowed values are <code>Global</code> and <code>None</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The privilege type is single\-selection. An error is reported if multiple privileges are passed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only the GrantDBAccountPrivilege API supports setting AccountPrivilege to <code>None</code>. When AccountPrivilege is set to <code>None</code>,</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If DBName is an empty string, all global privileges of the account are cleared.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If DBName is a specified database, all privileges of the account on that database are cleared.</div><br> |
|AccountPrivilegeDetail |String |SELECT,INSERT,UPDATE |The permission information of the account. Values are as follows:<br><br>\- `SELECT`<br><br>\- `INSERT`<br><br>\- `UPDATE`<br><br>\- `DELETE`<br><br>\- `CREATE`<br><br>\- `DROP`<br><br>\- `REFERENCES`<br><br>\- `INDEX`<br><br>\- `ALTER`<br><br>\- `CREATE TEMPORARY TABLES`<br><br>\- `LOCK TABLES`<br><br>\- `EXECUTE`<br><br>\- `CREATE VIEW`<br><br>\- `SHOW VIEW`<br><br>\- `EVENT`<br><br>\- `TRIGGER`<br><br>\- `CREATE ROUTINE`<br><br>\- `ALTER ROUTINE`<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when AccountPrivilege is set to <code>Custom</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In the CreateDBAccount interface, the Account is automatically granted the <code>REPLICATION SLAVE</code>, <code>PROCESS</code>, and <code>REPLICATION CLIENT</code> global privileges.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Multiple values are allowed. Separate multiple privileges with commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The write method is overwrite.</div><br> |
|DBName |String |testdb1 |The name of the database for which account authorization needs to be modified, or for which the account already has privileges.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter in the CreateDBAccount and GrantDBAccountPrivilege APIs, confirm that the database corresponding to DBName exists.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When modifying global authorization, pass an empty string for DBName.</div><br> |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDBAccounts&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-4674157d****",
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023011020222366CD533BB55250E27C28",
        "Action": "DescribeDBAccounts",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Accounts": [
            {
                "AccountName": "test-IAM",
                "AccountPrivileges": null,
                "AccountPrivilegesInfo": null,
                "AccountPrivilegesSQL": [
                    "GRANT PROCESS, REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'test-IAM'@'%'",
                    "GRANT SELECT, SHOW VIEW ON `mysql`.* TO 'test-IAM'@'%'"
                ],
                "AccountStatus": "Available",
                "AccountType": "Normal",
                "AuthenticationType": "IAM",
                "GlobalAccountPrivileges": [
                    "PROCESS",
                    "REPLICATION SLAVE",
                    "REPLICATION CLIENT"
                ],
                "Host": "%"
            }
        ],
        "Total": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
