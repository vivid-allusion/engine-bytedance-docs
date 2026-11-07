---
title: "ListDatabases"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/ListDatabases"
---

Call the ListDatabases API to query the database list of the instance.

<span id="Pcp3tGzo"></span>
## Request type

Synchronize request.

<span id="epktVLPv"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceID |String |Yes |mysql\-bf120f\*\*\*\*\*\* |Database instance ID<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the instance ID of veDB for MySQL.</div><br> |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL. |
|PageNumber |Integer |Yes |1 |Page number. |
|PageSize |Integer |Yes |20 |Page size. |


<span id="6XemikH7"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Total |Integer<br><br> |5<br><br> |The number of databases in the instance. |
|Items |Array of DatabaseInfo |[DatabaseInfo](https://docs.byteplus.com/en/docs/DBW/data-structure#mnybcxbN) |Database metadata list. |


<span id="kwaF2Kfj"></span>
## Request example

```JSON
POST /?Action=ListDatabases&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
  "InstanceID": "mysql-bf120f******",
  "InstanceType": "MySQL",
  "PageNumber": 1,
  "PageSize": 20
}
```


<span id="KuPaDuDP"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20251127180119BB7A62069093F9370963-6a1de6",
        "Action": "ListDatabases",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "CType": "",
                "CharacterSetName": "utf8",
                "CollationName": "utf8_general_ci",
                "Description": "",
                "IsSystemDB": true,
                "Limit": "",
                "Name": "information_schema"
            },
            {
                "CType": "",
                "CharacterSetName": "utf8",
                "CollationName": "utf8_general_ci",
                "Description": "",
                "IsSystemDB": false,
                "Limit": "",
                "Name": "__recycle_bin__"
            },
            {
                "CType": "",
                "CharacterSetName": "utf8mb4",
                "CollationName": "utf8mb4_general_ci",
                "Description": "",
                "IsSystemDB": false,
                "Limit": "",
                "Name": "company"
            },
            {
                "CType": "",
                "CharacterSetName": "utf8",
                "CollationName": "utf8_general_ci",
                "Description": "",
                "IsSystemDB": true,
                "Limit": "",
                "Name": "mysql"
            },
            {
                "CType": "",
                "CharacterSetName": "utf8",
                "CollationName": "utf8_general_ci",
                "Description": "",
                "IsSystemDB": true,
                "Limit": "",
                "Name": "performance_schema"
            },
            {
                "CType": "",
                "CharacterSetName": "utf8",
                "CollationName": "utf8_general_ci",
                "Description": "",
                "IsSystemDB": true,
                "Limit": "",
                "Name": "sys"
            }
        ],
        "Total": 6
    }
}
```


<span id="7E8c24KR"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
