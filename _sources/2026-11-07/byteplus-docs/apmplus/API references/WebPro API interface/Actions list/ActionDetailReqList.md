---
title: "ActionDetailReqList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ActionDetailReqList"
---

Get the list of requests that occurred for the specified action.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetReqListPerAction&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetReqListPerAction |The API name. The current API name is `GetReqListPerAction`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|action_type |String |Yes |click |Action type. Call the `GetActionOverviewList` API to view available values. |
|pid |String |Yes |Data explore |Page ID. Call the `GetActionOverviewList` API to view available values. |
|action_target_name |String |Yes |Description |Action name. Call the `GetActionOverviewList` API to view available values. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67915#commonparams) |Yes |\- |Common parameter. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67915#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67915#filtercondition) |No |\- |The filter condition. |
|order_by |String |No |count_descend |Sorting field.<br><br><br>* count_ascend: Ascending order<br><br>* count_descend (default): Descending order |
|pgno |Long |No |1 |The page number for a pagination query. Default value: 1. |
|pgsz |Long |No |30 |The number of items per page for a pagination query. Default value: 30. |

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
|granularity |Integer |No |3600 |Aggregation granularity, in seconds. |

### FilterCondition

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The first level type must be "and", and the second level type must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Condition values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67915#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetReqListPerAction&Version=2022-10-12
{
    "common":{
        "aid":12345
    },
    "time_filter":{
        "start_time":1664621845,
        "end_time":1665140253,
        "granularity":86400
    },
    "action_type":"click",
    "pid":"data explore",
    "action_target_name":"description",
    "metric_type":"avg",
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
    },
    "pgsz":20,
    "pgno":1,
    "order_by":"count_descend"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|errno |Integer |0 |Error code. 0 indicates success. |
|errmsg |String |"" |Error message. An empty string `""` indicates success. |
|data |Object of [ActionDetailReqListResponseData](https://docs.byteplus.com/en/docs/299/67915#actiondetailreqlistresponsedata) |\- |Response data. |

### ActionDetailReqListResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Long |10 |Number of requests in the list. |
|result |Array of [ActionReqItem](https://docs.byteplus.com/en/docs/299/67915#actionreqitem) |\- |Result data. |

### ActionReqItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|path |String |/api_web/common/field_values |Request path. |
|domain |String |demo.volcengine.net |Request domain. |
|duration |Long |26 |Request latency statistic. |
|duration_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67915#chartdata) |\- |Request latency trend. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67915#field) |\- |Dimensions of the line chart or pie chart. len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of data points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

### Field

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |date |Dimension key. |
|name |String |Date |Dimension name. |
|dataType |String |string |Dimension type. |
|aggregate |String |\- |Aggregation method. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "result":[
            {
                "domain":"demo.volcengine.net",
                "path":"/api_web/common/field_values",
                "duration":26,
                "duration_trend":{
                    "fields":[
                        {
                            "id":"date",
                            "dataType":"string",
                            "name":""
                        },
                        {
                            "id":"count",
                            "dataType":"number",
                            "name":"request time"
                        }
                    ],
                    "source":[
                        [
                            "1664553600",
                            "641"
                        ],
                        [
                            "1665158400",
                            "0"
                        ]
                    ]
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
