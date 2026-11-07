---
title: "DescribeDBInstanceParameters - Query instance parameters"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstanceparameters"
---

Call the DescribeDBInstanceParameters API to query instance parameters.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this API and some common parameters are listed below. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span>`Example value: DescribeDBInstanceParameters`

The action to perform. The value is `DescribeDBInstanceParameters`.



**Version ** <span data-label="purple">string   </span>`Example value: 2022-01-01`

The API version. The value is `2022-01-01`.



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-dab1be87****`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the instance ID.</div>




**ParameterNames ** <span data-label="purple">string </span>`Optional Example value: Agent XPs`

Parameter name.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Fuzzy search is supported. If this parameter is not specified, all parameters for the instance are returned.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, refer to [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-dab1be87****`

Instance ID.



**DBEngine ** <span data-label="purple">string </span>`Example value: Sqlserver`

Database type. The only supported value for the database type is `Sqlserver`.



**DBEngineVersion ** <span data-label="purple">string </span>`Example value: SQLServer_2019_Std`

Compatible version. The values are as follows:


* `SQLServer_2019_Std`: Indicates SQL Server 2019 Standard Edition.

* `SQLServer_2019_Web`: Indicates SQL Server 2019 Web Edition.

* `SQLServer_2019_Ent`: Indicates SQL Server 2019 Enterprise Edition.



**ParameterCount ** <span data-label="purple">integer </span>`Example value: 1`

Parameter count.



**InstanceParameters ** <span data-label="purple">object[] </span>`Example value: [ { "CheckingCode": "[0~1]", "ForceModify": false, "ForceRestart": false, "ParameterDefaultValue": "1", "ParameterDescription": "The Agent XPs option.` `This option enables the SQL Server Agent extended stored procedures on this server.` `If this option is disabled, the SQL Server Agent node is not displayed in the SQL Server Management Studio Object Explorer.` `", "ParameterName": "Agent XPs", "ParameterType": "Integer", "ParameterValue": "1" } ]`

The list of parameters currently running on the instance. For more details about InstanceParameters, see [Data Structure](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure#instanceparametersobject).


**CheckingCode ** <span data-label="purple">string </span>`Example value: [10-3000]`

Parameter value range.



**ParameterDefaultValue ** <span data-label="purple">string </span>`Example value: 1`

The default value for the parameter in the parameter template used by the instance.



**ParameterName ** <span data-label="purple">string </span>`Example value: automatic soft-NUMA disabled`

Parameter name.



**ParameterValue ** <span data-label="purple">string </span>`Example value: 1`

Indicates the value of the parameter.



**ForceModify ** <span data-label="purple">boolean </span>`Example value: false`

Indicates whether the running value of the parameter can be modified.


* `true`: The running value of the parameter can be modified.

* `false`: The running value of the parameter cannot be modified.



**ForceRestart ** <span data-label="purple">boolean </span>`Example value: false`

Indicates whether the instance must be restarted for the modified parameter to take effect.


* `true`: Indicates that the instance must be restarted for the modified parameter to take effect.

* `false`: Indicates that the instance does not need to be restarted.



**ParameterDescription ** <span data-label="purple">string </span>`Example value: Database Mail XPs option.` `The Database Mail XPs option enables database mail on this server.`

Parameter description.



**ParameterType ** <span data-label="purple">string </span>`Example value: Integer`

The parameter type. The value can be:


* `String`

* `Integer`

* `Boolean`

* `List`

* `Float`




<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeDBInstanceParameters&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mssql-dab1be87****",
    "ParameterNames": "Agent XPs"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230131204425AB5D9AC0AB56989E8790",
        "Action": "DescribeDBInstanceParameters",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "DBEngine": "Sqlserver",
        "DBEngineVersion": "SQLServer_2019_Std",
        "InstanceId": "mssql-dab1be87****",
        "InstanceParameters": [
            {
                "CheckingCode": "[0~1]",
                "ForceModify": false,
                "ForceRestart": false,
                "ParameterDefaultValue": "1",
                "ParameterDescription": "代理XP选项。使用Agent XPs 选项可以启用此服务器上的 SQL Server 代理扩展存储过程。如果禁用此选项，则SQL Server Management Studio对象资源管理器将不显示 SQL Server 代理节点。",
                "ParameterName": "Agent XPs",
                "ParameterType": "Integer",
                "ParameterValue": "1"
            }
        ],
        "ParameterCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business logic\-related error codes for this API. For common error codes, see the [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to exist running import job. |This action can not be performed while the current instance is importing data. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The maximum number of manual backups has been reached. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to exist running backup job. |This operation cannot be performed because the instance is currently running a backup task. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |Operation not supported. |
|400 |InstanceIsNotRunning |The specified instance is not running. |The current instance is not running. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |This operation can not be performed on an incremental backup. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |The {parameter1} parameter is missing. |
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |DB validation failed due to {parameter1}. |
|400 |InvalidParameter |The specified parameter %s is not valid. |The value for parameter {parameter1} is invalid. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |The quota for database restores has been exceeded. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |Insufficient resources in the current availability zone. |
|404 |BackupNotFound |The specified instance does not exist available backup records. |No available backup records found. |
|404 |InstanceNotFound |The specified instance does not exist. |Instance not found. |
|500 |InternalError |The request failed with internal server error. |Internal error. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are running. Please try again later. |
