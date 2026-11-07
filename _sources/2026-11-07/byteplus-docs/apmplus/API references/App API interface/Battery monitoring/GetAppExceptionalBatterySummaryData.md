---
title: "GetAppExceptionalBatterySummaryData"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatterySummaryData"
---

Get app battery metrics.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppExceptionalBatterySummaryData&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppExceptionalBatterySummaryData |The API name. The current API name is `GetAppExceptionalBatterySummaryData`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |No |1619827200 |Current period start time (Unix timestamp). |
|end_time |Integer |No |1619913600 |Current period end time (Unix timestamp). |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67905#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|compare_start_time |Integer |No |1619730800 |Comparison period start time (Unix timestamp). |
|compare_end_time |Integer |No |1619817200 |Comparison period end time (Unix timestamp). |
|is_new |Integer |No |1 |New issue. |
|status |Array of String |No |["closed"] |A processing state that requires attention. |
|managers |Array of Long |No |[123456789, 987654321] |A list of manager IDs that require attention. |
|tags |Array of Long |No |[111, 222] |A list of tag IDs that require attention. |
|token |String |No |keyword |The search keyword. |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67905#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppExceptionalBatterySummaryData&Version=2022-10-12
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
    "compare_start_time": 1619730800,
    "compare_end_time": 1619817200,
    "is_new": 1,
    "status": [
        "closed"
    ],
    "managers": [
        123456789,
        987654321
    ],
    "tags": [
        111,
        222
    ],
    "token": "keyword"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [SummaryResponseData](https://docs.byteplus.com/en/docs/299/67905#summaryresponsedata) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="summaryresponsedata"></span>
### SummaryResponseData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|battery_trace_cnt |Object of [SummaryMetric](https://docs.byteplus.com/en/docs/299/67905#summarymetric) |\- |A metric indicates the number of battery anomalies |
|battery_trace_user |Object of [SummaryMetric](https://docs.byteplus.com/en/docs/299/67905#summarymetric) |\- |Affected user count metric |
|battery_trace_ratio |Object of [SummaryMetric](https://docs.byteplus.com/en/docs/299/67905#summarymetric) |\- |Anomaly rate |
|battery_trace_user_ratio |Object of [SummaryMetric](https://docs.byteplus.com/en/docs/299/67905#summarymetric) |\- |Affected user ratio metric |


<span id="summarymetric"></span>
### SummaryMetric


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|rate |Double |1.1 |The change rate. |
|compare |Double |90.0 |The comparison value. |
|current |Double |100.0 |Current value. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": {
        "battery_trace_cnt": {
            "rate": 1.1,
            "compare": 90,
            "current": 100
        },
        "battery_trace_user": {
            "rate": 1.1,
            "compare": 90,
            "current": 100
        },
        "battery_trace_ratio": {
            "rate": 1.1,
            "compare": 90,
            "current": 100
        },
        "battery_trace_user_ratio": {
            "rate": 1.1,
            "compare": 90,
            "current": 100
        }
    },
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
