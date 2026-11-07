---
title: "DeleteSQLConcurrencyControlRule"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/DeleteSQLConcurrencyControlRule"
---

Call the DeleteSQLConcurrencyControlRule API to delete SQL throttling rules.

## Request type

Asynchronous request.

## Precautions

Only PostgreSQL 14 to PostgreSQL 17 instances created on or after October 15, 2026 support deleting SQL throttling rules.

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-5d27abexxxx |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) API to query the instance ID.<br> |
|DatabaseName |String |Yes |pg_demo |Target database name. |
|RuleId |Long |Yes |136734987028564xxxx |Rule ID of the SQL throttling rule. |

## Response parameter

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Code |Integer |0 |Return status code. `0` means succeeded. |
|Message |String |success |Return information. |

## Sample

### Sample request

```json
POST /?Action=DeleteSQLConcurrencyControlRule&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-5d27abexxxx",
    "DatabaseName": "pg_demo",
    "RuleId": "136734987028564xxxx"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteSQLConcurrencyControlRule",
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
