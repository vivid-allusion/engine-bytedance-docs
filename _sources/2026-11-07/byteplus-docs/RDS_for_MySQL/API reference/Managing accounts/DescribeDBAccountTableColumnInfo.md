---
title: "DescribeDBAccountTableColumnInfo"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbaccounttablecolumninfo"
---

Call the RevokeDBAccountPrivilege API to revoke permissions from a database account.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-d6ce108d\*\*\*\* |Instance ID. |
|DBName |String |Yes |db1 |Database name. |
|AccountName |String |No |user1 |Account name.<br><br>tip<br><br>When the account name is not specified, all permission information will return null. |
|Host |String |No |% |Specify the IP address from which the account accesses the database. The default value is %. |
|TableName |String |No |table1 |Search for table column permission settings in the database by table name. |
|ColumnName |String |No |column1 |Search for table column permission settings in the database by column name. |
|TableLimit |Integer |No |5 |Specify the number of table column permission entries to return. Results exceeding this limit will be truncated. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|TableInfos |Object[] |Please refer to the response example. |Table column permission information of the specified database in the instance. |
|AccountPrivileges |String[] |[ "SELECT",<br><br>"INSERT", "REFERENCES",<br><br>"CREATE VIEW", "TRIGGER"<br><br>] |The table\-level permission information the account has in this table. Valid values (multiple options allowed):<br><br><br>* `ALTER`<br><br>* `CREATE`<br><br>* `DELETE`<br><br>* `DROP`<br><br>* `INDEX`<br><br>* `INSERT`<br><br>* `SELECT`<br><br>* `SHOW VIEW`<br><br>* `TRIGGER`<br><br>* `UPDATE`<br><br>* `CREATE VIEW`<br><br>* `REFERENCES` |
|ColumnInfos |Object[] |Please refer to the response example. |The column\-level permission information the account has in this table. |
|AccountPrivileges |String[] |[<br><br>"INSERT",<br><br>"REFERENCES"<br><br>] |The permission information configured for the column. Valid values (multiple selections allowed):<br><br><br>* `INSERT`<br><br>* `REFERENCES`<br><br>* `SELECT`<br><br>* `UPDATE` |
|ColumnName |String |column1 |The name of the column for which column\-level permissions are configured. |
|TableName |String |table1 |The name of the table with column\-level permission settings. |

## Sample request

```json
POST /?Action=DescribeDBAccountTableColumnInfo&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-d6ce108d742e",
    "DBName": "db1",
    "AccountName": "user2",
    "ColumnName": "column1",
    "TableLimit": 5
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250413160415A912F3D18FFE92BF5C5F-38c330",
        "Action": "DescribeDBAccountTableColumnInfo",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "TableInfos": [
            {
                "AccountPrivileges": [
                    "SELECT",
                    "INSERT",
                    "REFERENCES",
                    "CREATE VIEW",
                    "TRIGGER"
                ],
                "ColumnInfos": [
                    {
                        "AccountPrivileges": null,
                        "ColumnName": "column2"
                    }
                ],
                "TableName": "table1"
            },
            {
                "AccountPrivileges": [
                    "SELECT",
                    "INSERT",
                    "UPDATE",
                    "DELETE",
                    "CREATE",
                    "DROP",
                    "REFERENCES",
                    "INDEX",
                    "ALTER",
                    "CREATE VIEW",
                    "SHOW VIEW",
                    "TRIGGER"
                ],
                "ColumnInfos": [
                    {
                        "AccountPrivileges": null,
                        "ColumnName": "column2"
                    }
                ],
                "TableName": "table10"
            },
            {
                "AccountPrivileges": null,
                "ColumnInfos": [
                    {
                        "AccountPrivileges": [
                            "SELECT",
                            "INSERT",
                            "UPDATE",
                            "REFERENCES"
                        ],
                        "ColumnName": "column2"
                    }
                ],
                "TableName": "table2"
            },
            {
                "AccountPrivileges": null,
                "ColumnInfos": [
                    {
                        "AccountPrivileges": null,
                        "ColumnName": "column2"
                    }
                ],
                "TableName": "table3"
            },
            {
                "AccountPrivileges": null,
                "ColumnInfos": [
                    {
                        "AccountPrivileges": null,
                        "ColumnName": "column2"
                    }
                ],
                "TableName": "table4"
            }
        ]
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
