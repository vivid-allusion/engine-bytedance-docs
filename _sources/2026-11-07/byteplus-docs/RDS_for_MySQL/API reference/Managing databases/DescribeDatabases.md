---
title: "DescribeDatabases"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedatabases"
---

Call the DescribeDatabases API to view the database list.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-r3xq0zdl\*\*\*\* |Instance ID. |
|DBName |String |No |testdb1 |Database name. |
|PageNumber |Integer |No |1 |Current page number. The minimum value is 1. Default value is 1. |
|PageSize |Integer |No |10 |Number of records per page. The minimum value is 1, and the maximum value cannot exceed 1000. Default value is 10. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |1 |Total number of databases. |
|Databases |Object[] |[<br><br>{<br><br>"CharacterSetName": "utf8",<br><br>"DBDesc": "This is a description of the database testdb1.",<br><br>"DBName": "testdb1",<br><br>"DBPartition": 0,<br><br>"DBStatus": "Available",<br><br>"DatabasePrivileges": null,<br><br>"DatabasePrivilegesInfo": null<br><br>}<br><br>] |Database list. |
|DBName |String |db1 |Database name. |
|CharacterSetName |String |utf8mb4 |Database character set. |
|DBDesc |String |这是一段数据库的描述信息。 |The description information of the database. If the database has no description information, this field is empty. |
|DBStatus |String |Available |Database status. The possible values are:<br><br><br>* `Unavailable`: Unavailable.<br><br>* `Available`: Available. |
|DatabasePrivileges |Object[] |[<br><br>{<br><br>"AccountName": "user1",<br><br>"AccountPrivilege":"ReadWrite"<br><br>}<br><br>] |Database account permission list. |
|AccountName |String |testdb1 |The name of the account that requires authorization. |
|Host |String |% |The specified database account can access the IP address of the database. The default value is %.<br><br><br>* If the Host is specified as `%`, the account is allowed to access the database from any IP address.<br><br>* If the Host is specified as `192.10.10.%`, it means that the account can access the database from IP addresses between `192.10.10.0` and `192.10.10.255`.<br><br>* The specified Host needs to be added to the whitelist bound to the instance. |
|AccountPrivilege |String |ReadWrite |The type of account permission granted, with the following values:<br><br><br>* `ReadWrite`: Read and write permission.<br><br>* `ReadOnly`: Read\-only permission.<br><br>* `DDLOnly`: DDL\-only permission.<br><br>* `DMLOnly`: DML\-only permission.<br><br>* `Custom`: Custom permission.<br><br><br>tip<br><br>The permission type is single\-choice. An error will be reported if multiple permissions are passed. |
|AccountPrivilegeDetail |String |SELECT,INSERT,UPDATE |Database privilege string.<br><br>When used as a request parameter, it is required when the value of AccountPrivilege is `Custom`. The possible values are:<br><br><br>* `SELECT`<br><br>* `INSERT`<br><br>* `UPDATE`<br><br>* `DELETE`<br><br>* `CREATE`<br><br>* `DROP`<br><br>* `REFERENCES`<br><br>* `INDEX`<br><br>* `ALTER`<br><br>* `CREATE TEMPORARY TABLES`<br><br>* `LOCK TABLES`<br><br>* `EXECUTE`<br><br>* `CREATE VIEW`<br><br>* `SHOW VIEW`<br><br>* `CREATE ROUTINE`<br><br>* `ALTER ROUTINE`<br><br>* `EVENT`<br><br>* `TRIGGER`<br><br><br>When used as a return result, regardless of whether the value of AccountPrivilege is `Custom`, the detailed privileges of AccountPrivilege will be shown.<br><br>tip<br><br>Multiple strings are separated by English commas (,). |

## Sample request

```json
POST /?Action=DescribeDatabases&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-4674157d****",
    "PageSize": 10,
    "PageNumber": 1
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023011116092131FBB0733F03E98C9690",
        "Action": "DescribeDatabases",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Databases": [
            {
                "CharacterSetName": "utf8",
                "DBDesc": "这是一段数据库 testdb1 的描述。",
                "DBName": "testdb1",
                "DBPartition": 0,
                "DBStatus": "Available",
                "DatabasePrivileges": [
                    {
                        "AccountName": "TestAccount1",
                        "AccountPrivilege": "ReadOnly",
                        "AccountPrivilegeDetail": "LOCK TABLES,SELECT,SHOW VIEW",
                        "Host": "192.***.***.2"
                    },
                    {
                        "AccountName": "TestAccount2",
                        "AccountPrivilege": "ReadWrite",
                        "AccountPrivilegeDetail": "ALTER,ALTER ROUTINE,CREATE,CREATE ROUTINE,CREATE TMP TABLE,CREATE VIEW,DELETE,DROP,EVENT,EXECUTE,INDEX,INSERT,LOCK TABLES,REFERENCES,SELECT,SHOW VIEW,TRIGGER,UPDATE",
                        "Host": "%"
                    }
                ]
            },
            {
                "CharacterSetName": "utf8",
                "DBDesc": "这是一段数据库 testdb2 的描述信息。",
                "DBName": "testdb2",
                "DBPartition": 0,
                "DBStatus": "Available",
                "DatabasePrivileges": [
                    {
                        "AccountName": "TestAccount2",
                        "AccountPrivilege": "ReadOnly",
                        "AccountPrivilegeDetail": "LOCK TABLES,SELECT,SHOW VIEW",
                        "Host": "%"
                    }
                ]
            }
        ],
        "Total": 2
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
