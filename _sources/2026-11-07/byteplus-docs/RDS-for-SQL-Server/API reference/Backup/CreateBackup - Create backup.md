---
title: "CreateBackup - Create backup"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createbackup"
---

Call the CreateBackup API to create a backup set.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This topic describes only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span>`Example value: CreateBackup`

The action to perform. The value is `CreateBackup`.



**Version ** <span data-label="purple">string   </span>`Example value: 2022-01-01`

API version. The value is `2022-01-01`.



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-1be522b5****`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the instance ID.</div>




**BackupType** <span data-label="purple">string</span> `Optional. Example value: Full`

Backup type. Only full backup is supported. The value is `Full` (default value).



**BackupMeta ** <span data-label="purple">object[] </span>`Optional. Example value: BackupMetaObject`

The information of the backed up database.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this parameter is not set, an instance\-level backup is performed by default.</div>



**DBName ** <span data-label="purple">string </span>`Example value: dbname`

The database name of the backup.




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This topic describes only the response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-1be522b5****`

Instance ID.



**BackupId ** <span data-label="purple">string </span>`Example value: ca155ac99fcb4eed86617041bfe0****`

The backup task ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=CreateBackup&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "InstanceId":"mssql-1be522b5****",
    "BackupType":"Full",
    "BackupMeta":[{
        "DBName":"tets1"
    }]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230823161820C950B0CCB0F1175BFD5D",
        "Action": "CreateBackup",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupId": "2198ffde72d44d0ea9a5a465eb2e****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the error codes for this API and its business logic. For common error codes, see the [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to exist running import job. |The instance is currently importing data. This action can not be performed. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The number of manual backups has reached the limit. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to exist running backup job. |This action can not be performed because the instance is running a backup task. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |The operation is not supported. |
|400 |InstanceIsNotRunning |The specified instance is not running. |The current instance is not running. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |This operation does not support incremental backups. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |The {parameter1} parameter is missing. |
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |DB verification failed due to {parameter1}. |
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of parameter {parameter1} is invalid. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |The database restore exceeds the quota limit. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |Insufficient resources in the current availability zone. |
|404 |BackupNotFound |The specified instance does not exist available backup records. |No available backup records found. |
|404 |InstanceNotFound |The specified instance does not exist. |The instance was not found. |
|500 |InternalError |The request has failed with internal server error. |Internal error. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are being executed. Try again later. |
