---
title: "UrlList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/UrlList"
---

Get the page list.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=UrlList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UrlList |The API name. The current API name is `UrlList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67988#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67988#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67988#filtercondition) |Yes |\- |The filter condition. |
|page_num |Integer |No |1 |Page number. |
|page_size |Integer |No |10 |Number of items per page. |
|order |String |No |asc,desc |The sorting method.<br><br><br>* **asc**: Ascending order<br><br>* **desc**: Descending order |
|order_by_metric |String |No |js_error.count |Sorting basis. It can be obtained via the `OverviewMetrics` API. |
|search_text |String |No |pid_ |Fuzzy search for PID. It defaults to all if not provided. |
|metric_list |Array of [MetricList](https://docs.byteplus.com/en/docs/299/67988#metriclist) |No |\- |Page metric list. It can be obtained via the `OverviewMetrics` API. |
|top_pids |Array of String |No |[pid_1,pid_2] |A list of pinned PIDs. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time, in seconds. |
|end_time |Integer |Yes |1665744613 |End time, in seconds. |
|granularity |Integer |No |3600 |Aggregation time granularity, in seconds. |

### FilterCondition

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The first level type must be "and", and the second level type must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operators. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Map type field key. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67988#filtercondition) |No |\- |If there are further conditions at the lower level, place them here. This parameter is required when the type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

### MetricList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|name |String |No |js_error.count |Metric key. |
|type |String |No |number |Metric value type. It can be a numeric metric or a rate metric. |
|unit |String |No |ms |Metric value unit. |
|groupKey |String |No |js_error |Group key. |
|groupName |String |No |JS error |Group name. |
|isDefault |Boolean |No |true |Whether it is displayed by default. |
|description |String |No |PV |The metric name. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=UrlList&Version=2022-10-12
{
    "common": {
        "aid": 12345,
        "site_type": "web",
        "env": "online",
        "user": "test_user",
        "os": "webpro"
    },
    "time_filter": {
        "start_time": 1665485413,
        "end_time": 1665744613,
        "granularity": 3600
    },
    "filter_conditions": {
        "type": "and",
        "children": [
            {
                "type": "and",
                "op": "in",
                "children": [],
                "groupKey": "context",
                "field": "pid",
                "values": "[data explore]"
            }
        ],
        "op": "in",
        "field": "pid",
        "groupKey": "context",
        "values": "[data explore]"
    },
    "search_text": "pid_",
    "order_by_metric": "js_error.count",
    "top_pids": "[pid_1,pid_2]",
    "page_size": 10,
    "page_num": 1,
    "metric_list": [
        {
            "isDefault": true,
            "unit": "ms",
            "groupName": "JS error",
            "groupKey": "js_error",
            "description": "PV",
            "type": "number",
            "name": "js_error.count"
        }
    ],
    "order": "asc,desc"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ListData](https://docs.byteplus.com/en/docs/299/67988#listdata) |\- |List of page metric overview values. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### ListData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|count |Integer |20 |Total number of pages. |
|table_list |Array of [ListItem](https://docs.byteplus.com/en/docs/299/67988#listitem) |\- |Metric overview value for each page. |
|summary_metric |JSON Map |\- |Metric overview values for all pages. |

### ListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |/path_test |Page ID. |
|onTop |Boolean |true |Defaults to false. It is true if it is the page pinned by the user. |
|metric_map |JSON Map |\- |Overview metric value. |

### SummaryMetric

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |Page metric key. |
|value |Object of [MetricDetail](https://docs.byteplus.com/en/docs/299/67988#metricdetail) | | |

### MetricMap

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |Key corresponding to the metric. |
|value |Object of [MetricDetail](https://docs.byteplus.com/en/docs/299/67988#metricdetail) | | |

### MetricDetail

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |\- |Metric type. |
|value |Double |1,000 |The metric value. |
|change |Double |0.01 |Period\-over\-period metric comparison. |
|positive |Boolean |true |Whether it is improved.<br><br><br>* true: Improved<br><br>* false: Deteriorated |

## Sample response

```JSON
{
    "data": {
        "table_list": [
            {
                "link": "",
                "name": "/path_test",
                "onTop": true
            }
        ],
        "count": 20
    },
    "error_msg": "",
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
