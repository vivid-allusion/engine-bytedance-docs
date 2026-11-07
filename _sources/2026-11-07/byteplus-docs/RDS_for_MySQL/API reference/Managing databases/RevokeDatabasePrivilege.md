---
title: "RevokeDatabasePrivilege"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/revokedatabaseprivilege"
---

Call the RevokeDatabasePrivilege API to revoke authorization from a database account.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-r3xq0zdl\*\*\*\* |Instance ID. |
|DBName |String |Yes |testdb |Database name. |
|AccountNames |String |Yes |testuser1,testuser2 |Database account name. Multiple accounts should be separated by English commas (,).<br><br>tip<br><br><br>* Revoke all permissions of the account in this database.<br><br>* If the account was created with a specified access IP address for the database, the full account name must be provided here, e.g., `user1@192.168.1.1`. |

## Response parameters

null

## Sample request

```json
POST /?Action=RevokeDatabasePrivilege&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-7582b02b****",
    "DBName": "testdb1",
    "AccountNames": "testuser1@192.***.***.2,testuser2"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230116153522F8E4647F54A7BB12694A",
        "Action": "RevokeDatabasePrivilege",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
