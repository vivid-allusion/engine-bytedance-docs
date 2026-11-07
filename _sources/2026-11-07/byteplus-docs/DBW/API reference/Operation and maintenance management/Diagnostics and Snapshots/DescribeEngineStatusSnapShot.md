---
title: "DescribeEngineStatusSnapShot"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeEngineStatusSnapShot"
---

Call the DescribeEngineStatusSnapShot API to query session snapshot engine status details.

<span id="Hc8iV9Rd"></span>
## Request type

Synchronous request

<span id="rx1OIatP"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String<br><br> |Yes |mysql\-c\*\*\*\*\*\* |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API to query the instance ID of veDB MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?_vtm_=a106466.b106468.0_0.0_0.0.2109_7610615829733918244&lang=en) API to query the instance ID of RDS for PostgreSQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances?lang=en) API to query the instance ID of Document Database for MongoDB. |
|DSType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL.<br><br>* `Mongo`: Document Database for MongoDB. |
|SnapshotTime |Integer |Yes |1782349500 |Session snapshot timestamp in seconds. |
|NodeId |String |Yes |mysql\-bf120f\*\*\*\*\*\* |Database instance node ID. |


<span id="J2o8n216"></span>
## Response parameters


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Type |String |InnoDB |Engine type. |
|Status |String |\n=====================================\n2026\-06\-25 16:02:48 140562380879616 INNODB MONITOR OUTPUT\n |Engine status details. |
|NodeId |String |mysql\-c28c25\*\*\*\*\*\*\-ma822\-0 |Database instance node ID. |


<span id="U0zWxljL"></span>
## Request example

```JSON
POST /?Action=DescribeEngineStatusSnapShot&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "DSType":"MySQL",
    "InstanceId":"mysql-c28c25******",
    "SnapshotTime":1782791281,
    "NodeId": "mysql-c28c25******-ma822-0"
}
```


<span id="oJ8veDn6"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202606301505382254CF3000D4BF35878A-2bfb68",
        "Action": "DescribeEngineStatusSnapShot",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "Name": "",
        "NodeId": "mysql-c28c25******-ma822-0",
        "Status": "\n=====================================\n2026-06-25 16:02:48 140562380879616 INNODB MONITOR OUTPUT\n",
        "Type": "InnoDB"
    }
}
```


<span id="ctn9COkS"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
