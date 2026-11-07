---
title: "DescribeAvailableCrossRegion - Query destination regions for cross-regional backups."
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describeavailablecrossregion"
---

Call the DescribeAvailableCrossRegion API to view destination regions for cross\-regional backups.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this API and some common parameters are listed below. For more information, refer to [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span>`Example value: DescribeAvailableCrossRegion`

The action to be performed. The value is `DescribeAvailableCrossRegion`.



**Version ** <span data-label="purple">string </span>`Example value: 2022-01-01`

API version. The value is `2022-01-01`.



**RegionId ** <span data-label="purple">string </span>`Optional. Example value: cn-guangzhou`

The Region ID of the source instance.



**InstanceId ** <span data-label="purple">string </span>`Optional. Example value: mssql-37e2cc******`

Instance ID. If this parameter is specified, you can query the regions available for the cross\-regional backup of the instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the instance ID.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, refer to [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Regions ** <span data-label="purple">string[] </span>`Example value: [ "cn-beijing", "cn-shanghai" ]`

A list of destination regions for cross\-regional backups.



<span id=".6ZSZ6K-v56CB"></span>
## Request example

```JSON
POST /?Action=DescribeAvailableCrossRegion&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "InstanceId": "mssql-37e2cc******",
    "RegionId": "cn-guangzhou"
}
```


<span id="6rOtasrV"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20250513113943F4910389BFFB1DE92398-f7184b",
        "Action": "DescribeAvailableCrossRegion",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Regions": [
            "cn-beijing",
            "cn-shanghai"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

You can visit [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information on error codes.
