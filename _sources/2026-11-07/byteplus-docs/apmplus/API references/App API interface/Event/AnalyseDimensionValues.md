---
title: "AnalyseDimensionValues"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/AnalyseDimensionValues"
---

View the event list.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=AnalyseRank&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |AnalyseRank |The API name. The current API name is `AnalyseRank`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |Yes |1630473600 |Start time. |
|end_time |Integer |Yes |1630560000 |End time. |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67873#condition) |Yes |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|event_name |String |No |example_event |The event name. |
|order_by |String |Yes |count |The sorting method.<br><br><br>* count: Number of event reports. <br><br>* per_capita: Event reports per capita.<br><br>* user: Event user count. |
|keyword |String |Yes |example_keyword |Keyword. |
|os |String |Yes |Android |The operating system.<br><br><br>* Android<br><br>* iOS |
|page_no |Integer |Yes |1 |Page number. |
|page_size |Integer |Yes |20 |Page size. |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67873#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=AnalyseRank&Version=2022-10-12
{
    "start_time": 1658664000,
    "end_time": 1658750543,
    "keyword":"",
    "OS":"iOS",
    "page_no": 1,
    "page_size": 10,
    "filters": {
        "type": "and",
        "sub_conditions": [
            {
                "dimension": "os",
                "op": "in",
                "type": "expression",
                "values": [
                    "iOS"
                ]
            }
        ]
    },
    "order_by": "count"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [RankData](https://docs.byteplus.com/en/docs/299/67873#rankdata) |\- |Event list data. |
|error_msg |String |success |Error message. |
|error_no |Integer |500 |Error code. 0 indicates success. |


<span id="rankdata"></span>
### RankData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|items |Array of [RankItem](https://docs.byteplus.com/en/docs/299/67873#rankitem) | |Ranking list |
|total |Integer |100 |Total number of events. |


<span id="rankitem"></span>
### RankItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |event |The event name. |
|type |String |metric |Event type.<br><br><br>* metric: Metric<br><br>* dimension: Dimension |
|label |String |example_label |Metric or dimension tag. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": {
        "items": [
            {
                "name": "event",
                "label": "example_label",
                "type": "metric"
            }
        ],
        "total": 1
    },
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
