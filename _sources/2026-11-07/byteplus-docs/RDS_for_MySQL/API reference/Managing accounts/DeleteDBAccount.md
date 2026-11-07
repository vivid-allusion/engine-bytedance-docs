---
title: "DeleteDBAccount"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbaccount"
---

Call the DeleteDBAccount API to delete an account.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-r3xq0zdl\*\*\*\* |The instance ID. |
|AccountName |String |Yes |testuser |The name of the database account. |
|Host |String |No |% |The IP address used by the account to access the database. The default value is %. |

## Response parameters

null

## Sample request

```json
POST /?Action=DeleteDBAccount&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-4674157d****",
    "AccountName": "test",
    "Host": "%"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230110210058472469D3023864E46249",
        "Action": "DeleteAccount",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
