---
title: "GrantDatabasePrivilege"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/grantdatabaseprivilege"
---

Call the GrantDatabasePrivilege API to add authorized database accounts for the specified database.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-r3xq0zdl\*\*\*\* |Instance ID. |
|DBName |String |Yes |testuser1 |Database name. |
|DatabasePrivileges |Object[] |Yes |[<br><br>{<br><br>"AccountName":"testuser",<br><br>"Host": "192. ** *.* ** .2",<br><br>"AccountPrivilege":"ReadWrite"<br><br>}<br><br>] |List of database account permissions. |
|AccountName |String |Yes |testdb1 |The name of the account that requires authorization. |
|Host |String |No |% |The specified database account can access the IP address of the database. The default value is %.<br><br><br>* If the Host is specified as `%`, the account is allowed to access the database from any IP address.<br><br>* If the Host is specified as `192.10.10.%`, it means that the account can access the database from IP addresses between `192.10.10.0` and `192.10.10.255`.<br><br>* The specified Host needs to be added to the whitelist bound to the instance. |
|AccountPrivilege |String |Yes |ReadWrite |The type of account permission granted, with the following values:<br><br><br>* `ReadWrite`: Read and write permission.<br><br>* `ReadOnly`: Read\-only permission.<br><br>* `DDLOnly`: DDL\-only permission.<br><br>* `DMLOnly`: DML\-only permission.<br><br>* `Custom`: Custom permission.<br><br><br>tip<br><br>The permission type is single\-choice. An error will be reported if multiple permissions are passed. |
|AccountPrivilegeDetail |String |No |SELECT,INSERT,UPDATE |Database privilege string.<br><br>When used as a request parameter, it is required when the value of AccountPrivilege is `Custom`. The possible values are:<br><br><br>* `SELECT`<br><br>* `INSERT`<br><br>* `UPDATE`<br><br>* `DELETE`<br><br>* `CREATE`<br><br>* `DROP`<br><br>* `REFERENCES`<br><br>* `INDEX`<br><br>* `ALTER`<br><br>* `CREATE TEMPORARY TABLES`<br><br>* `LOCK TABLES`<br><br>* `EXECUTE`<br><br>* `CREATE VIEW`<br><br>* `SHOW VIEW`<br><br>* `CREATE ROUTINE`<br><br>* `ALTER ROUTINE`<br><br>* `EVENT`<br><br>* `TRIGGER`<br><br><br>When used as a return result, regardless of whether the value of AccountPrivilege is `Custom`, the detailed privileges of AccountPrivilege will be shown.<br><br>tip<br><br>Multiple strings are separated by English commas (,). |

## Response parameters

null

## Sample request

```json
POST /?Action=GrantDatabasePrivilege&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-7582b02b****",
    "DBName": "testdb1",
    "DatabasePrivileges": [
        {
            "AccountName": "testuser1",
            "Host": "192.***.***.2",
            "AccountPrivilege": "ReadWrite"
        }
    ]
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202301161533354BFF2A1927E50A101666",
        "Action": "GrantDatabasePrivilege",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
