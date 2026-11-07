---
title: "UrlOverview"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/UrlOverview"
---

Get the overview values for all pages.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=UrlOverview&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UrlOverview |The API name. The current API name is `UrlOverview`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67987#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67987#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67987#filtercondition) |No |\- |Filter conditions. |

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
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The type of the first level must be "and", and the type of the second level must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Condition values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67987#filtercondition) |No |\- |If there are further conditions at the lower level, place them here. This parameter is required when the type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=UrlOverview&Version=2022-10-12
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
        "field": "pid",
        "groupKey": "context",
        "op": "in",
        "children": [
            {
                "type": "and",
                "children": [],
                "op": "in",
                "field": "pid",
                "groupKey": "context",
                "values": "[data explore]"
            }
        ],
        "values": "[data explore]"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [UrlOverview](https://docs.byteplus.com/en/docs/299/67987#urloverview) |\- |Page metric overview value. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### UrlOverview

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|count |Integer |20 |Total PID count. |
|overview_list |Array of [SingleOverview](https://docs.byteplus.com/en/docs/299/67987#singleoverview) |\- |Metric overview value. |

### SingleOverview

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|link |String |/test |Page ID, pid. |
|detail |Object of [MetricDescription](https://docs.byteplus.com/en/docs/299/67987#metricdescription) |\- |Metric details. |
|ev_type |String |js_error |Metric type. |
|description |String |Highest JS error count |Metric description. |

### MetricDescription

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|unit |String |ms |Metric value unit. |
|good_metric |Boolean |true |Whether it is a positive metric or a negative metric. |
|metric_value |Integer |1,000 |The metric value. |

## Sample response

```JSON
{
    "data": {
        "count": 20,
        "overview_list": [
            {
                "description": "JS error count",
                "detail": {
                    "good_metric": true,
                    "metric_value": 1000,
                    "unit": "ms",
                    "metric_name": ""
                },
                "ev_type": "js_error",
                "link": "/test"
            }
        ]
    },
    "error_no": 0,
    "error_msg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
