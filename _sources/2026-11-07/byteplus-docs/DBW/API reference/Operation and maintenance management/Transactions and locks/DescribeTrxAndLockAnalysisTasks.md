---
title: "DescribeTrxAndLockAnalysisTasks"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/describetrxandlockanalysistasks"
---

Call the DescribeTrxAndLockAnalysisTasks API to query the transaction and lock analysis task list.

## Precautions

This API applies only to RDS for MySQL, NDB for MySQL instances, and RDS for PostgreSQL. Request type

Synchronous request

## Request parameters

|**Name** |**Type** |**Required** |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String |Yes |mysql\-0e08f1\*\*\*\*\*\* |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API to query the instance ID of NDB for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?_vtm_=a106466.b106468.0_0.0_0.0.2109_7610615829733918244&lang=en) API to query the instance ID of RDS for PostgreSQL. |
|DSType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL<br><br>* `Postgres`: RDS for PostgreSQL. |
|DiagnosisType<br><br> |String |Yes |TrxAndLock |Transaction and lock analysis task type. Valid values:<br><br><br>* `TrxAndLock`: Transaction and lock analysis.<br><br>* `Deadlock`: Deadlock analysis.<br><br>* `LockWait`: Lock wait analysis.<br><br><br>> **tip**<br><br><br>> When `DSType` is set to `Postgres`, deadlock information is not supported, meaning the value `Deadlock` is not available.<br> |
|StartTime |Integer |Yes |1788192000000 |Timestamp for creating the transaction and lock task query, in milliseconds. |
|EndTime |Integer |Yes |1788192100000 |Query the end timestamp of the transaction and lock task creation, in milliseconds.<br><br>> **tip**<br><br><br>> The end time must be later than the start time.<br> |
|RegionId |String |Yes |cn\-beijing |Region ID. |
|NodeId |String |No |mysql\-0e08f1\*\*\*\*\*\*\-mbebd\-0 |Database instance node ID. If not specified, transaction and lock information on the primary node of the instance is queried by default. |
|PageNumber |Integer |No |1 |Page number. The value range is 1 to 1,000, with a default of 1. |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1,000, with a default of 10. |

## Response parameters

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Total |Integer |100 |Total number of transaction and lock analysis tasks. |
|Tasks |Array of [TrxAndLockAnalysisTask](https://docs.byteplus.com/en/docs/DBW/data-structure?TagIDs=2&lang=en#1BJ4koCL) |```JSON```<br>```{```<br>```    "AnalyzedData": "information_schema.INNODB_TRX, information_schema.INNODB_LOCKS",```<br>```    "DSType": "MySQL",```<br>```    "DiagnosisTime": 1792140054833,```<br>```    "HasTrxAndLock": false,```<br>```    "InstanceId": "mysql-0e0******",```<br>```    "NodeId": "mysql-0e0******-mbebd-0",```<br>```    "Trigger": "Manual"```<br>```}```<br> |Transaction and lock analysis task details. |

## Request example

```JSON
POST https://dbw.volcengineapi.com/?Action=DescribeTrxAndLockAnalysisTasks&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
    "InstanceId": "mysql-0e0******",
    "DSType": "MySQL",
    "DiagnosisType": "TrxAndLock",
    "StartTime": 1792129255630,
    "EndTime": 1792140055630,
    "NodeId": "mysql-0e0******-mbebd-0",
    "RegionId": "cn-beijing",
    "PageNumber": 1,
    "PageSize": 10
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202610161640568D7E1C9401FF8E008138-5d25ec",
        "Action": "DescribeTrxAndLockAnalysisTasks",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "Tasks": [
            {
                "AnalyzedData": "information_schema.INNODB_TRX, information_schema.INNODB_LOCKS",
                "DSType": "MySQL",
                "DiagnosisTime": 1792140054833,
                "HasTrxAndLock": false,
                "InstanceId": "mysql-0e0******",
                "NodeId": "mysql-0e0******-mbebd-0",
                "Trigger": "Manual"
            }
        ],
        "Total": 1
    }
}
```

## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes?lang=en).
