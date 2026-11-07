---
title: "DescribeSqlKillRules"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/describesqlkillrules"
---

Call the DescribeSqlKillRules API to query persistent Kill tasks.

<span id="oh7EQHe3"></span>
## Request type

Synchronous request

<span id="FplQu4wI"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String |Yes |mysql\-80d3af\*\*\*\*\*\*<br><br> |Database instance ID<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the instance ID of NDB for MySQL.</div><br> |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL. |
|PageNumber |Integer |No |1 |Page number. The value range is 1 to 1000, with a default of 1. |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1000, with a default of 10. |
|SortBy |String |No |DESC |Results are sorted by task creation time, with the following options:<br><br><br>* `ASC`: Sorts tasks in ascending order by time.<br><br>* `DESC`: (Default) Sorts tasks in descending order by time. |


<span id="Dj1yEW5K"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Number of persistent Kill tasks. |
|SQLKillRules |Arrar of [SQLKillRule](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=zh#uJS3af4g) |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```            "CreateTime": "2025-12-29T07:36:51Z",```<br>```            "EffectiveTime": 60,```<br>```            "MaxExecTime": 1,```<br>```            "NodeType": "Primary,ReadOnly",```<br>```            "RemainingTime": 0,```<br>```            "SqlType": "select,update,insert,delete",```<br>```            "State": "DONE",```<br>```            "TaskId": "2005543523536******",```<br>```            "User": "RootAccount"```<br>```    }```<br>```]```<br> |Persistent Kill task list. |


<span id="gdNpZTO2"></span>
## Request example

```Bash
POST https://dbw.volcengineapi.com/?Action=DescribeSqlKillRules&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
  "InstanceID": "mysql-bf120f******",
  "InstanceType": "MySQL",
  "PageNumber": 1,
  "PageSize": 10,
  "SortBy": "DESC"
}
```


<span id="FanLg97o"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260104114852037F85B8FE7DD31B060A-544aeb",
        "Action": "DescribeSqlKillRules",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "SQLKillRules": [
            {
                "CreateTime": "2025-12-29T07:36:51Z",
                "EffectiveTime": 60,
                "MaxExecTime": 1,
                "NodeType": "Primary,ReadOnly",
                "RemainingTime": 0,
                "SqlType": "select,update,insert,delete",
                "State": "DONE",
                "TaskId": "2005543523536******",
                "User": "RootAccount"
            }
        ],
        "Total": 1
    }
}
```


<span id="pnk5efFb"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
