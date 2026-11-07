---
title: "RevokeDBAccountPrivilege"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/revokedbaccountprivilege"
---

Call the RevokeDBAccountPrivilege API to revoke permissions from a database account.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-r3xq0zdl\*\*\*\* |Instance ID. |
|AccountName |String |Yes |testuser1 |Database account name. |
|Host |String |No |% |The IP address from which the account accesses the database. The default value is `%`. |
|DBNames |String |Yes |testdb1,testdb2 |Database name. Multiple database names should be separated by commas (,).<br><br>tip<br><br>Revokes all permissions of the account for the specified database. |

## Response parameters

null

## Sample request

```json
POST /?Action=RevokeDBAccountPrivilege&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-62e07c2c****",
    "AccountName": "test",
    "DBNames": "testdb1,testdb2"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230116115904B5947AA89ED2C9040D17",
        "Action": "RevokeDBAccountPrivilege",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
