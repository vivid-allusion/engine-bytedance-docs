---
title: "ModifyInstanceAdvancedFeatures - Modify instance advanced features"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifyInstanceadvancedfeatures"
---

Call the ModifyInstanceAdvancedFeatures API to modify an instance's advanced features.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

This API is released via an Allowlist. To use it, [submit a ticket](https://console.byteplus.com/workorder/create) to the SQL Server technical team for access.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can only adjust the maximum number of databases of instance.

* After a successful call to this API, the instance's log backup frequency will change from every 5 minutes to every 30 minutes.

* You can adjust advanced features for Single node edition instances, whose compatible versions are SQL Server 2019 Standard Edition, SQL Server 2022 Standard Edition, SQL Server 2019 Enterprise Edition, and SQL Server 2022 Enterprise Edition.

* When an instance with adjusted advanced features is restored to a new instance, the new instance does not inherit the advanced features.

* When an instance's specification is changed, its maximum number of databases is adjusted proportionally. For example:

   * Changing the instance specification from 16C to 2C changes the maximum number of creatable databases from 1200 to 100.

   * Changing the instance specification from 8C to 4C changes the maximum number of creatable databases from 600 to 300.

   * If the instance specification is changed from 4C to 16C, the maximum number of databases that can be created changes from 300 to 1200.

* When you downgrade an instance to a lower specification, only the maximum number of supported databases is adjusted. Your existing databases are retained.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyInstanceAdvancedFeatures&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=rds_mssql&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|mRy5Xe">必选</span> `Example value: ModifyInstanceAdvancedFeatures`

The action to perform. The value is `ModifyInstanceAdvancedFeatures`.



**Version** <span data-label="purple">string</span><span data-api-tag="require|3mIeEy">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|cylLm6">必选</span> `Example: mssql-300aab95****`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstancedetail">DescribeDBInstanceDetail</a> API to view the instance ID.</div>




**AdvancedFeatures ** <span data-label="purple">string </span><span data-api-tag="require|NRuSrn">必选</span> `Example value: {\"LimitDBNumber\": \"300\"} or {\\\"LimitDBNumber\\\": \\\"300\\\"}`

Modifies the maximum number of databases for the instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When calling the API via a POST request, you need to add escape characters for the parameters. The example format is: <code>{\\\"LimitDBNumber\\\": \\\"300\\\"}</code>.</div>


* <div data-tips="true" data-tips-type="tip">If you use the API Explorer tool to debug the API, you do not need to add escape characters. The example format is:<code>{"LimitDBNumber": "300"}</code>。</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section describes only the response parameters specific to this API. For more information, refer to [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-300aab95****`

Instance ID.



**AdvancedFeatures ** <span data-label="purple">string </span>`Example: {\\\"LimitDBNumber\\\": \\\"300\\\"}`

The maximum number of databases that can be created.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=ModifyInstanceAdvancedFeatures&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
  "InstanceId": "mssql-300aab95****",
  "AdvancedFeatures": "{\"LimitDBNumber\": \"300\"}"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202411141917386983DD621F94EA06C82B-f52e6b",
        "Action": "ModifyInstanceAdvancedFeatures",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "AdvancedFeatures": "{\"LimitDBNumber\": \"300\"}",
        "InstanceId": "mssql-300aab95****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business logic\-related error codes for this API. For public error codes, see the [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to existing running import jobs. |This operation can not be performed because a data import task is running on the current instance. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of Parameter {parameter1} is invalid. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |DB verification failed: {parameter1}. |
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |Missing the {parameter1} parameter. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |This operation can not be performed on an incremental backup. |
|400 |InstanceIsNotRunning |The specified instance is not running. |The instance is not Running. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |Operation not supported. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to running backup jobs. |This operation cannot be performed because the instance is currently running a backup task. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The maximum number of manual backups has been reached. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |The quota for database restores has been exceeded. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |The current availability zone has insufficient resources. |
|404 |BackupNotFound |The specified instance does not have available backup records. |No available backup records found. |
|404 |InstanceNotFound |The specified instance does not exist. |Instance not found. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are currently running. Try submitting again later. |
|500 |InternalError |The request failed with internal server error. |Internal error. |
