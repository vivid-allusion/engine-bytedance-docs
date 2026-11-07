---
title: "AutoScale"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/AutoScale"
---

Call the AutoScale API to configure scaling rules.

<span id="TM6SbQJE"></span>
## Request type

Asynchronous request.

<span id="WinLmC14"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceType |String |Yes |Postgres |Database type. Currently, only `Postgres` is supported, which indicates RDS for PostgreSQL. |
|InstanceId |String |Yes |postgres\-5d1\*\*\*\*\*\*<br><br> |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance IDs of all RDS for PostgreSQL instances in the target region.</div><br> |
|InstanceName |String |Yes |test |Instance name. |
|RegionId |String |Yes |cn\-guangzhou |Region. |
|ObservationWindow |Integer |Yes |5 |Observation window. |
|Configs |Array of [RuleConfig](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#DESUz5I5) |Yes |```JSON```<br>```[```<br>```    {```<br>```        "Action": "Expand",```<br>```        "IsOpen": true,```<br>```        "ScalingLimit": "3000",```<br>```        "Threshold": 48```<br>```    }```<br>```]```<br> |Auto scaling rule list.<br><br> |
|Metric |String<br><br> |Yes |Disk<br><br> |Scaling indicator. Currently, only disk scaling out is supported, meaning this parameter is set to `Disk`. |


<span id="mYx8TuXc"></span>
## Response parameters

Null.

<span id="4Hy711oM"></span>
## Request example

```JSON
POST /?Action=AutoScale&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "InstanceId": "postgres-5d1******",
    "InstanceType": "Postgres",
    "InstanceName": "test",
    "RegionId": "cn-guangzhou",
    "ObservationWindow": 5,
    "Metric": "Disk",
    "Configs": [
        {
            "Action": "Expand",
            "IsOpen": true,
            "ScalingLimit": "3000",
            "Threshold": 48
        }
    ]
}
```


<span id="O3jHLVBP"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260825113937DAD8BD1919BA40DCD66D-c0d7bf",
        "Action": "AutoScale",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-guangzhou"
    },
    "Result": {}
}
```


<span id="AOl9Eox0"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
