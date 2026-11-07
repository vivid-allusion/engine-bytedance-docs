---
title: "CreateDBAccount"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbaccount"
---

Call the CreateDBAccount API to create a database account.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDBAccount&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-r3xq0zdl\*\*\*\* |Instance ID. |
|AccountName |String |Yes |testuser1 |Database account name. Naming rules are as follows:<br><br><br>* The name's length is limited to 2~32 characters.<br><br>* The name must start with a letter and ends with a letter or a digit.<br><br>* The name consists of letters, digits, underscores (_), and hyphens (\-).<br><br>* The account name must be unique within the instance.<br><br>* The name can not contain certain reserved words and forbidden keywords. For all forbidden keywords, refer to [List of forbidden keywords](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_forbidden_keywords).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The keywords root and admin can be used in the Super account name.</div><br> |
|AccountDesc |String |No |Account description. |The description of the account, with a maximum length of 256 characters. |
|Host |String |No |% |Specifies the IP address where the account accesses the database. Default value is %.<br><br><br>* If the host is set to %, the account can access the database from any internet protocol address.<br><br>* You can use wildcards to specify the range of IP addresses that can access the database. For example, if the host is set to 192.10.10.%, the account can access the database from any IP address in the range of `192.10.10.0` to `192.10.10.255`.<br><br>* The specified host must be added to the allowlist associated with the instance. Otherwise, the instance cannot be accessed. You can call the [ModifyAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyallowlist1) API to add the host to the allowlist.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the account type created is a super account, the host IP can only be specified as <code>%</code>. That is, when AccountType is <code>Super</code>, Host can only be <code>%</code>.</div><br> |
|AccountPassword |String |Yes |Test@123456 |The password of the database account. The rules are as follows:<br><br><br>* The length is 8~32 characters.<br><br>* It contains at least three of the following: uppercase letters, lowercase letters, digits, and special characters.<br><br>* Special characters are `!#$%&()*+,-.=?@^_\|/`. |
|AccountType |String |Yes |Normal |Database account type, with the following values:<br><br><br>* `Super`: super account. Only one can be created for each instance.<br><br>* `Normal`: normal account. |
|AccountPrivileges |Array of [AccountPrivilegeObject](https://docs.byteplus.com/en/docs/40/15505#accountprivilegeobject) |No |[<br><br>{<br><br>"DBName":"testdb1",<br><br>"AccountPrivilege":"ReadWrite"<br><br>},<br><br>{<br><br>"DBName":"testdb2",<br><br>"AccountPrivilege":"ReadOnly"<br><br>}<br><br>] |Account database permission information.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When AccountType is <code>Super</code>, you do not need to pass a value for AccountPrivileges.</div><br> |
|DryRun |Boolean |No |true |Specifies whether to preview the SQL statement for creating the account. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the value is <code>true</code>, the CreateAccountSQL field is returned, but the account is not created. When the value is <code>false</code> or left empty, null is returned.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If an account is granted privileges on a database whose name contains an underscore (_), the underscore in the SQL statement returned in the CreateAccountSQL field is escaped as (\\_).</div><br> |
|TableColumnPrivileges |Array of [AccountTableColumnPrivilegeObject](https://docs.byteplus.com/en/docs/40/15505#accounttablecolumnprivilegeobject) |No |See the request example. |Table and column permission settings for the account. |
|AuthenticationType |String |No |IAM |The authentication type of the database account. Values:<br><br><br>* `MySQLNative`: MySQL native authentication.<br><br>* `IAM`: IAM authentication.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter, the default value is <code>MySQLNative</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The authentication type can only be specified when creating an account and cannot be modified afterward.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">It is recommended to select the IAM verification method only when the number of new IAM authenticated database connections created by the application per second is less than 200.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The total number of new IAM\-authenticated database connections created per second across all instances under the primary account must not exceed 20,000. Exceeding this limit will trigger traffic throttling and prevent new connections.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After you select the IAM verification method, the application uses a generated temporary token for verification when connecting to the database. Frequent creation of IAM\-authenticated database connections may exceed the connection limit. It is recommended to use a connection pool for centralized connection management. This allows applications to reuse existing connections and lowers the IAM authentication overhead from repeated connection creation.</div><br> |


<span id="accountprivilegeobject"></span>
### AccountPrivilegeObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|AccountPrivilege |String |Yes |ReadWrite |Database privilege type. Range:<br><br><br>* `ReadWrite`: read/write privilege.<br><br>* `ReadOnly`: read\-only privilege.<br><br>* `DDLOnly`: only DDL privilege.<br><br>* `DMLOnly`: only DML privilege.<br><br>* `Custom`: custom privilege.<br><br>* `Global`: global privilege.<br><br>* `None`: clear account privileges.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Note the following when this parameter is used as a request parameter:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter, the only allowed values are <code>Global</code> and <code>None</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The privilege type is single\-selection. An error is reported if multiple privileges are passed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only the GrantDBAccountPrivilege API supports setting AccountPrivilege to <code>None</code>. When AccountPrivilege is set to <code>None</code>,</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If DBName is an empty string, all global privileges of the account are cleared.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If DBName is a specified database, all privileges of the account on that database are cleared.</div><br> |
|AccountPrivilegeDetail |String |No |SELECT,INSERT,UPDATE |The permission information of the account.<br><br><br>* When AccountPrivilege is set to `Custom`, the value range is as follows:<br><br>   * `SELECT`<br><br>   * `INSERT`<br><br>   * `UPDATE`<br><br>   * `DELETE`<br><br>   * `CREATE`<br><br>   * `DROP`<br><br>   * `REFERENCES`<br><br>   * `INDEX`<br><br>   * `ALTER`<br><br>   * `CREATE TEMPORARY TABLES`<br><br>   * `LOCK TABLES`<br><br>   * `EXECUTE`<br><br>   * `CREATE VIEW`<br><br>   * `SHOW VIEW`<br><br>   * `EVENT`<br><br>   * `TRIGGER`<br><br>   * `CREATE ROUTINE`<br><br>   * `ALTER ROUTINE`<br><br>* When the AccountPrivilege Value is `Global`, the Value range for this field is as follows:<br><br>   * `PROCESS`<br><br>   * `REPLICATION SLAVE`<br><br>   * `REPLICATION CLIENT`<br><br>   * `SELECT`<br><br>   * `INSERT`<br><br>   * `UPDATE`<br><br>   * `DELETE`<br><br>   * `CREATE`<br><br>   * `DROP`<br><br>   * `RELOAD`<br><br>   * `REFERENCES`<br><br>   * `INDEX`<br><br>   * `ALTER`<br><br>   * `LOCK TABLES`<br><br>   * `EXECUTE`<br><br>   * `CREATE VIEW`<br><br>   * `SHOW VIEW`<br><br>   * `CREATE ROUTINE`<br><br>   * `ALTER ROUTINE`<br><br>   * `CREATE USER`<br><br>   * `EVENT`<br><br>   * `TRIGGER`<br><br>   * `SHOW DATABASES`<br><br>   * `CREATE TEMPORARY TABLES`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when AccountPrivilege is set to <code>Custom</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In the CreateDBAccount interface, the Account is automatically granted the <code>REPLICATION SLAVE</code>, <code>PROCESS</code>, and <code>REPLICATION CLIENT</code> global privileges.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Multiple values are allowed. Separate multiple privileges with commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The write method is overwrite.</div><br> |
|DBName |String |Yes |testdb1 |The name of the database for which account authorization needs to be modified, or for which the account already has privileges.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter in the CreateDBAccount and GrantDBAccountPrivilege APIs, confirm that the database corresponding to DBName exists.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When modifying global authorization, pass an empty string for DBName.</div><br> |


<span id="accounttablecolumnprivilegeobject"></span>
### AccountTableColumnPrivilegeObject


|Parameter |Type |Is it required? |Example |Description |
|---|---|---|---|---|
|DBName |String |Yes |TestDatabase |The name of the database that contains the table for account permission settings. |
|TablePrivileges |Array of [TablePrivilegeObject](https://docs.byteplus.com/en/docs/40/15505#tableprivilegeobject) |No |See the request example. |Table permission information for the account. |
|ColumnPrivileges |Array of [ColumnPrivilegeObject](https://docs.byteplus.com/en/docs/40/15505#columnprivilegeobject) |No |See the request example. |Column permission information for the account. |


<span id="tableprivilegeobject"></span>
### TablePrivilegeObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|TableName |String |Yes |TestTable |The name of the table for setting account privileges. |
|AccountPrivilegeDetail |String |No |"ALTER,CREATE" |Table privileges of the account. Value range (multiple selections allowed):<br><br><br>* `ALTER`<br><br>* `CREATE`<br><br>* `DELETE`<br><br>* `DROP`<br><br>* `INDEX`<br><br>* `INSERT`<br><br>* `SELECT`<br><br>* `SHOW VIEW`<br><br>* `TRIGGER`<br><br>* `UPDATE`<br><br>* `CREATE VIEW`<br><br>* `REFERENCES`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Separate multiple privileges with commas (,).</div><br> |


<span id="columnprivilegeobject"></span>
### ColumnPrivilegeObject


|Parameter |Type |Is it required? |Example |Description |
|---|---|---|---|---|
|TableName |String |Yes |Table1 |The name of the database that contains the table for which column permissions are set for the account. |
|ColumnName |String |Yes |Column1 |The name of the column for which column permissions are set for an account. |
|AccountPrivilegeDetail |String |No |"UPDATE,INSERT" |Permission information for setting column\-level permissions for an account. Values (select one or more):<br><br><br>* `INSERT`<br><br>* `REFERENCES`<br><br>* `SELECT`<br><br>* `UPDATE`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Separate multiple privileges with commas (,).</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|CreateAccountSQL |Array of String |[<br><br>"CREATE USER IF NOT EXISTS TestAccount@'%' IDENTIFIED WITH 'mysql_native_password' BY '\*\*\*\*\* *';",* <br><br> *"GRANT PROCESS,REPLICATION SLAVE,REPLICATION CLIENT ON . TO TestAccount@'%';",* <br><br> *"GRANT SELECT,SHOW VIEW ON * `*mysql*` *.*  TO TestAccount@'%';"<br><br>] |The SQL statement to create an account based on the request parameters. Returned when DryRun is set to `true`. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CreateDBAccount&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-4674157d****",
    "AccountName": "tester",
    "Host": "%",
    "AccountDesc": "这是一段账号 tester 的描述信息。",
    "AccountPassword": "Admin@1234",
    "AccountType": "Super"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230110175057044F3DC5036E863466E8",
        "Action": "CreateAccount",
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
