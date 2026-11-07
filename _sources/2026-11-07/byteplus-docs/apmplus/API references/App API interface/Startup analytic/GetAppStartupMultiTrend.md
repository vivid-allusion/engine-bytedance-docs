---
title: "GetAppStartupMultiTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppStartupMultiTrend"
---

Obtain the trend of application startup analysis.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppStartupMultiTrend&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppStartupMultiTrend |The API name. The API name is `GetAppStartupMultiTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |No |1665417600 |Start time. |
|end_time |Integer |No |1665504000 |The end time. |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67889#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data.<br><br>launch_mode: The application startup mode:<br><br><br>* 1: First start<br><br>* 2: Cold start<br><br>* 3: Hot start<br><br>* 4: Warm start<br><br><br>The operating system:<br><br><br>* Android<br><br>* iOS |
|granularity |Integer |No |5 |The aggregation granularity. Unit: minutes. |
|group_by_field |String |No |os |The grouping field. An empty string is passed if no grouping is required. |
|metrics |Array of String |No |startup_count |The metric list.<br><br><br>* startup_count: The startup count.<br><br>* startup_time_avg: The average startup time.<br><br>* time_pct50: The 50th percentile of startup time.<br><br>* time_pct75: The 75th percentile of startup time.<br><br>* time_pct95: The 95th percentile of startup time.<br><br>* time_pct99: The 99th percentile of startup time. |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67889#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppStartupMultiTrend&Version=2022-10-12
{
    "start_time": 1665417600,
    "end_time": 1665504000,
    "filters": {
        "op": "in",
        "type": "expression",
        "value": "123456",
        "values": [
            123456
        ],
        "map_key": "key_1",
        "dimension": "aid",
        "sub_conditions": []
    },
    "granularity": 5,
    "group_by_field": "os",
    "metrics": [
        ""
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |JSON Map |\- |The returned error data.<br><br>The key is the metric name. For a request without metric grouping, the list contains only one element. When grouping is applied, the list contains multiple elements, and each element represents one line in the trend chart. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="data"></span>
### Data


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String | | |
|value |Array of [TrendLine](https://docs.byteplus.com/en/docs/299/67889#trendline) | | |


<span id="trendline"></span>
### TrendLine


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |test123 |The name of the line. When grouped, the name needs to be set to the value of the grouping dimension. For example, it is used as the legend label for the curve. |
|points |Array of [TrendPoint](https://docs.byteplus.com/en/docs/299/67889#trendpoint) |\- |The data points on the curve. |
|total |Double | |The total count. |


<span id="trendpoint"></span>
### TrendPoint


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alert |Object of [AlertPoint](https://docs.byteplus.com/en/docs/299/67889#alertpoint) |\- |The alert message. |
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
    "data": {},
    "error_msg": "-",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
