---
title: "Data structure"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/data-structure"
---

This article summarizes the data structure definition details used in the API interface of Database Workshop (DBW).

## AggregateSlowLogs

Slow log aggregation information array. Referenced by the following interfaces:

* DescribeAggregateSlowLogs

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DB |String |test |Database name. |
|ExecuteCount |Integer |2 |Execution times |
|ExecuteCountRatio |Integer |66.67 |The percentage of total execution count. |
|FirstAppearTime |Integer |1702613263 |The time of the first occurrence, in seconds timestamp format. |
|LastAppearTime |Integer |1702613273 |The time of the last occurrence, in seconds timestamp format. |
|LockTimeRatio |Integer |0 |Percentage of total lock time. |
|LockTimeStats |LockTimeStatsObject |```json```<br>```{```<br>```  "Average": 0,```<br>```   "Max": 0,```<br>```   "Min": 0,```<br>```   "Total": 0```<br>```}```<br> |Statistics for lock duration in seconds. |
|PTAnalysisResult |String |```json```<br>```\n# Attribute     pct   total     min     max     avg\n#*******```<br> |Text string of the PT\-like parsing tool output result. |
|QueryTimeRatio |Integer |77.78 |Percentage of total query time. |
|QueryTimeStats |QueryTimeStatsObject |```json```<br>```{```<br>```  "Average": 3.5001745,```<br>```  "Max": 4.00016,```<br>```  "Min": 3.000189,```<br>```  "Total": 7.000349```<br>```}```<br> |Statistics for lock duration in seconds. |
|RowsExaminedRatio |Integer |0 |Percentage of total rows scanned. |
|RowsExaminedStats |RowsExaminedStatsObject |```json```<br>```{```<br>```"Average": 0,```<br>```"Max": 0,```<br>```"Min": 0,```<br>```"Total": 0```<br>```}```<br> |Statistical results of rows scanned. |
|RowsSentRatio |Integer |66.67 |Returns the percentage of total rows. |
|RowsSentStats |RowsSentStatsObject |```json```<br>```{```<br>```  "Average": 1,```<br>```  "Max": 1,```<br>```  "Min": 1,```<br>```  "Total": 2```<br>```}```<br> |Statistical results of the number of returned rows. |
|SQLTemplate |String |```json```<br>```select sleep(?)```<br> |SQL template |
|SQLTemplateID |String |eb4a2b85844fd80206871a75c065411778729031ded219d92281062e8473\*\*\*\*\*\*\* |Hash value of the Slow SQL template. |
|SourceIP |String |172.23.\*\*\*.\*\*\* |IP address. |
|User |String |test_user |Executor name |
|Table |String |testtable |Table name. |
|SqlMethod |String |SELECT |SQL type |
|SqlFingerprint |String |8c6976e5b5410415bde908bd4dee15df |SQL fingerprint |
|RowsAffectedRatio |Double |0 |Rows affected ratio. |
|RowsAffectedStats |Object of StatisticResult | <br><br>```JSON```<br>```{```<br>```  "max": 1250.0,```<br>```  "min": 1.0,```<br>```  "total": 28650.0,```<br>```  "average": 114.6```<br>```}```<br><br><br> |Statistical results of the number of affected rows. |

## AggregationSQLTemplateDetail

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SqlFingerprint |String |a1b2c3d4 |SQL fingerprint |
|SqlTemplate |String |select \* from orders where id = ? |SQL template |
|InstanceID |String |mysql\-76eda4\*\*\*\*\*\* |Instance ID. |
|TenantID |String |2105\*\*\*\*\*\* |Tenant ID. |
|DBName |String |order_db |Database name. |
|ExecTime |Integer |12.5 |average execution time. |
|CpuTime |Integer |3.2 |Average CPU time. |
|RowsExamined |Integer |1,000 |Average rows scanned. |
|RowsAffected |Integer |10 |Average number of affected rows. |
|RowsSent |Integer |20 |Average rows returned. |
|TotalExecTime |Integer |1250 |Total execution time. |
|Count |Integer |100 |Execution times |
|SqlTable |String |orders |Table name. |
|SqlType |String |SELECT |SQL type Values include: `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `ALTER`, `CREATE`, `DROP`, `RENAME`, `TRUNCATE`, `OTHER`. |
|IsCollectSqlFingerprint |Boolean |TRUE |Whether to collect SQL fingerprints. The values are as follows:<br><br><br>* `true`: Collects SQL fingerprints.<br><br>* `false`: Does not collect SQL fingerprints. |
|ServerPort |String |3306 |Service port. |
|BytesSent |Integer |1024 |Send bytes. |
|CclWaitTime |Integer |0 |SQL rate limiting wait time. |
|GroupFollowerWaitTime |Integer |0 |Copy the wait time from the node. |
|InnodbIoReadBytes |Integer |4096 |InnoDB IO read bytes. |
|InnodbIoReads |Integer |10 |The number of InnoDB I/O read pages. |
|InnodbPageAccess |Integer |150 |InnoDB logical page reads. |
|LatchWaitTime |Integer |0 |Latch wait time. |
|MdlWaitTime |Integer |0 |MDL lock wait time. |
|RedoLogFlushTime |Integer |2 |Redo Log Time Consumption. |
|RowlockWaitTime |Integer |0 |Row lock wait time. |
|SemiSyncWaitTime |Integer |0 |Semi\-synchronous replication wait duration |
|SocketSendTime |Integer |1 |Socket sending time. |
|TablelockWaitTime |Integer |0 |Table lock wait time. |
|TcCommitTime |Integer |3 |Transaction commit time. |
|TcFlushTime |Integer |1 |Transaction log flush duration. |
|ThreadSchedTime |Integer |5 |Thread scheduling wait duration. |
|ThreadWaitTime |Integer |0 |Thread wait time. |
|TmpDiskTables |Integer |0 |Number of disk temporary tables. |
|TotalCpuTime |Integer |50 |Total CPU time. |
|TrxCommitTime |Integer |3 |Transaction commit time. |
|WaitLockTime |Integer |0 |Lock wait total time. |

## AutoScaleSearchParam

|**Name** |**Type** |**Required** |**Sample** |**Description** |
|---|---|---|---|---|
|EventId |String |No |2092137580354129920 |Event ID. |
|Action |String<br><br> |No<br><br> |Expand |Scaling configuration. Valid values:<br><br><br>* `Scale out`: indicates scaling out.<br><br>* `Reduce`: indicates scaling in. |
|StartTime |Integer |No |1661222493 |Event start time. |
|EndTime |Integer |No |1661222493 |End time of the event. |
|EventStatus |String |No |EventScaling |Event state. The values are as follows:<br><br><br>* `EventUndo`: Indicates not executed.<br><br>* `EventScaling`: Indicates scaling out.<br><br>* `EventFinished`: Indicates completed.<br><br>* `EventError`: Indicates an error.<br><br>* `EventIgnore`: Indicates ignore. |

## AutoScaleEvent

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Action<br><br> |String |Expand |Scaling configuration. Valid values:<br><br><br>* `Scale out`: indicates scaling out.<br><br>* `Reduce`: indicates scaling in. |
|After |String |0G |General display value after scaling. |
|AfterAutoScale |Integer |0 |Value after scaling. |
|AutoScaleMetricName<br><br> |String<br><br> |Disk<br><br> |Scaling indicator. Currently, only disk scaling out is supported, meaning this parameter takes the value Disk. |
|Before |String |300G |General display value before scaling. |
|BeforeAutoScale |Integer |10 |Value before scaling. |
|EndTime |String |2026\-08\-24T21:21:43Z |End time. |
|EventId |String |2091984066520817664 |Event ID. |
|EventStatus<br><br> |String |EventScaling<br><br> |Event state. The values are as follows:<br><br><br>* `EventUndo`: Indicates not executed.<br><br>* `EventScaling`: Indicates scaling out.<br><br>* `EventFinished`: Indicates completed.<br><br>* `EventError`: Indicates an error.<br><br>* `EventIgnore`: Indicates ignore. |
|Memo |String |Test |Remarks. |
|MetricUnit |String | **%**  |Indicator unit. |
|RuleId |String |2031045967368716288 |Rule ID. |
|RuleType<br><br> |String |Auto<br><br> |Rule type. The values are as follows:<br><br><br>* `Auto`: Indicates an automatic rule.<br><br>* `Cron`: Indicates a scheduled rule. |
|StartTime |String |2026\-08\-24T20:20:43Z |Start time. |
|TriggerCondition |Array of [TriggerCondition](http://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#bcn2LLgm) |```JSON```<br>```[```<br>```    {```<br>```        "ComparisonOperator": "\u003e",```<br>```        "MetricName": "磁盘使用率",```<br>```        "Threshold": "90.00%",```<br>```        "TimeInfo": ""```<br>```    }```<br>```]```<br> |List of trigger conditions. |
|TriggerInfo |String |Insufficient resources. Scale out failed. |Error message. |
|TriggerValue |String |80% |Trigger value. |

## ApprovalNodes

Approval node information. Referenced by the following interfaces:

* ListApprovalNode

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ApprovalUsers |Object[] |```JSON```<br>```{```<br>```    "UserId": "",```<br>```    "UserName": ""```<br>```}```<br> |Node approver information, including the User ID and Username.<br><br> |
|CreateUser |String[] |```JSON```<br>```{```<br>```    "UserId": "",```<br>```    "UserName": ""```<br>```}```<br> |Node creator information, including user ID and username.<br><br> |
|Memo |String |Remarks of the approval node. |DBA |
|NodeId |String |Approval node ID. |0 |
|NodeName |String |Approval node name. |DBA |
|NodeType |String |Approval node type. The return values are as follows.<br><br><br>* `System`: System node.<br><br>* `Customize`: Custom node. |System |

## Array of ResList Object

Array of diagnosis history. Referenced by the following interfaces:

* SlowQueryAdviceTaskHistoryApi

|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Db |String |tpch |Database name. |
|Date |String |20250427 |Diagnosis date. Use the UTC+8 time zone, for example, 20250427. |
|Status |String |SUCCESS |Diagnostic task status. Include:<br><br><br>* `INIT`: Diagnosing.<br><br>* `SUCCESS`: Diagnosis was successfully.<br><br>* `EXCEPTION`: Diagnostic exception. |
|AdviceNum |Integer |0 |Number of SQL statements to be optimized<br><br>> **tip**<br><br><br>> The total number of SQL statements with index suggestions and SQL statements to be rewritten after deduplication, that is, the number of SQL statements to be optimized<br> |
|SummaryId |String |9853ae90\-4052\-4953\-b117\-b1f59035\*\*\*\* |The unique identifier for each diagnosis. |
|SlowQueryNum |Integer |0 |Total number of slow SQL diagnoses. |
|AdviceIndexNum |Integer |0 |Number of index suggestion SQLs. |
|NoAdviceSQLNum |Integer |142 |No suggested SQL queries. |
|AdviceRewriteNum |Integer |0 |Number of SQL statements to be rewritten. |

## Array of AdvicesByGroup Object

Array of diagnostic suggestions. Referenced by the following interfaces:

* ListSlowQueryAdviceApi

|**Name** |**Type** |Sample |**Description** |
|---|---|---|---|
|Advice |String |It is recommended that users optimize and adjust SQL according to business logic |Diagnostic suggestions aggregated according to recommendations.<br><br><br>* If the `AdviceType` in the request parameters is `index_advice`, this field is the index SQL.<br><br>* If the `AdviceType` in the request parameters is `rewrite_sql_advice`, this field is the SQL suggestion. |
|advices |Array of Object |[Array of advices Object](https://docs.byteplus.com/en/docs/64/24723#array-of-advices-object) |Diagnostic advice aggregated by module. If the aggregation type in the request parameter is `Module`, the response parameter is `Advices`. |

## Array of advices Object

Array of diagnosis module information. Referenced by the following interfaces:

* ListSlowQueryAdviceApi

|**Name** |**Type** |Sample |**Description** |
|---|---|---|---|
|DB |String |tpch |Database name. |
|agg |Object |[agg Object](https://docs.byteplus.com/en/docs/64/24723#agg-object) |Aggregate information. |
|Risk |String |None |Risk. |
|User |Array of String |sqlbrain |Username. |
|Advice |String |It is recommended that users optimize and adjust SQL according to business logic |Diagnostic suggestion<br><br><br>* If the `AdviceType` in the request parameters is `index_advice`, this field is the index SQL.<br><br>* If the `AdviceType` in the request parameters is `rewrite_sql_advice`, this field is the SQL suggestion. |
|Benefit |Double |0 |Estimated total time saved after optimization. |
|SpeedUp |Double |1 |Estimated performance improvement multiple after optimization. |
|SQLModule |String |SELECT `nation`,`o_year`,SUM(`amount`) AS `sum_profit` FROM (SELECT `n_name` AS `nation`,EXTRACT(YEAR FROM `o_orderdate`) AS `o_year`,`l_extendedprice` *(?\-* `*l_discount*` *)\-* `*ps_supplycost*l_quantity` AS `amount` FROM ((((((`part`) JOIN `supplier`) JOIN `lineitem`) JOIN `partsupp`) JOIN `orders`) JOIN `nation`) WHERE `s_suppkey`=`l_suppkey` AND `ps_suppkey`=`l_suppkey` AND `ps_partkey`=`l_partkey` AND `p_partkey`=`l_partkey` AND `o_orderkey`=`l_orderkey` AND `s_nationkey`=`n_nationkey` AND `p_name` LIKE ?) AS `profit` GROUP BY `nation`,`o_year` ORDER BY `nation`,`o_year` DESC |SQL template |
|SourceIPs |Array of String |100.65.\*\*.\*\* |Client address. |
|TableName |String |L |Table name. |
|AdviceLevel |String |Low |Optimize recommendation level. |
|AdviceIndexSize |Double |0 |Estimated size of recommended indexes. |
|QueryTimeAvgAfter |Double |33.352660417661085 |Estimated query time after optimization. |

## Agg Object

|**Name** |**Type** |Sample |**Description** |
|---|---|---|---|
|DB |String |tpch |Database name. |
|PSM |String |\- |Internal PSM. |
|User |String |sqlbrain |Username. |
|Table |String |lineitem,nation,orders,part,partsupp,supplier |Table name. |
|SourceIP |String |100.65.\*\*.\*\* |Client address. |
|SqlMethod |String |SELECT |SQL type |
|SQLTemplate |String |55c9cb442b6418e35b79ac8797ecde33b664768318f2ed997c13bfe8c5e\*\*\*\* |Slow SQL template. |
|ExecuteCount |Integer |419 |Execution times |
|LockTimeRatio |Double |0.03 |Percentage of total lock time. |
|LockTimeStats |Object |```json```<br>```{```<br>```"Max": 0.000013,```<br>```"Min": 0.000002,```<br>```"Total": 0.0017869999999999997,```<br>```"Average": 0.000004264916467780429```<br>```}```<br> |Statistics for lock duration in seconds. |
|RowsSentRatio |Double |0.04 |Returns the percentage of total rows. |
|RowsSentStats |Object |```json```<br>```{```<br>```"Max": 175,```<br>```"Min": 175,```<br>```"Total": 73325,```<br>```"Average": 175```<br>```}```<br> |Statistical results of the number of returned rows. |
|SQLTemplateID |String |55c9cb442b6418e35b79ac8797ecde33b664768318f2ed997c13bfe8c5e\*\*\*\* |Slow SQL template hash value. |
|LastAppearTime |Integer |1750982260 |The time of the last occurrence. |
|QueryTimeRatio |Double |15.12 |Percentage of total query time. |
|QueryTimeStats |Object |```json```<br>```{```<br>```"Max": 37.44366,```<br>```"Min": 30.146108,```<br>```"Total": 461.0285326293491,```<br>```"Average": 13974.764714999996```<br>```}```<br> |Statistics for query time consumption, in seconds. |
|SqlFingerprint |String |\-\- |SQL fingerprint |
|FirstAppearTime |Integer |1750809748 |Time of first appearance |
|PTAnalysisResult |String |# Attribute pct total min max avg # ============= === ======= ======= ======= ======= # Count 0 419 # Exec time 15 13974.76s 30.15s 37.44s 33.35s # Lock time 0 1.8ms 2.0us 13.0us 4.3us # Rows sent 0 73.33k 175 175 175.00 # Rows examined 2 412.05M 965.28k 1.00M 983.41k # String: # Databases tpch # # EXPLAIN / *!50100 PARTITIONS*/ SELECT `nation`,`o_year`,SUM(`amount`) AS `sum_profit` FROM (SELECT `n_name` AS `nation`,EXTRACT(YEAR FROM `o_orderdate`) AS `o_year`,`l_extendedprice` *(?\-* `*l_discount*` *)\-* `*ps_supplycost*l_quantity` AS `amount` FROM ((((((`part`) JOIN `supplier`) JOIN `lineitem`) JOIN `partsupp`) JOIN `orders`) JOIN `nation`) WHERE `s_suppkey`=`l_suppkey` AND `ps_suppkey`=`l_suppkey` AND `ps_partkey`=`l_partkey` AND `p_partkey`=`l_partkey` AND `o_orderkey`=`l_orderkey` AND `s_nationkey`=`n_nationkey` AND `p_name` LIKE ?) AS `profit` GROUP BY `nation`,`o_year` ORDER BY `nation`,`o_year` DESC\G |Text string of the PT\-like parsing tool output result. |
|ExecuteCountRatio |Double |0.03 |The percentage of total execution count. |
|RowsExaminedRatio |Double |1.77 |Percentage of total rows scanned. |
|RowsExaminedStats |Object |```json```<br>```{```<br>```"Max": 1003217,```<br>```"Min": 965281,```<br>```"Total": 412050589,```<br>```"Average": 983414.2935560859```<br>```}```<br> |Statistical results of rows scanned. |

## Column

Column information of the table.

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Name |String |name |Field Name. |
|Type |String |varchar |Field type. |
|Length |String |32 |Field length. |
|AllowBeNull |Bool |false |Whether the field allows NULL. |
|Comment |String |gender |Field comment. |
|IsPrimaryKey |Bool |false |Whether the field is a primary key. |
|IsAutoIncrement |Bool |false |Whether the field is auto\-increment. |
|DefaultValue |String |male |Field default value. |

## DatabaseInfo

Database information. Referenced by the following interfaces:

* ListDatabases

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Name |String |mysql |Database name. |
|CharacterSetName |String |utf8 |Database character set name. |
|CollationName |String |utf8_general_ci |Database sorting rule set. |
|IsSystemDB |Bool |false |Whether the database is a system database. |
|Description |String |Employee information table |Database description information. |

## DataPoint

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|TimeStamp |Integer |1787627086 |Data point time, using second\-level timestamps. |
|Value |Integer |2 |Indicator value. |
|Abnormal |Integer |0 |Whether it is marked as an anomaly. This API operation usually returns 0. |

## DbwUsers

Administrator information. Referenced by the following interfaces:

* DescribeManagedUsers

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|AccountType<br><br> |String<br><br> |CHILD |Account type. |
|GroupDetails |String[] |```JSON```<br>```{```<br>```                        "GroupId": "1962656497431244800",```<br>```                        "GroupName": "1111"```<br>```                    }```<br> |User group information, including user group ID and user group name. |

## DescribeAuditLogDetailRow

Parameter information of the audit log to be queried. Referenced by the following interfaces:

* DescribeAuditLogDetail

Database Workshop DBW provides two versions of database audit functionality: V1 and V2. You can select appropriate parameters based on the version of database audit.

|**Parameter** |**Type** |**Sample** |**Description** |**Supported database types** |
|---|---|---|---|---|
|User |String |root |Executor name |* MySQL（V1、V2）<br><br>* veDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* Redis<br><br>* MongoDB |
|DB |String |information_schema |Database name. |* MySQL（V1、V2）<br><br>* veDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* Redis<br><br>* MongoDB |
|SourceIP |String |127.0.0.1 |IP address. |* MySQL（V1、V2）<br><br>* veDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* Redis<br><br>* MongoDB |
|OriSql |String |Select \* from func; |Original SQL text.<br><br>> **tip**<br><br><br>> When multiple SQL statements need to be executed, use semicolons (;) to separate them.<br> |* MySQL（V1、V2）<br><br>* veDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* Redis<br><br>* MongoDB |
|AffectRow |Integer |0 |Rows affected. |* MySQL（V1、V2）<br><br>* veDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* Redis |
|ExecTime |Integer |0 |Execution start time, unit: second. |* MySQL（V1、V2）<br><br>* veDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* Redis<br><br>* MongoDB |
|Duration<br><br> |Integer |0 |Execution duration in microseconds. |* MySQL（V1、V2）<br><br>* veDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* Redis<br><br>* MongoDB |
|LogLevel |String |Normal |Log level, the values are as follows:<br><br><br>* `Normal`: Indicates a normal log.<br><br>* `Incident`: Indicates a conflict log.<br><br>* `Warning`: Indicates a warning log. |* MySQL（V1、V2）<br><br>* veDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* MongoDB |
|LogType |String |Query action |Log type. The following are common log type values:<br><br><br>* Modify database<br><br>* Modify table<br><br>* Modify user<br><br>* Start transaction<br><br>* Submit transaction<br><br>* Create new table<br><br>* Create view<br><br>* Creating a user<br><br>* Create database<br><br>* Creating index<br><br>* Create import<br><br>* Execute expression<br><br>* Delete database<br><br>* Delete an index<br><br>* Delete view<br><br>* Drop table<br><br>* Delete user<br><br>* Delete all data in table<br><br>* Delete data<br><br>* Query execution plan<br><br>* Flush operation<br><br>* Replace data<br><br>* Insert data<br><br>* Call stored procedure<br><br>* Index suggestion<br><br>* Terminate session<br><br>* Load data<br><br>* Lock table<br><br>* Plan<br><br>* Prepare preprocessing<br><br>* Execute preprocessing<br><br>* Release preprocessing<br><br>* PURGE action<br><br>* Query action<br><br>* Rename table<br><br>* Rename user<br><br>* Delete user privilege<br><br>* Rollback<br><br>* Set variable action<br><br>* Show information<br><br>* Query execution information<br><br>* Clear the table<br><br>* Unlock table<br><br>* Update operation<br><br>* Full update<br><br>* Select database |* MySQL（V1、V2）<br><br>* veDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* MongoDB |
|Table |String |tablename |Table name. |* MySQL（V1、V2）<br><br>* veDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* MongoDB |
|SqlMethod |String |SELECT |SQL type The values are as follows:<br><br><br>* `SELECT`: Query.<br><br>* `INSERT`: Insert.<br><br>* `UPDATE`: Update.<br><br>* `DELETE`: Delete.<br><br>* `ALTER`: Modify.<br><br>* `CREATE`: Create.<br><br>* `DROP`: Drop.<br><br>* `RENAME`: Rename.<br><br>* `TRUNCATE`: Clear.<br><br>* `LOGIN`: Log in.<br><br>* `LOGOUT`: Log out. |* MySQL（V1、V2）<br><br>* veDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* MongoDB |
|NodeId |String |proxy\-redis\-cnlfxwjm8wl\*\*\*\*\*\*\-1 |Node ID |* MySQL（V2）<br><br>* PostgreSQL（V2）<br><br>* Redis |
|ScanRows |Integer |0 |Rows scanned. |* MySQL（V2）<br><br>* veDB MySQL（V2）<br><br>* PostgreSQL（V1、V2） |
|WaitLockConsumingTime |Integer |0 |Lock wait time. |* PostgreSQL（V1） |
|SessionId |String |860422 |Session ID |* MySQL（V2）<br><br>* veDB MySQL（V2）<br><br>* PostgreSQL（V1、V2） |
|SqlFingerprint |String |d41d8cd98f00b204e9800998ecf\*\*\*\*\*\* |SQL fingerprint |* MySQL（V2）<br><br>* veDB MySQL（V2）<br><br>* PostgreSQL（V1、V2） |
|ReturnRows |Integer |1 |Rows returned. |* MySQL（V2）<br><br>* veDB MySQL（V2）<br><br>* PostgreSQL（V2） |

## DescribeFullSQLDetailRow

|**Parameter** |**Type** |**Sample** |**Description** |**Supported database types** |
|---|---|---|---|---|
|DBName |String |order_db |Database name. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|SessionID |String |12345 |Session ID |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|SqlType |String |SELECT |SQL type Values include: `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `ALTER`, `CREATE`, `DROP`, `RENAME`, `TRUNCATE`, `OTHER`. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|QueryString |String |select \* from orders where id = 1 |Original SQL text. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|StartTimestamp |String |1787566212355943 |SQL start time. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|EndTimestamp |String |1787566212356016 |SQL end time. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|ExecTime |Integer |73 |Execution time. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|CpuTime |Integer |0 |CPU time consuming. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|RowsExamined |Integer |100 |Rows scanned. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|RowAffected |Integer |1 |Rows affected. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|RowsSent |Integer |10 |Rows returned. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|UserName |String |app_user |Database username. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|ClientIp |String |10.0.0.10 |Client IP. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|ClientPort |String |55880 |Client port. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|ServerPort |String |3306 |Service port. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|ExecErrorNo |String |0 |SQL execution error code. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|SqlFingerprint |String |a1b2c3d4 |SQL fingerprint |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|SqlTable |String |orders |Table name. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|NodeId |String |node\-a |Node ID |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|SqlTemplate |String |select \* from orders where id = ? |SQL template |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |

## DeadlockInfo

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DeadlockCollectionTime |String |1791441738725 |Collection time of the deadlock snapshot. |
|DeadlockTime |String |2026\-10\-08 14:42:10 |Deadlock occurrence time. |
|DeadlockList |Array of Deadlock |```JSON```<br>```[```<br>```    {```<br>```        "HoldLock": "RECORD LOCKS",```<br>```        "HoldLockIndex": "PRIMARY",```<br>```        "HoldLockMode": "X",```<br>```        "ProcessId": "17295451",```<br>```        "RelateTable": "`dbw`.`dbw_lw_dl_z1m2iaz4`",```<br>```        "ReqType": "Update",```<br>```        "Sql": "/* DBW CONSOLE psm=dbw.bytecloud.connection */ UPDATE dbw_lw_dl_z1m2iaz4 SET lock_value = lock_value + 1 WHERE id = 2\n",```<br>```        "TrxInfo": "1",```<br>```        "TrxTreat": "ROLL BACK TRANSACTION 2",```<br>```        "WaitIndex": "PRIMARY",```<br>```        "WaitLock": "RECORD LOCKS",```<br>```        "WaitLockMode": "X"```<br>```    }```<br>```]```<br> |Deadlock transaction list.<br><br> |
|NodeId |String |mysql\-bf120f\*\*\*\*\*\*\-abc |Database instance node ID. |

## Deadlock

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|TrxInfo |String |1 |Transaction information. |
|ProcessId |String |11731197 |Session ID |
|ReqType |String |Update |Request type. |
|RelateTable |String |test |Involving table. |
|WaitLock |String |RECORD LOCKS |Wait for lock. |
|WaitIndex |String |PRIMARY |Lock\-wait index name. |
|WaitLockMode |String |X |Wait lock type. |
|HoldLock |String |RECORD LOCKS |Hold lock. |
|HoldLockIndex |String |PRIMARY |Index name of hold lock. |
|HoldLockMode |String |X |Hold lock type. |
|Sql |String |/\* DBW CONSOLE psm=dbw.bytecloud.connection \*/ UPDATE dbw_lw_dl_z1m2iaz4 SET lock_value = lock_value + 1 WHERE id = 2\n |Involving statement. |
|TrxTreat |String |ROLL BACK TRANSACTION 2 |Transaction processing. |

## DescribeLockCurrentWaitsDetail

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|RTrxId |String |52514179 |Transaction ID. |
|RTrxState<br><br> |String |LOCK WAIT |Transaction state, with possible values:<br><br><br>* `RUNNING`: Running.<br><br>* `LOCKWAIT`: Waiting for lock.<br><br>* `ROLLING BACK`: Indicates that the rollback is in progress.<br><br>* `COMMITTING`: Indicates the transaction is being committed. |
|RWaitingQuery |String |UPDATE dbw_lw_dl_2voy1zp9 SET lock_value = lock_value + 100 WHERE id = 3 |Lock wait SQL. |
|RTrxStarted |String |2026\-10\-08T14:42:30+08:00 |Transaction start time. |
|RTrxWaitStarted |String |2026\-10\-08T14:42:30+08:00 |Transaction wait since. |
|RBlockedWaitSecs |String |12 |Blocking wait time. |
|RTrxRowsModified |String |0 |Number of rows modified by the transaction. |
|RTrxRowsLocked |String |1 |Transaction locked rows. |
|RTrxOperationState |String |starting index read |Transaction operation status. |
|BTrxId |String |52514160 |Blocking transaction ID. |
|BTrxState |String |RUNNING |Blocking transaction status. Possible values:<br><br><br>* `RUNNING`: Running.<br><br>* `LOCKWAIT`: Waiting for lock.<br><br>* `ROLLINGBACK`: Rolling back.<br><br>* `COMMITTING`: Indicates the transaction is being committed. |
|BWaitingQuery |String |\- |Blocker SQL. |
|BTrxStarted |String |2026\-10\-08T14:42:21+08:00 |Blocking transaction start time. |
|BTrxWaitStarted |String |\- |Blocking transaction wait start time. |
|BTrxRowsModified |String |1 |Blocking transaction modified row count. |
|BTrxRowsLocked |String |1 |Number of locked rows for blocking transactions. |
|BTrxOperationState |String |\- |Blocking transaction operation status. |
|NodeId |String |mysql\-bf120f\*\*\*\*\*\*\-abc |Database instance node ID. |
|CollectTime |Integer |1791441927069 |Transaction snapshot collection time. |

## DialogDetail

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SnapshotTime |Integer |1782349500 |Session snapshot time. |
|ProcessID |String |10000 |Session ID. |
|User |String |test |Username. |
|Host |String |192.168.1.100:6666 |Client IP. |
|DB |String |company |Database name. |
|Command |String |Query |Command type. |
|State |String |executing |State. |
|Info |String |select \* from employee |Execute statement. |
|LowerExecTimeLimit |String |1 |Duration in current status (seconds). |

## DialogSnapshot

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SnapshotTime |Integer |1782465540 |Session snapshot time point (unit: second). |

## ErrLog

Error log list information. Referenced by the following interfaces:

* DescribeErrLogs

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Timestamp |Integer |1705525166 |Log collection time, in seconds timestamp format. |
|LogLevel |String |Note |Error log level. Log levels include `Note`, `Warning`, and `Error`. |
|Content |String |Storing MySQL user name or password information in the master info repository is not secure and is therefore not recommended. Please consider using the USER and PASSWORD connection options for START SLAVE; see the 'START SLAVE Syntax' in the MySQL Manual for more information. |Error log content |
|NodeId |String |mysql\-898e213\*\*\*\*\*\*\-s58cb\-0 |Node ID |

## ErrLogSearchParam

Query parameters for error logs. Referenced by the following interfaces:

* DescribeErrLogs

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|NodeIds |Array of String |["mysql\-898e21\*\*\*\*\*\*\-s58cb\-0"] |Node ID list information. |
|LogLevel |Array of ErrLogLevel |["Warning"] |Error log level. The values are as follows:<br><br><br>* `Note`: Indicates a normal log.<br><br>* `Warning`: Indicates a warning log.<br><br>* `Error`: Indicates an error log. |
|Keyword |String |test1 |Fuzzy keyword search. |

## FlowConfigs

Approval workflow information. Referenced by the following interfaces:

* ListApprovalFlowConfig

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|AssociatedInstanceNum<br><br> |String |1<br><br> |The number of times the current approval workflow is referenced by the instance.<br><br> |
|ConfigId |String |1811243361378508800 |Approval workflow ID. |
|ConfigName |String |cx\-test\-only |Approval workflow name. |
|CreateUser |String[] |```JSON```<br>```{```<br>```    "UserId": "2100067216",```<br>```    "UserName": "RootAccount"```<br>```}```<br> |Approval workflow creator information, including User ID and username<br><br> |
|Memo |String |Administrator single point |Remarks for the approval process. |
|Type |String |Customize |Approval Workflow Type. The return values are as follows.<br><br><br>* `System`: System node.<br><br>* `Customize`: Custom node. |

## FullSqlInstanceInfo

|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|CreateTime |String |2006\-01\-02 15:04:05 |Creation time of the instance mapping relationship, in the format YYYY\-MM\-DD HH:mm:ss. |
|Deleted |Boolen |false<br><br> |Whether the instance mapping is deleted. The values are as follows:<br><br><br>* `true`: The instance mapping is deleted.<br><br>* `false`: The instance mapping is not deleted. |
|FollowInstanceID |String |mysql\-76eda4\*\*\*\*\*\* |Instance ID. |
|InstanceID |String |DBW_FullSql_ed8b2b04\-b985\-4861\-b19d\-e0d2bd\*\*\*\*\*\* |Billing instance ID. |
|ModifyTime |String |2006\-01\-02 15:04:05 |The time when the instance mapping was modified, in the format YYYY\-MM\-DD HH:mm:ss. |
|ProductType |String |FullSqlLog |Product type. |
|Region |String |cn\-beijing |Instance ID. |

## QueryFilter

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ShowSleepConnection<br><br> |Bool |true |Display inactive sessions. The values are as follows:<br><br><br>* `true`: Display inactive sessions.<br><br>* `false`: Do not display inactive sessions. |
|ProcessID |String |10000 |Session ID |
|User |String |test |Username. |
|Host |String |192.168.1.100:6666 |Client IP. |
|DB |String |company |Database name. |
|Command |String |Query |Command type. |
|State |String |Executing |State. |
|Info |String |select \* from employee |Execute statement. |
|LowerExecTimeLimit |String |1 |Duration in current status (seconds). |

##

## RegionEnableFunctions

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SQLAuditDetail<br><br> |Boolean |true |Whether SQL Audit details are enabled. The values are as follows:<br><br><br>* `true`: Indicates that SQL Audit details are enabled. This parameter must be true when enabling the subscription.<br><br>* `false`: Indicates that SQL Audit details are not enabled. |
|SQLInsight |Boolean |true<br><br> |Whether SQL Audit and Analysis is enabled. The values are as follows:<br><br><br>* `true`: Indicates that SQL Audit and Analysis is enabled.<br><br>* `false`: Indicates that SQL Audit and Analysis is not enabled. |
|EnableHierarchicalStorage |Boolean |true |Whether to enable tiered storage of hot and cold data. The values are as follows:<br><br><br>* `true`: Indicates that hot/cold tiered storage is enabled.<br><br>* `false`: Indicates that hot/cold tiered storage is not enabled. |

## RowsAffectedStats

|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Max<br><br> |Double |1250.0 |Maximum value.<br><br> |
|Min<br><br> |Double |1.0 |Minimum value.<br><br> |
|Total<br><br> |Double |28650.0 |Total.<br><br> |
|Average<br><br> |Double |114.6 |Average value. |

## RuleConfig

|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |Expand |Scaling configuration. Valid values:<br><br><br>* `Scale out`: indicates scaling out.<br><br>* `Reduce`: indicates scaling in. |
|IsOpen |Boolen |Yes<br><br> |true |Whether to enable the rule. Values are as follows:<br><br><br>* `true`: Indicates the rule is enabled.<br><br>* `false`: Indicates the rule is not enabled. |
|Threshold |Integer |Yes |48 |Trigger rule threshold. |
|ScalingLimit |String |No |3000 |Scaling limit. The value range is from 20 GB to 3,000 GB. |
|ObservationWindow |Integer |No |5 |Single rule observation window. |

## Result

Detailed information about the SQL command execution result. Referenced by the following interfaces:

* [DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands)

* [ExecuteSQL](https://docs.byteplus.com/en/docs/DBW/ExecuteSQL)

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|CommandStr |String |Select \* from func; |The executed statement content |
|State |String |Success |Command execution status, the values are as follows:<br><br><br>* `Succeeded`: Command executed successfully.<br><br>* `Failed`: Command failed to execute.<br><br>* `Cancel`: Cancel command execution.<br><br>* `Pending`: Command is waiting to execute.<br><br>* `Executing`: Command is in progress. |
|ReasonDetail |String |UnknownError |The information returned when the command fails to execute. |
|RunTime |int64 |1665741434000 |The start timestamp for executing SQL statements, in milliseconds (ms). |
|ColumnNames |array of String | <br><br>```JSON```<br>```[```<br>```"name",```<br>```"ret",```<br>```"dl",```<br>```"type"```<br>```]```<br> |List of result set fields returned when executing a query script |
|RowCount |long |1,000 |The total number of rows in the list. |
|Rows |Array of Cell | <br><br>```JSON```<br>```[```<br>```{```<br>```"Cells": [```<br>```"87",```<br>```"01",```<br>```"权限管理",```<br>```"/admin/auth",```<br>```"1"```<br>```]```<br>```}```<br>```]```<br> |Information of rows in the list. |

## RuleDetail

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|TaskId |String |2108115634582761472 |SQL throttling task ID. |
|RuleState |String |ACTIVE |SQL throttling task state, with the following possible values:<br><br><br>* `ACTIVE`: Running.<br><br>* `STOPPED`: Terminated.<br><br>* `DONE`: Completed.<br><br>* `STOP_FAILED`: Termination failed.<br><br>* `DELETE_FAILED`: Deletion failed. |
|ThrottleTarget |String |MaxConcurrencyCount |Rate limiting object. Currently, only `MaxConcurrencyCount` is supported, which indicates SQL keyword\-based rate limiting. |
|KeyWords |String |select~from~test |SQL keywords. |
|SqlType |String |SELECT |SQL types that require rate limiting include `SELECT`, `UPDATE`, `DELETE`, `INSERT`, and `REPLACE`. |
|TerminationType |String |Manual |End of task for the SQL throttling task. Valid values:<br><br><br>* `Manual`: Manually end the throttling task.<br><br>* `Auto`: Automatically end the throttling task. |
|EffectiveTime |Integer |10 |The throttling time of the SQL throttling task, in minutes.<br><br>> **tip**<br><br><br>> This parameter is returned when the `TerminationType` parameter is set to `Auto`.<br> |
|ConcurrencyCount |Integer |0 |Maximum concurrency for SQL statements on each node. |
|CreateTime |String |2025\-12\-25T12:00:00Z |Creation time of SQL throttling task. |
|EndTime |String |2025\-12\-25T12:10:00Z |End time of the SQL throttling task. |
|RemainingTime |Integer |1 |Remaining time for the SQL throttling task. |
|RejectCount |Integer |100 |Number of rejections for the SQL throttling task. |

## SearchParam

Parameter information of the audit log to be queried. Referenced by the following interfaces:

* DescribeAuditLogDetail

Database Workshop DBW provides two versions of database audit functionality: V1 and V2. You can select appropriate parameters based on the version of database audit.

|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |**Supported database types** |
|---|---|---|---|---|---|
|DBs<br><br> |Array of String |No |[ "information_schema" ] |Database list information. |* MySQL（V1、V2）<br><br>* VeDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* Redis<br><br>* MongoDB |
|Users |Array of String |No |[ "rootgg" ] |Database account list information. |* MySQL（V1、V2）<br><br>* VeDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* Redis<br><br>* MongoDB |
|SourceIPs |Array of String |No |[ "192.168.0.33" ] |IP list. |* MySQL（V1、V2）<br><br>* VeDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* Redis<br><br>* MongoDB |
|LogLevels |Array of String |No |["Normal", "Incident", "Warning"] |Log level, the values are as follows:<br><br><br>* Normal: Indicates a normal log.<br><br>* Incident: Indicates a conflict log.<br><br>* Warning: Indicates a warning log. |* MySQL（V1）<br><br>* VeDB MySQL（V1）<br><br>* PostgreSQL（V1）<br><br>* MongoDB |
|LogType |Array of String |No |["Create table", "Query Actions"] |Log type. The following are common log type values:<br><br><br>* Modify database<br><br>* Modify table<br><br>* Modify user<br><br>* Start transaction<br><br>* Submit transaction<br><br>* Create new table<br><br>* Create view<br><br>* Creating a user<br><br>* Create database<br><br>* Creating index<br><br>* Create import<br><br>* Execute expression<br><br>* Delete database<br><br>* Delete an index<br><br>* Delete view<br><br>* Drop table<br><br>* Delete user<br><br>* Delete all data in table<br><br>* Delete data<br><br>* Query execution plan<br><br>* Flush operation<br><br>* Replace data<br><br>* Insert data<br><br>* Call stored procedure<br><br>* Index suggestion<br><br>* Terminate session<br><br>* Load data<br><br>* Lock table<br><br>* Plan<br><br>* Prepare preprocessing<br><br>* Execute preprocessing<br><br>* Release preprocessing<br><br>* PURGE action<br><br>* Query action<br><br>* Rename table<br><br>* Rename user<br><br>* Delete user privilege<br><br>* Rollback<br><br>* Set variable action<br><br>* Show information<br><br>* Query execution information<br><br>* Clear the table<br><br>* Unlock table<br><br>* Update operation<br><br>* Full update<br><br>* Select database |* MySQL（V1）<br><br>* VeDB MySQL（V1）<br><br>* PostgreSQL（V1）<br><br>* MongoDB |
|DuringUp |Integer |No |100 |Execution time limit, unit: microseconds. |* MySQL（V1、V2）<br><br>* VeDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* Redis<br><br>* MongoDB |
|DuringDown |Integer |No |10 |Minimum execution time in microseconds. |* MySQL（V1、V2）<br><br>* VeDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* Redis<br><br>* MongoDB |
|AffectRowUp |Integer |No |100 |Upper limit of the number of rows affected. |* MySQL（V1、V2）<br><br>* VeDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2） |
|AffectRowDown |Integer |No |100 |Minimum number of rows affected. |* MySQL（V1、V2）<br><br>* VeDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2） |
|SqlMethods |Array of String |No |["SELECT", "INSERT"] |SQL operations, taking the following values:<br><br><br>* `SELECT`: Query.<br><br>* `INSERT`: Insert.<br><br>* `UPDATE`: Update.<br><br>* `DELETE`: Delete.<br><br>* `ALTER`: Modify.<br><br>* `CREATE`: Create.<br><br>* `DROP`: Drop.<br><br>* `RENAME`: Rename.<br><br>* `TRUNCATE`: Clear.<br><br>* `LOGIN`: Log in.<br><br>* `LOGOUT`: Log out. |* MySQL（V1、V2）<br><br>* VeDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* MongoDB |
|Tables |Array of String |No |["table1"] |Table name, obtained from the list of candidates |* MySQL（V1、V2）<br><br>* VeDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2）<br><br>* MongoDB |
|SqlFingerprint |String |No |asdf\-asdf\-asdf\-xxxxx |SQL fingerprint |* MySQL（V1、V2）<br><br>* VeDB MySQL（V1、V2）<br><br>* PostgreSQL（V1、V2） |
|NodeId |String |No |proxy\-redis\-xxxx |Node ID |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2）<br><br>* Redis<br><br>* MongoDB |
|CmdKey |String |No |keyword |Keyword. |* Redis<br><br>* MongoDB |
|CommandResult |String |No |Success<br><br> |SQL command execution result, with the following values:<br><br><br>* `0`: Indicates command execution failed.<br><br>* `1`: Command executed successfully.<br><br>* `2`: Command execution canceled.<br><br>* `3`: Command waiting for execution.<br><br>* `4`: Command in progress. |* MongoDB |
|SqlFingerprints |Array of string |No |  |SQL fingerprint list. Recommended.<br><br> |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|SqlCommands |Array of string |No |  |SQL command filter condition. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|KeyWords |Array of string |No |  |SQL keywords filter condition. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|ErrorNos |String |No |  |The filter condition for error codes. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|SessionIDs |Array of string |No |  |Session ID filter condition. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|DisplaySqlTemplate |String |No |true |Whether to return the SqlTemplate. The values are as follows:<br><br><br>* `true`: Returns the SqlTemplate.<br><br>* `false`: Does not return the SqlTemplate. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|CollectSqlFingerprint |String |No |true |Whether to query only the data with collected SQL fingerprints. The values are as follows:<br><br><br>* `true`: Queries only the data with collected SQL fingerprints.<br><br>* `false`: Queries all data. |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |
|LogTypes |Array of string |No | <br><br>```JSON```<br>```"SQL"```<br><br><br> |Log type filter condition.<br><br> |* MySQL（V2）<br><br>* VeDB MySQL（V2）<br><br>* PostgreSQL（V2） |

## SearchParamObject

Slow log execution search information. Referenced by the following interfaces:

* DescribeAggregateSlowLogs

|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|GroupIgnored |Array of String |No |["SourceIP", "User"] |Aggregation parameter. The following optional parameters are available:<br><br><br>* `SourceIP`: IP address.<br><br>* `User`: User name. |
|DBs |Array of string |No |["test1", "test2"] |Database name. You can enter multiple database names, separated by commas (,). |
|Users |Array of string |No |["root1", "root2"] |Username. You can enter multiple usernames, separated by commas (,). |
|Keywords |Array of string |No |["select", "insert"] |SQL template keyword. You can enter multiple keywords, separated by commas (,). |
|MinQueryTime |Integer |No |20 |Minimum execution time threshold for slow SQL, in seconds (s). |
|MaxQueryTime |Integer |No |30 |The maximum time spent on Slow SQL, in seconds (s). |
|Collection |Array of string |No |["test1", "test2"] |List of collections in Document Database for MongoDB.<br><br>> **tip**<br><br><br>> This parameter is optional when querying slow logs of Document Database for MongoDB instances.<br> |

## SecGroupSearchParam

Security rule set array. Referenced by the following interfaces:

* DescribeSecurityGroups

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|InstanceType<br><br>         |String |MySQL<br><br> |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL.<br><br>* `Mongo`: Document Database for MongoDB.<br><br>* `MSSQL`: RDS for SQL Server<br><br>* `Redis`: Cache for Redis. |
|Keyword |String |mysql default |Rule set name. |
|SecurityGroupId |String |1740264867044012032 |Rule set ID. |

## SecurityGroups

Security rule set information. Referenced by the following interfaces:

* DescribeSecurityGroups

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|AssociatedInstanceNum |String |10 |Number of associated instances. |
|Category |String |Default |Rule set type, the return value is as follows:<br><br><br>* `Default`: Default<br><br>* `Custom`: Customize |
|Comment |String |auto created by trigger 2100067216 |Remarks information. |
|ID |String |1740264867044012032 |Security rule set ID |
|InstanceType |String |MySQL |Database types: The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL<br><br>* `VeDBMySQL`: NDB for MySQL<br><br>* `Postgres`: Cloud Database PostgreSQL<br><br>* `Mongo`: Document Database for MongoDB<br><br>* `MSSQL`: RDS for SQL Server |
|Name |String |mysql default |Security rule set name |
|UpdateTime |String |1703746451 |Last modified time. |

## Slowlog

Detailed information of the slow log. Referenced by the following interfaces:

* DescribeSlowLogs

|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ConnectionId |Integer |2145056 |Connection ID. |
|DB |String |information_schema |Database name. |
|LockTime |Float |0 |Indicates the lock wait time required to execute the queried object. the queried object may be locked in another session, and other languages need to wait for the lock to be released before the query operation can be executed. this time is the lock wait time. |
|QueryTime |Float |3.000151 |Indicates the query statement duration. |
|Timestamp |Integer |1681097392 |Sorted by query start time. |
|RowsExamined |Integer |1 |Indicates the number of rows to scan during the query. |
|RowsSent |Integer |1 |The number of rows of data returned after the query result is hit. |
|SQLTemplate |String |`select sleep(?);` |SQL template |
|SQLText |String |```Plain Text```<br>```select sleep(3);\n/usr/sbin/mysqld, Version: 8.0.26 (MySQL Community Server (GPL)). started with:\nTcp port: 3306  Unix socket: /var/run/mysqld/mysqld.sock\nTime  Id Command    Argument```<br> |SQL text refers to the actual query statement executed. |
|SourceIP |String |192.168.0.33 |IP address. |
|User |String |rootgg |Executor name |

## SlowLogSearchParam

|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|SQLTemplate |String |No |```json```<br>```select * from test where id =?```<br> |SQL template |
|DBs |Array of String |No |[test1,test2] |List of database names. |
|Users |Array of String |No |[root1,root2] |List of usernames. |
|SourceIPs |Array of String |No |[127.0.0.1,127.0.0.2] |IP list. |
|MinQueryTime |Float |No |0.05 |Shortest execution time. |
|MaxQueryTime |Float |No |1.05 |Maximum execution time consumption. |
|SQLTemplateID |String |No |a86e95364af941743630cf16d94d09788ee171af3397afafb89401cb6\*\*\*\*\*\* |SQL template ID. |

## SQLKillRules

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|TaskId |String |2005543523536\*\*\*\*\*\* |Persistent kill task ID. |
|CreateTime |String |2025\-12\-29T07:36:51Z |Creation time of the persistent kill task. |
|State |String<br><br> |DONE<br><br> |Persistent kill task status, with the following values:<br><br><br>* `ACTIVE`: Indicates the task is running.<br><br>* `STOPPED`: Indicates the task has been terminated.<br><br>* `DONE`: Indicates the task is completed.<br><br>* `STOP_FAILED`: Indicates the task termination failed.<br><br>* `DELETE_FAILED`: Indicates the task deletion failed. |
|SqlType |String |select,update,insert,delete |SQL type for persistent kill tasks. Values include `select`, `update`, `delete`, and `insert`. |
|NodeType |String |Primary,ReadOnly<br><br> |Node type for persistent kill tasks. Values include `Primary node` and `Read-only Node`. |
|MaxExecTime |Integer |1 |SQL execution time, indicating SQL requests exceeding this duration will be killed. Unit: second (s), value range: 1~9999. |
|EffectiveTime |Integer |60 |Task duration, indicating that after the persistent Kill task reaches this duration, it will be automatically closed. The unit is second(s), with a valid range from 1 to 99,999,999. |
|RemainingTime |Integer |0 |Remaining duration of persistent kill tasks in seconds (s). |
|User |String |RootAccount |Creator of the persistent kill task. |

## TableMeta

Table metadata information. Referenced by the following interfaces:

* GetTableInfo

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Name |String |employee |Table name. |
|Engine |String |InnoDB |Storage engine. |
|CharacterSet |String |utf8mb4 |Table character set. |
|Collations |String |utf8mb4_general_ci |Table validation rule. |
|Definition |String |CREATE TABLE employee (\n id bigint(11) NOT NULL AUTO_INCREMENT,\n name varchar(60) NOT NULL,\n age smallint(10) NOT NULL,\n city varchar(60) NOT NULL,\n department varchar(60) NOT NULL,\n PRIMARY KEY (id)\n) ENGINE=InnoDB AUTO_INCREMENT=16394 DEFAULT CHARSET=utf8mb4 |Table creation DDL statement.; |
|Columns |Array of Column |[Columns](https://docs.byteplus.com/en/docs/DBW/data-structure) |Table field metadata list |

## TagObject

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Key |String |Yes |Label key. Naming rules are as follows:<br><br><br>* Naming restrictions: Tag keys cannot start with volc: (case\-insensitive, such as Volc:, VOLC:, etc. are not allowed).<br><br>* Character support: Supports uppercase and lowercase letters, numbers, spaces, and specific English symbols (_, ., :, /, =, +, \-, @).<br><br>* Length limit: Must be between 1 and 128 characters.<br><br>* Encoding format: Supports Unicode in UTF\-8 encoding. |
|Value |String |Yes |Label value. Naming rules are as follows:<br><br><br>* Naming restrictions: Tag keys cannot start with volc: (case\-insensitive, such as Volc:, VOLC:, etc. are not allowed).<br><br>* Character support: Supports uppercase and lowercase letters, numbers, spaces, and specific English symbols (_, ., :, /, =, +, \-, @).<br><br>* Length limit: Must be between 1 and 128 characters.<br><br>* Encoding format: Supports Unicode in UTF\-8 encoding. |

## TemplatesContrast

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SqlFingerprint |String |a1b2c3d4 |SQL fingerprint |
|DbName |String |order_db |Database name. |
|TbName |String |orders |Table name. |
|SqlType |String |SELECT |SQL type Values include: `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `ALTER`, `CREATE`, `DROP`, `RENAME`, `TRUNCATE`, `OTHER`. |
|FirstTemplatesDetail |[AggregationSQLTemplateDetail](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#MD0J8VyY) |```JSON```<br>```{```<br>```    "BinlogSyncTime": 0,```<br>```    "BytesSent": 0,```<br>```    "CclWaitTime": 0,```<br>```    "Count": 2,```<br>```    "CpuTime": 490,```<br>```    "DBName": "test_zhudi",```<br>```    "ExecTime": 794,```<br>```    "GroupFollowerWaitTime": 0,```<br>```    "InnodbIoReadBytes": 0,```<br>```    "InnodbIoReads": 0,```<br>```    "InnodbPageAccess": 16,```<br>```    "InstanceID": "mysql-cf8d83a2ea63",```<br>```    "IsCollectSqlFingerprint": false,```<br>```    "LatchWaitTime": 0,```<br>```    "MdlWaitTime": 0,```<br>```    "RedoLogFlushTime": 0,```<br>```    "RowlockWaitTime": 0,```<br>```    "RowsAffected": 0,```<br>```    "RowsExamined": 4,```<br>```    "RowsSent": 0,```<br>```    "SemiSyncWaitTime": 0,```<br>```    "ServerPort": "",```<br>```    "SocketSendTime": 0,```<br>```    "SqlFingerprint": "01c4dbcc021b24e3beff902d78115f5e",```<br>```    "SqlTable": "TABLES",```<br>```    "SqlTemplate": "SELECT `TABLE_NAME` FROM `information_schema`.`TABLES` WHERE `TABLE_SCHEMA`=? AND `TABLE_TYPE` IN (?+) LIMIT ?+",```<br>```    "SqlType": "SELECT",```<br>```    "TablelockWaitTime": 0,```<br>```    "TcCommitTime": 0,```<br>```    "TcFlushTime": 0,```<br>```    "TenantID": "2100067216",```<br>```    "ThreadSchedTime": 3,```<br>```    "ThreadWaitTime": 0,```<br>```    "TmpDiskTables": 0,```<br>```    "TotalCpuTime": 980,```<br>```    "TotalExecTime": 1588,```<br>```    "TrxCommitTime": 0,```<br>```    "WaitLockTime": 0```<br>```}```<br> |The aggregated metrics for the first time range.<br><br> |
|SecondTemplatesDetail |[AggregationSQLTemplateDetail](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#MD0J8VyY)<br><br> |```JSON```<br>```{```<br>```    "BinlogSyncTime": 0,```<br>```    "BytesSent": 0,```<br>```    "CclWaitTime": 0,```<br>```    "Count": 14,```<br>```    "CpuTime": 0,```<br>```    "DBName": "test_zhudi",```<br>```    "ExecTime": 8,```<br>```    "GroupFollowerWaitTime": 0,```<br>```    "InnodbIoReadBytes": 0,```<br>```    "InnodbIoReads": 0,```<br>```    "InnodbPageAccess": 0,```<br>```    "InstanceID": "mysql-cf8d83a2ea63",```<br>```    "IsCollectSqlFingerprint": false,```<br>```    "LatchWaitTime": 0,```<br>```    "MdlWaitTime": 0,```<br>```    "RedoLogFlushTime": 0,```<br>```    "RowlockWaitTime": 0,```<br>```    "RowsAffected": 0,```<br>```    "RowsExamined": 0,```<br>```    "RowsSent": 0,```<br>```    "SemiSyncWaitTime": 0,```<br>```    "ServerPort": "",```<br>```    "SocketSendTime": 0,```<br>```    "SqlFingerprint": "quit",```<br>```    "SqlTable": "-",```<br>```    "SqlTemplate": "",```<br>```    "SqlType": "Quit",```<br>```    "TablelockWaitTime": 0,```<br>```    "TcCommitTime": 0,```<br>```    "TcFlushTime": 0,```<br>```    "TenantID": "2100067216",```<br>```    "ThreadSchedTime": 5,```<br>```    "ThreadWaitTime": 0,```<br>```    "TmpDiskTables": 0,```<br>```    "TotalCpuTime": 0,```<br>```    "TotalExecTime": 113,```<br>```    "TrxCommitTime": 0,```<br>```    "WaitLockTime": 0```<br>```}```<br> |The aggregated metrics for the second time range. |

## TriggerCondition

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|MetricName |String |Disk usage |Metric name. |
|ComparisonOperator |String |\>= |Comparison operator. Returns ASCII code. You can decode it using Unicode escape sequences. |
|Threshold |String |90% |Threshold. |
|TimeInfo |String |5m |Time information for scheduled scaling. |

## TrxAndLockAnalysisTask

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|InstanceId |String |mysql\-0e08f1\*\*\*\*\*\* |Database instance ID |
|DSType |String |mysql\-0e08f1\*\*\*\*\*\* |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API to query the NDB MySQL instance ID.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?_vtm_=a106466.b106468.0_0.0_0.0.2109_7610615829733918244&lang=en) API to query the instance ID of RDS for PostgreSQL. |
|NodeId |String |mysql\-0e08f1\*\*\*\*\*\*\-mbebd\-0 |Database instance node ID. |
|DiagnosisTime |Integer |1788192000000 |Creation time of the transaction and lock analysis task. |
|Trigger |String |Manual |Transaction and lock analysis task trigger method, with the following possible values:<br><br><br>* `Manual`: Create the transaction and lock analysis task manually.<br><br>* `Auto`: Create the transaction and lock analysis task automatically. |
|AnalyzedData |String |information_schema.INNODB_TRX, information_schema.INNODB_LOCKS |Data source for transaction and lock analysis tasks. |
|HasTrxAndLock |Boolean |true |Whether transactions and locks exist, with the following values:<br><br><br>* `true`: Transactions and locks exist.<br><br>* `false`: No transactions or locks exist. |

## TrxAndLock

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ProcessId |String |11732383 |Session ID |
|TrxId |String |52514539 |Transaction ID. |
|Trxstatus |String |RUNNING |Transaction state, with possible values:<br><br><br>* `RUNNING`: Running.<br><br>* `LOCKWAIT`: Waiting for lock.<br><br>* `ROLLING BACK`: Indicates that the rollback is in progress.<br><br>* `COMMITTING`: Indicates the transaction is being committed. |
|Lockstatus |String |LockHold |Lock status, with the following values:<br><br><br>* `LockHold`: Indicates holding a lock.<br><br>* `LockWait`: Indicates waiting for a lock.<br><br>* `LockHoldAndWait`: Indicates waiting for a lock and holding a lock.<br><br>* `None`: Indicates no lock. |
|TrxIsoLevel |String |READ COMMITTED |Transaction isolation level. Valid values include:<br><br><br>* `READ UNCOMMITTED`: Indicates that uncommitted data can be read.<br><br>* `READ COMMITTED`: Indicates that committed data can be read.<br><br>* `REPEATABLE READ`: Indicates repeatable reads.<br><br>* `SERIALIZABLE`: Indicates serializable execution. |
|TrxExecTime |Integer |20 |Time when the transaction is executed. |
|TrxStartTime |String |2026\-10\-08 14:45:07 |Transaction start time. |
|TrxWaitStartTime |String |2026\-10\-08 14:45:14 |Transaction wait since. |
|SqlBlocked |String |UPDATE dbw_trx_lock_case_mutx6o1o SET lock_value = lock_value + 1 WHERE id = 1 |Executing SQL... |
|TrxTablesLocked |Integer |1 |Transaction locked tables. |
|TrxRowsLocked |Integer |1 |Transaction locked rows. |
|TrxRowsModified |Integer |1 |Number of rows modified by the transaction. |
|NodeId |String |mysql\-bf120f\*\*\*\*\*\*\-abc |Database instance node ID. |
|SnapshotTime |Integer |1791441927069 |Transaction snapshot collection time. |

## PreCheckDetails

|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|IsItemCanBeIgnore |Boolen |true |Whether this item can be automatically ignored. Valid values:<br><br><br>* `true`: Indicates this check item can automatically ignore this warning and proceed.<br><br>* `false`: Indicates that this check item cannot automatically ignore the alarm and must be fixed, such as syntax errors, insufficient permissions, etc. |
|IsItemIgnored |Boolen |true |Whether the check item is ignored. Possible values:<br><br><br>* `true`: Indicates the check item is ignored.<br><br>* `false`: Indicates the check item is not ignored. |
|ItemDetails |Array of string |```SQL```<br>```[```<br>```    {```<br>```        "Result": "Pass",```<br>```        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('王五', 28, '13800138000');"```<br>```    }```<br>```]```<br> |Inspection results of the SQL statement pre\-check. For details, see [ItemDetails](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#psTnczhc).<br><br> |
|ItemName |String |Permission check |Name of the pre\-check item. |
|PreCheckItem |String |Permission |Classification of check items. The values are as follows:<br><br><br>* `Permission`: Indicates permission checks.<br><br>* `Explain`: Indicates rows affected checks.<br><br>* `Param`: Indicates parameter checks.<br><br>* `Instance`: Indicates instance state checks.<br><br>* `SecurityRule`: Represents security rule check.<br><br>* `Syntax`: Represents syntax check. |
|PreCheckState |String |Success |The current state of the pre\-check item. The values are as follows:<br><br><br>* `Succeeded`: Indicates the pre\-check item passed.<br><br>* `Failed`: Indicates the pre\-check item did not passed. |
|Result |String |Pass |Inspection results of pre\-check items, with the following possible values:<br><br><br>* `Pass`: Indicates the pre\-check item passed.<br><br>* `Reject`: Indicates the pre\-check item failed. |

## ItemDetails

|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|Result |String |Inspection results of the check item for the SQL statement to be executed |Pass |
|SQL |String |SQL statement to be executed. |INSERT INTO `tb1` (name, age, phone) VALUES ('Wang Wu', 28, '13800138000'); |
