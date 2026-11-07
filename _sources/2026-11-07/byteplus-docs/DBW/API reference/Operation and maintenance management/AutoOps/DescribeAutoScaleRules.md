---
title: "DescribeAutoScaleRules"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeAutoScaleRules"
---

Call the DescribeAutoScaleRules API to query the automatic or scheduled scaling configuration of an instance.

<span id="qNY9yCzf"></span>
## Request type

Synchronous request

<span id="pPW82LIp"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceType |String |Yes |Postgres |Database type. Currently, only `Postgres` is supported, which represents RDS for PostgreSQL. |
|InstanceId |String |Yes |postgres\-5d1\*\*\*\*\*\*<br><br> |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en">DescribeDBInstances</a> operation to query the instance IDs of all RDS for PostgreSQL instances in the target region.</div><br> |
|RegionId |String |Yes |cn\-beijing |Region. |
|Metric |String<br><br> |Yes |Disk<br><br> |Scaling indicator. Currently, only disk scaling out is supported, meaning the parameter value is `Disk`. |


<span id="ncRyu7Bg"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|InstanceId |String |postgres\-5d1\*\*\*\*\*\* |Instance ID. |
|ObservationWindow |Integer |5 |Observation window. |
|Configs |Array of [RuleConfig](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#DESUz5I5) |```JSON```<br>```[```<br>```    {```<br>```        "Action": "Expand",```<br>```        "IsOpen": true,```<br>```        "MaintainWindow": 0,```<br>```        "ScalingLimit": 3000,```<br>```        "Step": 0,```<br>```        "Threshold": 10```<br>```    }```<br>```]```<br> |Automatic rule configuration.<br><br> |
|RuleType |String |Auto<br><br> |Rule type. The values are as follows:<br><br><br>* `Auto`: Indicates an automatic rule.<br><br>* `Cron`: Indicates a scheduled rule. |


<span id="vK9GJUyY"></span>
## Request example

```JSON
POST /?Action=DescribeAutoScaleRules&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "InstanceType": "Postgres",
    "InstanceId": "postgres-5d1******",
    "RegionId": "cn-beijing",
    "Metric": "Disk"
}
```


<span id="7623VKsc"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202609041711503D56EF7E0EEAED9BA027-3a3caf",
        "Action": "DescribeAutoScaleRules",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "Configs": [
            {
                "Action": "Expand",
                "IsOpen": true,
                "MaintainWindow": 0,
                "ScalingLimit": "jdbc:mysql:*****8",
                "Step": 0,
                "Threshold": 10
            }
        ],
        "InstanceId": "postgres-5d1******",
        "ObservationWindow": 5
    }
}
```


<span id="tjKjQG3Y"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
