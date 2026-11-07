---
title: "DescribeFullSQLFingerprintExample"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeFullSQLFingerprintExample"
---

Call the DescribeFullSQLFingerprintExample operation to query full SQL detail samples based on SQL fingerprints.

<span id="BgAsRK1y"></span>
## Request type

Synchronous request

<span id="kdUrNJxq"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|FollowInstanceID |String |Yes |mysql\-fcfc2c\*\*\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances?lang=en">DescribeDBInstances</a> API to query the instance ID of veDB MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for PostgreSQL.</div><br> |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL. |
|StartTime |Integer |Yes |1719820800 |Query start time, using second\-level timestamps. |
|EndTime |Integer |Yes |1719824400 |The end time of the query, in the format of a second\-level timestamp.<br><br>The end time must be later than the start time. |
|RegionId |String |Yes |cn\-beijing |Region ID. |
|SearchParam |[FullSQLSearchParam](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#searchparam) |No |```JSON```<br>```{```<br>```    "DisplaySqlTemplate": true,```<br>```    "SqlFingerprints": [```<br>```        "17c76a2458cb3cca182d8247f43f7333"```<br>```    ]```<br>```}```<br> |Query filter criteria.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">It is recommended to pass this parameter. Otherwise, the API will not return data based on fingerprints.</div><br><br><br> |


<span id="DnuTUp9Q"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DescribeFullSQLDetailRows |Array of [DescribeFullSQLDetailRow](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#MJyim8S9) |```JSON```<br>```[```<br>```    {```<br>```        "BinlogSyncTime": 0,```<br>```        "BytesSent": 0,```<br>```        "CclWaitTime": 0,```<br>```        "ClientIp": "172.30.116.80",```<br>```        "ClientPort": "60778",```<br>```        "ComponentType": "",```<br>```        "CpuTime": 0,```<br>```        "DBName": "test_a",```<br>```        "EndTimestamp": "1787566212356016",```<br>```        "ExecErrorMsg": "",```<br>```        "ExecErrorNo": "",```<br>```        "ExecTime": 73,```<br>```        "GroupFollowerWaitTime": 0,```<br>```        "GroupIds": "",```<br>```        "InnodbIOReadBytes": 0,```<br>```        "InnodbIOReads": 0,```<br>```        "InnodbIoWait": 0,```<br>```        "InnodbPageAccess": 0,```<br>```        "IsBroadcast": false,```<br>```        "IsCollectSqlFingerprint": false,```<br>```        "LatchWaitTime": 0,```<br>```        "LockTime": 0,```<br>```        "LogId": "",```<br>```        "LogLevel": "Normal",```<br>```        "LogType": "-",```<br>```        "MaxMem": 0,```<br>```        "MdlWaitTime": 0,```<br>```        "NodeId": "mysql-cf8d83******-sb2e3-0",```<br>```        "ProcessId": "",```<br>```        "ProxyTraceID": "",```<br>```        "QueryString": "",```<br>```        "QueryTruncated": "false",```<br>```        "RdbBlockCacheHitCount": 0,```<br>```        "RdbBlockDecompressTime": 0,```<br>```        "RdbBlockReadByte": 0,```<br>```        "RdbBlockReadCount": 0,```<br>```        "RdbBlockReadTime": 0,```<br>```        "RdbFindNextUserEntryTime": 0,```<br>```        "RdbInternalKeySkipCount": 0,```<br>```        "RdbInternalRecentSkipCount": 0,```<br>```        "RdbLockWaitTime": 0,```<br>```        "RdbNewTableBlockIterTime": 0,```<br>```        "RdbSeekInternalTime": 0,```<br>```        "RdbTrxId": "",```<br>```        "RecordId": "5fc409b1-cdc8-4ac9-964a-d484df056587",```<br>```        "RedoLogFlushTime": 0,```<br>```        "RequestSize": 0,```<br>```        "RowAffected": 0,```<br>```        "RowlockWaitTime": 0,```<br>```        "RowsExamined": 0,```<br>```        "RowsSent": 0,```<br>```        "SemiSyncWaitTime": 0,```<br>```        "ServerCommand": "Connect",```<br>```        "ServerExecs": "",```<br>```        "ServerPort": "0",```<br>```        "SessionID": "662029",```<br>```        "ShardID": "",```<br>```        "ShardIds": "",```<br>```        "SocketSendTime": 28,```<br>```        "SqlFingerprint": "connect",```<br>```        "SqlTable": "-",```<br>```        "SqlTemplate": "",```<br>```        "SqlType": "Connect",```<br>```        "StartTimestamp": "1787566212355943",```<br>```        "TablelockWaitTime": 0,```<br>```        "TcCommitTime": 0,```<br>```        "TcFlushTime": 0,```<br>```        "ThreadSchedTime": 0,```<br>```        "ThreadWaitTime": 16,```<br>```        "TmpDiskTables": 0,```<br>```        "TraceID": "0",```<br>```        "TrxCommitTime": 0,```<br>```        "TrxId": "0",```<br>```        "UserName": "test-a",```<br>```        "UserPsm": "",```<br>```        "Version": "4",```<br>```        "WaitLockTime": 0,```<br>```        "WarningNum": 0```<br>```    }```<br>```]```<br> |A list of full SQL detail samples corresponding to the SQL fingerprint. A maximum of one sample is returned for each fingerprint.<br><br> |


<span id="VXy4iSMg"></span>
## Request example

```JSON
POST /?Action=DescribeFullSQLFingerprintExample&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "FollowInstanceID": "mysql-cf8d83******",
    "InstanceType": "MySQL",
    "StartTime": 1787562620,
    "EndTime": 1787566220,
    "SearchParam": {
        "DisplaySqlTemplate": true,
        "SqlFingerprints": [
            "connect"
        ]
    },
    "RegionId": "cn-beijing"
}
```


<span id="fbjUfth7"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026082418112882C3F79E243440D87217-7c6e18",
        "Action": "DescribeFullSQLFingerprintExample",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "DescribeFullSQLDetailRows": [
            {
                "BinlogSyncTime": 0,
                "BytesSent": 0,
                "CclWaitTime": 0,
                "ClientIp": "172.30.116.80",
                "ClientPort": "60778",
                "ComponentType": "",
                "CpuTime": 0,
                "DBName": "test_a",
                "EndTimestamp": "1787566212356016",
                "ExecErrorMsg": "",
                "ExecErrorNo": "",
                "ExecTime": 73,
                "GroupFollowerWaitTime": 0,
                "GroupIds": "",
                "InnodbIOReadBytes": 0,
                "InnodbIOReads": 0,
                "InnodbIoWait": 0,
                "InnodbPageAccess": 0,
                "IsBroadcast": false,
                "IsCollectSqlFingerprint": false,
                "LatchWaitTime": 0,
                "LockTime": 0,
                "LogId": "",
                "LogLevel": "Normal",
                "LogType": "-",
                "MaxMem": 0,
                "MdlWaitTime": 0,
                "NodeId": "mysql-cf8d83******-sb2e3-0",
                "ProcessId": "",
                "ProxyTraceID": "",
                "QueryString": "",
                "QueryTruncated": "false",
                "RdbBlockCacheHitCount": 0,
                "RdbBlockDecompressTime": 0,
                "RdbBlockReadByte": 0,
                "RdbBlockReadCount": 0,
                "RdbBlockReadTime": 0,
                "RdbFindNextUserEntryTime": 0,
                "RdbInternalKeySkipCount": 0,
                "RdbInternalRecentSkipCount": 0,
                "RdbLockWaitTime": 0,
                "RdbNewTableBlockIterTime": 0,
                "RdbSeekInternalTime": 0,
                "RdbTrxId": "",
                "RecordId": "5fc409b1-cdc8-4ac9-964a-d484df056587",
                "RedoLogFlushTime": 0,
                "RequestSize": 0,
                "RowAffected": 0,
                "RowlockWaitTime": 0,
                "RowsExamined": 0,
                "RowsSent": 0,
                "SemiSyncWaitTime": 0,
                "ServerCommand": "Connect",
                "ServerExecs": "",
                "ServerPort": "0",
                "SessionID": "662029",
                "ShardID": "",
                "ShardIds": "",
                "SocketSendTime": 28,
                "SqlFingerprint": "connect",
                "SqlTable": "-",
                "SqlTemplate": "",
                "SqlType": "Connect",
                "StartTimestamp": "1787566212355943",
                "TablelockWaitTime": 0,
                "TcCommitTime": 0,
                "TcFlushTime": 0,
                "ThreadSchedTime": 0,
                "ThreadWaitTime": 16,
                "TmpDiskTables": 0,
                "TraceID": "0",
                "TrxCommitTime": 0,
                "TrxId": "0",
                "UserName": "test-a",
                "UserPsm": "",
                "Version": "4",
                "WaitLockTime": 0,
                "WarningNum": 0
            }
        ]
    }
}
```


<span id="JSfb8J68"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
