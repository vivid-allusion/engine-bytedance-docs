---
title: "GetAppBatteryTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryTrend"
---

Get trends of foreground current and battery temperature related to app power consumption.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppBatteryTrend&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppBatteryTrend |The API name. The current API name is `GetAppBatteryTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |No |1617225600 |Query start time (Unix timestamp). |
|end_time |Integer |No |1617312000 |Query end time (Unix timestamp). |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67907#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|granularity |Integer |No |5 |Aggregation granularity, in minutes. |
|metrics |String |No |battery_electric |Metric name to query |
|statistic_scale |String |No |avg |Statistical scope.<br><br><br>* avg<br><br>* pct25<br><br>* pct50<br><br>* pct75<br><br>* pct90<br><br>* pct99 |
|scene |String |No |main_activity |Page name. |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67907#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppBatteryTrend&Version=2022-10-12
{
    "start_time": 1617225600,
    "end_time": 1617312000,
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
    "granularity": 5,
    "metrics": "battery_electric",
    "statistic_scale": "avg",
    "scene": "main_activity"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [TrendLine](https://docs.byteplus.com/en/docs/299/67907#trendline) |\- |For requests without grouping, the list contains only one element. With grouping enabled, there are multiple elements, each representing a line. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="trendline"></span>
### TrendLine


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |test123 |The name of the line. When grouped, the name needs to be set to the value of the grouping dimension. For example, it is used as the legend label for the curve. |
|points |Array of [TrendPoint](https://docs.byteplus.com/en/docs/299/67907#trendpoint) |\- |The data points on the curve. |
|total |Double | |The total count. |


<span id="trendpoint"></span>
### TrendPoint


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alert |Object of [AlertPoint](https://docs.byteplus.com/en/docs/299/67907#alertpoint) |\- |The alert message. |
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
    "data": [
        {
            "name": "test123",
            "points": [
                {
                    "alert": {
                        "alert": "true",
                        "msg": "No error"
                    },
                    "value": 123,
                    "timestamp": 1665417600,
                    "readable_timestamp": "2022-10-11"
                }
            ]
        }
    ],
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
