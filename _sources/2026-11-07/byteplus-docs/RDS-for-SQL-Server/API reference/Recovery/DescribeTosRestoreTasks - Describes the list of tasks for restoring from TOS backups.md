---
title: "DescribeTosRestoreTasks - Describes the list of tasks for restoring from TOS backups"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describetosrestoretasks"
---

Describes the list of tasks for restoring instance backups.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this API and some common parameters are listed below. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span>`Example value: DescribeTosRestoreTasks`

The action to perform. The value is `DescribeTosRestoreTasks`.



**Version ** <span data-label="purple">string   </span>`Example value: 2022-01-01`

The API version. The value is `2022-01-01`.



**ProjectName ** <span data-label="purple">string </span>`Optional. Example value: default`

Project name.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Sub\-user accounts must include this parameter for authentication when calling the API. Otherwise, the API call will fail. Primary accounts have all permissions by default and do not need to include this parameter.</div>




**RestoreTaskIds ** <span data-label="purple">string[] </span>`Optional. Example value: [\"90\", \"100\", \"10\" ]`

Restore task ID. Separate multiple restore task IDs with a comma (,).



**PageNumber ** <span data-label="purple">integer </span>`Optional. Example value: 1`

The number of the page to return. The minimum value is 1, the maximum value is 2147483647, and the default value is 1.



**PageSize ** <span data-label="purple">integer </span>`Optional. Example value: 10`

Number of records per page. The minimum value is 1, the maximum is 1,000, and the default is 10.



**InstanceId ** <span data-label="purple">string </span>`Optional. Example value: mssql-bbe31c86****`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the instance ID.</div>




**InstanceName ** <span data-label="purple">string </span>`Optional Example value: testname`

Instance name.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the instance name.</div>




**QueryStartTime ** <span data-label="purple">string </span>`Optional Example value: 2023-08-25T01:03:00.000Z`

The start time of the task creation to query. Format: yyyy\-MM\-ddTHH:mm:ssZ (UTC time).



**QueryEndTime ** <span data-label="purple">string </span>`Optional. Example value: 2023-08-25T01:00:01.000Z`

The end of the time range for the task creation query. Format: yyyy\-MM\-ddTHH:mm:ssZ (UTC time).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The query end time must be later than the query start time.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Total ** <span data-label="purple">integer </span>`Example value: 1`

Total number of restore tasks



**RestoreTasks ** <span data-label="purple">object[] </span>`Example value: RestoreTaskObject`

Restore task list.


**RestoreTaskId ** <span data-label="purple">string </span>`Example value: 90`

Restore task ID.



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-bbe31c86****`

Instance ID.



**InstanceName ** <span data-label="purple">string </span>`Example value: testname`

Instance name.



**TaskStartTime ** <span data-label="purple">string </span>`Example value: 2023-08-22T09:51:00.000Z`

Task start time. Format: yyyy\-MM\-ddTHH:mm:sssZ (UTC).



**TaskEndTime ** <span data-label="purple">string </span>`Example value: 2023-08-22T09:50:45.000Z`

The end time of the task. The format is yyyy\-MM\-ddTHH:mm:sssZ (UTC time).



**TaskStatus ** <span data-label="purple">string </span>`Example value: Failed`

Task status. The possible values are as follows:


* `NoStart`: Indicates that the task is not started.

* `Running`: The task is running.

* `Success`: The task was successful.

* `Failed`: The task failed.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For failed restore tasks, some databases may have been successfully restored. You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describetosrestoretaskdetail">DescribeTosRestoreTaskDetail</a> interface for more details.</div>




**TaskType ** <span data-label="purple">string </span>`Example value: OpenDB`

Task type. The possible values are:


* `OpenDB`: Open the database.

* `NotOpenDB`: Do not open the database.



**RestoreType ** <span data-label="purple">string </span>`Example value: FULL`

Recovery type. The values are as follows:


* `Full`: Indicates full recovery.

* `Diff`: Indicates incremental recovery.

* `LOG`: Indicates log recovery.



**TaskDesc ** <span data-label="purple">string </span>`Example value: Restore file verification failed`

Task backup description.



**IsReplace ** <span data-label="purple">boolean </span>`Example value: false`

A value of `false` indicates that existing databases on the target instance are not overwritten during the restore.




<span id=".6ZSZ6K-v56CB"></span>
## Request example

```JSON
POST /?Action=DescribeTosRestoreTasks&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "InstanceId": "mssql-bbe31c86****",
    "InstanceName":"testname",
    "QueryStartTime":"2020-03-01T00:00Z",
    "QueryEndTime":"2024-03-01T12:00Z",
    "PageNumber": 1,
    "PageSize":100
}
```


<span id="Nn0ftMn9"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230823114957F13CF2FFF8431E8E50FC",
        "Action": "DescribeTosRestoreTasks",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "RestoreTasks": [
            {
                "InstanceId": "mssql-bbe31c86****",
                "InstanceName": "testname",
                "IsReplace": false,
                "RestoreTaskId": "90",
                "RestoreType": "FULL",
                "TaskDesc": "备份文件校验失败",
                "TaskEndTime": "2023-08-22T09:51:00.000Z",
                "TaskStartTime": "2023-08-22T09:50:45.000Z",
                "TaskStatus": "Failed",
                "TaskType": "OpenDB"
            }
        ],
        "Total": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the error codes related to the business logic of this API. For common error codes, see the [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to existing running import jobs. |This action cannot be performed because a data import task is in progress. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The number of manual backups has exceeded the limit. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to running backup jobs. |This operation cannot be performed because the instance is running a backup task. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |Operation not supported. |
|400 |InstanceIsNotRunning |The specified instance is not running. |The current instance is not in the Running state. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |Incremental backups do not support this operation. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |Missing the {parameter1} parameter. |
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |Database validation failed: {parameter1}. |
|400 |InvalidParameter |The specified parameter %s is not valid. |Invalid value for parameter {parameter1}. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |The database restore exceeds the quota limit. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |Insufficient resources in the current availability zone. |
|404 |BackupNotFound |The specified instance does not exist available backup records. |No available backup records were found. |
|404 |InstanceNotFound |The specified instance does not exist. |The instance was not found. |
|500 |InternalError |The request failed with internal server error. |Internal error. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are running. Try again later. |
