---
title: "DescribeAvailabilityZones - Query availability zones"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describeavailabilityzones"
---

Call the DescribeAvailabilityZones API to query availability zones.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span>`Example value: DescribeAvailabilityZones`

The action to perform. Value: `DescribeAvailabilityZones`.



**Version ** <span data-label="purple">string   </span>`Example value: 2022-01-01`

The API version. The value is `2022-01-01`.



**RegionId ** <span data-label="purple">string </span>`Optional. Example: cn-beijing`

The region ID. Call the [DescribeRegions](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describeRegions) API to query it. If this parameter is empty, availability zones for all regions are returned.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section describes only the response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RegionId ** <span data-label="purple">string </span>`Example: cn-beijing`

Region ID.



**Zones ** <span data-label="purple">object[] </span>`Example value: { "Description": "North China 2 (Beijing) - Availability Zone A", "ZoneId": "cn-beijing-a", "ZoneName": "cn-beijing-a" }`

Availability zone list. For details about Zones, see [Data structure](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure#zonesobject).


**ZoneId ** <span data-label="purple">string </span>`Example value: cn-beijing-a`

Availability zone ID.



**ZoneName ** <span data-label="purple">string </span>`Example: cn-beijing-a`

Availability zone name.



**Description ** <span data-label="purple">string </span>`Example: Huabei 2 (Beijing)-Availability zone A`

The name of the region and availability zone.




<span id=".6ZSZ6K-v56CB"></span>
## Request example

```JSON
POST /?Action=DescribeAvailabilityZones&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "RegionId": "cn-beijing"
}
```


<span id=".6ZSZ6K-v56CB"></span>
## **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202301312006356ACDD9E7DF2F2F3B9D03",
        "Action": "DescribeAvailabilityZones",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "RegionId": "cn-beijing",
        "Zones": [
            {
                "Description": "华北2（北京）-可用区A",
                "ZoneId": "cn-beijing-a",
                "ZoneName": "cn-beijing-a"
            },
            { 
                    "Description": "华北2（北京）-可用区B", 
                    "ZoneId": "cn-beijing-b", 
                    "ZoneName": "cn-beijing-b" 
                        }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The table below lists the error codes related to this API and its business logic. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to exist running import job. |This action can not be performed while a data import task is in progress. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The number of manual backups exceeds the limit. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to exist running backup job. |This action cannot be performed while a backup task is in progress. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |Unsupported operation. |
|400 |InstanceIsNotRunning |The specified instance is not running. |The current instance is not running. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |This action is not supported for incremental backups. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |The {parameter1} parameter is missing. |
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |DB validation failed: {parameter1}. |
|400 |InvalidParameter |The specified parameter %s is not valid. |The value for parameter {parameter1} is invalid. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |The database restore quota has been exceeded. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |Insufficient resources in the current availability zone. |
|404 |BackupNotFound |The specified instance does not have available backup records. |No available backup records found. |
|404 |InstanceNotFound |The specified instance does not exist. |Instance not found. |
|500 |InternalError |The request has failed with internal server error. |Internal error. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are running. Try again later. |
