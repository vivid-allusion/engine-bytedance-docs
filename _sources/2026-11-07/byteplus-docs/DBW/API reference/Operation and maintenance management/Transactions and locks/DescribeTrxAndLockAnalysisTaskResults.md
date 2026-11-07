---
title: "DescribeTrxAndLockAnalysisTaskResults"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/describetrxandlockanalysistaskresults"
---

Call the DescribeTrxAndLockAnalysisTaskResults API to query the transaction and lock analysis results that match the query conditions.

## Precautions

This API is only applicable to RDS for MySQL, NDB for MySQL, and RDS for PostgreSQL instances.

## Request type

Synchronous request

## Request parameters

|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String |Yes |mysql\-0e08f1\*\*\*\*\*\* |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API to query the instance ID of NDB for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?_vtm_=a106466.b106468.0_0.0_0.0.2109_7610615829733918244&lang=en) API to query the instance ID of RDS for PostgreSQL. |
|DSType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL<br><br>* `Postgres`: RDS for PostgreSQL. |
|DiagnosisType |String |Yes |TrxAndLock |Transaction and lock analysis task type. Valid values:<br><br><br>* `TrxAndLock`: transaction and lock analysis.<br><br>* `Deadlock`: deadlock analysis.<br><br>* `LockWait`: lock wait analysis.<br><br><br>> **tip**<br><br><br>> When `DSType` is set to `Postgres`, viewing deadlock information is not supported, that is, the value `Deadlock`.<br> |
|DiagnosisTime |Integer |Yes |1788192000000 |Generation time of the transaction and lock analysis task, in milliseconds. |
|RegionId |String |Yes |cn\-beijing |Region ID. |
|NodeId |String |No |mysql\-0e08f1\*\*\*\*\*\*\-mbebd\-0 |Database instance node ID. If not specified, transaction and lock information on the primary node of the instance is queried by default. |
|PageNumber |Integer |No |1 |Page number. The value range is 1 to 1,000, with a default of 1. |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1000, with a default of 10. |

## Response parameters

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of transaction and lock analysis tasks. |
|TrxAndLockList |Array of [TrxAndLock](https://docs.byteplus.com/en/docs/DBW/data-structure?TagIDs=2&lang=en#KjdKNfXu) |```JSON```<br>```[```<br>```    {```<br>```        "BlockTrxId": "",```<br>```        "LockList": [```<br>```            {```<br>```                "LockAssociateIndex": "PRIMARY",```<br>```                "LockAssociateTable": "`dbw`.`dbw_trx_lock_case_11vxsb1f`",```<br>```                "LockId": "54420786:3227:3:2",```<br>```                "LockModel": "X",```<br>```                "LockProperty": "",```<br>```                "LockType": "RECORD",```<br>```                "TrxId": "54420786"```<br>```            }```<br>```        ],```<br>```        "Lockstatus": "LockHold",```<br>```        "NodeId": "mysql-1f02b3******-s3c9a-0",```<br>```        "ProcessId": "17276255",```<br>```        "SnapshotTime": 1792392468939,```<br>```        "SqlBlocked": "",```<br>```        "TrxExecTime": 18,```<br>```        "TrxId": "54420786",```<br>```        "TrxIsoLevel": "READ COMMITTED",```<br>```        "TrxRowsLocked": 1,```<br>```        "TrxRowsModified": 1,```<br>```        "TrxStartTime": "2026-10-19 14:47:30",```<br>```        "TrxTablesLocked": 1,```<br>```        "TrxWaitStartTime": "",```<br>```        "Trxstatus": "RUNNING"```<br>```    }```<br>```]```<br> |Details list of the transaction and lock analysis task results, returned when `DiagnosisType` is set to `TrxAndLock`.<br><br> |
|DeadlockList |Array of [DeadlockInfo](https://docs.byteplus.com/en/docs/DBW/data-structure?TagIDs=2&lang=en#xqPI3GFT) |```JSON```<br>```[```<br>```    {```<br>```        "DeadlockCollectionTime": "1792395718554",```<br>```        "DeadlockList": [```<br>```            {```<br>```                "HoldLock": "",```<br>```                "HoldLockIndex": "",```<br>```                "HoldLockMode": "",```<br>```                "ProcessId": "17295451",```<br>```                "RelateTable": "`dbw`.`dbw_lw_dl_z1m2iaz4`",```<br>```                "ReqType": "Update",```<br>```                "Sql": "/* DBW CONSOLE psm=dbw.bytecloud*******",```<br>```                "TrxInfo": "1",```<br>```                "TrxTreat": "",```<br>```                "WaitIndex": "PRIMARY",```<br>```                "WaitLock": "RECORD LOCKS",```<br>```                "WaitLockMode": "X"```<br>```            }```<br>```        ],```<br>```        "DeadlockTime": "2026-10-19 15:41:49",```<br>```        "NodeId": "mysql-1f02b3******-s3c9a-0"```<br>```    }```<br>```]```<br> |Details list of deadlock analysis task results, returned when `DiagnosisType` is set to `Deadlock`. |
|LockWaitList |Array of [DescribeLockCurrentWaitsDetail](https://docs.byteplus.com/en/docs/DBW/data-structure?TagIDs=2&lang=en#Cc61N3e5) |```JSON```<br>```[```<br>```    {```<br>```        "BBlockingQuery": "",```<br>```        "BTrxId": "54433842",```<br>```        "BTrxMysqlThreadId": "17314083",```<br>```        "BTrxOperationState": "",```<br>```        "BTrxRowsLocked": "1",```<br>```        "BTrxRowsModified": "1",```<br>```        "BTrxStarted": "2026-10-19T16:34:28+08:00",```<br>```        "BTrxState": "RUNNING",```<br>```        "BTrxWaitStarted": "",```<br>```        "CollectTime": "1792398886952",```<br>```        "NodeId": "mysql-1f02b3******-s3c9a-0",```<br>```        "RBlockedWaitSecs": "12",```<br>```        "RTrxId": "54433861",```<br>```        "RTrxMysqlThreadId": "17314155",```<br>```        "RTrxOperationState": "starting index read",```<br>```        "RTrxRowsLocked": "1",```<br>```        "RTrxRowsModified": "0",```<br>```        "RTrxStarted": "2026-10-19T16:34:34+08:00",```<br>```        "RTrxState": "LOCK WAIT",```<br>```        "RTrxWaitStarted": "2026-10-19T16:34:34+08:00",```<br>```        "RWaitingQuery": "/* DBW CONSOLE psm=dbw.bytecloud.connection */ UPDATE dbw_lw_dl_hxk91pyq SET lock_value = lock_value + 100 WHERE id = 3"```<br>```    }```<br>```]```<br> |Details of the lock wait analysis task results, returned when `DiagnosisType` is set to `LockWait`. |

## Example

**Transaction and lock information example**

### Request example

```JSON
POST https://dbw.volcengineapi.com/?Action=DescribeTrxAndLockAnalysisTaskResults&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
    "InstanceId": "mysql-1f02b3******",
    "DSType": "MySQL",
    "PageNumber": 1,
    "PageSize": 10,
    "DiagnosisType": "TrxAndLock",
    "DiagnosisTime": 1792392468939,
    "NodeId": "mysql-1f02b3******-s3c9a-0",
    "RegionId": "cn-beijing"
}
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026101915411884DD94EACCF92C777EC3-ecbebf",
        "Action": "DescribeTrxAndLockAnalysisTaskResults",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "DeadlockList": null,
        "LockWaitList": null,
        "Total": 1,
        "TrxAndLockList": [
            {
                "BlockTrxId": "",
                "LockList": [
                    {
                        "LockAssociateIndex": "PRIMARY",
                        "LockAssociateTable": "`dbw`.`dbw_trx_lock_case_11vxsb1f`",
                        "LockId": "54420786:3227:3:2",
                        "LockModel": "X",
                        "LockProperty": "",
                        "LockType": "RECORD",
                        "TrxId": "54420786"
                    }
                ],
                "Lockstatus": "LockHold",
                "NodeId": "mysql-1f02b3******-s3c9a-0",
                "ProcessId": "17276255",
                "SnapshotTime": 1792392468939,
                "SqlBlocked": "",
                "TrxExecTime": 18,
                "TrxId": "54420786",
                "TrxIsoLevel": "READ COMMITTED",
                "TrxRowsLocked": 1,
                "TrxRowsModified": 1,
                "TrxStartTime": "2026-10-19 14:47:30",
                "TrxTablesLocked": 1,
                "TrxWaitStartTime": "",
                "Trxstatus": "RUNNING"
            }
        ]
    }
}
```

**Deadlock example**

### Request example

```JSON
POST https://dbw.volcengineapi.com/?Action=DescribeTrxAndLockAnalysisTaskResults&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
    "InstanceId": "mysql-1f02b3******",
    "DSType": "MySQL",
    "NodeId": "mysql-1f02b3******-s3c9a-0",
    "RegionId": "cn-beijing",
    "DiagnosisType": "Deadlock",
    "DiagnosisTime": 1792456943406
}
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20261019161049AF702D23812A8575175F-88bf1a",
        "Action": "DescribeTrxAndLockAnalysisTaskResults",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "DeadlockList": [
            {
                "DeadlockCollectionTime": "1792395718554",
                "DeadlockList": [
                    {
                        "HoldLock": "",
                        "HoldLockIndex": "",
                        "HoldLockMode": "",
                        "ProcessId": "17295451",
                        "RelateTable": "`dbw`.`dbw_lw_dl_z1m2iaz4`",
                        "ReqType": "Update",
                        "Sql": "/* DBW CONSOLE psm=dbw.bytecloud*******",
                        "TrxInfo": "1",
                        "TrxTreat": "",
                        "WaitIndex": "PRIMARY",
                        "WaitLock": "RECORD LOCKS",
                        "WaitLockMode": "X"
                    }
                ],
                "DeadlockTime": "2026-10-19 15:41:49",
                "NodeId": "mysql-1f02b3******-s3c9a-0"
            }
        ],
        "LockWaitList": null,
        "Total": 1,
        "TrxAndLockList": null
    }
}
```

**Lock wait example**

### Request example

```JSON
POST https://dbw.volcengineapi.com/?Action=DescribeTrxAndLockAnalysisTaskResults&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
    "InstanceId": "mysql-1f02b3******",
    "DSType": "MySQL",
    "PageNumber": 1,
    "PageSize": 10,
    "DiagnosisType": "LockWait",
    "DiagnosisTime": 1792456963999,
    "NodeId": "mysql-1f02b3******-s3c9a-0",
    "RegionId": "cn-beijing"
}
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202610191744079641822A62E5C878384C-694c32",
        "Action": "DescribeTrxAndLockAnalysisTaskResults",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "DeadlockList": null,
        "LockWaitList": [
            {
                "BBlockingQuery": "",
                "BTrxId": "54433842",
                "BTrxMysqlThreadId": "17314083",
                "BTrxOperationState": "",
                "BTrxRowsLocked": "1",
                "BTrxRowsModified": "1",
                "BTrxStarted": "2026-10-19T16:34:28+08:00",
                "BTrxState": "RUNNING",
                "BTrxWaitStarted": "",
                "CollectTime": "1792398886952",
                "NodeId": "mysql-1f02b3******-s3c9a-0",
                "RBlockedWaitSecs": "12",
                "RTrxId": "54433861",
                "RTrxMysqlThreadId": "17314155",
                "RTrxOperationState": "starting index read",
                "RTrxRowsLocked": "1",
                "RTrxRowsModified": "0",
                "RTrxStarted": "2026-10-19T16:34:34+08:00",
                "RTrxState": "LOCK WAIT",
                "RTrxWaitStarted": "2026-10-19T16:34:34+08:00",
                "RWaitingQuery": "/* DBW CONSOLE psm=dbw.bytecloud.connection */ UPDATE dbw_lw_dl_hxk91pyq SET lock_value = lock_value + 100 WHERE id = 3"
            }
        ],
        "Total": 1,
        "TrxAndLockList": null
    }
}
```

## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes?lang=en).
