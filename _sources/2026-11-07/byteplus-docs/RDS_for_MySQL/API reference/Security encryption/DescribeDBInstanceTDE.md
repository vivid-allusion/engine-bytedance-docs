---
title: "DescribeDBInstanceTDE"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancetde"
---

Call the DescribeDBInstanceTDE API to query the enablement status of transparent data encryption for an instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-d759ceaf\*\*\*\* |Instance ID. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|TDEStatus |String |Enable |The status of transparent data encryption. Valid values:<br><br><br>* `Enable`: Enabled.<br><br>* `Disable`: Disabled. |

## Sample request

```json
POST /?Action=DescribeDBInstanceTDE&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-a4cbc113****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202401042112522FCB0C814DE81D66FCCB",
        "Action": "DescribeDBInstanceTDE",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "TDEStatus": "Disable"
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
