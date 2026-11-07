---
title: "DescribeCrossBackupPolicy - Query a cross-regional backup policy"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describecrossbackuppolicy"
---

Call the DescribeCrossBackupPolicy API to view the cross\-regional backup policy.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section lists only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span>`Example value: DescribeCrossBackupPolicy`

The action to perform. The value is `DescribeCrossBackupPolicy`.



**Version ** <span data-label="purple">string</span>`Example value: 2022-01-01`

The API version. The value is `2022-01-01`.



**InstanceId ** <span data-label="purple">string   </span>`Example value: mssql-37e2cc******`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the instance ID.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section lists only the response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-37e2cc******`

Instance ID.



**BackupEnabled ** <span data-label="purple">boolean </span>`Example value: true`

Specifies whether to enable cross\-regional backup. Valid values:


* `true`: Enables cross\-regional backup.

* `false`: Disables cross\-regional backup.



**CrossBackupRegion ** <span data-label="purple">string </span>`Example value: cn-shanghai`

The destination region ID for the cross\-regional backup.



**Retention ** <span data-label="purple">integer </span>`Example value: 7`

Number of days to retain cross\-regional backups.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeCrossBackupPolicy&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "InstanceId": "mssql-37e2cc******"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20250513113941DC90D701D6B34F478849-129d82",
        "Action": "DescribeCrossBackupPolicy",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupEnabled": true,
        "CrossBackupRegion": "cn-shanghai",
        "InstanceId": "mssql-37e2cc******",
        "Retention": 14
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more information on error codes, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
