---
title: "GetAppAlarmTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmTrend"
---

Get the app alert trend.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppAlarmTrend&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppAlarmTrend |The API name. The current API name is `GetAppAlarmTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|aid |Long |Yes |123456 |Application ID. |
|monitor_types |Array of String |No |["crash"] |Monitoring type.<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* app_page_js_err: Page monitoring / JS error<br><br>* app_page_ajax_err: Page monitoring / Request error<br><br>* app_page_perf: Page monitoring / Performance<br><br>* app_event: Event alert<br><br>* net_err: Network error<br><br>* custom_exception: Custom error<br><br>* traffic_exception: Traffic<br><br>* disk_exception: Disk<br><br>* battery_trace: Battery<br><br>* cpu_exception：CPU |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67876#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|start_time |Long |Yes |1665417600 |Start time. |
|end_time |Long |Yes |1666417600 |The end time. |
|granularity |Long |Yes |1440 |The aggregation granularity. Unit: minutes. |
|group_by_field |String |No |rule_id |The grouping field. An empty string is passed if no grouping is required. |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67876#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppAlarmTrend&Version=2022-10-12
{
    "aid": 123456,
    "start_time": 1665417600,
    "end_time": 1666417600,
    "granularity": 1440,
    "monitor_types": [
        "crash"
    ],
    "filters": {
        "sub_conditions": [
            {
                "op": "in",
                "values": [
                    "717"
                ],
                "type": "expression",
                "dimension": "aid"
            }
        ],
        "type": "expression"
    },
    "group_by_field": "rule_id"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [TrendLine](https://docs.byteplus.com/en/docs/299/67876#trendline) |\- |Alert trend. |
|error_msg |String |\- |Error message. It is empty if the request succeeds. |
|error_no |Long |0 |Error code. If the request was successful, its value is 0. |


<span id="trendline"></span>
### TrendLine


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |"test |The name of the line. When grouped, the name needs to be set to the value of the grouping dimension. For example, it is used as the legend label for the curve. |
|points |Array of [TrendPoint](https://docs.byteplus.com/en/docs/299/67876#trendpoint) |\- |The data points on the curve. |


<span id="trendpoint"></span>
### TrendPoint


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|value |Double |0 |The metric value. |
|timestamp |Long |1653696000 |The time when the metric occurred (Unix timestamp). |
|readable_timestamp |String |2022\-05\-28 08:00:00 |The time when the metric occurred (natural time). |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "err_detail":"",
    "error_msg": "",
    "error_no": 0,
    "data": [
        {
            "name": "test",
            "points": [
                {
                    "readable_timestamp": "2022-05-28 08:00:00",
                    "timestamp": 1653696000,
                    "value": 915
                }
            ]
        }
    ]
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
