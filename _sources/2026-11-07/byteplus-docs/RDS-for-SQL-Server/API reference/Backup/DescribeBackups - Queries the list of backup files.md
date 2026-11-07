---
title: "DescribeBackups - Queries the list of backup files"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackups"
---

Call the DescribeBackups API to view the list of backup sets.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section lists only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span>`Example value: DescribeBackups`

The action to perform. The value is `DescribeBackups`.



**Version ** <span data-label="purple">string </span>`Example value: 2022-01-01`

The API version. The value is `2022-01-01`.



**InstanceId ** <span data-label="purple">string   </span>`Example value: mssql-d59138f3****`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> operation to query the instance ID.</div>




**PageNumber ** <span data-label="purple">integer </span>`Optional Example value: 1`

Query offset for the current page. The minimum value is 1, the maximum value is 2147483647, and the default value is 1.



**PageSize ** <span data-label="purple">integer </span>`Optional Example value: 10`

Number of records per page. The minimum value is 1, the maximum value is 1000, and the default value is 10.



**BackupStartTime ** <span data-label="purple">string </span>`Optional. Example value: 2023-08-23T04:07:02.000Z`

The start time for the query. Format: yyyy\-MM\-ddTHH:mm:ss.sZ (UTC time).



**BackupEndTime ** <span data-label="purple">string </span>`Optional. Example value: 2023-08-23T04:06:49.000Z`

The end time of the query. Format: yyyy\-MM\-ddTHH:mm:ss.sZ (UTC time).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The query end time must be later than the query start time.</div>




**BackupType ** <span data-label="purple">string </span>`Optional. Example value: Full`

Backup type. By default, all backup information is returned. Valid values are as follows:


* `Full`: Full backup.

* `Diff`: Incremental backup.

* `Log`: Log backup.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When this parameter is not passed, a list of full and incremental backup sets is returned by default.</div>




**BackupId ** <span data-label="purple">string </span>`Optional. Example value: ca155ac99fcb4eed86617041bfe0****`

The backup ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackups">DescribeBackups</a> operation to query the backup ID.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Total ** <span data-label="purple">integer </span>`Example: 1`

Total number of backups.



**BackupsInfo ** <span data-label="purple">object[] </span>`Example value: BackupInfoObject`

Backup list.


**BackupEndTime ** <span data-label="purple">string </span>`Example value: 2023-04-17T18:48:00.000Z`

The end time of the backup, in yyyy\-MM\-ddTHH:mm:sssZ format (UTC).



**BackupId ** <span data-label="purple">string </span>`Example: 8d4ce0cbd1d643cc8287cedbf421****`

The backup ID.



**BackupStartTime ** <span data-label="purple">string </span>`Example value: 2023-04-17T18:48:00.000Z`

The start time of the backup, in yyyy\-MM\-ddTHH:mm:sssZ format (UTC time).



**BackupMethod ** <span data-label="purple">string </span>`Example value: Physical`

The backup method. The values are:


* `Logical`: Indicates a logical backup.

* `Physical`: Physical backup.

* `Snapshot`: Snapshot backup.



**BackupStatus ** <span data-label="purple">string </span>`Example value: Success`

The backup status can be one of the following:


* `Success`: Success.

* `Failed`: Failed.

* `Running`: Running.



**CreateType ** <span data-label="purple">string </span>`Example value: System`

Creation type. The values are:


* `System`: System.

* `User`: User.



**BackupType ** <span data-label="purple">string </span>`Example: Full`

Backup type. Value:


* `Full`: Full backup.

* `Diff`: Incremental backup.



**BackupFileSize ** <span data-label="purple">long </span>`Example value: 5129555`

Backup file size in bytes.



**DownloadProgress ** <span data-label="purple">integer </span>`Example value: 10`

The progress of backup file preparation as a percentage.



**DownloadStatus ** <span data-label="purple">string </span>`Example value: Success`

Backup file preparation status. Value:


* `Success`: Preparation complete.

* `Failed`: Preparation failed.

* `Running`: Preparing.

* `NotDownload`: Not downloaded.



**BackupDatabaseDetail ** <span data-label="purple">object[] </span>`Example value: BackupDatabaseDetail`

Backup information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned only when you call the DescribeBackupDetail API to query the details of a backup file.</div>



**BackupFileName ** <span data-label="purple">string </span>`Example value: backup/mssql-bbe31c86****/D/1692648480-master-D-06bf4b6a4313495c9debd28bf3ab****.bak`

The name of the backup file.



**BackupFileSize ** <span data-label="purple">long </span>`Example: 1048576`

Backup file size in bytes.



**BackupStartTime ** <span data-label="purple">string </span>`Example value: 2023-08-22T08:17:14.000Z`

The time when the backup started. Format: yyyy\-MM\-ddTHH:mm:ss.sZ (UTC time).



**BackupEndTime ** <span data-label="purple">string </span>`Example value: 2023-08-22T08:17:14.000Z`

The backup end time. Format: yyyy\-MM\-ddTHH:mm:ss.sZ (UTC time).



**DatabaseName ** <span data-label="purple">string </span>`Example value: testname`

Database name.



**DownloadProgress ** <span data-label="purple">integer </span>`Example value: 10`

The progress of backup file preparation as a percentage.



**BackupType ** <span data-label="purple">string </span>`Example: Full`

Backup type. The values are as follows:


* `Full`: Full backup.

* `Diff`: Differential backup.



**BackupDownloadLinkInner ** <span data-label="purple">string </span>`Example value: https://*****`

Private network download link.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before accessing private network backup download link, you need to call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackupdetail">DescribeBackupDetail</a> API to get the private network download link.</div>




**BackupDownloadLinkEIP ** <span data-label="purple">string </span>`Example: https://*****`

Public download link.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To get the public download link, call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackupdetail">DescribeBackupDetail</a> API.</div>




**DownloadStatus ** <span data-label="purple">string </span>`Example value: Success`

Backup file preparation status. Value:


* `Success`: Preparation complete.

* `Failed`: Preparation failed.

* `Running`: Preparing.

* `NotDownload`: Not downloaded.



**LinkExpiredTime ** <span data-label="purple">string </span>`Example value: 2023-05-11T02:55:44.000Z`

The expiration time of the download link. Format: yyyy\-MM\-ddTHH:mm:sssZ (UTC time).





<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeBackups&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "InstanceId":"mssql-bbe31c86****",
    "PageNumber":2,
    "PageSize":2,
    "BackupStartTime":"2023-07-22T08:17:14.000Z",
    "BackupEndTime":"2023-08-28T08:17:14.000Z",
    "BackupType":"Full"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202308251632083CF07BEFDEE44595C73B",
        "Action":"DescribeBackups",
        "Version":"2022-01-01",
        "Service":"rds_mssql",
        "Region":"cn-chongqing-sdv"
    },
    "Result":{
        "BackupsInfo":[
            {
                "BackupDatabaseDetail":[
                    {
                        "BackupEndTime":"2023-08-23T15:50:46.000Z",
                        "BackupFileName":"backup/mssql-1be522b55907/D/1692805800-tets9-D-f5a088501fab445d9debde68dc90****.bak",
                        "BackupFileSize":477868,
                        "BackupStartTime":"2023-08-23T15:50:46.000Z",
                        "BackupType":"Full",
                        "DatabaseName":"tets9",
                        "DownloadProgress":0,
                        "DownloadStatus":"Success",
                        "LinkExpiredTime":""
                    }
                ],
                "BackupEndTime":"2023-08-23T15:50:47.000Z",
                "BackupFileSize":13442833,
                "BackupId":"f5a088501fab445d9debde68dc90****",
                "BackupMethod":"Physical",
                "BackupStartTime":"2023-08-23T15:50:00.000Z",
                "BackupStatus":"Success",
                "BackupType":"Full",
                "CreateType":"System"
            }
        ],
        "Total":1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the error codes related to the business logic of this API. For common error codes, see the [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to exist running import job. |This operation can not be performed while the current instance is importing data. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The number of manual backups exceeds the limit. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to exist running backup job. |This operation can not be performed because the instance is currently running a backup task. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |The operation is not supported. |
|400 |InstanceIsNotRunning |The specified instance is not running. |The instance is not Running. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |This operation can not be performed on incremental backups. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |The {parameter1} parameter is missing. |
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |DB verification failed because {parameter1}. |
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of parameter {parameter1} is invalid. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |Restoring the database exceeds the quota limit. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |Insufficient resources in the current availability zone. |
|404 |BackupNotFound |The specified instance does not exist available backup records. |No available backup records found. |
|404 |InstanceNotFound |The specified instance does not exist. |The instance was not found. |
|500 |InternalError |The request failed with internal server error. |Internal error. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are in progress. Try again later. |
