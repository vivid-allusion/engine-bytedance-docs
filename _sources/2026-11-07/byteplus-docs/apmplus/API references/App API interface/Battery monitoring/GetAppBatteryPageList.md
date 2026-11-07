---
title: "GetAppBatteryPageList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryPageList"
---

Get app battery foreground list.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppBatteryPageList&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppBatteryPageList |The API name. The current API name is `GetAppBatteryPageList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |No |1619827200 |Query start time (Unix timestamp). |
|end_time |Integer |No |1619913600 |Query end time (Unix timestamp). |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67908#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|page_no |Integer |No |1 |Page number to query. |
|page_size |Integer |No |20 |Number of items displayed per page. |
|metrics |String |No |battery_usage |Battery metric name used for the query. |
|order_by |String |No |avg_ascend |Sorting basis.<br><br><br>* avg_ascend: Sort by average value in ascending order<br><br>* avg_descend: Sort by average value in descending order<br><br>* pct25_ascend: Sort by 25th percentile value in ascending order<br><br>* pct25_descend: Sort by 25th percentile value in descending order<br><br>* pct50_ascend: Sort by 50th percentile value in ascending order<br><br>* pct50_descend: Sort by 50th percentile value in descending order<br><br>* pct75_ascend: Sort by 75th percentile value in ascending order<br><br>* pct75_descend: Sort by 75th percentile value in descending order<br><br>* pct90_ascend: Sort by 90th percentile value in ascending order<br><br>* pct90_descend: Sort by 90th percentile value in descending order<br><br>* pct99_ascend: Sort by 99th percentile value in ascending order<br><br>* pct99_descend: Sort by 99th percentile value in descending order<br><br>* statistics_cnt_ascend: Sort by statistical count in ascending order<br><br>* statistics_cnt_descend: Sort by statistical count in descending order |
|scene |String |No |HomePage |Page name to search. |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67908#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppBatteryPageList&Version=2022-10-12
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
    "page_no": 1,
    "page_size": 20,
    "metrics": "battery_usage",
    "order_by": "avg_ascend",
    "scene": "HomePage"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [SearchResponseData](https://docs.byteplus.com/en/docs/299/67908#searchresponsedata) |\- |Returned content |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="searchresponsedata"></span>
### SearchResponseData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Integer |10 |Total number of items in the list |
|result |Array of [BatteryScenePageItem](https://docs.byteplus.com/en/docs/299/67908#batteryscenepageitem) |\- |List details. |


<span id="batteryscenepageitem"></span>
### BatteryScenePageItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|pct25 |Double |10.5 |25th percentile value. |
|pct50 |Double |14.0 |50th percentile value (median). |
|pct75 |Double |17.8 |75th percentile value. |
|pct90 |Double |19.6 |90th percentile value. |
|pct99 |Double |23.4 |99th percentile value. |
|scene |String |HomePage |Page name. |
|avg_value |Double |15.2 |Average metric value. |
|statistics_cnt |Double |200 |Sample count. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": {
        "total": 10,
        "result": [
            {
                "pct25": 10.5,
                "pct50": 14,
                "pct75": 17.8,
                "pct90": 19.6,
                "pct99": 23.4,
                "scene": "HomePage",
                "avg_value": 15.2,
                "statistics_cnt": 200
            }
        ]
    },
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
