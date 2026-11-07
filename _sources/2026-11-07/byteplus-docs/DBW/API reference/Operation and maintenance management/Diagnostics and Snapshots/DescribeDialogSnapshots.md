---
title: "DescribeDialogSnapshots"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeDialogSnapshots"
---

Call the DescribeDialogSnapshots API to query the list of session snapshot time points.

<span id="C05qMsKO"></span>
## Request type

Synchronous request

<span id="OQpd1ZM2"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String |Yes |mysql\-760f29\*\*\*\*\*\* |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API to query the instance ID of veDB MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?_vtm_=a106466.b106468.0_0.0_0.0.2109_7610615829733918244&lang=en) API to query the instance ID of RDS for PostgreSQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances?lang=en) API to query the instance ID of Document Database for MongoDB. |
|DSType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL.<br><br>* `Mongo`: Document Database for MongoDB. |
|StartTime |Integer |Yes |1782349200 |Start time of the query range, in seconds timestamp format. |
|EndTime |Integer |Yes |1782360000 |End time of the query range, in seconds timestamp format. |
|PageNumber |Integer |Yes |1 |Page number. |
|PageSize |Integer |Yes |20 |Page size. |
|NodeId |String |No |mysql\-bf120f\*\*\*\*\*\* |Database instance node ID. |


<span id="YUMUrw5O"></span>
## Response parameters


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Total |Integer |100 |Total number of session snapshot time points. |
|DialogSnapshots |Array of [DialogSnapshot](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#JOguEEdy)<br><br> |```JSON```<br>```[```<br>```    {```<br>```        "SnapshotTime": 1782465540```<br>```    }```<br>```]```<br> |List of session snapshot time points. |


<span id="9rpKvWt1"></span>
## Request example

```JSON
POST /?Action=DescribeDialogSnapshots&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "InstanceId":"mysql-760f29******",
    "DSType":"MySQL",
    "StartTime":1782292712,
    "EndTime":1782465562,
    "PageNumber":1,
    "PageSize":10
}
```


<span id="EXsOb0RX"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260626172703384330B840DB8F792B58-280d93",
        "Action": "DescribeDialogSnapshots",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "DialogSnapshots": [
            {
                "SnapshotTime": 1782465540
            },
            {
                "SnapshotTime": 1782465510
            },
            {
                "SnapshotTime": 1782465480
            },
            {
                "SnapshotTime": 1782465450
            },
            {
                "SnapshotTime": 1782465420
            },
            {
                "SnapshotTime": 1782465390
            },
            {
                "SnapshotTime": 1782465360
            },
            {
                "SnapshotTime": 1782465330
            },
            {
                "SnapshotTime": 1782465300
            },
            {
                "SnapshotTime": 1782465270
            }
        ],
        "Total": 2966
    }
}
```


<span id="yyq5lZWv"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
