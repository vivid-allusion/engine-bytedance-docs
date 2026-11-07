---
title: "EventTypeDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/EventTypeDetail"
---

Get the category and metric aggregation list of a specific custom event.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=EventTypeDetail&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |EventTypeDetail |The API name. The API name is `EventTypeDetail`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67942#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67942#timefilter) |Yes |\- |Time range. |
|event_name |String |Yes |event_test |Custom event name. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67942#filtercondition) |No |\- |The filter condition. |

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
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, and not_regex. |
|groupKey |String |No |context |Map type field key. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[data explore] |Condition values. The available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67942#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. This level cannot coexist with field, op, groupkey, and values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=EventTypeDetail&Version=2022-10-12
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
    "event_name": "event_test",
    "filter_conditions": {
        "type": "and",
        "op": "in",
        "values": "[data explore]",
        "children": [
            {
                "type": "and",
                "field": "pid",
                "op": "in",
                "values": "[data explore]",
                "groupKey": "context",
                "children": []
            }
        ],
        "groupKey": "context",
        "field": "pid"
    }
}
```

## Response parameters

|**Parameters** |**type** |**Sample value** |**Description** |
|---|---|---|---|
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |\- |Error code. 0 indicates success. |
|data |Object of [EventTypeDetailResponseData](https://docs.byteplus.com/en/docs/299/67942#eventtypedetailresponsedata) |\- |Lists of categories and metrics of a specific custom event. |

### EventTypeDetailResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|metric_list |Array of [EventTypeDetailMetric](https://docs.byteplus.com/en/docs/299/67942#eventtypedetailmetric) |\- |Metric aggregation list of the specific custom event. |
|category_list |Array of [EventTypeDetailCategory](https://docs.byteplus.com/en/docs/299/67942#eventtypedetailcategory) |\- |Category aggregation list of the specific custom event. |

### EventTypeDetailMetric

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|avg |Double |1.2 |Average value of the metric values corresponding to the metric key. |
|count |Integer |10 |Number of reports for the metric key. |
|pct25 |Double |1.0 |The pct25 of the metric values corresponding to the metric key. |
|pct50 |Double |1.2 |The pct50 of the metric values corresponding to the metric key. |
|pct70 |Double |1.3 |The pct70 of the metric values corresponding to the metric key. |
|pct90 |Double |1.4 |The pct90 of the metric values corresponding to the metric key. |
|pct99 |Double |1.5 |The pct99 of the metric values corresponding to the metric key. |
|metric_name |String |metric_key_test |Metric key. |

### EventTypeDetailCategory

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|count |Integer |10 |Number of reports for the category key. |
|top_values |Array of [EventTypeDetailCategoryValue](https://docs.byteplus.com/en/docs/299/67942#eventtypedetailcategoryvalue) |\- |The top 20 values reported for this category key. |
|category_name |String |category_key_test |Category key. |

### EventTypeDetailCategoryValue

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|pct |Double |0.12 |The proportion of reports for this value under the category key to the total reports for all values. |
|count |Integer |10 |Number of reported values corresponding to the category key. |
|value |String |category_value_test |Value corresponding to the category key. |

## Sample response

```JSON
{
    "error_no": 0,
    "data": {
        "metric_list": [
            {
                "metric_name": "metric_key_test",
                "pct70": 1.3,
                "pct25": 1,
                "pct99": 1.5,
                "count": 10,
                "pct90": 1.4,
                "pct50": 1.2,
                "avg": 1.2
            }
        ],
        "category_list": [
            {
                "top_values": [
                    {
                        "pct": 0.12,
                        "value": "category_value_test",
                        "count": 10
                    }
                ],
                "count": 10,
                "category_name": "category_key_test"
            }
        ]
    },
    "error_msg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
