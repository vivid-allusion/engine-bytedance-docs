---
title: "DescribeBinlogFiles"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebinlogfiles"
---

Call the DescribeBinlogFiles API to query Binlog backup files.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

If Binlog backup is not enabled for the instance, this API call returns a null value.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBinlogFiles&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-ce48081d\*\*\*\* |Instance ID. |
|StartTime |String |Yes |2022\-06\-01T15:00:00Z |Query start time. The format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time). |
|EndTime |String |Yes |2022\-06\-20T15:00:00Z |Query end time. The format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time). The query end time must be later than the query start time, and the time range cannot be greater than 15 days. |
|Context |String |No |rds/mysql\-603e30xxxx/mysql\-603e30xxxx\-0/binlog/binlog\-16834098316xxxx\-binlog.000041 |Index information that specifies the starting position of the returned backup information. If specified, backup information is returned starting from the next backup file after the one specified by Context. |
|BackupFileNumber |Integer |No |10 |The quantity of backup files. The default value is 10 and the maximum value is 250. |
|ResultSorter |String |No |SortByFileSizeAsc |Supports sorting by a specified condition. Values:<br><br><br>* `Default`: Data backups are sorted by start time in descending order, and log backups are sorted by backup time in descending order.<br><br>* `SortByTimeAsc`: Data backups are sorted by start time in ascending order, and log backups are sorted by backup time in ascending order.<br><br>* `SortByTimeDesc`: Data backups are sorted by start time in descending order, and log backups are sorted by backup time in descending order.<br><br>* `SortByFileSizeAsc`: Sorts by file size in ascending order.<br><br>* `SortByFileSizeDesc`: Sorts by file size in descending order. |
|NodeId |String |No |mysql\-f4091b4a\*\*\*\*\-mda8b\-0 |The ID of the Node where the binlog is located first.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a node is specified, only the binlog for that node is returned.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Integer |9 |Number of backup files. |
|Context |String |rds/mysql\-603e30e6\*\*\*\*/mysql\-603e30e6\*\*\*\*\-0/binlog/binlog\-1683547416864283247\-binlog.000081 |Index information. Use the last backup file as the index for return. Can be used as the parameter for the next request. Select when loading more. |
|BinlogFiles |Array of [BinlogFileObject](https://docs.byteplus.com/en/docs/40/15438#binlogfileobject) |Refer to the sample response. |Backup list. |


<span id="binlogfileobject"></span>
### BinlogFileObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|BackupRegion |String |cn\-shanghai |The region where the binlog backup is located. |
|BackupStatus |String |Success |Backup status, values:<br><br><br>* `Succeeded`: succeeded.<br><br>* `Failed`: failed.<br><br>* `In progress`: in progress. |
|DownloadStatus |String |NotDownload |Download status. Values:<br><br><br>* `NotDownload`: Not downloaded.<br><br>* `Success`: Downloaded.<br><br>* `Failed`: Download failed.<br><br>* `Running`: Downloading. |
|FileName |String |binlog\-168348183442461\*\*\*\*\-binlog.000061 |File name first. |
|FileSize |Long |1024 |File size. Unit: Byte. |
|NodeId |String |mysql\-f4091b4a\*\*\*\*\-mda8b\-0 |The ID of the Node where the binlog is located first. |
|UpdateTime |String |2023\-05\-06T04:50:29.000Z |Update time. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|IsEncrypted |Boolean |true |Indicates whether the data backup is encrypted. Values:<br><br><br>* `true`: encrypted.<br><br>* `false`: not encrypted. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeBinlogFiles&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-603e30e6****",
    "StartTime": "2023-05-05T10:49:59Z",
    "EndTime": "2023-05-17T10:49:59Z",
    "BackupFileNumber": 5
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202305082058412F29109E3B606793D1F7",
        "Action": "DescribeBinlogFiles",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BinlogFiles": [
            {
                "BackupRegion": "cn-beijing",
                "BackupStatus": "Success",
                "DownloadStatus": "NotDownload",
                "FileName": "binlog-1683269409494461068-binlog.000001",
                "FileSize": 169,
                "NodeId": "mysql-f4091b4a****-mda8b-0",
                "UpdateTime": "2023-05-05T07:13:33.000Z"
            },
            {
                "BackupRegion": "cn-beijing",
                "BackupStatus": "Success",
                "DownloadStatus": "NotDownload",
                "FileName": "binlog-1683269413387493959-binlog.000002",
                "FileSize": 3011622,
                "NodeId": "mysql-f4091b4a****-mda8b-0",
                "UpdateTime": "2023-05-05T07:13:33.000Z"
            },
            {
                "BackupRegion": "cn-beijing",
                "BackupStatus": "Success",
                "DownloadStatus": "NotDownload",
                "FileName": "binlog-1683273026662514347-binlog.000003",
                "FileSize": 1123725,
                "NodeId": "mysql-f4091b4a****-seed3-0",
                "UpdateTime": "2023-05-05T07:50:28.000Z"
            },
            {
                "BackupRegion": "cn-beijing",
                "BackupStatus": "Success",
                "DownloadStatus": "NotDownload",
                "FileName": "binlog-1683276626773091536-binlog.000004",
                "FileSize": 1140025,
                "NodeId": "mysql-f4091b4a****-seed3-0",
                "UpdateTime": "2023-05-05T08:50:29.000Z"
            },
            {
                "BackupRegion": "cn-beijing",
                "BackupStatus": "Success",
                "DownloadStatus": "NotDownload",
                "FileName": "binlog-1683280226892626614-binlog.000005",
                "FileSize": 1140087,
                "NodeId": "mysql-f4091b4a****-mda8b-0",
                "UpdateTime": "2023-05-05T09:50:27.000Z"
            }
        ],
        "Context": "rds/mysql-f4091b4a****/mysql-f4091b4a****-0/binlog/binlog-1683280226892626614-binlog.000005",
        "Total": 5
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
