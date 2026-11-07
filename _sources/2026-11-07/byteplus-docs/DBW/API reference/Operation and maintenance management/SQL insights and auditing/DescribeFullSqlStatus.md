---
title: "DescribeFullSqlStatus"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeFullSqlStatus"
---

Call the DescribeFullSqlStatus API to query the full SQL enablement status, feature status, and subscription configuration of the specified instance.

<span id="DJxvKRhF"></span>
## Request type

Synchronous request

<span id="xtLwFWrI"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|FollowInstanceID |String |Yes |mysql\-fcfc2c\*\*\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances?lang=en">DescribeDBInstances</a> API to query the instance ID of veDB MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for PostgreSQL.</div><br> |
|DSType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL. |
|RegionId |String |Yes |cn\-beijing |Region ID. |


<span id="Y5DfLWRC"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DetailStatus |String |RUN |SQL Audit details feature status. The values are as follows:<br><br><br>* `RUN`: SQL insight is enabled.<br><br>* `STARTING`: SQL insight is being enabled.<br><br>* `CLOSE`: Indicates that SQL audit details are disabled.<br><br>* `DELETE`: Indicates that SQL audit details are being deleted.<br><br>* `MODIFYING`: Indicates that SQL audit details are being modified. |
|BusinessStatus |String |InstanceBusinessRunning<br><br> |Billing status. The values are as follows:<br><br><br>* `InstanceBusinessPending`: Waiting for payment.<br><br>* `InstanceBusinessRunning`: Billing instance in progress. |
|SqlAnalysisFunStatus |String |RUN |SQL insight feature state. The values are as follows:<br><br><br>* `RUN`: SQL insight is enabled.<br><br>* `STARTING`: SQL insight is being enabled.<br><br>* `CLOSE`: SQL insight is disabled.<br><br>* `DELETE`: SQL insight is being deleted.<br><br>* `MODIFYING`: SQL insight is being modified. |
|InstanceID |String |DBW_FullSql_ed82b2b4\-b985\-4861\-b19d\-e0d2bd\*\*\*\*\*\* |Full SQL service instance ID. |
|EnableFunctions |RegionEnableFunctions<br><br> |```JSON```<br>```{```<br>```    "EnableHierarchicalStorage": true,```<br>```    "SQLAuditDetail": true,```<br>```    "SQLInsight": true```<br>```}```<br> |The collection of features currently enabled for the full SQL instance. |
|SqlRetentionDay |Integer |30 |SQL data storage duration. |
|CustomStorageSqlMethods |Array of string |```JSON```<br>```[```<br>```    "SELECT",```<br>```    "INSERT"```<br>```]```<br> |SQL types that are collected and stored.<br><br>Values include: `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `ALTER`, `CREATE`, `DROP`, `RENAME`, `TRUNCATE`, `OTHER`.<br><br> |
|HotStorageDays |Integer |7 |Standard storage days. The value range is 1 to 1095. |
|ColdStorageDays |Integer |23 |Infrequent\-access retention period, ranging from 30 to 3648 days. Default value: 30. |


<span id="UHViOxBn"></span>
## Request example

```JSON
POST /?Action=DescribeFullSqlStatus&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "FollowInstanceID": "mysql-fcfc2c******",
    "DSType": "MySQL",
    "RegionId": "cn-beijing"
}
```


<span id="NxaD9g92"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260824153433A83D2926F422A237031E-cee933",
        "Action": "DescribeFullSqlStatus",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "ArchiveStorageDays": 0,
        "BusinessStatus": "InstanceBusinessPending",
        "ColdStorageDays": 30,
        "CustomStorageSqlMethods": [
            "SELECT",
            "INSERT",
            "UPDATE",
            "DELETE",
            "ALTER",
            "CREATE",
            "DROP",
            "RENAME",
            "TRUNCATE",
            "OTHER"
        ],
        "DetailStatus": "RUN",
        "EnableFunctions": {
            "EnableHierarchicalStorage": true,
            "SQLAuditDetail": true,
            "SQLInsight": true
        },
        "HotStorageDays": 1,
        "InstanceID": "DBW_FullSql_43******-ac6e-4199-bf2b-c38dbec672c7",
        "InstanceStatus": "InstanceStatusPending",
        "SqlAnalysisFunStatus": "RUN",
        "SqlRetentionDay": 31
    }
}
```


<span id="hJGQPO2m"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
