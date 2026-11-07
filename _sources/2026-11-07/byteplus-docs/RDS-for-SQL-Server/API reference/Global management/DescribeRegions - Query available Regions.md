---
title: "DescribeRegions - Query available Regions"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describeRegions"
---

Call the DescribeRegionsAPI to query the Regions supported by RDS for SQL Server.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section lists only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span>`Example: DescribeRegions`

The action to perform. Value: `DescribeRegions`.



**Version ** <span data-label="purple">string </span>`Example value: 2022-01-01`

The API version. The value is `2022-01-01`.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section lists only the response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Regions ** <span data-label="purple">object[] </span>`Example value: { "RegionId": "cn-beijing", "RegionName": "cn-beijing" }`

Region list.


**RegionId ** <span data-label="purple">string </span>`Example value: cn-beijing`

Region ID.



**RegionName ** <span data-label="purple">string </span>`Example value: North China 2 (Beijing)`

Region name.




<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeRegions&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023013120291925D91FEED8ABBC247808",
        "Action": "DescribeRegions",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Regions": [
            {
                "RegionId": "cn-beijing",
                "RegionName": "cn-beijing"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the error codes related to the business logic of this API. For common error codes, see the [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) Document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InstanceIsNotRunning |The specified instance is not running. |The instance is not running. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|400 |InvalidParameter |The specified parameter %s is not valid. |Invalid value for parameter {parameter1}. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |Database validation failed due to {parameter1}. |
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |The {parameter1} parameter is missing. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |This action is not supported for incremental backups. |
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to exist running import job. |This operation cannot be performed while the instance is importing data. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |Operation not supported. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to exist running backup job. |This action cannot be performed because the instance is currently running a backup task. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The number of manual backups has exceeded the limit. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |Insufficient resources in the current availability zone. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |The database restore quota has been exceeded. |
|404 |InstanceNotFound |The specified instance does not exist. |The instance is not found. |
|404 |BackupNotFound |The specified instance does not exist available backup records. |No available backup records found. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are running. Try again later. |
|500 |InternalError |The request failed due to an internal server error. |Internal error. |
