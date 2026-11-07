---
title: "ListTables"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/ListTables"
---

Call the ListTables API to query the table list in the database of the instance.

<span id="iI42zNJA"></span>
## Request type

Synchronize request.

<span id="l1UWaEEp"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceID |String |Yes |mysql\-bf120f\*\*\*\*\*\* |Database instance ID<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the instance ID of veDB for MySQL.</div><br> |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL. |
|Database |String |Yes |mysql |Database name. |
|PageNumber |Integer |Yes |1 |Page number. |
|PageSize |Integer |Yes |20 |Page size. |


<span id="1wCKC0vB"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Total |Integer<br><br> |3<br><br> |Total number of tables |
|Items |Array of String |["city", "department", "employee"] |Table name list. |


<span id="MQ2g3HHl"></span>
## Request example

```JSON
POST /?Action=ListTables&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
  "InstanceID": "mysql-bf120f******",
  "InstanceType": "MySQL",
  "Database": "company",
  "PageNumber": 1,
  "PageSize": 20
}
```


<span id="74BWSu71"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202511271804411DE3182D312FB6E2F51A-d6730c",
        "Action": "ListTables",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            "city",
            "department",
            "employee"
        ],
        "Total": 3
    }
}
```


<span id="n1bQk4rF"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
