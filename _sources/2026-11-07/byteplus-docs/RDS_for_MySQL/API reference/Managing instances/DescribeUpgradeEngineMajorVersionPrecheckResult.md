---
title: "DescribeUpgradeEngineMajorVersionPrecheckResult"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeUpgradeEngineMajorVersionPrecheckResult"
---

Call the DescribeUpgradeEngineMajorVersionPrecheckResult API to query the pre\-check results of upgrading the major kernel version of the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After the required parameter InstanceId is passed in:


* If EventId is passed in, the pre\-check result specified by the EventId is returned.

* If EventId is not passed in, all pre\-check results for the instance are returned.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeUpgradeEngineMajorVersionPrecheckResult&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-7510ba07\*\*\*\* |Instance ID. |
|EventId |String |No |20250410145924BA7FA42A930CFDBD\*\*\*\*\-83bd31 |Event ID for the pre\-check of upgrading the instance major version.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Default value. If not specified, the system returns results based on the query conditions of other fields.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|PrecheckResults |Array of [UpgradeEngineMajorVersionPrecheckResult](https://docs.byteplus.com/en/docs/40/61001#upgradeenginemajorversionprecheckresult) |Refer to the Sample response. |Result of the pre\-check for upgrading the instance major version. |


<span id="upgradeenginemajorversionprecheckresult"></span>
### UpgradeEngineMajorVersionPrecheckResult


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|CheckTime |String |2025\-04\-10T06:22:12.223Z |The time when the pre\-check was performed. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|EffectiveTime |String |2025\-04\-11T06:22:12.223Z |The expiration time of the pre\-check result. The pre\-check result is valid for 24 hours. |
|MySqlShellLog |String |Refer to the Sample response. |Mysql\-shell execution log. |
|PrecheckItems |Array of [CheckItem](https://docs.byteplus.com/en/docs/40/61001#checkitem) |Refer to the Sample response. |Details of the item in the pre\-check result. |
|Progress |Long |100 |The execution progress of the pre\-check. The unit is %. |
|Result |String |Pass |Pre\-check result. Values:<br><br><br>* `Pass`: passed.<br><br>* `Failed`: failed. |
|SourceMajorVersion |String |MySQL 5.7.32 |The current major version of the instance. |
|TargetMajorVersion |String |MySQL 8.0.43 |The target major version for the instance upgrade. Only `MySQL 8.0.43` is currently supported. |
|TaskId |String |202504101422038F2D335B42B87473\*\*\*\*\-dd6b85 |Task ID. |


<span id="checkitem"></span>
### CheckItem


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|CheckDetail |Object of [CheckDetail](https://docs.byteplus.com/en/docs/40/61001#checkdetail) |{<br><br>"Impact": "The sort order of results returned after SQL execution may differ from the order before the upgrade.",<br><br>"Issue": "The default collation is changed to utf8mb4_0900_ai_ci after the upgrade."<br><br>} |Details of the check items that failed. |
|Description |String |initConnectCheck |Description of the check items. |
|ItemName |String |initConnectCheck |Check item name. |
|RiskLevel |String |Warning |The risk level of failed check items. Values:<br><br><br>* `Notice`: prompt.<br><br>* `Warning`: warning.<br><br>* `Error`: error. |


<span id="checkdetail"></span>
### CheckDetail


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Issue |String |The sort order of the results returned by SQL execution may differ from the order before the upgrade. |The problem that caused the check item to fail. |
|Impact |String |The default collation is changed to utf8mb4_0900_ai_ci after the upgrade. |The impact of the problem that caused the check item to fail after the upgrade. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeUpgradeEngineMajorVersionPrecheckResult&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-7510ba07****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250410142702096CC29BD0CB77B6337B-27c823",
        "Action": "DescribeUpgradeEngineMajorVersionPrecheckResult",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "PrecheckResults": [
            {
                "CheckTime": "2025-04-10T06:22:12.223Z",
                "EffectiveTime": "2025-04-11T06:22:12.223Z",
                "MySqlShellLog": "{\"serverVersion\":\"5.7.32-log - MySQL Community Server (GPL)\",\"targetVersion\":\"8.0.43\",\"checksPerformed\":[{\"id\":\"circularDirectory\",\"status\":\"OK\",\"title\":\"Circular directory references in tablespace data file paths\"},{\"id\":\"engineMixup\",\"status\":\"OK\",\"title\":\"Tables recognized by InnoDB that belong to a different engine\"},{\"id\":\"changedFunctionsInGeneratedColumns\",\"status\":\"OK\",\"title\":\"Indexes on functions with changed semantics\"},{\"id\":\"columnsWhichCannotHaveDefaults\",\"status\":\"OK\",\"title\":\"Columns which cannot have default values\"},{\"id\":\"dollarSignName\",\"status\":\"OK\",\"title\":\"Check for deprecated usage of single dollar signs in object names\"},{\"id\":\"emptyDotTableSyntax\",\"status\":\"OK\",\"title\":\"Check for deprecated '.<table>' syntax used in routines.\"},{\"id\":\"authMethodUsage\",\"status\":\"OK\",\"title\":\"Check for deprecated or invalid user authentication methods.\"},{\"id\":\"deprecatedDefaultAuth\",\"status\":\"OK\",\"title\":\"Check for deprecated or invalid default authentication methods in system variables.\"},{\"id\":\"deprecatedRouterAuthMethod\",\"status\":\"OK\",\"title\":\"Check for deprecated or invalid authentication methods in use by MySQL Router internal accounts.\"},{\"id\":\"deprecatedTemporalDelimiter\",\"status\":\"OK\",\"title\":\"Check for deprecated temporal delimiters in table partitions.\"},{\"id\":\"indexTooLarge\",\"status\":\"OK\",\"title\":\"Check for indexes that are too large to work on higher versions of MySQL Server than 5.7\"},{\"id\":\"oldTemporal\",\"status\":\"OK\",\"title\":\"Usage of old temporal type\"},{\"id\":\"mysqlSchema\",\"status\":\"OK\",\"title\":\"Table names in the mysql schema conflicting with new tables in the latest MySQL.\"},{\"id\":\"nonNativePartitioning\",\"status\":\"OK\",\"title\":\"Partitioned tables using engines with non native partitioning\"},{\"id\":\"foreignKeyLength\",\"status\":\"OK\",\"title\":\"Foreign key constraint names longer than 64 characters\"},{\"id\":\"maxdbSqlModeFlags\",\"status\":\"OK\",\"title\":\"Usage of obsolete MAXDB sql_mode flag\"},{\"id\":\"obsoleteSqlModeFlags\",\"status\":\"OK\",\"title\":\"Usage of obsolete sql_mode flags\",\"detectedProblems\":[{\"dbObject\":\"@@global.sql_mode\",\"dbObjectType\":\"SystemVariable\",\"description\":\"defined using obsolete NO_AUTO_CREATE_USER option\",\"level\":\"Notice\"}]},{\"id\":\"enumSetElementLength\",\"status\":\"OK\",\"title\":\"ENUM/SET column definitions containing elements longer than 255 characters\"},{\"id\":\"groupbyAscSyntax\",\"status\":\"OK\",\"title\":\"Usage of removed GROUP BY ASC/DESC syntax\"},{\"id\":\"invalid57Names\",\"status\":\"OK\",\"title\":\"Check for invalid table names and schema names used in 5.7\",\"solutions\":[\"In order to fix them use the mysqlcheck utility as follows:\\n\\n  $ mysqlcheck --check-upgrade --all-databases\\n  $ mysqlcheck --fix-db-names --fix-table-names --all-databases\\n\\nOR via mysql client, for eg:\\n\\n  ALTER DATABASE `#mysql50#lost+found` UPGRADE DATA DIRECTORY NAME;\"]},{\"id\":\"invalidEngineForeignKey\",\"status\":\"OK\",\"title\":\"Check for columns that have foreign keys pointing to tables from a different database engine.\"},{\"id\":\"routineSyntax\",\"status\":\"OK\",\"title\":\"MySQL syntax check for routine-like objects\"},{\"id\":\"reservedKeywords\",\"status\":\"OK\",\"title\":\"Usage of db objects with names conflicting with new reserved keywords\"},{\"id\":\"partitionedTablesInSharedTablespaces\",\"status\":\"OK\",\"title\":\"Usage of partitioned tables in shared tablespaces\"},{\"id\":\"removedFunctions\",\"status\":\"OK\",\"title\":\"Usage of removed functions\"},{\"id\":\"zeroDates\",\"status\":\"OK\",\"title\":\"Zero Date, Datetime, and Timestamp values\"},{\"id\":\"orphanedObjects\",\"status\":\"OK\",\"title\":\"Check for orphaned routines and events in 5.7\"},{\"id\":\"pluginUsage\",\"status\":\"OK\",\"title\":\"Check for deprecated or removed plugin usage.\"}]}",
                "PrecheckItems": [
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
                "Progress": 100,
                "Result": "Pass",
                "SourceMajorVersion": "MySQL 5.7.32",
                "TargetMajorVersion": "MySQL 8.0.43",
                "TaskId": "202504101422038F2D335B42B87473AE92-dd6b85"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
