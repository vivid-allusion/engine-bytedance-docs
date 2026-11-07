---
title: "RestoreToExistedInstance - Restore to an existing instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/restoretoexistedinstance"
---

Call the RestoreToExistedInstance API to restore databases to an existing instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The following limitations apply to data recovery based on the compatible version of the instance:


* When the source instance is a Web edition (`DBEngineVersion`: `SQLServer_2019_Web`), it can be restored to an Enterprise, Standard, or Web edition instance (`DBEngineVersion`: `SQLServer_2019_Std`, `SQLServer_2019_Ent`, or `SQLServer_2019_Web`).

* When the source instance is a Standard edition (`DBEngineVersion`: `SQLServer_2019_Std`), it can be restored to an Enterprise or Standard edition instance (`DBEngineVersion`: `SQLServer_2019_Std` or `SQLServer_2019_Ent`).

* When the source instance is an Enterprise edition (`DBEngineVersion`: `SQLServer_2019_Ent`), it can be restored to an Enterprise edition instance (`DBEngineVersion`: `SQLServer_2019_Ent`).


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this API and some common parameters are listed below. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span>`Example value: RestoreToExistedInstance`

The action to perform. The value is RestoreToExistedInstance.



**Version ** <span data-label="purple">string   </span>`Example value: 2022-01-01`

API version. The value is 2022\-01\-01.



**SourceDBInstanceId ** <span data-label="purple">string </span>`Example value: mssql-bbe31c86****`

Source instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the instance ID.</div>




**TargetDBInstanceId ** <span data-label="purple">string </span>`Example value: mssql-bbe31c86****`

The target instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the instance ID.</div>


* <div data-tips="true" data-tips-type="tip">If this ID is the same as the source instance ID, the data is restored to the source instance.</div>




**Databases ** <span data-label="purple">object[] </span>`Example value: None`

Information on the databases to restore.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can specify up to 100 databases.</div>



**DBName ** <span data-label="purple">string   </span>`Example value: test`

Original database name.



**NewDBName ** <span data-label="purple">string </span>`Optional. Example: test_bak`

New database name. Naming rules are as follows:


* Start with a letter and end with a letter or digit.

* The length must be between 2 and 60 characters.

* Consists of letters, numbers, and underscores (_), and is case\-insensitive.

* Do not use reserved words such as master, msdb, model, tempdb, resource, rdsadmin, and distribution.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When creating a TOS backup recovery task with the CreateTosRestore API, note the following:</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is not configured, the original database name is used by default.</div>


* <div data-tips="true" data-tips-type="tip">When this parameter is set, the new database name can not be the same as an existing one if BackupType is Full, and it must already exist if BackupType is Diff or LOG.</div>





**BackupId ** <span data-label="purple">string </span>`Optional. Example value: f569f53bf60a48d5b****`

The backup set ID of the source instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When restoring a database from a backup set, you can obtain the <code>BackupId</code> by calling DescribeBackups.</div>


* <div data-tips="true" data-tips-type="tip">Provide either <code>BackupId</code> or <code>RestoreTime</code>.</div>




**RestoreTime ** <span data-label="purple">string </span>`Optional. Example: 2023-08-23T08:04:59Z`

Restore the database to a point in time. You can select any point in time within the backup retention period. Format: yyyy\-MM\-ddTHH:mm:ssZ (UTC time).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Provide either <code>BackupId</code> or <code>RestoreTime</code>.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters for this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId ** <span data-label="purple">string </span>`Example: mssql-1be522b5****`

Source instance ID.



<span id=".6K-35rGC56S65L6LLTE="></span>
## Request example 1

```JSON
POST /?Action=RestoreToExistedInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "SourceDBInstanceId":"mssql-1be522b5****",
    "TargetDBInstanceId":"mssql-1be522b5****",
    "RestoreTime":"2023-08-23T08:04:59Z",
    "Databases":[{
        "DBName":"tets1",
        "NewDBName":"tewy222"
    }]
}
```


<span id=".6L-U5Zue56S65L6LLTE="></span>
## Response example 1

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230823161248951129B6A9EC3C53ELLD",
        "Action": "RestoreToExistedInstance",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "mssql-1be522b5****"
    }
}
```


<span id=".6K-35rGC56S65L6LLTI="></span>
## Request example 2

```JSON
POST /?Action=RestoreToExistedInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.volcengineapi.com
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "SourceDBInstanceId":"mssql-1be522b5****",
    "TargetDBInstanceId":"mssql-1be522b5****",
    "BackupId": "94fe801db98d41848197266ecaecc878",
    "Databases":[{
        "DBName":"tets1",
        "NewDBName":"tjy3"
    }]
}
```


<span id=".6L-U5Zue56S65L6LLTI="></span>
## Response example 2

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023082316124895D97DB6A9EC3C53E9EC",
        "Action": "RestoreToExistedInstance",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "mssql-1be522b5****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The table below lists the error codes for this API's business logic. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to exist running import job. |This operation cannot be performed because the current instance is importing data. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The number of manual backups exceeded the limit. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to exist running backup job. |Cannot perform this operation while the instance is backing up. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |The operation is not supported. |
|400 |InstanceIsNotRunning |The specified instance is not running. |The instance is not running. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |Incremental backups do not support this operation. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |The {parameter1} parameter is missing. |
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |Database verification failed because {parameter1}. |
|400 |InvalidParameter |The specified parameter %s is not valid. |The value for parameter {parameter1} is invalid. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |The database restoration quota has been exceeded. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |The current availability zone has insufficient resources. |
|404 |BackupNotFound |The specified instance does not exist available backup records. |No available backup records found. |
|404 |InstanceNotFound |The specified instance does not exist. |The instance was not found. |
|500 |InternalError |The request has failed with internal server error. |Internal error. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are currently running. Try to submit again later. |
