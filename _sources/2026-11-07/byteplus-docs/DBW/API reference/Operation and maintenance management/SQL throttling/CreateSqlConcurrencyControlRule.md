---
title: "CreateSqlConcurrencyControlRule"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/CreateSqlConcurrencyControlRule"
---

Call the CreateSqlConcurrencyControlRule API to create a SQL throttling task.

<span id="MHzpcNH0"></span>
## Request type

Synchronous request

<span id="f51l1bHw"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String |Yes |mysql\-383906\*\*\*\*\*\* |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API to query the instance ID of NDB MySQL. |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL. |
|RegionId |String |Yes |cn\-beijing |Region ID. |
|ThrottleTarget |String |Yes |MaxConcurrencyCount |Rate limiting object. Currently, only `MaxConcurrencyCount` is supported, which indicates SQL keyword\-based rate limiting. |
|KeyWords |String |Yes |select~from~test |SQL keywords.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DBW/DescribeSqlKeywords?TagIDs=2&lang=en">DescribeSqlKeywords</a> operation to generate SQL keywords.</div><br> |
|SqlType |String |Yes |SELECT |SQL types that require rate limiting include `SELECT`, `UPDATE`, `DELETE`, `INSERT`, and `REPLACE`. |
|TerminationType |String |Yes |Manual |End of task for the SQL throttling task. Valid values:<br><br><br>* `Manual`: Manually end the throttling task.<br><br>* `Auto`: Automatically end the throttling task. |
|ConcurrencyCount |Integer |Yes |1 |Maximum concurrency for SQL statements on each node, with a value range of 0 to 99999.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>ConcurrencyCount</code> is 0, execution of matching SQL statements is prohibited.</div><br> |
|EffectiveTime |Integer |No |10<br><br> |Throttling time for the SQL throttling task. Valid range: 1 to 9,999,999 minutes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the <code>TerminationType</code> parameter is set to <code>Auto</code>.</div><br> |


<span id="086EU2k1"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|RuleId |Integer |2108098738466619392 |SQL throttling task ID. |


<span id="Umqzj9PK"></span>
## Request example

```JSON
POST /?Action=CreateSqlConcurrencyControlRule&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "TerminationType": "Auto",
    "ConcurrencyCount": 1,
    "ThrottleTarget": "MaxConcurrencyCount",
    "SqlType": "SELECT",
    "KeyWords": "select~from~test",
    "InstanceId": "mysql-383906******",
    "InstanceType": "MySQL",
    "EffectiveTime": 10,
    "RegionId":"cn-beijing"
}
```


<span id="sLBbA4wV"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20261008153440FDEC164725BAFD66357F-c1e95d",
        "Action": "CreateSqlConcurrencyControlRule",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "RuleId": 2108098738466619392
    }
}
```


<span id="KY1pQUXK"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes?_vtm_=a106466.b106468.0_0.0_0.0.4527_7694130500017817107&lang=en).
