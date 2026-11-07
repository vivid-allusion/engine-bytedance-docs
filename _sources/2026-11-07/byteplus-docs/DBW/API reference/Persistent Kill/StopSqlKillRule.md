---
title: "StopSqlKillRule"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/stopsqlkillrule"
---

Call the StopSqlKillRule API to stop persistent Kill tasks.

<span id="H36vEqdU"></span>
## Request type

Synchronous request

<span id="DP11i6IE"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String |Yes |mysql\-80d3af\*\*\*\*\*\*<br><br> |Database instance ID<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the instance ID of NDB for MySQL.</div><br> |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL. |
|TaskId |Array of String |Yes |["2007653765569\*\*\*\*\*\*"] |List of persistent Kill task IDs to stop.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DBW/describesqlkillrules?lang=zh">DescribeSqlKillRules</a> API to query the Kill task ID.</div><br> |


<span id="fks55MOP"></span>
## Response parameters

Null

<span id="eqhQIWTo"></span>
## Request example

```JSON
POST https://dbw.volcengineapi.com/?Action=StopSqlKillRule&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
  "InstanceID": "mysql-80d3afa******",
  "InstanceType": "MySQL",
  "TaskId": ["2007653765569******"]
}
```


<span id="AF0APNTJ"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026010411290402673B62B82953F51102-1e43d4",
        "Action": "StopSqlKillRule",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id="jKcCoRba"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
