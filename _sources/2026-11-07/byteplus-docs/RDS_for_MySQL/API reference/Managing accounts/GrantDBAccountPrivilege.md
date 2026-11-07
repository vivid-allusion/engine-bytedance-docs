---
title: "GrantDBAccountPrivilege"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/grantdbaccountprivilege"
---

Call the GrantDBAccountPrivilege API to grant database privileges to a specified database account.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-62e07c2c\*\*\*\* |Instance ID. |
|AccountName |String |Yes |testuser |Account name. |
|Host |String |No |% |The IP address from which the account accesses the database. Default value: `%`. |
|AccountPrivileges |Object[] |Yes |[<br><br>{<br><br>"DBName":"db1",<br><br>"AccountPrivilege":"ReadWrite"<br><br>}<br><br>] |Reset account authorization information. |
|AccountPrivilege |String |Yes |ReadWrite |The type of database privilege. Valid values:<br><br><br>* `ReadWrite`: Read and write privileges.<br><br>* `ReadOnly`: Read\-only privileges.<br><br>* `DDLOnly`: DDL privileges only.<br><br>* `DMLOnly`: DML privileges only.<br><br>* `Custom`: Custom privileges.<br><br>* `Global`: Global privileges.<br><br>* `None`: Clear account privileges.<br><br><br>tip<br><br>When used as a request parameter, note the following:<br><br><br>* Only `Global` and `None` are allowed as values when used as a request parameter.<br><br>* The privilege type is single\-select; passing multiple values will result in an error.<br><br>* Only the GrantDBAccountPrivilege API supports setting AccountPrivilege to `None`. When AccountPrivilege is set to `None`:<br><br>   * If DBName is an empty string, all global privileges of the account are cleared.<br><br>   * If DBName is a specified database, all privileges of the account on that database are cleared. |
|AccountPrivilegeDetail |String |No |SELECT,INSERT,UPDATE |The privilege information of the account.<br><br><br>* When AccountPrivilege is set to `Custom`, the valid values for this field are:<br><br>   * `SELECT`<br><br>   * `INSERT`<br><br>   * `UPDATE`<br><br>   * `DELETE`<br><br>   * `CREATE`<br><br>   * `DROP`<br><br>   * `REFERENCES`<br><br>   * `INDEX`<br><br>   * `ALTER`<br><br>   * `CREATE TEMPORARY TABLES`<br><br>   * `LOCK TABLES`<br><br>   * `EXECUTE`<br><br>   * `CREATE VIEW`<br><br>   * `SHOW VIEW`<br><br>   * `EVENT`<br><br>   * `TRIGGER`<br><br>   * `CREATE ROUTINE`<br><br>   * `ALTER ROUTINE`<br><br>* When AccountPrivilege is set to `Global`, the valid values for this field are:<br><br>   * `PROCESS`<br><br>   * `REPLICATION SLAVE`<br><br>   * `REPLICATION CLIENT`<br><br>   * `SELECT`<br><br>   * `INSERT`<br><br>   * `UPDATE`<br><br>   * `DELETE`<br><br>   * `CREATE`<br><br>   * `DROP`<br><br>   * `RELOAD`<br><br>   * `REFERENCES`<br><br>   * `INDEX`<br><br>   * `ALTER`<br><br>   * `LOCK TABLES`<br><br>   * `EXECUTE`<br><br>   * `CREATE VIEW`<br><br>   * `SHOW VIEW`<br><br>   * `CREATE ROUTINE`<br><br>   * `ALTER ROUTINE`<br><br>   * `CREATE USER`<br><br>   * `EVENT`<br><br>   * `TRIGGER`<br><br>   * `SHOW DATABASES`<br><br>   * `CREATE TEMPORARY TABLES`<br><br><br>tip<br><br><br>* When used as a request parameter, this field is required if AccountPrivilege is set to `Custom`.<br><br>* In the CreateDBAccount API, the account is automatically granted the global privileges `REPLICATION SLAVE`, `PROCESS`, and `REPLICATION CLIENT`.<br><br>* Multiple values are allowed. Separate multiple privileges with commas (,).<br><br>* The write method is overwrite. |
|DBName |String |Yes |testdb1 |The name of the database for which the account authorization needs to be modified or for which the account already has permissions.<br><br>tip<br><br><br>* When used as a request parameter in the CreateDBAccount and GrantDBAccountPrivilege APIs, ensure that the database corresponding to DBName already exists.<br><br>* When modifying global authorization, pass an empty string for DBName. |
|DryRun |Boolean |No |true |Whether to retrieve the SQL statements for granting privileges to the account. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. Default value.<br><br><br>tip<br><br>When the value is `true`, the `GrantPrivilegeSQL` field will be returned (the account will not actually be granted privileges). When the value is `false` or not provided, it returns null. |
|TableColumnPrivileges |Object[] |No |Refer to the request example. |Column\-level privilege settings for the account. |
|DBName |String |Yes |TestDatabase |The name of the database to which the table for account permission settings belongs. |
|TablePrivileges |Object[] |No |Please refer to the request example. |The table permission information of the account. |
|TableName |String |Yes |TestTable |The name of the table for setting account permissions. |
|AccountPrivilegeDetail |String |No |"ALTER,CREATE" |Table permissions for the account. Valid values (multiple selections allowed):<br><br><br>* `ALTER`<br><br>* `CREATE`<br><br>* `DELETE`<br><br>* `DROP`<br><br>* `INDEX`<br><br>* `INSERT`<br><br>* `SELECT`<br><br>* `SHOW VIEW`<br><br>* `TRIGGER`<br><br>* `UPDATE`<br><br>* `CREATE VIEW`<br><br>* `REFERENCES`<br><br><br>tip<br><br>Separate multiple permissions with English commas (,). |
|ColumnPrivileges |Object[] |No |Please refer to the request example. |The column permission information of the account. |
|TableName |String |Yes |Table1 |The name of the database to which the table with column\-level permissions for the account belongs. |
|ColumnName |String |Yes |Column1 |The name of the column for which column\-level permissions are set for the account. |
|AccountPrivilegeDetail |String |No |"UPDATE,INSERT" |The permission information for column\-level permissions set for the account. Valid values (multiple selections allowed):<br><br><br>* `INSERT`<br><br>* `REFERENCES`<br><br>* `SELECT`<br><br>* `UPDATE`<br><br><br>tip<br><br>Separate multiple permissions with English commas (,). |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|GrantPrivilegeSQL |String[] |[<br><br>"REVOKE ALL PRIVILEGES ON `t1`.\* FROM TestAccount@'%';",<br><br>"GRANT SELECT,LOCK TABLES,SHOW VIEW ON `t1`.\* TO TestAccount@'%';"<br><br>] |The SQL statement used to grant privileges to the account based on the request parameters. Returned when `DryRun` is set to `true`. |

## Sample request

```json
POST /?Action=GrantDBAccountPrivilege&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-62e07c2c****",
    "AccountName": "test",
    "AccountPrivileges": [
        {
            "DBName": "testdb",
            "AccountPrivilege": "DDLOnly",
            "AccountPrivilegeDetail": ""
        },
        {
            "DBName": "testdb1",
            "AccountPrivilege": "ReadOnly",
            "AccountPrivilegeDetail": ""
        }
    ]
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230116115015A96C208EE46C00F7D56B",
        "Action": "GrantDBAccountPrivilege",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
