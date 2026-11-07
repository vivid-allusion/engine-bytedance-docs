---
title: "DescribeDBInstanceParameters"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstanceparameters"
---

Call the DescribeDBInstanceParameters API to query instance parameters.

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|ParameterName |String |No |auto_explain.log_analyze |Parameter name. It supports fuzzy queries.<br><br>> **tip**<br><br><br>> When no value or an empty value is passed, all parameters under the specified instance will be queried.<br> |

## Response parameter

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |postgres\-21a3333b\*\*\*\* |Instance ID. |
|DBEngineVersion |String |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。 |
|ParameterCount |String |56 |Number of parameters. |
|Parameters |Array of [ParameterObject](https://docs.byteplus.com/en/docs/61/15722#parameterobject) |Refer to the Sample response. |Current parameter configuration of the instance (kernel parameters). |
|NoneKernelParameters |Array of [ParameterObject](https://docs.byteplus.com/en/docs/61/15722#parameterobject) |Refer to the sample response. |Current parameter configuration of the instance (non\-kernel parameters). |

### ParameterObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CheckingCode |String |[on\|off] |Parameter value range. |
|DefaultValue |String |off |Parameter default value. Refers to the default value provided in the default template corresponding to this instance. |
|Description |String |Use EXPLAIN ANALYZE for plan logging. |Parameter description in English. |
|DescriptionZH |String |Enable the sampling of EXPLAIN ANALYZE output. |Parameter description in Chinese. |
|ForceRestart |Boolean |false |Is a restart required to take effect? Values: `true` or `false`. |
|Name |String |auto_explain.log_analyze |Parameter name. |
|Type |String |bool |Parameter value type. Values: `string`, `integer`, `real`, `bool`, and `enum`. |
|Value |String |off |Parameter value. Refers specifically to the current instance running value. |

## Example

### Sample request

```json
POST /?Action=DescribeDBInstanceParameters&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230804115231D0A40DAC141F3F09F3A9",
        "Action": "DescribeDBInstanceParameters",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "DBEngineVersion": "PostgreSQL_12",
        "InstanceId": "postgres-ca7b7019****",
        "NoneKernelParameters": [
            {
                "CheckingCode": "[60-3600]",
                "DefaultValue": "60",
                "Description": "For counting slow queries, you can customize the specified time range, with the unit being seconds (s). The default value is 60 seconds, which means it counts the number of slow queries in the last 60 seconds.",
                "DescriptionZH": "对于慢查询的计数，可以自定义指定时间范围，单位为s。默认值为60s，表示统计近60s内的慢查询数量，最大值为3600s。",
                "ForceRestart": false,
                "Name": "slow_query_custom_count_range",
                "Type": "integer",
                "Value": "60"
            }
        ],
        "ParameterCount": "40",
        "Parameters": [
            {
                "CheckingCode": "[on|off]",
                "DefaultValue": "off",
                "Description": "Use EXPLAIN ANALYZE for plan logging.",
                "DescriptionZH": "启用 EXPLAIN ANALYZE 输出的采样。",
                "ForceRestart": false,
                "Name": "auto_explain.log_analyze",
                "Type": "bool",
                "Value": "off"
            },
            ……,
            {
                "CheckingCode": "[replica|logical]",
                "DefaultValue": "replica",
                "Description": "Set the level of information written to the WAL.",
                "DescriptionZH": "设置写入 WAL 的信息级别。",
                "ForceRestart": true,
                "Name": "wal_level",
                "Type": "enum",
                "Value": "replica"
            }
        ]
    }
}
```
