---
title: "AnalyseMetricList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/AnalyseMetricList"
---

View the list on the metric detail page.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=AnalyseMetricList&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |AnalyseMetricList |The API name. The current API name is `AnalyseMetricList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|os |String |Yes |Android |Operating system (Android, iOS) |
|start_time |Integer |Yes |1630473600 |Start time |
|end_time |Integer |Yes |1630560000 |End time |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67871#condition) |Yes |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|order_by |String |Yes |count |Sorting method (count, user, per_capita) |
|keyword |String |No |example_keyword |Keyword |
|event_name |String |No |event |Event name (optional) |
|attribute_name |String |No |name |Attribute name (optional) |
|attribute_type |String |No |string |Attribute type (optional) |
|page_no |Integer |Yes |1 |Page number |
|page_size |Integer |Yes |20 |Page size |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67871#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=AnalyseMetricList&Version=2022-10-12
{
    "os": "Android",
    "start_time": 1630473600,
    "end_time": 1630560000,
    "filters": {
        "op": "in",
        "type": "expression",
        "value": "Android",
        "values": [
            "Android"
        ],
        "map_key": "key_1",
        "dimension": "aid",
        "sub_conditions": []
    },
    "order_by": "count",
    "keyword": "example_keyword",
    "event_name": "event",
    "attribute_name": "name",
    "attribute_type": "string",
    "page_no": 1,
    "page_size": 20
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [MetricListData](https://docs.byteplus.com/en/docs/299/67871#metriclistdata) | |Metric data |
|error_msg |String |success |Error message |
|error_no |Integer |500 |Error codes |


<span id="metriclistdata"></span>
### MetricListData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [MetricListItem](https://docs.byteplus.com/en/docs/299/67871#metriclistitem) | |Metric list |
|total |Integer |10 |Total metric count |


<span id="metriclistitem"></span>
### MetricListItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|avg |Double |2 |Event metric average |
|var |Double |2 |Event metric variance |
|name |String |kk |Metric Name |
|user |Long |2 |Reporting user count |
|count |Long |50 |Event reports |
|pct25 |Double |2 |Event metric percentile value pct25 |
|pct50 |Double |2 |Event metric percentile value pct50 |
|pct75 |Double |2 |Event metric percentile value pct75 |
|pct90 |Double |2 |Event metric percentile value pct90 |
|pct99 |Double |2 |Event metric percentile value pct99 |
|attribute_id |Long |2 |Attribute ID |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": {
        "data": [
            {
                "avg": 2,
                "var": 2,
                "name": "kk",
                "user": 2,
                "count": 50,
                "pct25": 2,
                "pct50": 2,
                "pct75": 2,
                "pct90": 2,
                "pct99": 2,
                "attribute_id": 2
            }
        ],
        "total": 10
    },
    "error_msg": "success",
    "error_no": 500
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
