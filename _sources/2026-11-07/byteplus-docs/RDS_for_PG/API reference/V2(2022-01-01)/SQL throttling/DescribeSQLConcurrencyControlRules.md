---
title: "DescribeSQLConcurrencyControlRules"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeSQLConcurrencyControlRules"
---

Call the DescribeSQLConcurrencyControlRules API to view SQL throttling rules.

## Request type

Synchronous request.

## Precautions

Only PostgreSQL 14 to PostgreSQL 17 instances created on or after October 15, 2026 support viewing SQL throttling rules.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-5d27abexxxx |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) API to query the instance ID.<br> |
|DatabaseName |String |Yes |pg_demo |Target database name. |
|MatchType |String |No |keywords |Filter by runtime match type. Values:<br><br><br>* `query_id`。<br><br>* `keywords`。<br><br>* `all`。 |
|QueryId |Long |No |12345 |Filter by `query_id`. |
|QueryString |String |No |SELECT \* FROM |Filter by SQL text, with a minimum length of 1 character. |
|Keywords |Array of String |No |["slow_query"] |Filter by keyword. The array supports a maximum of 512 elements, and each keyword cannot exceed 256 characters in length. |
|LimitType |String |No |concurrency |Filter by throttling type. Values:<br><br><br>* `concurrency`: Concurrency throttling.<br><br>* `qps`: QPS throttling. |
|Action |String |No |reject |Handling method adopted after the throttling rule threshold is exceeded. Values:<br><br><br>* `reject`: Requests are rejected directly. Supported only for QPS throttling.<br><br>* `queue`: Requests are queued for execution. Supported only for concurrency throttling. |
|NodeType |String |No |Primary |Nodes where the rule takes effect. Values:<br><br><br>* `Primary`: Primary node.<br><br>* `Standby`: Secondary node.<br><br>* `all`: All nodes. |
|Enabled |Boolean |No |true |Filter by enabled state. Values:<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. |
|Offset |Integer |No |0 |Pagination offset, the default value is 0. |
|Limit |Integer |No |20 |Page size. The default value is 100, and the value range is 1~100. |

## Response parameter

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Code |Integer |0 |Return status code. `0` means succeeded. |
|Message |String |success |Return information. |
|TotalCount |Long |5 |Total number of rules that meet the filter conditions. |
|Rules |Array of [SQLConcurrencyControlRuleInfo](https://docs.byteplus.com/en/docs/61/121809#sqlconcurrencycontrolruleinfo) |Refer to the sample response. |Rule list returned by the current pagination. |

### SQLConcurrencyControlRuleInfo

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|QPS |Integer |100 |The number of requests allowed per second. |
|Burst |Integer |200 |Token Bucket capacity. |
|Action |String |reject |Handling method adopted after the throttling rule threshold is exceeded. Values:<br><br><br>* `reject`: Requests are rejected directly. Supported only for QPS throttling.<br><br>* `queue`: Requests are queued for execution. Supported only for concurrency throttling. |
|RuleId |Long |136734987028564xxxx |Rule ID of the SQL throttling rule. |
|Status |String |Applied |Whether the running state of the target node is consistent with the `Primary` rule. Values:<br><br><br>* `Pending`.<br><br>* `Applied`.<br><br>* `Failed`. |
|Comment |String |Limit QPS concurrency |Comment of the throttling rule. |
|Enabled |Boolean |true |Whether the rule is enabled. |
|QueryId |Long |12345 |Final match value of the `query_id` rule. |
|Keywords |Array of String |["slow_query"] |`Keyword` array of the keywords rule. The array supports a maximum of 512 elements, and each keyword cannot exceed 256 characters in length. |
|NodeType |String |All |Nodes where the rule takes effect. Values:<br><br><br>* `Primary`: Primary node.<br><br>* `Standby`: Secondary node.<br><br>* `all`: All nodes. |
|CreatedAt |String |2026\-09\-01T00:00:00Z |Rule creation time. |
|LimitType |String |concurrency |Throttling type of the rule. Values:<br><br><br>* `concurrency`: Concurrency throttling.<br><br>* `qps`: QPS throttling. |
|MatchType |String |keywords |Runtime match type. Values:<br><br><br>* `query_id`。<br><br>* `keywords`。<br><br>* `all`。 |
|MaxWaitMs |Integer |1000 |Maximum waiting time for concurrent throttling, unit: millisecond. 0 means no waiting time limit. |
|UpdatedAt |String |2026\-09\-10T00:00:00Z |Rule update time. |
|MaxWaiting |Integer |20 |Maximum pending count for concurrent throttling. |
|SearchPath |String |public |Search_path used to calculate the queryId corresponding to SQL text when the throttling rule matches by SQL fingerprint. |
|QueryString |String |SELECT \* FROM orders |Original SQL used when users create rules via SQL text, for audit and recalculation only. |
|MaxConcurrency |Integer |10 |Maximum concurrency for concurrent throttling. |

## Example

### Sample request

```json
POST /?Action=DescribeSQLConcurrencyControlRules&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-5d27abexxxx",
    "DatabaseName": "pg_demo",
    "MatchType": "keywords",
    "QueryId": 12345,
    "QueryString": "SELECT * FROM",
    "Keywords": [
        ""
    ],
    "LimitType": "concurrency",
    "Action": "reject",
    "NodeType": "Primary",
    "Enabled": true,
    "Offset": 0,
    "Limit": 20
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeSQLConcurrencyControlRules",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "TotalCount": 5,
        "Rules": [
            {
                "QPS": 100,
                "Burst": 200,
                "Action": "reject",
                "RuleId": 136734987028564,
                "Status": "Applied",
                "Comment": "限制 QPS 并发",
                "Enabled": true,
                "QueryId": 12345,
                "Keywords": [
                    "slow_query"
                ],
                "NodeType": "Primary",
                "CreatedAt": "2026-09-01T00:00:00Z",
                "LimitType": "concurrency",
                "MatchType": "keywords",
                "MaxWaitMs": 1000,
                "UpdatedAt": "2026-09-10T00:00:00Z",
                "MaxWaiting": 20,
                "SearchPath": "public",
                "QueryString": "SELECT * FROM orders",
                "MaxConcurrency": 10
            }
        ]
    }
}
```
