---
title: "GetAppThreadCPUUsageList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppThreadCPUUsageList"
---

Get the CPU usage of each thread.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppThreadCPUUsageList&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppThreadCPUUsageList |The API name. The current API name is `GetAppThreadCPUUsageList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |No |1619827200 |Query start time (Unix timestamp). |
|end_time |Integer |No |1619913600 |Query end time (Unix timestamp). |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67895#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|order_by |String |No |avg_descend |The sorting method.<br><br><br>* avg_ascend: Sort by average value in ascending order<br><br>* avg_descend: Sort by average value in descending order<br><br>* pct25_ascend: Sort by 25th percentile value in ascending order<br><br>* pct25_descend: Sort by 25th percentile value in descending order<br><br>* pct50_ascend: Sort by 50th percentile value in ascending order<br><br>* pct50_descend: Sort by 50th percentile value in descending order<br><br>* pct75_ascend: Sort by 75th percentile value in ascending order<br><br>* pct75_descend: Sort by 75th percentile value in descending order<br><br>* pct90_ascend: Sort by 90th percentile value in ascending order<br><br>* pct90_descend: Sort by 90th percentile value in descending order<br><br>* pct99_ascend: Sort by 99th percentile value in ascending order<br><br>* pct99_descend: Sort by 99th percentile value in descending order<br><br>* sample_cnt_ascend: Sort by sample count in ascending order<br><br>* sample_cnt_descend: Sort by sample count in descending order |


<span id="condition"></span>
### Condition


|**Parameters** |**type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |The operator.<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|type |String |No |expression |The type of the filter condition.<br><br><br>* expression: The current condition is an expression.<br><br>* and: The current condition is a compound expression, and multiple sub\-conditions are in an AND logical relationship.<br><br>* or: The current condition is a compound expression, and multiple sub\-conditions are in an OR logical relationship.<br><br>* map: The current condition is of map type. |
|value |String |No |123456 |The filter value. |
|values |Array of String |No |[123456] |The filter value. Multiple filter values are supported. |
|map_key |String |No |key_1 |The key of the map type. It is required when the type is set to map. |
|dimension |String |No |aid |The name of the condition. |
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67895#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppThreadCPUUsageList&Version=2022-10-12
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
    "order_by": "avg_descend"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_msg |String |success |Error description. Returns **success** if the request succeeds. |
|error_no |Integer |0 |Error code. Returns 0 if the request succeeds. |
|data |Array of [MetricListItem](https://docs.byteplus.com/en/docs/299/67895#metriclistitem) |\- |The metric list. |


<span id="metriclistitem"></span>
### MetricListItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|avg |Double |75.5 |Average value. |
|key |String |metric_key |Metric identifier |
|pct25 |Double |50.0 |25th percentile value. |
|pct50 |Double |75.0 |50th percentile value. |
|pct70 |Double |80.0 |70th percentile value. |
|pct90 |Double |95.0 |90th percentile value. |
|sample_cnt |Integer |100 |Sample size. It indicates the number of data points involved in the calculation. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "error_msg": "success",
    "error_no": 0,
    "data": [
        {
            "avg": 75.5,
            "key": "metric_key",
            "pct25": 50,
            "pct50": 75,
            "pct70": 80,
            "pct90": 95,
            "sample_cnt": 100
        }
    ]
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
