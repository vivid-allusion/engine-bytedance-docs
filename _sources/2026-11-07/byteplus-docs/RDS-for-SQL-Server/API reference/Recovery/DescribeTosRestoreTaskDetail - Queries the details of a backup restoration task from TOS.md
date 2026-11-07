---
title: "DescribeTosRestoreTaskDetail - Queries the details of a backup restoration task from TOS"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describetosrestoretaskdetail"
---

Call the DescribeTosRestoreTaskDetail API to query the details of a backup restoration task for an RDS for SQL Server instance.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span>`Example value: DescribeTosRestoreTaskDetail`

The action to perform. The value is `DescribeTosRestoreTaskDetail`.



**Version ** <span data-label="purple">string   </span>`Example value: 2022-01-01`

The API version. The value is `2022-01-01`.



**ProjectName ** <span data-label="purple">string </span>`Optional. Example value: default`

Project name.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are using a sub\-user account, you must pass this parameter for authentication. Otherwise, the API call will fail. The primary account has all permissions by default, so this parameter is not required.</div>




**RestoreTaskId ** <span data-label="purple">string   </span>`Example value: 490`

Restore task ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describetosrestoretasks">DescribeTosRestoreTasks</a> API to view the restore task ID.</div>




**PageNumber ** <span data-label="purple">integer </span>`Optional. Example value: 1`

The query offset of the current page. The minimum value is 1, the maximum is 2147483647, and the default value is 1.



**PageSize ** <span data-label="purple">integer </span>`Optional. Example value: 10`

Number of records per page. The minimum value is 1, the maximum is 1,000, and the default value is 10.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section describes only the response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Total ** <span data-label="purple">integer </span>`Example value: 1`

Total number of recovery tasks.



**RestoreTaskDetails ** <span data-label="purple">object[] </span>`Example value: RestoreTaskDetailObject`

Details of restore tasks.


**RestoreFileName ** <span data-label="purple">string </span>`Example value: copyonly_log.bak`

Restore file name.



**RestoreFileSize ** <span data-label="purple">string </span>`Example value: 202394112`

Size of the restored file in bytes.



**RestoreStartTime ** <span data-label="purple">string </span>`Example value: 2023-05-11T02:55:38.000Z`

The recovery start time in yyyy\-MM\-ddTHH:mm:sssZ (UTC) format.



**RestoreEndTime ** <span data-label="purple">string </span>`Example value: 2023-05-11T02:55:44.000Z`

Recovery end time. Format: yyyy\-MM\-ddTHH:mm:sssZ (UTC time).



**DBName ** <span data-label="purple">string </span>`Example value: testdb`

Database name.



**RestoreDesc ** <span data-label="purple">string </span>`Example value: Restore success`

Recovery details.



**BackupType ** <span data-label="purple">string </span>`Example value: LOG`

Recovery type. The values are as follows:


* `Full`: Full recovery.

* `Diff`: Differential recovery.

* `LOG`: Log recovery.



**NewDBName ** <span data-label="purple">string </span>`Example value: newtestdb`

The new database name after modification.




<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeTosRestoreTaskDetail&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "RestoreTaskId":"90",
    "PageNumber": 1,
    "PageSize": 1
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230824112349490DFCBD85F41E00CAAD",
        "Action": "DescribeTosRestoreTaskDetail",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "RestoreTaskDetails": [
            {
                "BackupType": "Log",
                "DBName": "testdb",
                "RestoreDesc": "恢复成功",
                "RestoreEndTime": "2023-05-11T02:55:44.000Z",
                "RestoreFileName": "copyonly_log.bak",
                "RestoreFileSize": "202394112",
                "RestoreStartTime": "2023-05-11T02:55:38.000Z"
            }
        ],
        "Total": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the error codes related to the API and business logic. For common error codes, see the [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to existing running import jobs. |This operation can not be performed because a data import task is running on the current instance. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The number of manual backups exceeds the limit. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to exist running backup job. |This operation cannot be performed while the current instance is running a backup task. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |Operation unsupported. |
|400 |InstanceIsNotRunning |The specified instance is not running. |The instance is not running. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |This operation is not supported for incremental backups. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |The {parameter1} parameter is missing. |
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |Database validation failed: {parameter1}. |
|400 |InvalidParameter |The specified parameter %s is not valid. |The value for parameter {parameter1} is invalid. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |The number of databases to restore exceeds the quota limit. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |The current availability zone has insufficient resources. |
|404 |BackupNotFound |The specified instance does not exist available backup records. |No available backup records were found. |
|404 |InstanceNotFound |The specified instance does not exist. |The specified instance was not found. |
|500 |InternalError |The request has failed with internal server error. |Internal error. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are running. Please try again later. |
