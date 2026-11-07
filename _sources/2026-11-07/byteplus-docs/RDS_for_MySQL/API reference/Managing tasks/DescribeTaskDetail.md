---
title: "DescribeTaskDetail"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describetaskdetail"
---

Call the DescribeTaskDetail interface to query task details.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TaskId |String |Yes |6f415b1c8f394b0eaad4ea5f1439\*\*\*\* |Task ID. |
|ProjectName |String |No |default |Project name. |
|InstanceId |String |No |mysql\-a63c49e8\*\*\*\* |Instance ID. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|TaskInfo |Object |Please refer to the return example. |Detailed information about the task. |
|CostTimeMS |Long |3391 |Task duration. The unit is milliseconds. |
|CreateTime |String |2024\-01\-29T13:13:49.955Z |The creation time of the task. |
|FinishTime |String |2024\-01\-29T12:38:29.116Z |The completion time of the task. |
|Progress |Integer |45 |Task progress. The unit is percentage.<br><br>tip<br><br>Only tasks with the task status of **In Progress**, i.e., tasks where the value of TaskStatus is Running, will return the task progress. |
|RelatedInstanceInfos |Object |{<br><br>"InstanceID": "mysql\-5bde124c\*\*\*\*"<br><br>} |Instances related to the task. |
|InstanceID |String |mysql\-d4942fd7\*\*\*\* |Instance ID. |
|ScheduledExecuteEndTime |String |2024\-12\-20T17:59:00Z |The deadline for starting the plan. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br>This field will only be returned for tasks in the "Waiting to start", "Waiting to execute", or "Waiting to switch" states. |
|ScheduledExecuteStartTime |String |2024\-12\-20T16:00:00Z |The start time when the plan is scheduled to begin. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br>This field will only be returned for tasks that are in the "Waiting to start", "Waiting to execute", or "Waiting to switch" state. |
|ScheduledSwitchEndTime |String |2024\-12\-20T17:59:00Z |The deadline for the planned switch. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br>This field will only be returned for tasks in the "Waiting to start", "Waiting to execute", or "Waiting to switch" status. |
|ScheduledSwitchStartTime |String |2024\-12\-20T16:00:00Z |The start time of the planned switch. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br>This field is only returned for tasks in the "Waiting to start", "Waiting to execute", or "Waiting to switch" state. |
|StartTime |String |2024\-01\-29T12:38:25.725Z |The start time of the task. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time). |
|TaskAction |String |CreateDBAccount |Task name. |
|TaskCategory |String |BackupRecoveryManagement |Task classification. Values:<br><br><br>* `BackupRecoveryManagement`: Backup and recovery management.<br><br>* `DatabaseAdminManagement`: Database administration management.<br><br>* `DatabaseProxy`: Database proxy.<br><br>* `HighAvailability`: High availability.<br><br>* `InstanceAttribute`: Instance attributes.<br><br>* `InstanceManagement`: Instance management.<br><br>* `MonitoringPerformance`: Monitoring and performance.<br><br>* `NetworkManagement`: Network management.<br><br>* `SecurityManagement`: Security management.<br><br>* `SystemMaintainManagement`: System operation and maintenance management.<br><br>* `VersionUpgrade`: Version upgrade. |
|TaskDesc |String |This is a description of a task. |Task description information. |
|TaskId |String |202401221959431F6913166F6F5A21\*\*\*\*\-682d5d |Task ID. |
|TaskParams |String | |Task parameters. |
|TaskSource |String |User |Task source. Values:<br><br><br>* `User`: Tenant.<br><br>* `System`: System.<br><br>* `SystemUser`: Internal operation and maintenance.<br><br>* `UserMaintain`: Maintenance operations initiated by system/operation and maintenance administrators and visible to tenants. |
|TaskStatus |String |Success |Task status, valid values:<br><br><br>* `WaitSwitch`: Waiting to switch.<br><br>* `WaitStart`: Waiting to execute.<br><br>* `Canceled`: Canceled.<br><br>* `Stopped`: Terminated.<br><br>* `Running_BeforeSwitch`: Running (before switching).<br><br>* `Timeout`: Execution timed out.<br><br>* `Success`: Execution succeeded.<br><br>* `Failed`: Execution failed.<br><br>* `Running`: Executing.<br><br>* `Stopping`: Terminating. |
|TaskProgress |Object[] |[<br><br>{<br><br>"Name": "InstanceInitialization",<br><br>"StepStatus": "Success"<br><br>},<br><br>{<br><br>"Name": "InstanceRecoveryPreparation",<br><br>"StepStatus": "Failed"<br><br>},<br><br>{<br><br>"Name": "DataBackupImport",<br><br>"StepStatus": "UnExecuted"<br><br>},<br><br>{<br><br>"Name": "LogBackupBinlogAdd",<br><br>"StepStatus": "UnExecuted"<br><br>},<br><br>{<br><br>"Name": "TaskSuccessful",<br><br>"StepStatus": "UnExecuted"<br><br>}<br><br>] |Progress details. |
|Name |String |InstanceInitialization |Step name. Values:<br><br><br>* `InstanceInitialization`: Task initialization.<br><br>* `InstanceRecoveryPreparation`: Instance recovery preparation.<br><br>* `DataBackupImport`: Cold backup import.<br><br>* `LogBackupBinlogAdd`: Binlog replay.<br><br>* `TaskSuccessful`: Task successful. |
|StepStatus |String |Success |Step status. Values:<br><br><br>* `Running`: In progress.<br><br>* `Success`: Succeeded.<br><br>* `Failed`: Failed.<br><br>* `Unexecuted`: Not executed. |
|StepExtraInfo |Object[] |[<br><br>{<br><br>"Type": "CurDataSize",<br><br>"Unit": "Bytes",<br><br>"Value": 7579256<br><br>},<br><br>{<br><br>"Type": "RemainDataSize",<br><br>"Unit": "Bytes",<br><br>"Value": 0<br><br>}<br><br>] |Specific information about the steps. |
|Type |String |CurDataSize |Current stage<br><br><br>* `CostTime`: The time consumed in the current stage.<br><br>* `CurDataSize`: The amount of data imported currently.<br><br>* `CurBinlog`: The number of Binlog files being replayed currently.<br><br>* `RemainCostTime`: The remaining time to be consumed.<br><br>* `RemainDataSize`: The remaining amount of data to be imported.<br><br>* `RemainBinlog`: The remaining number of Binlog files to be replayed. |
|Unit |String |Bytes |Unit. Valid values:<br><br><br>* `MS`: Milliseconds.<br><br>* `Bytes`: Bytes.<br><br>* `Files`: (Number of) files. |
|Value |Double |7579256 |The specific values corresponding to the `Type` field. |
|OriginConfig |String | |JSON format |
|CheckItems |Object[] |Please refer to the return example. |Results of the major version upgrade check.<br><br>tip<br><br>This field is only returned in the task details of UpgradeDBInstanceEngineMajorVersion. |
|CheckDetail |Object |{<br><br>"Impact": "The sorting of the results returned after SQL execution may differ from that before the upgrade.",<br><br>"Issue": "After the upgrade, the default character collation is changed to utf8mb4_0900_ai_ci."<br><br>} |Detailed information on the inspection items that failed to pass. |
|Issue |String |The sorting of the results returned after SQL execution may differ from that before the upgrade. |Problems that cause the inspection items to fail. |
|Impact |String |After the upgrade, the default character order is changed to utf8mb4_0900_ai_ci. |The impact brought by the issues that caused the failure of the inspection items after the upgrade. |
|Description |String |initConnectCheck |Description information of the inspection item. |
|ItemName |String |initConnectCheck |The name of the inspection item. |
|RiskLevel |String |Warning |The risk level of the items that failed the check. Values:<br><br><br>* `Notice`: Prompt.<br><br>* `Warning`: Warning.<br><br>* `Error`: Error. |
|CheckItemLog |String |Please refer to the return examples. |Detection project log for major version upgrade of the instance.<br><br>tip<br><br>This field is only returned in the task details of UpgradeDBInstanceEngineMajorVersion. |

## Sample request

```json
POST /?Action=DescribeTaskDetail&Version=2022-01-01
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json
X-Date: 20180614T114308Z
Authorization: HMAC-SHA256 Credential=AKIAIAGMBG4SXSQQ****/20180614/ap-southeast-1/rds_mysql/request, SignedHeaders=accept;content-type;host;x-date, Signature=6a593bf5f59e7c1109fb205c739d1cff4c672fe2d251963f4d48c8701d16****
{
    "TaskId": "20250410195816F9163BF4884FB4D2****-d4a831"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025041020230200DE5340D9C3CDD649F0-88e6d8",
        "Action": "DescribeTaskDetail",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "CheckItemLog": "{\"serverVersion\":\"5.7.32-log - MySQL Community Server (GPL)\",\"targetVersion\":\"8.0.32\",\"checksPerformed\":[{\"id\":\"circularDirectory\",\"status\":\"OK\",\"title\":\"Circular directory references in tablespace data file paths\"},{\"id\":\"engineMixup\",\"status\":\"OK\",\"title\":\"Tables recognized by InnoDB that belong to a different engine\"},{\"id\":\"changedFunctionsInGeneratedColumns\",\"status\":\"OK\",\"title\":\"Indexes on functions with changed semantics\"},{\"id\":\"columnsWhichCannotHaveDefaults\",\"status\":\"OK\",\"title\":\"Columns which cannot have default values\"},{\"id\":\"dollarSignName\",\"status\":\"OK\",\"title\":\"Check for deprecated usage of single dollar signs in object names\"},{\"id\":\"emptyDotTableSyntax\",\"status\":\"OK\",\"title\":\"Check for deprecated '.<table>' syntax used in routines.\"},{\"id\":\"authMethodUsage\",\"status\":\"OK\",\"title\":\"Check for deprecated or invalid user authentication methods.\"},{\"id\":\"deprecatedDefaultAuth\",\"status\":\"OK\",\"title\":\"Check for deprecated or invalid default authentication methods in system variables.\"},{\"id\":\"deprecatedRouterAuthMethod\",\"status\":\"OK\",\"title\":\"Check for deprecated or invalid authentication methods in use by MySQL Router internal accounts.\"},{\"id\":\"deprecatedTemporalDelimiter\",\"status\":\"OK\",\"title\":\"Check for deprecated temporal delimiters in table partitions.\"},{\"id\":\"indexTooLarge\",\"status\":\"OK\",\"title\":\"Check for indexes that are too large to work on higher versions of MySQL Server than 5.7\"},{\"id\":\"oldTemporal\",\"status\":\"OK\",\"title\":\"Usage of old temporal type\"},{\"id\":\"mysqlSchema\",\"status\":\"OK\",\"title\":\"Table names in the mysql schema conflicting with new tables in the latest MySQL.\"},{\"id\":\"nonNativePartitioning\",\"status\":\"OK\",\"title\":\"Partitioned tables using engines with non native partitioning\"},{\"id\":\"foreignKeyLength\",\"status\":\"OK\",\"title\":\"Foreign key constraint names longer than 64 characters\"},{\"id\":\"maxdbSqlModeFlags\",\"status\":\"OK\",\"title\":\"Usage of obsolete MAXDB sql_mode flag\"},{\"id\":\"obsoleteSqlModeFlags\",\"status\":\"OK\",\"title\":\"Usage of obsolete sql_mode flags\",\"detectedProblems\":[{\"dbObject\":\"@@global.sql_mode\",\"dbObjectType\":\"SystemVariable\",\"description\":\"defined using obsolete NO_AUTO_CREATE_USER option\",\"level\":\"Notice\"}]},{\"id\":\"enumSetElementLength\",\"status\":\"OK\",\"title\":\"ENUM/SET column definitions containing elements longer than 255 characters\"},{\"id\":\"groupbyAscSyntax\",\"status\":\"OK\",\"title\":\"Usage of removed GROUP BY ASC/DESC syntax\"},{\"id\":\"invalid57Names\",\"status\":\"OK\",\"title\":\"Check for invalid table names and schema names used in 5.7\",\"solutions\":[\"In order to fix them use the mysqlcheck utility as follows:\\n\\n  $ mysqlcheck --check-upgrade --all-databases\\n  $ mysqlcheck --fix-db-names --fix-table-names --all-databases\\n\\nOR via mysql client, for eg:\\n\\n  ALTER DATABASE `#mysql50#lost+found` UPGRADE DATA DIRECTORY NAME;\"]},{\"id\":\"invalidEngineForeignKey\",\"status\":\"OK\",\"title\":\"Check for columns that have foreign keys pointing to tables from a different database engine.\"},{\"id\":\"routineSyntax\",\"status\":\"OK\",\"title\":\"MySQL syntax check for routine-like objects\"},{\"id\":\"reservedKeywords\",\"status\":\"OK\",\"title\":\"Usage of db objects with names conflicting with new reserved keywords\"},{\"id\":\"partitionedTablesInSharedTablespaces\",\"status\":\"OK\",\"title\":\"Usage of partitioned tables in shared tablespaces\"},{\"id\":\"removedFunctions\",\"status\":\"OK\",\"title\":\"Usage of removed functions\"},{\"id\":\"zeroDates\",\"status\":\"OK\",\"title\":\"Zero Date, Datetime, and Timestamp values\"},{\"id\":\"orphanedObjects\",\"status\":\"OK\",\"title\":\"Check for orphaned routines and events in 5.7\"},{\"id\":\"pluginUsage\",\"status\":\"OK\",\"title\":\"Check for deprecated or removed plugin usage.\"}]}",
        "CheckItems": [
            {
                "CheckDetail": {
                    "Impact": "SQL 执行后返回结果的排序可能与升级前有差异。",
                    "Issue": "升级后默认字符序变更为 utf8mb4_0900_ai_ci。"
                },
                "Description": "检查 init_connect 参数：检测是否配置了连接初始化 SQL 语句，评估其在 MySQL 8.0 中的执行安全性。",
                "ItemName": "initConnectCheck",
                "RiskLevel": "Warning"
            },
            {
                "CheckDetail": {
                    "Impact": "升级后 default_collation_for_utf8mb4 参数默认配置为 utf8mb4_general_ci。"
                },
                "Description": "检查 utf8mb4 默认排序规则：确认 utf8mb4 字符集的默认排序规则是否为 utf8mb4_0900_ai_ci（MySQL 8.0 推荐值）。",
                "ItemName": "defaultCollationForUTF8MB4Check",
                "RiskLevel": "Warning"
            },
            {
                "CheckDetail": {
                    "Impact": "升级后SQL行为可能存在差异。",
                    "Issue": "使用了已废弃的 sql_mode 选项（如 NO_FIELD_OPTIONS）。"
                },
                "Description": "检查已废弃的 SQL_MODE 模式：识别使用了 MySQL 8.0 中已删除的 SQL 模式（如 NO_FIELD_OPTIONS），需更新配置以避免意外行为。",
                "ItemName": "obsoleteSqlModeFlags",
                "RiskLevel": "Warning"
            },
            {
                "CheckDetail": {
                    "Impact": "升级后相关参数将被忽略，涉及参数包含 [innodb_large_prefix,innodb_stats_sample_pages,metadata_locks_cache_size,query_cache_limit,query_cache_min_res_unit,query_cache_size,query_cache_type,query_cache_wlock_invalidate,secure_auth,sync_frm]。",
                    "Issue": "使用了在 MySQL 8.0 中废弃的参数。"
                },
                "Description": "检查系统参数变更：验证参数是否被废弃（如 query_cache_size）。",
                "ItemName": "removedSysVars",
                "RiskLevel": "Warning"
            }
        ],
        "TaskInfo": {
            "CostTimeMS": 601800,
            "CreateTime": "2025-04-10T08:29:06.577Z",
            "FinishTime": "2025-04-10T08:39:08.377Z",
            "ModifyTime": "2025-04-10T08:40:10.548Z",
            "OwnerHostIP": "10.56.55.154",
            "OwnerIP": "11.209.236.103",
            "OwnerName": "rdsmgr-6594668b96-btd54",
            "Progress": 0,
            "RelatedInstanceInfos": {
                "InstanceID": "mysql-0f7032f1****"
            },
            "StartTime": "2025-04-10T08:29:06.577Z",
            "TaskAction": "UpgradeDBInstanceEngineMajorVersion",
            "TaskCategory": "VersionUpgrade",
            "TaskComplexity": "High",
            "TaskDesc": "",
            "TaskId": "20250410162906B3FB2CBF4C3BBEC5****-964567",
            "TaskParams": "{\"InstanceId\":\"mysql-0f7032f1****\",\"TargetMajorVersion\":\"MySQL 8.0.32\",\"MySQLSlaveDelayThreshold\":10}",
            "TaskProgressInfo": [
                {
                    "Name": "任务初始化",
                    "StepProgress": 100,
                    "StepStatus": "Success"
                },
                {
                    "Name": "资源处理",
                    "StepProgress": 100,
                    "StepStatus": "Success"
                },
                {
                    "Name": "数据处理",
                    "StepExtraInfo": [
                        "节点1：当前已完成：4.11 GiB，共需要处理：4.11 GiB",
                        "节点2：当前已完成：4.11 GiB，共需要处理：4.11 GiB",
                        "节点3：当前已完成：4.11 GiB，共需要处理：4.11 GiB",
                        "节点4：当前已完成：4.11 GiB，共需要处理：4.11 GiB"
                    ],
                    "StepProgress": 100,
                    "StepStatus": "Success"
                },
                {
                    "Name": "数据追齐",
                    "StepProgress": 100,
                    "StepStatus": "Success"
                },
                {
                    "Name": "切换",
                    "StepProgress": 100,
                    "StepStatus": "Success"
                },
                {
                    "Name": "等待任务继续",
                    "StepExtraInfo": [
                        "实例切换到目标版本后，任务将进入\"等待执行\"阶段，实例状态将保持为\"升级中\"。在此期间，您可选择“取消”以回退到升级前状态，或选择\"立即执行\"以完成升级。如果\"等待执行\"阶段持续时间超过观测时长，系统则会自动完成升级。"
                    ],
                    "StepProgress": 100,
                    "StepStatus": "Success"
                },
                {
                    "Name": "后置维护",
                    "StepProgress": 100,
                    "StepStatus": "Success"
                },
                {
                    "Name": "任务结束",
                    "StepProgress": 100,
                    "StepStatus": "Success"
                }
            ],
            "TaskReason": "User operation",
            "TaskSource": "User",
            "TaskStatus": "Success"
        }
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
