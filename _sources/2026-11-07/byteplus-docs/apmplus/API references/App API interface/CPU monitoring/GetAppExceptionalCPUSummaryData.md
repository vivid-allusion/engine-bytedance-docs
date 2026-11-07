---
title: "GetAppExceptionalCPUSummaryData"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalCPUSummaryData"
---

Get CPU abnormal metrics.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppExceptionalCPUSummaryData&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppExceptionalCPUSummaryData |The API name. The current API name is `GetAppExceptionalCPUSummaryData`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |No |1619827200 |Current period start time (Unix timestamp). |
|end_time |Integer |No |1619913600 |Current period end time (Unix timestamp). |
|compare_start_time |Integer |No |1619740800 |Comparison period start time (Unix timestamp). |
|compare_end_time |Integer |No |1619827200 |Comparison period end time (Unix timestamp). |
|is_new |Integer |No |1 |Whether it is a new issue.<br><br><br>* 1: Only view new issues<br><br>* 0: All issues |
|token |String |No |OutOfMemory |The search keyword. |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67899#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|status |Array of String |No |[pending] |Processing state.<br><br><br>* pending<br><br>* processing<br><br>* ignored<br><br>* solved<br><br>* reopen |
|tags |Array of Long |No |[123456, 789012] |Tag filtering. |
|managers |Array of Long |No |[555666, 777888] |Filter the owner by the user ID list. |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67899#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppExceptionalCPUSummaryData&Version=2022-10-12
{
    "start_time": 1619827200,
    "end_time": 1619913600,
    "compare_start_time": 1619740800,
    "compare_end_time": 1619827200,
    "is_new": 1,
    "token": "OutOfMemory",
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
    "status": [
        "pending"
    ],
    "tags": [
        123456,
        789012
    ],
    "managers": [
        555666,
        777888
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_msg |String |success |Error message. |
|error_no |Integer |0 |Error code. |
|data |JSON Map |\- |Returned metric value. |


<span id="data"></span>
### Data


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |crash_count |CPU abnormal metrics.<br><br><br>* crash_count: Anomaly count<br><br>* crash_ratio: Anomaly rate<br><br>* crash_user: Affected user count<br><br>* crash_user_ratio_avg: Average affected user ratio<br><br>* crash_user_ratio: Overall affected user ratio<br><br>* cpu_report_cnt_per_launch: Average number of reports per launch<br><br>* avg_process_cpu_rate: Average process CPU utilization<br><br>* avg_process_cpu_speed_rate: Average process CPU usage speed rate |
|value |Object of [SummaryMetric](https://docs.byteplus.com/en/docs/299/67899#summarymetric) |\- |Value of the CPU abnormal metric. |


<span id="summarymetric"></span>
### SummaryMetric


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|rate |Double |0.4 |The change rate. |
|compare |Double |30.0 |The comparison value. |
|current |Double |42.0 |Current value. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "error_msg": "success",
    "error_no": 0,
    "data": {
        "key": "crash_count",
        "value": {
            "rate": "0.4",
            "compart": "30.0",
            "current": "42.0"
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
