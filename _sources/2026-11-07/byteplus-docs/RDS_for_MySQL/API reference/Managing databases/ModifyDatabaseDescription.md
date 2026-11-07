---
title: "ModifyDatabaseDescription"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydatabasedescription1"
---

Call the ModifyDatabaseDescription API to modify the description of a database.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-r3xq0zdl\*\*\*\* |Instance ID. |
|DBName |String |Yes |db1 |Database name. |
|DBDesc |String |No |This is a new database description. |The description of the database, with a maximum length of 256 characters. This field is optional. If the field is not set, or if it is set but an empty string (length 0) is passed, the original remarks will be cleared. |

## Response parameters

null

## Sample request

```json
POST /?Action=ModifyDatabaseDescription&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-603e30e6****",
    "DBName": "testdb1",
    "DBDesc": "这是一段数据库 testdb1 新的描述。"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230506162526C6E0CB21D56530F9CBC6",
        "Action": "ModifyDatabaseDescription",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
