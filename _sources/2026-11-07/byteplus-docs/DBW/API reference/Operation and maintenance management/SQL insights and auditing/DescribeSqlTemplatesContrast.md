---
title: "DescribeSqlTemplatesContrast"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeSqlTemplatesContrast"
---

Call the DescribeSqlTemplatesContrast API to query the aggregated indicator comparison of full SQL templates in two time periods.

<span id="2oMezzLr"></span>
## Request type

Synchronous request

<span id="8T4nQdwq"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-fcfc2c\*\*\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances?lang=en">DescribeDBInstances</a> API to query the instance ID of veDB MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for PostgreSQL.</div><br> |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL. |
|FirstStartTime |Integer |Yes |1719820800 |Start time of the second comparison period, using a first\-level timestamp. |
|FirstEndTime |Integer |Yes |1719824400 |The end time of the first comparison period, using a second\-level timestamp.<br><br>The end time must be later than the start time. |
|SecondStartTime |Integer |Yes |1719907200 |Start time of the second comparison period, using a second\-level timestamp. |
|SecondEndTime |Integer |Yes |1719910800 |The end time of the second comparison period, using a second\-level timestamp.<br><br>The end time must be later than the start time. |
|RegionId |String |Yes |cn\-beijing |Region ID. |
|DbName |String |No |order_db |The filter condition for database names. |
|SortBy |String |No |DESC |Sort direction. The values are as follows:<br><br><br>* `ASC`: ascending order.<br><br>* `DESC`: descending order. |
|OrderBy |String |No |ExecTime |Sort indicator. The values are as follows:<br><br><br>* `TotalExecTime`: The total SQL execution duration.<br><br>* `ExecTime`: Average Total SQL execution time.<br><br>* `Count`: Execution times.<br><br>* `TotalCpuTime`: Total CPU time.<br><br>* `CpuTime`: Average CPU time.<br><br>* `RowlockWaitTime`: The average InnoDB lock wait duration.<br><br>* `MdlWaitTime`: The average MDL lock wait duration.<br><br>* `LatchWaitTime`：平均 Latch 等待耗时。<br><br>* `TrxCommitTime`: The average transaction commit duration.<br><br>* `CclWaitTime`: Average SQL throttling wait time.<br><br>* `SocketSendTime`: Average socket send time.<br><br>* `ThreadSchedTime`: Average thread scheduling wait time.<br><br>* `ThreadWaitTime`: Average thread wait time.<br><br>* `RowsAffected`: Average rows affected.<br><br>* `RowsExamined`: Average rows scanned.<br><br>* `RowsSent`: Average rows returned.<br><br>* `BytesSent`: Average bytes sent.<br><br>* `InnodbPageAccess`: Average logical page reads.<br><br>* `InnodbIoReadBytes`: Average IO read bytes.<br><br>* `InnodbIoReads`: Average number of pages read by I/O.<br><br>* `TmpDiskTables`: Average number of disk temporary tables. |
|SqlMethods |Array of string |No |["SELECT","UPDATE"] |SQL type filter condition. Values include: `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `ALTER`, `CREATE`, `DROP`, `RENAME`, `TRUNCATE`, `OTHER`. |
|Tables |Array of string |No |["orders"] |Table name filter condition. |
|NodeId |String |No |node\-a |Node ID |
|CollectSqlFingerprint |Boolean |No |true |Whether to query only the favorited SQL templates. The values are as follows:<br><br><br>* `true`: Queries only the favorited SQL templates.<br><br>* `false`: Queries all data. |
|SqlCommands |Array of string |No |["SELECT"] |SQL command filter condition. |
|ExaminedRowDown |Integer |No |1,000 |Lower limit of rows scanned. Limits the maximum number of scanned rows in the returned results to prevent query timeout caused by excessive data volume. |
|CountDown |Integer |No |10 |Lower limit of execution times (or lower limit of record count). Used to limit the number of SQL records returned. |


<span id="BihbPBvr"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Details<br><br> |Array of [TemplatesContrast](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#CwgIdkxW)<br><br> |```JSON```<br>```[```<br>```    {```<br>```        "DbName": "test_a",```<br>```        "FirstTemplatesDetail": {```<br>```            "BinlogSyncTime": 0,```<br>```            "BytesSent": 0,```<br>```            "CclWaitTime": 0,```<br>```            "Count": 2,```<br>```            "CpuTime": 490,```<br>```            "DBName": "test_zhudi",```<br>```            "ExecTime": 794,```<br>```            "GroupFollowerWaitTime": 0,```<br>```            "InnodbIoReadBytes": 0,```<br>```            "InnodbIoReads": 0,```<br>```            "InnodbPageAccess": 16,```<br>```            "InstanceID": "mysql-cf8d83a2ea63",```<br>```            "IsCollectSqlFingerprint": false,```<br>```            "LatchWaitTime": 0,```<br>```            "MdlWaitTime": 0,```<br>```            "RedoLogFlushTime": 0,```<br>```            "RowlockWaitTime": 0,```<br>```            "RowsAffected": 0,```<br>```            "RowsExamined": 4,```<br>```            "RowsSent": 0,```<br>```            "SemiSyncWaitTime": 0,```<br>```            "ServerPort": "",```<br>```            "SocketSendTime": 0,```<br>```            "SqlFingerprint": "01c4dbcc021b24e3beff902d78115f5e",```<br>```            "SqlTable": "TABLES",```<br>```            "SqlTemplate": "SELECT `TABLE_NAME` FROM `information_schema`.`TABLES` WHERE `TABLE_SCHEMA`=? AND `TABLE_TYPE` IN (?+) LIMIT ?+",```<br>```            "SqlType": "SELECT",```<br>```            "TablelockWaitTime": 0,```<br>```            "TcCommitTime": 0,```<br>```            "TcFlushTime": 0,```<br>```            "TenantID": "2100067216",```<br>```            "ThreadSchedTime": 3,```<br>```            "ThreadWaitTime": 0,```<br>```            "TmpDiskTables": 0,```<br>```            "TotalCpuTime": 980,```<br>```            "TotalExecTime": 1588,```<br>```            "TrxCommitTime": 0,```<br>```            "WaitLockTime": 0```<br>```        },```<br>```        "SecondTemplatesDetail": {```<br>```            "BinlogSyncTime": 0,```<br>```            "BytesSent": 0,```<br>```            "CclWaitTime": 0,```<br>```            "Count": 14,```<br>```            "CpuTime": 0,```<br>```            "DBName": "test_zhudi",```<br>```            "ExecTime": 8,```<br>```            "GroupFollowerWaitTime": 0,```<br>```            "InnodbIoReadBytes": 0,```<br>```            "InnodbIoReads": 0,```<br>```            "InnodbPageAccess": 0,```<br>```            "InstanceID": "mysql-cf8d83a2ea63",```<br>```            "IsCollectSqlFingerprint": false,```<br>```            "LatchWaitTime": 0,```<br>```            "MdlWaitTime": 0,```<br>```            "RedoLogFlushTime": 0,```<br>```            "RowlockWaitTime": 0,```<br>```            "RowsAffected": 0,```<br>```            "RowsExamined": 0,```<br>```            "RowsSent": 0,```<br>```            "SemiSyncWaitTime": 0,```<br>```            "ServerPort": "",```<br>```            "SocketSendTime": 0,```<br>```            "SqlFingerprint": "quit",```<br>```            "SqlTable": "-",```<br>```            "SqlTemplate": "",```<br>```            "SqlType": "Quit",```<br>```            "TablelockWaitTime": 0,```<br>```            "TcCommitTime": 0,```<br>```            "TcFlushTime": 0,```<br>```            "TenantID": "2100067216",```<br>```            "ThreadSchedTime": 5,```<br>```            "ThreadWaitTime": 0,```<br>```            "TmpDiskTables": 0,```<br>```            "TotalCpuTime": 0,```<br>```            "TotalExecTime": 113,```<br>```            "TrxCommitTime": 0,```<br>```            "WaitLockTime": 0```<br>```        },```<br>```        "SqlFingerprint": "quit",```<br>```        "SqlType": "Quit",```<br>```        "TbName": "-"```<br>```    }```<br>```]```<br> |SQL template comparison details list. |
|Total |Integer |1 |Total number of comparison details. |


<span id="Ucl4lkDs"></span>
## Request example

```JSON
POST /?Action=DescribeSqlTemplatesContrast&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "InstanceId": "mysql-cf8d83a2ea63",
    "InstanceType": "MySQL",
    "FirstStartTime": 1787562620,
    "FirstEndTime": 1787566220,
    "SecondStartTime": 1787562620,
    "SecondEndTime": 1787566220,
    "SortBy": "DESC",
    "OrderBy": "ExecTime",
    "DbName": "test_a",
    "Tables": [
        "-",
        "example",
        "SCHEMATA",
        "TABLES",
        "KEY_COLUMN_USAGE",
        "REFERENTIAL_CONSTRAINTS",
        "tables"
    ],
    "NodeId": "mysql-cf8d83a2ea63-sb2e3-0",
    "SqlCommands": [
        "Connect",
        "SET_OPTION",
        "SELECT",
        "SHOW_FIELDS",
        "SHOW_KEYS",
        "SHOW_CREATE",
        "Quit",
        "CREATE_TABLE"
    ],
    "CollectSqlFingerprint": false,
    "RegionId": "cn-beijing"
}
```


<span id="tjN9kmDj"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026082418112882C3F79E243440D87214-15e625",
        "Action": "DescribeSqlTemplatesContrast",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "Details": [
            {
                "DbName": "test_a",
                "FirstTemplatesDetail": {
                    "BinlogSyncTime": 0,
                    "BytesSent": 0,
                    "CclWaitTime": 0,
                    "Count": 2,
                    "CpuTime": 490,
                    "DBName": "test_zhudi",
                    "ExecTime": 794,
                    "GroupFollowerWaitTime": 0,
                    "InnodbIoReadBytes": 0,
                    "InnodbIoReads": 0,
                    "InnodbPageAccess": 16,
                    "InstanceID": "mysql-cf8d83a2ea63",
                    "IsCollectSqlFingerprint": false,
                    "LatchWaitTime": 0,
                    "MdlWaitTime": 0,
                    "RedoLogFlushTime": 0,
                    "RowlockWaitTime": 0,
                    "RowsAffected": 0,
                    "RowsExamined": 4,
                    "RowsSent": 0,
                    "SemiSyncWaitTime": 0,
                    "ServerPort": "",
                    "SocketSendTime": 0,
                    "SqlFingerprint": "01c4dbcc021b24e3beff902d78115f5e",
                    "SqlTable": "TABLES",
                    "SqlTemplate": "SELECT `TABLE_NAME` FROM `information_schema`.`TABLES` WHERE `TABLE_SCHEMA`=? AND `TABLE_TYPE` IN (?+) LIMIT ?+",
                    "SqlType": "SELECT",
                    "TablelockWaitTime": 0,
                    "TcCommitTime": 0,
                    "TcFlushTime": 0,
                    "TenantID": "2100067216",
                    "ThreadSchedTime": 3,
                    "ThreadWaitTime": 0,
                    "TmpDiskTables": 0,
                    "TotalCpuTime": 980,
                    "TotalExecTime": 1588,
                    "TrxCommitTime": 0,
                    "WaitLockTime": 0
                },
                "SecondTemplatesDetail": {
                    "BinlogSyncTime": 0,
                    "BytesSent": 0,
                    "CclWaitTime": 0,
                    "Count": 14,
                    "CpuTime": 0,
                    "DBName": "test_zhudi",
                    "ExecTime": 8,
                    "GroupFollowerWaitTime": 0,
                    "InnodbIoReadBytes": 0,
                    "InnodbIoReads": 0,
                    "InnodbPageAccess": 0,
                    "InstanceID": "mysql-cf8d83a2ea63",
                    "IsCollectSqlFingerprint": false,
                    "LatchWaitTime": 0,
                    "MdlWaitTime": 0,
                    "RedoLogFlushTime": 0,
                    "RowlockWaitTime": 0,
                    "RowsAffected": 0,
                    "RowsExamined": 0,
                    "RowsSent": 0,
                    "SemiSyncWaitTime": 0,
                    "ServerPort": "",
                    "SocketSendTime": 0,
                    "SqlFingerprint": "quit",
                    "SqlTable": "-",
                    "SqlTemplate": "",
                    "SqlType": "Quit",
                    "TablelockWaitTime": 0,
                    "TcCommitTime": 0,
                    "TcFlushTime": 0,
                    "TenantID": "2100067216",
                    "ThreadSchedTime": 5,
                    "ThreadWaitTime": 0,
                    "TmpDiskTables": 0,
                    "TotalCpuTime": 0,
                    "TotalExecTime": 113,
                    "TrxCommitTime": 0,
                    "WaitLockTime": 0
                },
                "SqlFingerprint": "quit",
                "SqlType": "Quit",
                "TbName": "-"
            }
        ],
        "Total": 1
    }
}
```


<span id="Za3BrNcq"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
