---
title: "GetAppTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppTrend"
---

Obtain the trend data of app crashes.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppTrend&Version=2025\-12\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you call this API, specify the required public request parameters (such as <code>x-app-ids</code>). Otherwise, the call fails.</div>



|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppTrend |The API name. The name of the current API is `GetAppTrend`. |
|Version |String |Yes |2025\-12\-01 |The API version. The API version is `2025-12-01`. |
|Aid |Long |Yes |123456 |The app ID. |
|StartTime |Long |Yes |1665417600 |The timestamp of the query start time. Unit: seconds. |
|EndTime |Long |Yes |1665504000 |The timestamp of the query end time. Unit: seconds. |
|CompareStartTime |Long |Yes |1619740800 |The timestamp of the comparison start time. Unit: seconds.<br><br>The start time and end time form a query time window. The comparison start time and comparison end time form another time window for period\-over\-period analysis. Typically, the comparison time window has the same duration as the query time window and is the adjacent period immediately before the query time window.<br><br>For example, if the start time is 2023\-03\-05 00:00:00 and the end time is 2023\-03\-08 00:00:00, then the comparison start time is 2023\-03\-02 00:00:00 and the comparison end time is 2023\-03\-05 00:00:00. |
|CompareEndTime |Long |Yes |1619827200 |The timestamp of the comparison end time. Unit: seconds. |
|BizType |String |Yes |crash |The exception type. Values:<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* custom_exception: Custom exception |
|Filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67887#condition) |No |\- |The filter condition. |
|Granularity |Integer |Yes |60 |The aggregation granularity. Unit: minutes. |
|GroupByField |String |No |os_version |The grouping field. |
|Metric |String |Yes |crash_count |The metric name. Values:<br><br><br>* crash_count: The number of crashes.<br><br>* crash_user: The number of users affected by the crash.<br><br>* crash_ratio: The crash rate.<br><br>* crash_user_ratio: The ratio of users affected by the crash.<br><br>* session_count: Page view count.<br><br>* session_user: The number of users. |
|From |String |No |startup |The source module. Values:<br><br><br>* startup: Startup analysis module<br><br>* app_page: Page analysis module |
|Status |Array of String |No |["pending","solved"] |The list of issue states. You can configure multiple states simultaneously. Values:<br><br><br>* pending<br><br>* processing<br><br>* ignored<br><br>* solved<br><br>* reopen |
|Tags |Array of Long |No |[] |The list of tag IDs. |
|Token |String |No |keyword |The search keyword. |
|IsNew |Integer |No |0 |Whether it is a new issue. Values:<br><br><br>* 0: This is not a new issue.<br><br>* 1: This is a new issue. |
|Managers |Array of Long |No |[] |The IDs of the persons responsible for this issue. |
|TimeType |String |No |api_time |The time type. Values:<br><br><br>* api_time: Report time (default)<br><br>* event_time: Occurrence time |
|IsCustom |Boolean |No |false |Whether to use custom dimensions. Values:<br><br><br>* true: Enable custom dimensions<br><br>* false: Disable custom dimensions (default). |


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
|SubConditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67887#condition) |No |[] |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppTrend&Version=2025-12-01
{
    "Aid": 123456,
    "StartTime": 1665417600,
    "EndTime": 1665504000,
    "CompareStartTime": 1619740800,
    "CompareEndTime": 1619827200,
    "BizType": "crash",
    "Filters": {},
    "Granularity": 60,
    "GroupByField": "os_version",
    "Metric": "crash_count",
    "From": "startup",
    "Status": [
        "pending",
        "solved"
    ],
    "Tags": [],
    "Token": "keyword",
    "IsNew": 0,
    "Managers": [],
    "TimeType": "api_time",
    "IsCustom": false
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |test123 |The curve name. When grouped, the value is the grouping dimension value, which can be used as a legend label. |
|Total |Double |\- |The total count. |
|Points |Array of [TrendPoint](https://docs.byteplus.com/en/docs/299/67887#trendpoint) |\- |The data points on the curve. |


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
        "Action": "GetAppTrend",
        "Region": "cn-north-1",
        "Service": "apmplus_openapi",
        "Version": "2025-12-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": [
        {
            "Name": "v1.2.0",
            "Total": 156.5,
            "Points": [
                {
                    "Value": 12,
                    "Timestamp": 1665417600,
                    "ReadableTimestamp": "2022-10-11"
                },
                {
                    "Value": 18,
                    "Timestamp": 1665504000,
                    "ReadableTimestamp": "2022-10-12"
                },
                {
                    "Value": 15,
                    "Timestamp": 1665590400,
                    "ReadableTimestamp": "2022-10-13"
                }
            ]
        },
        {
            "Name": "v1.3.0",
            "Total": 89,
            "Points": [
                {
                    "Value": 5,
                    "Timestamp": 1665417600,
                    "ReadableTimestamp": "2022-10-11"
                },
                {
                    "Value": 7,
                    "Timestamp": 1665504000,
                    "ReadableTimestamp": "2022-10-12"
                },
                {
                    "Value": 10,
                    "Timestamp": 1665590400,
                    "ReadableTimestamp": "2022-10-13"
                }
            ]
        }
    ]
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
