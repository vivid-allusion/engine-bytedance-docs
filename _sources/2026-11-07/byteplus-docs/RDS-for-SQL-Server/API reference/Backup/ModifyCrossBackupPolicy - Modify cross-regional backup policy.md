---
title: "ModifyCrossBackupPolicy - Modify cross-regional backup policy"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifycrossbackuppolicy"
---

Call the ModifyCrossBackupPolicy API to modify a cross\-regional backup policy.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section lists only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span>`Example value: ModifyCrossBackupPolicy`

The action to perform. The value is `ModifyCrossBackupPolicy`.



**Version ** <span data-label="purple">string   </span>`Example: 2022-01-01`

The API version. Value: `2022-01-01`.



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-1be522b5****`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the instance ID.</div>




**BackupEnabled ** <span data-label="purple">boolean </span>`Optional. Example value: true`

Specifies whether to enable cross\-regional backup. Valid values:


* `true`: Enables cross\-regional backup.

* `false`: (Default value) Disables cross\-regional backup.



**CrossBackupRegion ** <span data-label="purple">string </span>`Optional. Example: cn-shanghai`

The ID of the destination region for the cross\-regional backup.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required when <code>BackupEnabled</code> is set to <code>true</code>.</div>




**Retention ** <span data-label="purple">integer </span>`Optional. Example value: 14`

The number of days to retain the cross\-regional backup. The value ranges from `7 to 1825`. The default value is `7`.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section lists only the response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-1be522b5****`

Instance ID.



**BackupEnabled ** <span data-label="purple">boolean </span>`Example value: true`

Specifies whether to enable cross\-regional backup. Valid values:


* `true`: Enables cross\-regional backup.

* `false`: Disables cross\-regional backup.



**CrossBackupRegion ** <span data-label="purple">string </span>`Example value: cn-shanghai`

The ID of the destination region for the cross\-regional backup.



**Retention ** <span data-label="purple">integer </span>`Example value: 7`

Number of days to retain cross\-regional backups.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=ModifyCrossBackupPolicy&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "InstanceId": "mssql-04a911******",
    "BackupEnabled": true,
    "CrossBackupRegion": "cn-shanghai",
    "Retention": 14
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202505131134570CAA14043DFE7FEFD9D2-0b0eeb",
        "Action": "ModifyCrossBackupPolicy",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupEnabled": true,
        "CrossBackupRegion": "cn-shanghai",
        "InstanceId": "mssql-04a911******",
        "Retention": 14
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the error codes related to this API and its business logic. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of parameter {parameter1} is invalid. |
