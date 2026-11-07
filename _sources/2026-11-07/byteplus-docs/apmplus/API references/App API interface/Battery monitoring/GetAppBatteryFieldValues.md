---
title: "GetAppBatteryFieldValues"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryFieldValues"
---

Get the available values for the battery filter criteria.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppBatteryFieldValues&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppBatteryFieldValues |The API name. The current API name is `GetAppBatteryFieldValues`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |No |1617225600 |Query start time (Unix timestamp). |
|end_time |Integer |No |1617312000 |Query end time (Unix timestamp). |
|field |String |No |region |Name of the field to be aggregated or filtered. |
|limit |Integer |No |10 |Limit on the number of records returned. |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67910#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|metrics |String |No |req_cnt_v2 |Optional metric name. |
|keyword |String |No |test |Fuzzy query keyword |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67910#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppBatteryFieldValues&Version=2022-10-12
{
    "start_time": 1617225600,
    "end_time": 1617312000,
    "field": "region",
    "limit": 10,
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
    "metrics": "req_cnt_v2"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [RangeItem](https://docs.byteplus.com/en/docs/299/67910#rangeitem) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="rangeitem"></span>
### RangeItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Label 123 |Tag for filter criteria. |
|value |String |value123 |Available values for filter criteria. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": [
        {
            "label": "Label 123",
            "value": "value123"
        }
    ],
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
