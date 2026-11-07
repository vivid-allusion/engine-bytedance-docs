---
title: "DescribeResourceUsage"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeResourceUsage"
---

Call the DescribeResourceUsage API to query the resource usage of the instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f83edc2e\*\*\*\* |Instance ID. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|StorageUse |Double |4.23 |The instance has used storage space, and the unit is GiB. |
|BackupUse |Double |0.08 |The space used by the backup of the instance, in units of GiB. |
|StorageDataSize |Long |4399611904 |The space used by the data in the instance storage space. |
|StorageLogSize |Long |29223884 |The space used by logs in the instance storage space. |
|StorageBinLogSize |Long |29179904 |The space used by Binlog in the instance storage space. |
|StorageErrorLogSize |Long |27596 |The space used by error logs in the instance storage space. |
|StorageAuditLogSize |Long |4096 |The space used by the audit logs in the instance storage space. |
|StorageSlowLogSize |Long |12288 |The space used by the slow log in the instance storage space. |
|BackupDataSize |Long |27276988 |The space used by the data in the backup. |
|BackupLogSize |Long |61358580 |The space used by logs in backup. |
|BackupBinLogSize |Long |61311932 |The space used by the Binlog log during backup. |
|BackupErrorLogSize |Long |29147 |The space used by the error logs in the backup. |
|BackupAuditLogSize |Long |0 |The space used by the audit log during backup. |
|BackupSlowLogSize |Long |17501 |The space used by the slow log in the backup. |
|BackupFreeQuotaSize |Long |100 |Free backup storage space, in units of GiB. |
|BasicBackupDataSize |Long |61311932 |The space used by data in the basic backup. |
|BasicBackupBinlogSize |Long |27276988 |The space used by the Binlog log in the basic backup. |
|BackupChargeStatus |String |Normal |The billing status of the backup space. |
|StorageSpace |Integer |100 |Total storage space of the instance, in GiB. |

## Sample request

```json
POST /?Action=DescribeResourceUsage&Version=2022-01-01
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json
X-Date: 20180614T114308Z
Authorization: HMAC-SHA256 Credential=AKIAIAGMBG4SXSQQ****/20180614/ap-southeast-1/rds_mysql/request, SignedHeaders=accept;content-type;host;x-date, Signature=6a593bf5f59e7c1109fb205c739d1cff4c672fe2d251963f4d48c8701d16****
{
    "InstanceId": "mysql-f83edc2e****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202507241419478DBE109A9F2704000B6E-b689ac",
        "Action": "DescribeResourceUsage",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "BackupAuditLogSize": 0,
        "BackupBinLogSize": 61311932,
        "BackupDataSize": 27276988,
        "BackupErrorLogSize": 29147,
        "BackupFreeQuotaSize": 100,
        "BackupLogSize": 61358580,
        "BackupSlowLogSize": 17501,
        "BackupUse": 0.08,
        "BasicBackupBinlogSize": 61311932,
        "BasicBackupDataSize": 27276988,
        "StorageAuditLogSize": 4096,
        "StorageBinLogSize": 29179904,
        "StorageDataSize": 4399611904,
        "StorageErrorLogSize": 27596,
        "StorageLogSize": 29223884,
        "StorageSlowLogSize": 12288,
        "StorageSpace": 100,
        "StorageUse": 4.23
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
