---
title: "GetAppCPUTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppCPUTrend"
---

Get trends of CPU metrics.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppCPUTrend&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppCPUTrend |The API name. The current API name is `GetAppCPUTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |No |1619827200 |Start time (Unix timestamp). |
|end_time |Integer |No |1619913600 |End time (Unix timestamp). |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67898#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|granularity |Integer |No |60 |Data granularity. For example, '60' indicates minute\-level granularity. |
|biz_type |String |No |cpu |Business type.<br><br><br>* cpu: CPU metric<br><br>* cpu_thread: CPU anomaly |
|metric |String |No |crash_count |CPU metric. |
|scales |Array of String |No |["avg", "pct95", "pct95"] |Statistical metric.<br><br><br>* avg: Average value<br><br>* pct25: 25th percentile value<br><br>* pct50: 50th percentile value<br><br>* pct70: 70th percentile value<br><br>* pct90: 90th percentile value<br><br>* pct95: 95th percentile value |


<span id="condition"></span>
### Condition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |The operator.<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|type |String |No |expression |The type of the filter condition.<br><br><br>* expression: The current condition is an expression.<br><br>* and: The current condition is a compound expression, and multiple sub\-conditions are in an AND logical relationship.<br><br>* or: The current condition is a compound expression, and multiple sub\-conditions are in an OR logical relationship.<br><br>* map: The current condition is of map type. |
|value |String |No |123456 |The filter value. |
|values |Array of String |No |[123456] |The filter value. Multiple filter values are supported. |
|map_key |String |No |key_1 |The key of the map type. It is required when the type is set to map. |
|dimension |String |No |aid |The name of the condition. |
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67898#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppCPUTrend&Version=2022-10-12
{
    "start_time": 1619827200,
    "end_time": 1619913600,
    "filters": {
        "type": "and",
        "sub_conditions": [
            {
                "dimension": "apm_version",
                "type": "expression",
                "op": "in",
                "values": [
                    "1.4.5"
                ]
            },
            {
                "dimension": "device_model",
                "type": "expression",
                "op": "in",
                "values": [
                    "MI 5X"
                ]
            }
        ]
    },
    "granularity": 60,
    "biz_type": "cpu",
    "metric": "crash_count",
    "scales": [
        "avg"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [MultiTrendResponseData](https://docs.byteplus.com/en/docs/299/67898#multitrendresponsedata) |\- |Returned data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="multitrendresponsedata"></span>
### MultiTrendResponseData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|use_rate |JSON Map |\- |User utilization. |
|sample_cnt |Object of [TrendLine](https://docs.byteplus.com/en/docs/299/67898#trendline) |\- |Metric trend. |
|sample_total |Integer |100 |Total sample size. |
|use_rate_avg |Double |0.5 |Average value. |


<span id="userate"></span>
### UseRate


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |metric |Metric key. |
|value |Object of [TrendLine](https://docs.byteplus.com/en/docs/299/67898#trendline) |\- |Sample size. |


<span id="trendline"></span>
### TrendLine


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |test123 |The name of the line. When grouped, the name needs to be set to the value of the grouping dimension. For example, it is used as the legend label for the curve. |
|points |Array of [TrendPoint](https://docs.byteplus.com/en/docs/299/67898#trendpoint) |\- |The data points on the curve. |
|total |Double |10 |The total count. |


<span id="trendpoint"></span>
### TrendPoint


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alert |Object of [AlertPoint](https://docs.byteplus.com/en/docs/299/67898#alertpoint) |\- |The alert message. |
|value |Double |123 |The metric value. |
|timestamp |Long |1665417600 |The time when the metric occurred (Unix timestamp). |
|readable_timestamp |String |2022\-10\-11 |The time when the metric occurred (natural time). |


<span id="alertpoint"></span>
### AlertPoint


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|msg |String |No error |The alert message. |
|alert |Boolean |true |Whether an alert is required. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": {
        "use_rate": {
            "key": "avg"
        },
        "sample_cnt": {
            "name": "test123",
            "points": [
                {
                    "alert": "-",
                    "value": 123,
                    "timestamp": 1665417600,
                    "readable_timestamp": "2022-10-11"
                }
            ]
        },
        "sample_total": 100,
        "use_rate_avg": 0.5
    },
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
