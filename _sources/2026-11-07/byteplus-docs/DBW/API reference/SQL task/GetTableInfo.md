---
title: "GetTableInfo"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/GetTableInfo"
---

Call the GetTableInfo API to query table metadata of the database instance.

<span id="seWcg2YW"></span>
## Request type

Synchronize request.

<span id="5jUHPMPs"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceID |String |Yes |mysql\-bf120f\*\*\*\*\*\* |Database instance ID<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the instance ID of veDB for MySQL.</div><br> |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL. |
|Database |String |Yes |company |Database name. |
|Table |String |Yes |employee |Table name. |


<span id="QOcrqgAg"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|TableMeta |TableMeta |[TableMeta](https://docs.byteplus.com/en/docs/DBW/data-structure#uJS3af4g) |Table meta information. |


<span id="iE0NwXdp"></span>
## Request example

```JSON
POST /?Action=GetTableInfo&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
  "InstanceID": "mysql-bf120f******",
  "InstanceType": "MySQL",
  "Database": "company",
  "Table": "employee"
}
```


<span id="RXeBiwAq"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025112718185428251AE9D8163504FCB4-a543ea",
        "Action": "GetTableInfo",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "TableMeta": {
            "CharacterSet": "utf8mb4",
            "Collations": "utf8mb4_general_ci",
            "Columns": [
                {
                    "AllowBeNull": false,
                    "Comment": "",
                    "IsAutoIncrement": true,
                    "IsPrimaryKey": true,
                    "Length": "11",
                    "Name": "id",
                    "PrimaryKeyOrder": "1",
                    "Type": "bigint"
                },
                {
                    "AllowBeNull": false,
                    "Comment": "",
                    "IsAutoIncrement": false,
                    "IsPrimaryKey": false,
                    "Length": "60",
                    "Name": "name",
                    "PrimaryKeyOrder": "",
                    "Type": "varchar"
                },
                {
                    "AllowBeNull": false,
                    "Comment": "",
                    "IsAutoIncrement": false,
                    "IsPrimaryKey": false,
                    "Length": "10",
                    "Name": "age",
                    "PrimaryKeyOrder": "",
                    "Type": "smallint"
                },
                {
                    "AllowBeNull": false,
                    "Comment": "",
                    "IsAutoIncrement": false,
                    "IsPrimaryKey": false,
                    "Length": "60",
                    "Name": "city",
                    "PrimaryKeyOrder": "",
                    "Type": "varchar"
                },
                {
                    "AllowBeNull": false,
                    "Comment": "",
                    "IsAutoIncrement": false,
                    "IsPrimaryKey": false,
                    "Length": "60",
                    "Name": "department",
                    "PrimaryKeyOrder": "",
                    "Type": "varchar"
                }
            ],
            "Definition": "CREATE TABLE `employee` (\n  `id` bigint(11) NOT NULL AUTO_INCREMENT,\n  `name` varchar(60) NOT NULL,\n  `age` smallint(10) NOT NULL,\n  `city` varchar(60) NOT NULL,\n  `department` varchar(60) NOT NULL,\n  PRIMARY KEY (`id`)\n) ENGINE=InnoDB AUTO_INCREMENT=16394 DEFAULT CHARSET=utf8mb4",
            "Engine": "InnoDB",
            "Name": "employee",
        }
    }
}
```


<span id="rfUqjNhI"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
