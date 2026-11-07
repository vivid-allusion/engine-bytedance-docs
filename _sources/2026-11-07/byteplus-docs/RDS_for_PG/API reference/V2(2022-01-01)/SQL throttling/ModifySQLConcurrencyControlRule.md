---
title: "ModifySQLConcurrencyControlRule"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/ModifySQLConcurrencyControlRule"
---

Call the ModifySQLConcurrencyControlRule API to modify SQL throttling rules.

## Request type

Asynchronous request.

## Precautions

Only PostgreSQL 14 to PostgreSQL 17 instances created on or after October 15, 2026 support modifying SQL throttling rules.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-5d27abexxxx |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) API to query the instance ID.<br> |
|DatabaseName |String |Yes |pg_demo |Target database name. |
|RuleId |Long |Yes |136734987028564xxxx |Rule ID of the SQL throttling rule. |
|Limit |Object of [RuleConfig](https://docs.byteplus.com/en/docs/61/121808#ruleconfig) |Yes |Refer to the request example. |New throttling configuration. |

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

## Sample

### Sample request

```json
POST /?Action=ModifySQLConcurrencyControlRule&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-5d27abexxxx",
    "DatabaseName": "pg_demo",
    "RuleId": 136734987028564,
    "Limit": {
        "QPS": 100,
        "Type": "qps",
        "Burst": 200,
        "MaxWaitMs": 1000,
        "MaxWaiting": 20,
        "MaxConcurrency": 10
    }
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifySQLConcurrencyControlRule",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Code": 0,
        "Message": "success"
    }
}
```
