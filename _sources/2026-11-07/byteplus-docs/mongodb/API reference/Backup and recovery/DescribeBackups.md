---
title: "DescribeBackups"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describebackups"
---

Call the DescribeBackups API to query the backup file list of the target MongoDB instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-shard\-f9e5d782\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information of all MongoDB instances in the target region, including the instance ID. |
|BackupType |String |No |Physical |Backup types. The value range is as follows:<br><br><br>* `Physical`: physical backup.<br><br>* `Logical`: logical backup.<br><br><br>tip<br><br>If this parameter is left blank, the backup list of all types under the current instance will be returned by default. |
|StartTime |String |No |2024\-04\-10T13:10:10Z |Query start time. The format is *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC).<br><br>tip<br><br>If this parameter is left blank, it means that the query start time is not specified, and by default, all existing backups under the current instance will be returned. |
|EndTime |String |No |2024\-04\-10T13:10:15Z |Query end time. The format is *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC).<br><br>tip<br><br><br>* If this parameter is left blank, it means that the query end time is not specified, and by default, all existing backups under the current instance will be returned.<br><br>* The query end time should be later than the query start time. |
|BackupStatus |String |No |Success |Backup status. The value range is as follows:<br><br><br>* `Success`: The backup is successful.<br><br>* `Failed`: The backup fails.<br><br>* `Running`: The backup is in progress.<br><br><br>tip<br><br>If this parameter is left blank, it means that the backup status is not used for filtering, and by default, backups of all statuses under the current instance will be returned. |
|BackupObject |String |No |Data |Backup object. The value range is as follows:<br><br><br>* `Data`: Data backup.<br><br>* `Log`: Log backup.<br><br><br>tip<br><br>If this parameter is left blank, it means that no backup object is used for filtering, and by default, the backups of all objects under the current instance will be returned. |
|PageNumber |Integer |No |1 |The page number of the backup file list, with a default value of 1. The value should not exceed the maximum value of the Integer data type, and the starting value is 1. |
|PageSize |Integer |No |10 |Number of records per page, the value range is 1 \- 1000, and the default value is 10. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer | |The total number of backup files. |
|Backups |Object[] | |Backup file list information. |
|BackupId |String |fb9a3679fe7b42e490172287eed7\*\*\*\* |Backup ID. |
|BackupStatus |String |Success |Backup status. The value range is as follows:<br><br><br>* `Success`: The backup is successful.<br><br>* `Failed`: The backup fails.<br><br>* `Running`: The backup is in progress. |
|BackupType |String |Physical |Backup types. The value range is as follows:<br><br><br>* `Physical`: physical backup.<br><br>* `Logical`: logical backup. |
|BackupObject |String |Data |Backup object. The value range is as follows:<br><br><br>* `Data`: Data backup.<br><br>* `Log`: Log backup. |
|Creator |String |System |The identity of the subject that creates the backup. The value range is as follows:<br><br><br>* `System`: Automatic backup by the system.<br><br>* `User`: Manual backup by the user. |
|BackupStartTime |String |2022\-10\-25T17:12:35Z |Backup start time. The format is *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC). |
|BackupEndTime |String |2015\-08\-30T15:27:50Z |Backup end time. The format is *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC). |
|BackupFileName |String |166668\*\*\*\*.zip |Backup file name. |
|BackupFileSize |Long |112036 |The size of the backup file. Unit: Byte. |
|BackupDownloadStatus |String |NotDownLoad |The download status of the backup file. The value range is as follows:<br><br><br>* `NotDownLoad`: The backup file has not been obtained yet.<br><br>   tip<br><br>   If the backup file is in the `NotDownLoad` state, you can call the [ModifyDBInstanceBackupURL](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancebackupurl) API to obtain the specified backup file.<br><br>* `Success`: The backup file is available for download.<br><br>   tip<br><br>   When the backup file is in the `Success` state, you can call the [DescribeDBInstanceBackupURL](https://docs.byteplus.com/en/docs/mongodb/describedinstancesbackupurl) API to view the download address information of the target backup file.<br><br>* `Running`: The backup file is being obtained. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeBackups&Version=2022-01-01 HTTP/1.1
Host: mongodb.volcengineapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-shard-f9e5d782****",
    "PageNumber": 1,
    "PageSize": 10,
    "StartTime": "2022-10-25T09:12:35Z",
    "EndTime": "2022-10-25T09:12:50Z"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104202D3110023228002****",
        "Action": "DescribeBackups",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Backups": [
            {
                "BackupDownloadStatus": "Success",
                "BackupEndTime": "2022-10-25T09:12:49Z",
                "BackupFileName": "1666689162.zip",
                "BackupFileSize": 112036,
                "BackupId": "fb9a3679fe7b42e490172287eed7****",
                "BackupObject": "Data",
                "BackupStartTime": "2022-10-25T09:12:37Z",
                "BackupStatus": "Success",
                "BackupType": "Logical",
                "Creator": "User"
            }
        ],
        "Total": 1
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
