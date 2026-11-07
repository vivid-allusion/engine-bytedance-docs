---
title: "DescribeSQLExecItemMetric"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeSQLExecItemMetric"
---

Call the DescribeSQLExecItemMetric API to query the metric curve of a single execution indicator for a specific SQL fingerprint within a specified time range.

<span id="DrKB1fvQ"></span>
## Request type

Synchronous request

<span id="gbKfxbqw"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-cf8d83\*\*\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances?lang=en">DescribeDBInstances</a> API to query the instance ID of veDB MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for PostgreSQL.</div><br> |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL. |
|StartTime |Integer |Yes |1719820800 |Query start time, using second\-level timestamps. |
|EndTime |Integer |Yes |1719824400 |The end time of the query, in the format of a second\-level timestamp. |
|ItemType |String |Yes |ExecTime |The type of metric to be queried. The values are as follows:<br><br><br>* `count`: The number of SQL executions.<br><br>* `ExecTime`: The SQL execution duration.<br><br>* `RowsAffected`: The number of affected rows.<br><br>* `RowsSent`: The number of returned rows. |
|RegionId |String |Yes |cn\-beijing |Region ID. |
|SqlFingerprint |String |Yes |a1b2c3d4 |SQL fingerprint |
|NodeId |String |No |node\-a |The filter condition for node IDs. If this parameter is specified, the results are aggregated by node. |
|DbName |String |No |order_db |The filter condition for database names. |


<span id="cUslnQRZ"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DataPoints |Array of [DataPoint](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#JQfxpFO8) |```JSON```<br>```[```<br>```    {```<br>```        "Abnormal": 0,```<br>```        "TimeStamp": 1787541550,```<br>```        "Value": 0```<br>```    },```<br>```    {```<br>```        "Abnormal": 0,```<br>```        "TimeStamp": 1787627086,```<br>```        "Value": 2```<br>```    }```<br>```]```<br> |List of metric curve data points. |


<span id="uWTrP7MD"></span>
## Request example

```JSON
POST /?Action=DescribeSQLExecItemMetric&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "InstanceId": "mysql-cf8d83******",
    "InstanceType": "MySQL",
    "StartTime": 1787541550,
    "EndTime": 1787627950,
    "SqlFingerprint": "9382a62734fc854f6c2df7431685bd75",
    "ItemType": "count",
    "DbName": "-",
    "RegionId": "cn-beijing"
}
```


<span id="b5xWAVcK"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260825111917371FF12D152EE64C2CB7-42b6db",
        "Action": "DescribeSQLExecItemMetric",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "DataPoints": [
            {
                "Abnormal": 0,
                "TimeStamp": 1787541550,
                "Value": 0
            },
            {
                "Abnormal": 0,
                "TimeStamp": 1787627086,
                "Value": 2
            }
        ]
    }
}
```


<span id="aljabboQ"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
