---
title: "DescribeBackupDetail - Describe backup details"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackupdetail"
---

Call the DescribeBackupDetail API to query the details of a backup file.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this API and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span>`Example value: DescribeBackupDetail`

The action to perform. The value is `DescribeBackupDetail`.



**Version ** <span data-label="purple">string   </span>`Example value: 2022-01-01`

The API version. The value is `2022-01-01`.



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-1a2e6******`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstancedetail">DescribeDBInstanceDetail</a> API to view the instance ID.</div>




**BackupId** <span data-label="purple">string</span> `Example value: 4969fcce7764447081c709c5********`

Backup ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackupdetail">DescribeBackupDetail</a> operation to query the backup ID.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**BackupsInfo** <span data-label="purple">object</span> `Example value: BackupInfoObject`

Backup details.


**BackupEndTime ** <span data-label="purple">string </span>`Example value: 2023-04-17T18:48:00.000Z`

The end time of the backup. The time is in UTC and follows the yyyy\-MM\-ddTHH:mm:sssZ format.



**BackupId ** <span data-label="purple">string </span>`Example: 8d4ce0cbd1d643cc8287cedbf421****`

Backup ID.



**BackupStartTime ** <span data-label="purple">string </span>`Example: 2023-04-17T18:48:00.000Z`

The backup start time, in yyyy\-MM\-ddTHH:mm:sssZ format (UTC time).



**BackupMethod ** <span data-label="purple">string </span>`Example value: Physical`

Backup method. The valid values are:


* `Logical`: Logical backup.

* `Physical`: Physical backup.

* `Snapshot`: Snapshot backup.



**BackupStatus ** <span data-label="purple">string </span>`Example: Success`

Status. The possible values are:


* `Success`: The backup is successful.

* `Failed`: The backup failed.

* `Running`: The backup is in progress.



**CreateType ** <span data-label="purple">string </span>`Example value: System`

The creation type. The value can be:


* `System`: System.

* `User`: User.



**BackupType ** <span data-label="purple">string </span>`Example: Full`

Backup type. Values:


* `Full`: Full backup.

* `Diff`: Incremental backup.



**BackupFileSize ** <span data-label="purple">long </span>`Example value: 5129555`

The size of the backup file in bytes.



**DownloadProgress ** <span data-label="purple">integer </span>`Example value: 10`

The preparation progress of the backup file, in percent.



**DownloadStatus ** <span data-label="purple">string </span>`Example value: Success`

Backup file preparation status. Values:


* `Success`: Preparation complete.

* `Failed`: Preparation failed.

* `Running`: Preparing.

* `NotDownload`: Not downloaded.



**BackupDatabaseDetail** <span data-label="purple">object[]</span> `Example value: BackupDatabaseDetail`

Backup information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned only when you call the DescribeBackupDetail API to query the details of a backup file.</div>



**BackupFileName ** <span data-label="purple">string </span>`Example value: backup/mssql-bbe31c86****/D/1692648480-master-D-06bf4b6a4313495c9debd28bf3ab****.bak`

Backup file name.



**BackupFileSize ** <span data-label="purple">long </span>`Example value: 1048576`

The size of the backup file in bytes.



**BackupStartTime ** <span data-label="purple">string </span>`Example value: 2023-08-22T08:17:14.000Z`

The start time of the backup. Format: yyyy\-MM\-ddTHH:mm:ss.sZ (UTC time).



**BackupEndTime ** <span data-label="purple">string </span>`Example value: 2023-08-22T08:17:14.000Z`

The end time of the backup. Format: yyyy\-MM\-ddTHH:mm:ss.sZ (UTC time).



**DatabaseName ** <span data-label="purple">string </span>`Example value: testname`

Database name.



**DownloadProgress ** <span data-label="purple">integer </span>`Example value: 10`

The preparation progress of the backup file, in percent.



**BackupType ** <span data-label="purple">string </span>`Example: Full`

Backup type. The values are as follows:


* `Full`: Full backup.

* `Diff`: Differential backup.



**BackupDownloadLinkInner ** <span data-label="purple">string </span>`Example value: https://*****`

Private network download link.

<div data-tips="true" data-tips-type="tip">Description</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackupdetail">DescribeBackupDetail</a> API to query the private network download link.</div>




**BackupDownloadLinkEIP** <span data-label="purple">string</span> `Example value: https://*****`

Public network backup download link.

<div data-tips="true" data-tips-type="tip">Description</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackupdetail">DescribeBackupDetail</a> API to query the public network download link.</div>




**DownloadStatus ** <span data-label="purple">string </span>`Example value: Success`

Backup file preparation status. Values:


* `Success`: Preparation complete.

* `Failed`: Preparation failed.

* `Running`: Preparing.

* `NotDownload`: Not downloaded.



**LinkExpiredTime ** <span data-label="purple">string </span>`Example value: 2023-05-11T02:55:44.000Z`

The expiration time of the download link, in yyyy\-MM\-ddTHH:mm:sssZ format (UTC).





<span id=".6ZSZ6K-v56CB"></span>
## Request example

```JSON
POST /?Action=DescribeBackupDetail&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "InstanceId":"mssql-1a2e6******",
    "BackupId":"4969fcce7764447081c709c5********"
}
```


<span id="SKQ7KRGU"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240903192655C04D26ABF3AEEBC8E21B-d98369",
        "Action": "DescribeBackupDetail",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupsInfo": {
            "BackupDatabaseDetail": [
                {
                    "BackupDownloadLinkEIP": "",
                    "BackupDownloadLinkInner": "",
                    "BackupEndTime": "",
                    "BackupFileName": "",
                    "BackupFileSize": 0,
                    "BackupStartTime": "",
                    "BackupType": "",
                    "DatabaseName": "#entireDBInstance#",
                    "DownloadProgress": 0,
                    "DownloadStatus": "NotDownload",
                    "LinkExpiredTime": ""
                }
            ],
            "BackupEndTime": "2024-09-02T17:09:25.000Z",
            "BackupFileSize": 5906809,
            "BackupId": "4969fcce7764447081c709c5ee1******",
            "BackupMethod": "Physical",
            "BackupStartTime": "2024-09-02T17:09:00.000Z",
            "BackupStatus": "Success",
            "BackupType": "Full",
            "CreateType": "System",
            "DownloadProgress": 0,
            "DownloadStatus": "NotDownload"
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The table below lists the error codes related to the API and business logic. For common error codes, see the [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) Document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |InstanceIsNotRunning |The specified instance is not running. |The current status of the instance is not Running. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |The operation is not supported. |
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to existing running import jobs. |This action can not be performed while the instance is importing data. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |DB validation failed because {parameter1}. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |This action can not be performed for incremental backups. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The number of manual backups has exceeded the limit. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |The {parameter1} parameter is missing. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to existing running backup jobs. |The instance is running a backup task. This operation can not be performed. |
|400 |InvalidParameter |The specified parameter %s is not valid. |Invalid value for parameter {parameter1}. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |The current availability zone has insufficient resources. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |Database restoration exceeds the quota limit. |
|404 |InstanceNotFound |The specified instance does not exist. |The instance is not found. |
|404 |BackupNotFound |The specified instance does not have available backup records. |No available backup records found. |
|500 |InternalError |The request has failed with internal server error. |Internal error. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are running. Try again later. |
