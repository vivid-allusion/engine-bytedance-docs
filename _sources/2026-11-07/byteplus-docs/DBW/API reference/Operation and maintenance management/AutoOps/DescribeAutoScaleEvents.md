---
title: "DescribeAutoScaleEvents"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeAutoScaleEvents"
---

Call the DescribeAutoScaleEvents API to query scaling events for a specified instance.

<span id="9hWGlIe6"></span>
## Request type

Synchronous request

<span id="Q64camW6"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceType |String |Yes |Postgres |Database type. Currently, only the value `Postgres` is supported, indicating RDS for PostgreSQL. |
|InstanceId |String |Yes |postgres\-5d1\*\*\*\*\*\*<br><br> |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance IDs of all RDS for PostgreSQL instances in the target region.</div><br> |
|RegionId |String |Yes |cn\-guangzhou |Region ID. |
|Metric |String |Yes |Disk<br><br> |Scaling indicator. Currently, only disk scaling out is supported, meaning this parameter takes the value `Disk`. |
|autoScaleSearchParam |[AutoScaleSearchParam](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#1yPwSTwc) |No |```JSON```<br>```{```<br>```    "StartTime": 1787638268,```<br>```    "EndTime": 1787640068```<br>```}```<br> |Event filter criteria. |
|PageNumber |Integer |No |1 |Page number. The value range is 1 to 1,000, with a default of 1. |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1,000, with a default of 10. |


<span id="U4KvG8sG"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Total |Integer |10 |Total number of scaling events. |
|AutoScaleEvents |Array of [AutoScaleEvent](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#FIXkJjAD)<br><br> |```JSON```<br>```[```<br>```    {```<br>```        "Action": "Expand",```<br>```        "After": "0G",```<br>```        "AfterAutoScale": 0,```<br>```        "AutoScaleMetricName": "Disk",```<br>```        "Before": "300G",```<br>```        "BeforeAutoScale": 0,```<br>```        "EndTime": "2026-08-25T06:30:44Z",```<br>```        "EventId": "2092137580354129920",```<br>```        "EventStatus": "EventScaling",```<br>```        "Memo": "",```<br>```        "MetricUnit": "%",```<br>```        "RuleId": "2031045967368716288",```<br>```        "RuleType": "Auto",```<br>```        "StartTime": "2026-08-25T06:30:44Z",```<br>```        "TriggerCondition": [```<br>```            {```<br>```                "ComparisonOperator": "\u003e",```<br>```                "MetricName": "磁盘使用率",```<br>```                "Threshold": "90.00%",```<br>```                "TimeInfo": ""```<br>```            }```<br>```        ],```<br>```        "TriggerInfo": "",```<br>```        "TriggerValue": "100.26%"```<br>```    }```<br>```]```<br> |Scaling event list. |


<span id="yombBfQO"></span>
## Request example

```JSON
POST /?Action=DescribeAutoScaleEvents&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "InstanceType": "Postgres",
    "PageSize": 10,
    "PageNumber": 1,
    "RegionId": "cn-beijing",
    "Metric": "ALL",
    "InstanceId": "postgres-e6a7239edcab",
    "AutoScaleSearchParam": {
        "StartTime": 1787638268,
        "EndTime": 1787640068
    }
}
```


<span id="YzCZcPMT"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260825144108880EAD48C32456E4DA8C-e74a6d",
        "Action": "DescribeAutoScaleEvents",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "AutoScaleEvents": [
            {
                "Action": "Expand",
                "After": "0G",
                "AfterAutoScale": 0,
                "AutoScaleMetricName": "Disk",
                "Before": "300G",
                "BeforeAutoScale": 0,
                "EndTime": "2026-08-25T06:30:44Z",
                "EventId": "2092137580354129920",
                "EventStatus": "EventScaling",
                "Memo": "",
                "MetricUnit": "%",
                "RuleId": "2031045967368716288",
                "RuleType": "Auto",
                "StartTime": "2026-08-25T06:30:44Z",
                "TriggerCondition": [
                    {
                        "ComparisonOperator": "\u003e",
                        "MetricName": "磁盘使用率",
                        "Threshold": "90.00%",
                        "TimeInfo": ""
                    }
                ],
                "TriggerInfo": "",
                "TriggerValue": "100.26%"
            }
        ],
        "Total": 1
    }
}
```


<span id="T5Hzi36p"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
