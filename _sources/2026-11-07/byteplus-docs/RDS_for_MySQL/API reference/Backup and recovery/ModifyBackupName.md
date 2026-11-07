---
title: "ModifyBackupName"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/ModifyBackupName"
---

Call the ModifyBackupName interface to modify the name of the data backup.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-534dbc2c\*\*\*\* |Instance ID |
|BackupId |String |Yes |e5c2a9a9f0aa4e2688d189652ac22587 |The ID of the data backup. |
|BackupName |String |Yes |Manual data backup 001 |Set the name of the backup. The naming rules are as follows:<br><br><br>* It cannot start with a hyphen (\-).<br><br>* It can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* The length needs to be between 1 and 128 characters. |

## Response parameters

null

## Sample request

```json
POST /?Action=ModifyBackupName&Version=2022-01-01
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json
X-Date: 20180614T114308Z
Authorization: HMAC-SHA256 Credential=AKIAIAGMBG4SXSQQ****/20180614/ap-southeast-1/rds_mysql/request, SignedHeaders=accept;content-type;host;x-date, Signature=6a593bf5f59e7c1109fb205c739d1cff4c672fe2d251963f4d48c8701d16****
{
    "InstanceId": "mysql-534dbc2c****",
    "BackupId": "e5c2a9a9f0aa4e2688d189652ac22587",
    "BackupName": "手动数据备份001"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202509182202261BFF602FF4CD08E0A04F-971667",
        "Action": "ModifyBackupName",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
