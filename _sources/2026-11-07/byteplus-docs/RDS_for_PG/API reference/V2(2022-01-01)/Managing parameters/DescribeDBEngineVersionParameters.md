---
title: "DescribeDBEngineVersionParameters"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBEngineVersionParameters"
---

Call the DescribeDBEngineVersionParameters API to query the list of parameters supported for a specified database engine version.

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|DBEngine |String |Yes |PostgreSQL |Parameter template type. The current value can only be `PostgreSQL`. |
|DBEngineVersion |String |Yes |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。 |

## Response parameter

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DBEngineVersion |String |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。 |
|ParameterCount |String |39 |The number of parameters supported for user settings under the specified database engine version. |
|Parameters |Array of [DBEngineVersionParameterObject](https://docs.byteplus.com/en/docs/61/48130#dbengineversionparameterobject) |Refer to the sample response. |Parameter list supported for user settings under the specified database engine version. |

### DBEngineVersionParameterObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CheckingCode |String |[on\|off] |Parameter value range. |
|DefaultValue |String |off |Parameter default value. |
|ForceRestart |Boolean |false |Is a restart required to take effect? Values: `true` or `false`. |
|Name |String |auto_explain.log_analyze |Parameter name. |
|Type |String |bool |Parameter value type. Values: `string`, `integer`, `real`, `bool`, and `enum`. |

## Example

### Sample request

```json
POST /?Action=DescribeDBEngineVersionParameters&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "DBEngine": "PostgreSQL",
    "DBEngineVersion": "PostgreSQL_12"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202505072036447244830F171F1504218C-550acb",
        "Action": "DescribeDBEngineVersionParameters",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "DBEngineVersion": "PostgreSQL_12",
        "ParameterCount": "39",
        "Parameters": [
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": false,
                "Name": "auto_explain.log_analyze",
                "Type": "bool"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": false,
                "Name": "auto_explain.log_buffers",
                "Type": "bool"
            },
            {
                "CheckingCode": "[text|xml|json|yaml]",
                "DefaultValue": "text",
                "ForceRestart": false,
                "Name": "auto_explain.log_format",
                "Type": "enum"
            },
            {
                "CheckingCode": "[-1-60000]",
                "DefaultValue": "-1",
                "ForceRestart": false,
                "Name": "auto_explain.log_min_duration",
                "Type": "integer"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": false,
                "Name": "auto_explain.log_nested_statements",
                "Type": "bool"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "on",
                "ForceRestart": false,
                "Name": "auto_explain.log_timing",
                "Type": "bool"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": false,
                "Name": "auto_explain.log_triggers",
                "Type": "bool"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": false,
                "Name": "auto_explain.log_verbose",
                "Type": "bool"
            },
            {
                "CheckingCode": "[0-1]",
                "DefaultValue": "1",
                "ForceRestart": false,
                "Name": "auto_explain.sample_rate",
                "Type": "real"
            },
            {
                "CheckingCode": "[0-50]",
                "DefaultValue": "2",
                "ForceRestart": false,
                "Name": "autovacuum_vacuum_cost_delay",
                "Type": "real"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "on",
                "ForceRestart": true,
                "Name": "cron.log_run",
                "Type": "bool"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": false,
                "Name": "default_transaction_deferrable",
                "Type": "bool"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "on",
                "ForceRestart": false,
                "Name": "enable_partitionwise_aggregate",
                "Type": "bool"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "on",
                "ForceRestart": false,
                "Name": "enable_partitionwise_join",
                "Type": "bool"
            },
            {
                "CheckingCode": "[3000-36000000]",
                "DefaultValue": "3600000",
                "ForceRestart": false,
                "Name": "idle_in_transaction_session_timeout",
                "Type": "integer"
            },
            {
                "CheckingCode": "[C|C.UTF-8|en_US.utf8|POSIX|zh_CN.utf8]",
                "DefaultValue": "C",
                "ForceRestart": false,
                "Name": "lc_monetary",
                "Type": "string"
            },
            {
                "CheckingCode": "[0-36000000]",
                "DefaultValue": "0",
                "ForceRestart": false,
                "Name": "lock_timeout",
                "Type": "integer"
            },
            {
                "CheckingCode": "[-1-2147483647]",
                "DefaultValue": "10000",
                "ForceRestart": false,
                "Name": "log_autovacuum_min_duration",
                "Type": "integer"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": false,
                "Name": "log_connections",
                "Type": "bool"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": false,
                "Name": "log_disconnections",
                "Type": "bool"
            },
            {
                "CheckingCode": "[-1-600000]",
                "DefaultValue": "1000",
                "ForceRestart": false,
                "Name": "log_min_duration_statement",
                "Type": "integer"
            },
            {
                "CheckingCode": "[ddl|mod|all]",
                "DefaultValue": "ddl",
                "ForceRestart": false,
                "Name": "log_statement",
                "Type": "enum"
            },
            {
                "CheckingCode": "[4096-1048576]",
                "DefaultValue": "131072",
                "ForceRestart": false,
                "Name": "log_temp_files",
                "Type": "integer"
            },
            {
                "CheckingCode": "[-1-2147483647]",
                "DefaultValue": "300000",
                "ForceRestart": false,
                "Name": "max_standby_archive_delay",
                "Type": "integer"
            },
            {
                "CheckingCode": "[-1-2147483647]",
                "DefaultValue": "300000",
                "ForceRestart": false,
                "Name": "max_standby_streaming_delay",
                "Type": "integer"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "on",
                "ForceRestart": false,
                "Name": "pgaudit.log_catalog",
                "Type": "bool"
            },
            {
                "CheckingCode": "[debug5|debug4|debug3|debug2|debug1|info|notice|warning|log]",
                "DefaultValue": "log",
                "ForceRestart": false,
                "Name": "pgaudit.log_level",
                "Type": "string"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": false,
                "Name": "pgaudit.log_parameter",
                "Type": "bool"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": false,
                "Name": "pgaudit.log_relation",
                "Type": "bool"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": false,
                "Name": "pgaudit.log_statement_once",
                "Type": "bool"
            },
            {
                "CheckingCode": "[*]",
                "DefaultValue": "",
                "ForceRestart": false,
                "Name": "pgaudit.role",
                "Type": "string"
            },
            {
                "CheckingCode": "[*auth_delay|pg_stat_statements|auto_explain|pgaudit|pgnodemx|pg_pathman|timescaledb|pg_stat_kcache|pg_hugepage_stat|pg_cron|pg_jieba|pg_hint_plan|pg_bigm]",
                "DefaultValue": "auth_delay,pg_stat_statements,auto_explain,pgaudit,pgnodemx",
                "ForceRestart": true,
                "Name": "shared_preload_libraries",
                "Type": "string"
            },
            {
                "CheckingCode": "[0-86400000]",
                "DefaultValue": "0",
                "ForceRestart": false,
                "Name": "statement_timeout",
                "Type": "integer"
            },
            {
                "CheckingCode": "[-1-2147483647]",
                "DefaultValue": "-1",
                "ForceRestart": false,
                "Name": "temp_file_limit",
                "Type": "integer"
            },
            {
                "CheckingCode": "[*]",
                "DefaultValue": "Asia/Shanghai",
                "ForceRestart": false,
                "Name": "timezone",
                "Type": "string"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": true,
                "Name": "track_commit_timestamp",
                "Type": "bool"
            },
            {
                "CheckingCode": "[0-1000000]",
                "DefaultValue": "0",
                "ForceRestart": false,
                "Name": "vacuum_defer_cleanup_age",
                "Type": "integer"
            },
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "ForceRestart": false,
                "Name": "wal_compression",
                "Type": "bool"
            },
            {
                "CheckingCode": "[replica|logical]",
                "DefaultValue": "replica",
                "ForceRestart": true,
                "Name": "wal_level",
                "Type": "enum"
            }
        ]
    }
}
```
