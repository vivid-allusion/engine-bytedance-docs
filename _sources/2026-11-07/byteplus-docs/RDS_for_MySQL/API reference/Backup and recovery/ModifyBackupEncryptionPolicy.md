---
title: "ModifyBackupEncryptionPolicy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifybackupencryptionpolicy"
---

Call the ModifyBackupEncryptionPolicy API to modify backup encryption settings.

## Request type

Synchronous request.

## Precautions

* When calling this API, if you encounter the error "Instance version is too low to support the requested operation," please [submit a ticket](https://console.byteplus.com/workorder/create/)to contact technical support for instance upgrade.

* Cloud disk instances do not currently support backup encryption.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-0d458bb5\*\*\*\* |Instance ID. |
|DataBackupEnabled |Boolean |No |true |Whether to encrypt data backups. Valid values:<br><br><br>* `true`: Encrypt data backups.<br><br>* `false`: Do not encrypt data backups.<br><br><br>tip<br><br>This field has no default value. If not passed, no modification will be made. |
|LogBackupEnabled |Boolean |No |true |Whether to encrypt log backups. Valid values:<br><br><br>* `true`: Encrypt log backups.<br><br>* `false`: Do not encrypt log backups.<br><br><br>tip<br><br>This field has no default value. If not passed, no modification will be made. |

## Response parameters

null

## Sample request

```json
POST /?Action=ModifyBackupEncryptionPolicy&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-0d458bb5****",
    "DataBackupEnabled": false,
    "LogBackupEnabled": true
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202405151146235EF356A9CB6A5E70EEB4-399688",
        "Action": "ModifyBackupEncryptionPolicy",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
