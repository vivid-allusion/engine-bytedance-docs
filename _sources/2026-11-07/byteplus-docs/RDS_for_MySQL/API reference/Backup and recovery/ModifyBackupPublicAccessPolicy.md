---
title: "ModifyBackupPublicAccessPolicy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifybackuppublicaccesspolicy"
---

Call the ModifyBackupPublicAccessPolicy API to modify the public network download policy for instance backups.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-25651c34\*\*\*\* |Instance ID. |
|PublicDownloadEnable |Boolean |Yes |true |Whether to allow downloading instance backup data from the public network environment. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|InstanceId |String |mysql\-25651c34\*\*\*\* |Instance ID. |
|PublicDownloadEnable |Boolean |true |Whether to allow downloading instance backup data from the public network environment. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |

## Sample request

```json
POST /?Action=ModifyBackupPublicAccessPolicy&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-25651c34****",
    "PublicDownloadEnable": false
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202506052010561781E768F61CA267EC43-dd5236",
        "Action": "ModifyBackupPublicAccessPolicy",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "mysql-25651c34****",
        "PublicDownloadEnable": false
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
