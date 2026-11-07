---
title: "CreateSqlKillRule"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/createSqlKillRule"
---

Call the CreateSqlKillRule API to create a persistent Kill task.

<span id="D6N50heA"></span>
## Request type

Synchronous request

<span id="M0txzXQK"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String |Yes |mysql\-80d3af\*\*\*\*\*\*<br><br> |Database instance ID<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the instance ID of NDB for MySQL.</div><br> |
|InstanceType |String |Yes |MySQL<br><br> |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `veDBMySQL`: NDB for MySQL. |
|SqlType |Array of String |Yes |["select", "update", "delete", "insert"] |List of SQL types to be killed. Supported SQL types include `select`, `update`, `delete`, and `insert`. |
|NodeType |Array of String |Yes |["Primary", "ReadOnly"] |List of node types to be killed. Supported node types include `Primary node` and `Read-only node`. |
|MaxExecTime |Integer |Yes |1 |SQL execution time, indicating SQL requests exceeding this duration will be killed. The unit is second(s), with a valid range from 1 to 9,999. |
|EffectiveTime |Integer |Yes |3600 |Task duration, indicating that after the persistent Kill task reaches this duration, it will be automatically closed. The unit is second(s), with a valid range from 1 to 99,999,999. |


<span id="y6ayV2GV"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|TaskId |Integer |2007653765569\*\*\*\*\*\* |Persistent Kill task ID. |


<span id="SFW12JLY"></span>
## Request example

```JSON
POST https://dbw.volcengineapi.com/?Action=CreateSqlKillRule&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
  "InstanceID": "mysql-80d3af******",
  "InstanceType": "MySQL",
  "SqlType": ["select", "update", "delete", "insert"],
  "NodeType": ["Primary", "ReadOnly"],
  "MaxExecTime": 1,
  "EffectiveTime": 3600
}
```


<span id="STEE3lFg"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202601041122120087DEC5225528237576-ad00ab",
        "Action": "CreateSqlKillRule",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "TaskId": 2007653765569601536
    }
}
```


<span id="33zHDkty"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
