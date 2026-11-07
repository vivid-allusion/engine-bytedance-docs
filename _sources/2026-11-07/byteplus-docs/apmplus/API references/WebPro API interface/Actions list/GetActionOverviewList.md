---
title: "GetActionOverviewList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetActionOverviewList"
---

Get the action event list.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetActionOverviewList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetActionOverviewList |The API name. The current API name is `GetActionOverviewList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67918#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67918#timefilter) |Yes |\- |Time range. |
|pgno |Long |No |1 |The page number for a pagination query. |
|pgsz |Long |No |10 |The number of items per page for a pagination query. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67918#filtercondition) |No |\- |The filter condition. |
|order_by |String |No |longtask_count |Sorting field.<br><br><br>* action_duration: Action duration<br><br>* frontend_duration: Frontend duration<br><br>* request_duration: Request duration<br><br>* count: Number of Action events triggered<br><br>* http_count: Average number of requests triggered<br><br>* js_err_count: Total JS error count<br><br>* longtask_count: Long task count<br><br>* longtask_duration: Long task duration |
|metric_type |String |No |avg |Statistical method for duration metrics.<br><br><br>* avg (default)<br><br>* pct50<br><br>* pct75<br><br>* pct90<br><br>* pct95 |

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

|**Parameters** |**type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The type of the first level must be "and", and the type of the second level must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67918#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at this level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetActionOverviewList&Version=2022-10-12
{
    "time_filter":{
        "start_time":1665485413,
        "end_time":1665744613
    },
    "common":{
        "aid":12345
    },
    "pgsz":20,
    "pgno":1,
    "metric_type":"avg",
    "order_by":"frontend_duration",
    "filter_conditions":{
        "type":"and",
        "children":[
            {
                "op":"in",
                "field":"pid",
                "values":[
                    "data explore"
                ]
            }
        ]
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|errno |Integer |0 |Error code. 0 indicates success. |
|errmsg |String |"" |Error message. |
|data |Object of [ActionListData](https://docs.byteplus.com/en/docs/299/67918#actionlistdata) |\- |Returned data. |

### ActionListData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [ActionListItem](https://docs.byteplus.com/en/docs/299/67918#actionlistitem) |\- |Returned data. |
|total |Long |10 |Number of items returned. |

### ActionListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|pid |String |Data explore |Page ID. |
|metric_map |JSON Map |\- |A set of metrics. |
|action_type |String |click |Action type. |
|action_target_name |String |Description |Action name. |

### MetricMap

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |action_count |Metric key. For example, duration, frontend_duration, and http_count. |
|value |String |128 |The metric value corresponding to the key. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "data":[
            {
                "action_type":"click",
                "pid":"data explore",
                "action_target_name":"description",
                "metric_map":{
                    "action_count":"14",
                    "duration":"1984.54",
                    "frontend_duration":"1220.10",
                    "http_count":"9",
                    "http_duration":"1070.22",
                    "js_err_count":"0",
                    "longtask_count":"40",
                    "longtask_duration":"457.78",
                    "max_js_err_count":"0"
                }
            }
        ]
    },
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
