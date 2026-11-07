---
title: "DeleteDBInstance - Delete instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deletedbinstance"
---

Call the DeleteDBInstance API to delete an instance.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this API and some common parameters are listed below. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span>`Example value: DeleteDBInstance`

The action to perform. Set the value to DeleteDBInstance.



**Version ** <span data-label="purple">string   </span>`Example value: 2022-01-01`

API version. The value is 2022\-01\-01.



**InstanceId ** <span data-label="purple">string   </span>`Example value: mssql-dab1be87****`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the instance ID.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".6ZSZ6K-v56CB"></span>
## Request example

```JSON
POST /?Action=DeleteDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "InstanceId": "mssql-37e2cc******"
}
```


<span id="5mqFr8Bh"></span>
## Response example

```JSON

{
    "ResponseMetadata": {
        "RequestId": "202409121945533F5BF46BC9700311825D-35381b",
        "Action": "DeleteDBInstance",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business error codes for this API. For common error codes, see the [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of parameter {parameter1} is invalid. |
