---
title: "CreateTosRestore - Create a task to migrate a TOS backup to the cloud"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createtosrestore"
---

Call the CreateTosRestore API to restore backup files from Object Storage Service (TOS) to an RDS for SQL Server instance, migrating data to the cloud.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section lists only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span>`Example value: CreateTosRestore`

The action to perform. Value: `CreateTosRestore`.



**Version ** <span data-label="purple">string </span>`Example value: 2022-01-01`

The API version. The value is `2022-01-01`.



**TargetDBInstanceId ** <span data-label="purple">string   </span>`Example value: mssql-d59138f3****`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the instance ID.</div>




**TosObjectPositions ** <span data-label="purple">string   </span>`Example value: tos-cn-beijing.volces.com:backname:slow_query.log`

The TOS object address. The format is `<TOS Endpoint Address>:<TOS Bucket Name>:<TOS backup file name>`, separated by colons (:).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The supported formats for backup files on TOS are <code>.bak</code>, <code>.diff</code>, <code>.trn</code>, and <code>.log</code>.</div>




**Databases ** <span data-label="purple">object[] </span>`Optional. Example value: None`

Database information to restore.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Restore up to 20 databases at a time.</div>



**DBName ** <span data-label="purple">string   </span>`Example value: test`

Original database name.



**NewDBName ** <span data-label="purple">string </span>`Optional. Example value: test_bak`

The new name for the database. Naming rules are as follows:


* Start with a letter and end with a letter or number.

* The length must be between 2 and 60 characters.

* Consists of letters, numbers, and underscores (_), and is case\-insensitive.

* You can not use reserved words, such as master, msdb, model, tempdb, resource, rdsadmin, and distribution.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When calling the CreateTosRestore API to create a TOS backup recovery task, note the following information:</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is not configured, the original database name is used by default.</div>


* <div data-tips="true" data-tips-type="tip">When this parameter is set and BackupType is Full, the new database name cannot be the same as an existing database name. If BackupType is Diff or LOG, the new database name must already exist.</div>





**RestoreType ** <span data-label="purple">string </span>`Optional. Example value: FULL`

The type of restore task. The valid values are as follows:


* `FULL`: Full recovery (default value).

* `DIFF`: Differential recovery.

* `LOG`: Log recovery.



**IsOnline ** <span data-label="purple">boolean </span>`Optional. Example value: true`

Specifies whether to bring the restored database online for access. The valid values are as follows:


* `true`: Brings the restored database online.

* `false`: Does not bring the restored database online (Default value).



**IsReplace ** <span data-label="purple">boolean </span>`Optional. Example value: true`

Indicates whether to overwrite existing databases on the target instance during a restore. Currently, only the value `false` is supported, which means that existing databases on the target instance will not be overwritten.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section lists only the response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RestoreTaskId ** <span data-label="purple">string </span>`Example value: 490`

Restore task ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=CreateTosRestore&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "TargetDBInstanceId":"mssql-1be522b5****",
    "TosObjectPositions":"tos-cn-beijing.volces.com:huahua:slow_query.log",
    "Databases":[
        {
        "DBName":"123",
        "NewDBName":"testname"
    }]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230823153339243D5B69711EB66B4DEF",
        "Action": "CreateTosRestore",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "RestoreTaskId": "490"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the error codes related to the API's business logic. For common error codes, see the [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to existing running import jobs. |This action can not be performed because the current instance is running a data import task. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The number of manual backups exceeds the limit. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to existing running backup jobs. |This action can not be performed because the current instance is running a backup task. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |The action is not supported. |
|400 |InstanceIsNotRunning |The specified instance is not running. |The instance is not running. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |This action cannot be performed for incremental backups. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |The {parameter1} parameter is missing. |
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |DB verification failed: {parameter1}. |
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of parameter {parameter1} is invalid. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |The database restoration quota has been exceeded. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |Insufficient resources in the current availability zone. |
|404 |BackupNotFound |The specified instance does not exist available backup records. |No available backup records found. |
|404 |InstanceNotFound |The specified instance does not exist. |Instance not found. |
|500 |InternalError |The request failed with internal server error. |Internal error. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are currently running. Try submitting again later. |
