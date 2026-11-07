---
title: "CreateSQLConcurrencyControlRule"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/CreateSQLConcurrencyControlRule"
---

Call the CreateSQLConcurrencyControlRule API to create SQL throttling rules.

## Request type

Asynchronous request.

## Precautions

Only PostgreSQL 14 to PostgreSQL 17 instances created on or after October 15, 2026 support creating SQL throttling rules.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-5d27abexxxx |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) API to query the instance ID.<br> |
|DatabaseName |String |Yes |pg_demo |Target database name. |
|Match |Object of [RuleMatch](https://docs.byteplus.com/en/docs/61/121805#rulematch) |Yes |Refer to the request example. |Matching rules. Supports matching by SQL fingerprint, keyword, and all SQL. |
|Limit |Object of [RuleConfig](https://docs.byteplus.com/en/docs/61/121805#ruleconfig) |Yes |Refer to the request example. |Throttling configuration. Supports concurrency throttling and QPS throttling. |
|Action |String |Yes |reject |Handling method adopted after the throttling rule threshold is exceeded. Values:<br><br><br>* `reject`: Requests are rejected directly. Supported only for QPS throttling.<br><br>* `queue`: Requests are queued for execution. Supported only for concurrency throttling. |
|NodeType |String |Yes |Primary |Nodes where the rule takes effect. Values:<br><br><br>* `Primary`: Primary node.<br><br>* `Standby`: Secondary node.<br><br>* `all`: All nodes. |
|Enabled |Boolean |No |true |Whether to enable the rule after creation. Values:<br><br><br>* `yes`: yes. Default value.<br><br>* `false`: no. |
|Comment |String |No |Limit QPS concurrency |Comment of the throttling rule. The maximum length is 256 characters. |
|SearchPath |String |No |public |Search_path used to calculate the queryId corresponding to SQL text when the throttling rule matches by SQL fingerprint. The default value is `"$user",public`, with a maximum length of 256 characters. |

### RuleMatch

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |query_string |Match type. Values:<br><br><br>* `query_string`: Match by SQL fingerprint.<br><br>* `keywords`: Match by keywords.<br><br>* `all`: Match all SQL. |
|Keywords |Array of String |No |["qps_query"] |Keywords. The array supports a maximum of 512 elements, and each keyword cannot exceed 256 characters in length.<br><br>> **tip**<br><br><br>> This parameter is required only when the `Type` parameter is `keywords`.<br> |
|QueryString |String |No |SELECT \* FROM demo |SQL text.<br><br>> **tip**<br><br><br>> This parameter is required only when the `Type` parameter is `query_string`.<br> |

### RuleConfig

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |qps |The type of SQL throttling rule. Values:<br><br><br>* `concurrency`: Concurrency throttling.<br><br>* `qps`: QPS throttling. |
|QPS |Integer |No |100 |The number of requests allowed per second. Value range: 0 ~ 100000.<br><br>> **tip**<br><br><br><br>* > This parameter is required only when the `Type` parameter is `qps`.<br><br><br>* > When `RuleMatch.Type` is set to `all`, the value of this parameter must be greater than 1.<br> |
|Burst |Integer |No |200 |Token Bucket capacity. Value range: 1 ~ 100000.<br><br>> **tip**<br><br><br>> This parameter is required only when the `Type` parameter is `qps`.<br> |
|MaxWaitMs |Integer |No |1000 |Maximum waiting time. The default value is `0`, which means no waiting time limit. Unit: millisecond. Value range: 0 ~ 864000000.<br><br>> **tip**<br><br><br>> This parameter is required only when the `Type` parameter is `concurrency`.<br> |
|MaxWaiting |Integer |No |20 |Maximum pending queue count. Value range: 0 ~ 100000.<br><br>> **tip**<br><br><br>> This parameter is required only when the `Type` parameter is `concurrency`.<br> |
|MaxConcurrency |Integer |No |10 |Maximum concurrency. Value range: 0 ~ 100000.<br><br>> **tip**<br><br><br><br>* > This parameter is required only when the `Type` parameter is `concurrency`.<br><br><br>* > When `RuleMatch.Type` is set to `all`, the value of this parameter must be greater than 1.<br> |

## Response parameters

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Code |Integer |0 |Return status code. `0` means succeeded. |
|Message |String |success |Return information. |
|RuleId |Long |136734987028564xxxx |Rule ID of the SQL throttling rule. |

## Sample

### Sample request

```json
POST /?Action=CreateSQLConcurrencyControlRule&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-5d27abexxxx",
    "DatabaseName": "pg_demo",
    "Match": {
        "Type": "query_string",
        "Keywords": [
            "qps_query"
        ],
        "QueryString": "SELECT * FROM demo"
    },
    "Limit": {
        "QPS": 100,
        "Type": "qps",
        "Burst": 200,
        "MaxWaitMs": 1000,
        "MaxWaiting": 20,
        "MaxConcurrency": 10
    },
    "Action": "reject",
    "NodeType": "Primary",
    "Enabled": true,
    "Comment": "限制 QPS 并发",
    "SearchPath": "public"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSQLConcurrencyControlRule",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "RuleId": "136734987028564xxxx"
    }
}
```
