---
title: "DescribeDBInstanceBackupPolicy"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describedbinstancebackuppolicy"
---

Call the DescribeDBInstanceBackupPolicy API to query the automatic backup policy of the target MongoDB instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-shard\-f9e5d782\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|AutoBackup |String |Enable |The automatic backup function is enabled by default and does not support being turned off. The value of this parameter is fixed as `Enable`. |
|DataFullBackupTime |String |01:00Z\-02:00Z |The execution time of the automatic backup, in the format of `HH:mmZ-HH:mmZ` (UTC). The interval time window is 1 hour. |
|DataBackupRetentionDay |Integer |7 |Backup retention days. |
|DataFullBackupPeriods |String[] |[<br><br>"MONDAY",<br><br>"TUESDAY",<br><br>"WEDNESDAY",<br><br>"THURSDAY",<br><br>"FRIDAY",<br><br>"SATURDAY",<br><br>"SUNDAY"<br><br>] |Backup cycle, that is, the time when backup will be performed within a week. It is subject to the start time of backup execution. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeDBInstanceBackupPolicy&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "InstanceId": "mongo-shard-f9e5d782****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104202D3110023228002****",
        "Action": "DescribeDBInstanceBackupPolicy",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "AutoBackup": "Enable",
        "DataBackupRetentionDay": 7,
        "DataFullBackupPeriods": [
            "MONDAY",
            "TUESDAY",
            "WEDNESDAY",
            "THURSDAY",
            "FRIDAY",
            "SATURDAY",
            "SUNDAY"
        ],
        "DataFullBackupTime": "01:00Z-02:00Z"
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
