---
title: "DescribeSqlConcurrencyControlRules"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeSqlConcurrencyControlRules"
---

Call the DescribeSqlConcurrencyControlRules API to query all SQL throttling tasks for a database instance.

<span id="kuNS3XXL"></span>
## Request type

Synchronous request

<span id="UQnfrNP4"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String |Yes |mysql\-383906\*\*\*\*\*\* |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) operation to query the instance ID of NDB MySQL. |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL. |
|RegionId |String |Yes |cn\-beijing |Region ID. |
|PageNumber |Integer |No |1 |Page number. The value range is 1 to 1,000, with a default of 1. |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1,000, with a default of 10. |
|SortBy |String |No |DESC |The query results are sorted by task creation time. Valid values are as follows:<br><br><br>* `ASC`: ascending order.<br><br>* `DESC`: (default) descending order. |


<span id="2sImw5XJ"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Number of SQL throttling tasks. |
|RuleDetails |Array of [RuleDetail](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#searchparam) |```JSON```<br>```[```<br>```    {```<br>```        "ConcurrencyCount": 0,```<br>```        "CreateTime": "2026-10-08T08:41:50Z",```<br>```        "KeyWord": "select~from~test",```<br>```        "RejectCount": 0,```<br>```        "RemainingTime": 0,```<br>```        "RuleState": "DONE",```<br>```        "SqlType": "UPDATE",```<br>```        "TaskId": "2108115634582761472",```<br>```        "TerminationType": "Auto",```<br>```        "ThrottleTarget": "MaxConcurrencyCount"```<br>```    }```<br>```]```<br> |SQL throttling task list. |


<span id="ccFLTSTf"></span>
## Request example

```JSON
POST /?Action=DescribeSqlConcurrencyControlRules&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "PageSize": 10,
    "InstanceId": "mysql-383906******",
    "InstanceType": "MySQL",
    "PageNumber": 1,
    "SortBy": "DESC",
    "RegionId":"cn-beijing"
}
```


<span id="iCVnCEfl"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026100816543635BFEF6A64C554080C4A-1f3749",
        "Action": "DescribeSqlConcurrencyControlRules",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "RuleDetails": [
            {
                "ConcurrencyCount": 0,
                "CreateTime": "2026-10-08T08:41:50Z",
                "KeyWord": "select~from~test",
                "RejectCount": 0,
                "RemainingTime": 0,
                "RuleState": "DONE",
                "SqlType": "UPDATE",
                "TaskId": "2108115634582761472",
                "TerminationType": "Auto",
                "ThrottleTarget": "MaxConcurrencyCount"
            }
        ],
        "Total": 1
    }
}
```


<span id="80J72AlM"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes?_vtm_=a106466.b106468.0_0.0_0.0.4527_7694130500017817107&lang=en).
