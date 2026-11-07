---
title: "GetAppHttpTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppHttpTrend"
---

Get metric trends for HTTP network monitoring.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppHttpTrend&Version=2025\-12\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you call this API, specify the required public request parameters (such as <code>x-app-ids</code>). Otherwise, the call fails.</div>



|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppHttpTrend |The name of the API action. The current API name is `GetAppHttpTrend`. |
|Version |String |Yes |2025\-12\-01 |The API version. The API version is `2025-12-01`. |
|StartTime |Integer |Yes |1617225600 |Timestamp of the query start time. |
|EndTime |Integer |Yes |1617312000 |Timestamp of the query end time. |
|Filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67901#condition) |No |filters |The filter condition. You can specify multiple key‑value pairs to filter data. |
|LastGroupFilters |Array of [Condition](https://docs.byteplus.com/en/docs/299/67901#condition) |No |last_group_filters |Previously selected grouping conditions. |
|GroupField |String |Yes |os_version |Name of the field to group the results by. Pass an empty string if there is no grouping. |
|Metrics |Array of String |Yes |["req_cnt_v2","req_cnt_rate_v2"] |Name of the metric to query. Values:<br><br><br>* all_report_cnt_v2: Report count<br><br>* req_cnt_v2: Request count<br><br>* req_cnt_rate_v2: Request rate<br><br>* req_success_cnt_v2: Request success count<br><br>* req_success_rate_v2: Request success rate<br><br>* reused_cnt_v2: Link reuse count<br><br>* reused_rate_v2: Link reuse rate<br><br>* reused_success_rate_v2: Link reuse success rate<br><br>* req_err_cnt_v2: Request error count<br><br>* req_all_err_cnt_v2: Total request error count<br><br>* req_err_rate_v2: Request error rate<br><br>* req_total_cost_v2: Total request count<br><br>* req_user_cnt_v2: Request user count<br><br>* req_success_user_cnt_v2: Request success user count<br><br>* req_success_user_rate_v2: Request success user rate |
|DomainTag |String |Yes |all |Host tag. Values:<br><br><br>* all: All<br><br>* self: Own service<br><br>* other: Third\-party |
|StatisticScale |String |No |avg |Statistical scope. Values:<br><br><br>* avg<br><br>* pct50<br><br>* pct75<br><br>* pct95<br><br>* pct99 |
|Granularity |Integer |Yes |5 |The aggregation granularity. Unit: minutes. |
|TopN |Integer |Yes |10 |Number of topN groups. Pass 0 if there is no grouping. |


<span id="condition"></span>
### Condition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Op |String |No |in |The operator. Values:<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|Type |String |No |expression |The type of the filter condition. Sample value:<br><br><br>* expression: The current condition is a single expression.<br><br>* and: The current condition is a compound expression, and the sub\-conditions in `SubConditions` are in a logical AND relationship.<br><br>* or: The current condition is a compound expression, and the sub\-conditions in `SubConditions` are in a logical OR relationship.<br><br>* map: The current condition is of the map type. |
|Value |String |No |123456 |The filter value. |
|MapKey |String |No |key_1 |The key of the map type.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>type</code> is set to map.</div><br> |
|Values |Array of String |No |[123456] |The filter values. You can configure multiple values simultaneously. |
|Dimension |String |No |aid |The name of the condition. |
|SubConditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67901#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppHttpTrend&Version=2025-12-01
{
    "StartTime": 1617225600,
    "EndTime": 1617312000,
    "Filters": "filters",
    "LastGroupFilters": [
        {
            "Op": "in",
            "Type": "expression",
            "Value": "123456",
            "MapKey": "key_1",
            "Values": [
                123456
            ],
            "Dimension": "aid",
            "SubConditions": []
        }
    ],
    "GroupField": "os_version",
    "Metrics": [
        "req_cnt_v2",
        "req_cnt_rate_v2"
    ],
    "DomainTag": "all",
    "StatisticScale": "avg",
    "Granularity": 5,
    "TopN": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |1 |The metric name. |
|value |Array of [TrendLine](https://docs.byteplus.com/en/docs/299/67901#trendline) |\- |Trend value. |


<span id="trendline"></span>
### TrendLine


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |test123 |The curve name. When grouped, the value is the grouping dimension value, which can be used as a legend label. |
|Total |Double |\- |The total count. |
|Points |Array of [TrendPoint](https://docs.byteplus.com/en/docs/299/67901#trendpoint) |\- |The data points on the curve. |


<span id="trendpoint"></span>
### TrendPoint


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Value |Double |123 |The metric value. |
|Timestamp |Long |1665417600 |The timestamp of the metric occurrence. |
|ReadableTimestamp |String |2022\-10\-11 |The occurrence time of the metric. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "Action": "GetAppHttpTrend",
        "Region": "cn-north-1",
        "Service": "apmplus_openapi",
        "Version": "2025-12-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "error_msg": "fail",
    "error_no": "0",
    "data": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
