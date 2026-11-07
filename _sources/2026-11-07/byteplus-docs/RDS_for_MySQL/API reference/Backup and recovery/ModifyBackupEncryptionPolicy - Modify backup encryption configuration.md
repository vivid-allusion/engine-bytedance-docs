---
title: "ModifyBackupEncryptionPolicy - Modify backup encryption configuration"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/ModifyBackupEncryptionPolicy"
---

Call the ModifyBackupEncryptionPolicy API to modify backup encryption settings.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If you receive the error "The instance version is too low to support the requested operation" when calling this API, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical staff to upgrade the instance.

* Cloud disk instances do not support backup encryption currently.

* MySQL 8.4 instances do not support backup encryption.


<span id=".6LCD6K-V"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-0d458bb5\*\*\*\* |Instance ID. |
|DataBackupEnabled |Boolean |No |true |Whether to encrypt the data backup. Values:<br><br><br>* `true`: encrypts data backup.<br><br>* `false`: does not encrypt data backup.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter has no default value. If omitted, no modification is made.</div><br> |
|LogBackupEnabled |Boolean |No |true |Specifies whether to encrypt log backups. Values:<br><br><br>* `true`: encrypts log backup.<br><br>* `false`: does not encrypt log backup.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter has no default value. If omitted, no modification is made.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyBackupEncryptionPolicy&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-0d458bb5****",
    "DataBackupEnabled": false,
    "LogBackupEnabled": true
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202405151146235EF356A9CB6A5E70EEB4-399688",
        "Action": "ModifyBackupEncryptionPolicy",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
