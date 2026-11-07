---
title: "SwitchDBInstanceHA"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/switchdbinstanceha"
---

Call the SwitchDBInstanceHA API to manually switch the primary and secondary nodes of a specified MySQL instance.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-46609cf2\*\*\*\* |Instance ID. |
|NodeId |String |Yes |mysql\-46609cf2\*\*\*\*\-1 |Secondary node ID. |

## Response parameters

null

## Sample request

```json
POST /?Action=SwitchDBInstanceHA&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-d4942fd7****",
    "NodeId": "mysql-d4942fd7****-1"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230810110301C4BCE9ED7378F7E82706",
        "Action": "SwitchDBInstanceHA",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
