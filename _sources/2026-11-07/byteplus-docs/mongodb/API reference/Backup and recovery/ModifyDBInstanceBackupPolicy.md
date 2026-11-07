---
title: "ModifyDBInstanceBackupPolicy"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifydbinstancebackuppolicy"
---

Call the ModifyDBInstanceBackupPolicy API to modify the automatic backup policy of the target MongoDB instance.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-shard\-f9e5d782\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information of all MongoDB instances in the target region, including the instance ID. |
|DataFullBackupTime |String |No |15:00\-16:00 |The time to execute backup, in the format of `HH:mm-HH:mm` (local time).<br><br>tip<br><br><br>* It supports setting any whole hour time in a day to execute backup, with a time interval of 1 hour.<br><br>* If this parameter is left blank, it means not to modify the backup execution time of the instance. |
|DataBackupRetentionDay |Integer |No |8 |backup retention days. The value range is: 7~365.<br><br>tip<br><br>If this parameter is left blank, it means that the backup retention days of the instance will not be modified. |
|DataFullBackupPeriods |String[] |No |["MONDAY","TUESDAY"] |backup cycle, and the value range is as follows:<br><br><br>* `MONDAY`: Monday.<br><br>* `TUESDAY`: Tuesday.<br><br>* `WEDNESDAY`: Wednesday.<br><br>* `THURSDAY`: Thursday.<br><br>* `FRIDAY`: Friday.<br><br>* `SATURDAY`: Saturday.<br><br>* `SUNDAY`: Sunday.<br><br><br>tip<br><br><br>* For security reasons, two or more days must be selected as the backup cycle. Multiple backup times are separated by a comma (,).<br><br>* If this parameter is left blank, it means that the backup cycle of the Instance will not be modified. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyDBInstanceBackupPolicy&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "InstanceId": "mongo-shard-f9e5d782****",
    "DataFullBackupTime": "01:00-02:00",
    "DataFullBackupPeriods": [
        "MONDAY",
        "TUESDAY"
    ],
    "DataBackupRetentionDay": 8
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104202D3110023228002****",
        "Action": "ModifyDBInstanceBackupPolicy",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
