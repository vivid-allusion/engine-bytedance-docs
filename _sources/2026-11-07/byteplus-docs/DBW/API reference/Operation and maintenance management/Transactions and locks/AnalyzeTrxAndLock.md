---
title: "AnalyzeTrxAndLock"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/analyzetrxandlock"
---

Call the AnalyzeTrxAndLock API to create a transaction and lock analysis task.

## Precautions

This API is only applicable to RDS for MySQL, NDB for MySQL instances, and RDS for PostgreSQL.

## Request type

Synchronize type.

## Request parameters

|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String |Yes |mysql\-0e08f1\*\*\*\*\*\* |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API to query the NDB MySQL instance ID.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?_vtm_=a106466.b106468.0_0.0_0.0.2109_7610615829733918244&lang=en) API to query the instance ID of RDS for PostgreSQL. |
|DSType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL<br><br>* `Postgres`: RDS for PostgreSQL. |
|DiagnosisType<br><br> |String |Yes |TrxAndLock |Transaction and lock analysis task type. Valid values:<br><br><br>* `TrxAndLock`: Transaction and lock analysis.<br><br>* `Deadlock`: Deadlock analysis.<br><br>* `LockWait`: Lock wait analysis.<br><br><br>> **tip**<br><br><br>> When `DSType` is set to `Postgres`, deadlock information is not supported, meaning the value `Deadlock` is not available.<br> |
|RegionId |String |Yes |cn\-beijing |Region ID. |
|NodeId |String |No |mysql\-0e08f1\*\*\*\*\*\*\-mbebd\-0 |Database instance node ID. If not specified, the transaction and lock analysis task is created on the primary node of the instance by default. |

## Response parameters

|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DiagnosisTime |Integer |1792140054833 |Creation timestamp of the transaction and lock analysis task, in milliseconds. |

## Request example

```JSON
POST https://dbw.volcengineapi.com/?Action=AnalyzeTrxAndLock&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
    "InstanceId": "mysql-0e08f1******",
    "DSType": "MySQL",
    "DiagnosisType": "TrxAndLock",
    "NodeId": "mysql-0e08f1******-mbebd-0",
    "RegionId": "cn-beijing"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202610161640530EEAED8E8DF943018731-46b989",
        "Action": "AnalyzeTrxAndLock",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "DiagnosisTime": 1792140054833
    }
}
```

## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes?lang=en).
