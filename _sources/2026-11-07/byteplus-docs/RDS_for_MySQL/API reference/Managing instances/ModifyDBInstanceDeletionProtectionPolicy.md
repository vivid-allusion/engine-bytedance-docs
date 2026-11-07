---
title: "ModifyDBInstanceDeletionProtectionPolicy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancedeletionprotectionpolicy"
---

Call the ModifyDBInstanceDeletionProtectionPolicy API to set the deletion protection feature for an instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-b7d05f76\*\*\*\* |Instance ID. |
|DeletionProtection |String |Yes |Enabled |Whether to enable the deletion protection function of the instance. Values:<br><br><br>* `Enabled`: Yes.<br><br>* `Disabled`: No. |

## Response parameters

null

## Sample request

```json
POST /?Action=ModifyDBInstanceDeletionProtectionPolicy&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-b7d05f76****",
    "DeletionProtection": "Enabled"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202504031438164594B516F7019965F6D0-d83165",
        "Action": "ModifyDBInstanceDeletionProtectionPolicy",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
