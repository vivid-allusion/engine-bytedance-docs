---
title: "DescribeDBInstanceBackupURL"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describedinstancesbackupurl"
---

Call the DescribeDBInstanceBackupURL API to query information such as the acquisition progress, download URL, and validity period of the download URL of a specified backup file in the target MongoDB instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-3b96fa21\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|BackupId |String |Yes |ff4ab943f6ef450f8f48c1c258b4\*\*\*\* |It is necessary to obtain the backup ID of the backup file.<br><br>tip<br><br>For backups generated through physical backup methods, since these backup files are stored in a sharded form in the object storage TOS. You need to first call the [ModifyDBInstanceBackupURL](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancebackupurl) API to obtain the backup file, and then call the DescribeDBInstanceBackupURL API to view the download address of the backup file, and download the specified backup file to the local through the download address. Therefore, this backup ID needs to be consistent with the `BackupId` in the ModifyDBInstanceBackupURL request parameter. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|InstanceId |String |mongo\-replica\-3b96fa21\*\*\*\* |Instance ID. |
|BackupId |String |ff4ab943f6ef450f8f48c1c258b4\*\*\*\* |Backup ID. |
|BackupDownloadLink |String |https://mongodb.tos\-s3\-ap\-southeast\-1.bytepluses.com/mongo/mongo\-replica\-3b96fa21\*\*\*\* |The public network download address of the backup file.<br><br>tip<br><br>You can first copy this download address, then paste it into the address bar of the browser and press Enter, and the browser can automatically complete the download. |
|PrivateDownloadLink |String |https://mongodb.tos\-s3\-ap\-southeast\-1.ibytepluses.com/mongo/mongo\-replica\-3b96fa21\*\*\*\* |The private network download address of the backup file.<br><br>tip<br><br>You need to be in a private network environment (for example, under the same VPC as the current MongoDB instance) to use this address for downloading. For more details, refer to [Managing backup files](https://docs.byteplus.com/en/docs/mongodb/manage-backup-file). |
|LinkExpiredTime |String |2022\-10\-26T07:32:16Z |The expiration time of the backup file download address, in the format of `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>tip<br><br>The validity period of the download address is 15 minutes. After the download address expires, you can call the DescribeDBInstanceBackupURL interface again to obtain the latest download address. |
|DownloadProgress |Integer |100 |The acquisition progress of the backup file, in units of %.<br><br>tip<br><br>You need to wait until the progress reaches 100% before downloading. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeDBInstanceBackupURL&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "InstanceId": "mongo-replica-3b96fa21****",
    "BackupId": "ff4ab943f6ef450f8f48c1c258b4****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104202D3110023228002****",
        "Action": "DescribeDBInstanceBackupURL",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "BackupDownloadLink": "https://mongodb.tos-s3-ap-southeast-1.bytepluses.com/mongo/mongo-replica-3b96fa21****",
        "PrivateDownloadLink": "https://mongodb.tos-s3-ap-southeast-1.ibytepluses.com/mongo/mongo-replica-3b96fa21****",
        "BackupId": "ff4ab943f6ef450f8f48c1c258b4****",
        "DownloadProgress": 100,
        "InstanceId": "mongo-shard-f9e5d782****",
        "LinkExpiredTime": "2022-10-26T07:32:16Z"
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
