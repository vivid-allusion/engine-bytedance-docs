---
title: "ModifyDBProxyConfig"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxyconfig"
---

Call the ModifyDBProxyConfig API to modify the connection pool mode of a specified MySQL instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-46609cf2\*\*\*\* |Instance ID. |
|ConnectionPoolType |String |No |Transaction |The type of connection pool. Supported values are as follows.<br><br><br>* `Direct`: Direct connection mode.<br><br>* `Transaction`: Transaction\-level connection pool (default). |

## Response parameters

null

## Sample request

```json
POST /?Action=ModifyDBProxyConfig&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-46609cf2****",
    "ConnectionPoolType": "Transaction"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023081010543697567834532E89F00585",
        "Action": "ModifyDBProxyConfig",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
