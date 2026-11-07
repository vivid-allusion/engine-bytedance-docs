---
title: "DeleteSqlConcurrencyControlRule"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DeleteSqlConcurrencyControlRule"
---

Call the DeleteSqlConcurrencyControlRule API to delete SQL throttling tasks.

<span id="vfxT0wBa"></span>
## Precautions

Supports deleting tasks with states of `ACTIVE`, `STOPPED`, `DONE`, `STOP_FAILED`, `DELETE_FAILED`, and others.

<span id="bTAAN9wC"></span>
## Request type

Synchronous request

<span id="yxXpA6zs"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String |Yes |mysql\-383906\*\*\*\*\*\* |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API to query the instance ID of NDB MySQL. |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL |
|RegionId |String |Yes |cn\-beijing |Region ID. |
|TaskId |Array of string |Yes |["2108098738466619392"] |SQL throttling task ID list (currently only one task ID is supported).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DBW/DescribeSqlConcurrencyControlRules?lang=en">DescribeSqlConcurrencyControlRules</a> API to query the task IDs in the database instance.</div><br> |


<span id="FyWOSWLr"></span>
## Response parameters

Null

<span id="DH4alhWu"></span>
## Request example

```JSON
POST /?Action=DeleteSqlConcurrencyControlRule&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "InstanceId": "mysql-383906******",
    "InstanceType": "MySQL",
    "RegionId":"cn-beijing",
    "TaskId": [
        "2108098738466619392"
    ]
}
```


<span id="qvj5wtmU"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20261008163211EC33A4E9D37F5E17E3F1-2ed49b",
        "Action": "DeleteSqlConcurrencyControlRule",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {

    }
}
```


<span id="Efyph3Fm"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes?_vtm_=a106466.b106468.0_0.0_0.0.4527_7694130500017817107&lang=en).
