---
title: "DescribeBackups"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeBackups"
---

Call the DescribeBackups to query the backup file list of the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBackups&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-gzwdsf9b\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|BackupType |String |No |Full |The backup type. The value is `Full` because only full backup is supported. |
|BackupStartTime |String |No |2023\-07\-14T18:43:00Z |The earliest backup creation time, in yyyy\-MM\-ddTHH:mm:ssZ format (UTC time). This is the time when the backup task started. |
|BackupEndTime |String |No |2023\-07\-16T18:52:31Z |The latest time the backup was created, in yyyy\-MM\-ddTHH:mm:ssZ format (UTC). The time is based on the start time of the backup task. |
|BackupStatus |String |No |Success |The backup state. The value can be:<br><br><br>* `Success`: Succeeded.<br><br>* `Failed`: Failed.<br><br>* `Running`: Executing. |
|BackupMethod |String |No |Physical |The backup method. Only physical backup is supported, and the value is `Physical`. |
|PageNumber |Integer |No |1 |The page number of the backup file list. The value cannot exceed the maximum value of the Integer data type. The default value is 1. |
|PageSize |Integer |No |10 |Number of records per page. The value is an integer from 1 to 1000. The default value is 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |2 |Total number of backup files. |
|BackupsInfo |Array of [BackupInfo](https://docs.byteplus.com/en/docs/265/57386#backupinfo) |Refer to the return example. |Backup list. |


<span id="backupinfo"></span>
### BackupInfo


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|BackupId |String |snap\-64b6\*\*\*\*\-7837 |Backup ID. |
|BackupStatus |String |Success |The backup state. The value can be:<br><br><br>* `Success`: Succeeded.<br><br>* `Failed`: Failed.<br><br>* `Running`: Executing. |
|CreateType |String |Physical |Creation type, with the following values:<br><br><br>* `System`: Automatic backup.<br><br>* `User`: Manual backup. |
|BackupMethod |String |Physical |The backup method. Only physical backup is supported, and the value is `Physical`. |
|BackupType |String |Full |The backup type. The value is `Full` because only full backup is supported. |
|BackupFileSize |Long |437 |Backup file size in KiB. |
|BackupStartTime |String |2023\-07\-19T06:20:22Z |Backup start time, format: yyyy\-MM\-ddTHH:mm:ssZ (UTC time). |
|BackupEndTime |String |2023\-07\-19T06:31:28Z |Backup end time, format: yyyy\-MM\-ddTHH:mm:ssZ (UTC time). |
|ConsistentTime |String |2023\-07\-19T06:20:22Z |The time point of the consistent backup. Format: yyyy\-MM\-ddTHH:mm:ssZ (UTC time). |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeBackups&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-gzwdsf9b****",
    "PageSize": 10,
    "PageNumber": 1
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230719142514583A11C78B08A3A0AEB6",
        "Action": "DescribeBackups",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupsInfo": [
            {
                "BackupEndTime": "2023-07-18T19:21:28Z",
                "BackupFileSize": 437,
                "BackupId": "snap-64b6****-7837",
                "BackupMethod": "Physical",
                "BackupStartTime": "2023-07-18T19:14:00Z",
                "BackupStatus": "Success",
                "BackupType": "Full",
                "ConsistentTime": "2023-07-18T19:14:00Z",
                "CreateType": "System"
            },
            {
                "BackupEndTime": "",
                "BackupFileSize": 0,
                "BackupId": "snap-64b7****-6144",
                "BackupMethod": "Physical",
                "BackupStartTime": "2023-07-19T06:20:22Z",
                "BackupStatus": "Running",
                "BackupType": "Full",
                "ConsistentTime": "2023-07-19T06:20:22Z",
                "CreateType": "User"
            }
        ],
        "Total": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
