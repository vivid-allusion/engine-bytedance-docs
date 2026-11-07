---
title: "GetTrendPerAction"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetTrendPerAction"
---

Get the trend in the number of occurrences of the specified action.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetTrendPerAction&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetTrendPerAction |The API name. The current API name is `GetTrendPerAction`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|action_type |String |Yes |clik |Action type. Call the `GetActionOverviewList` API to view available values. |
|pid |String |Yes |Data explore |Page ID. Call the `GetActionOverviewList` API to view available values. |
|action_target_name |String |Yes |Description |Action name. Call the `GetActionOverviewList` API to view available values. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67916#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67916#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67916#filtercondition) |No |\- |The filter condition. |
|metric_type |String |No |avg |Statistical method for duration metrics. Supported methods include **avg** (default), **pct50**, **pct75**, **pct90**, and **pct95**. |

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
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, and not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Condition values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67916#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetTrendPerAction&Version=2022-10-12
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
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [OverviewTrendResponseData](https://docs.byteplus.com/en/docs/299/67916#overviewtrendresponsedata) |\- |Response data. |
|error_no |Integer |0 |Error code. 0 indicates success. |
|error_msg |String |"" |Error message. Empty indicates success. |

### OverviewTrendResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|info |Array of [OverviewTrendInfoItem](https://docs.byteplus.com/en/docs/299/67916#overviewtrendinfoitem) |\- |Custom event overview value. |
|chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67916#chartdata) |\- |Trend of reported custom events. |
|extra |Object of [TrendExtra](https://docs.byteplus.com/en/docs/299/67916#trendextra) |\- |Additional information about custom events. |

### OverviewTrendInfoItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |count |Aggregate value key. |
|name |String |Blank screen count |Aggregate value name. |
|unit |String |ms |Aggregate value unit. |
|count |String |1 |Aggregate value unit. |
|change |String |1.0 |Period\-over\-period. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67916#field) |\- |Dimensions of the line chart or pie chart. len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of data points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

### TrendExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|release_info |Array of [ReleaseInfo](https://docs.byteplus.com/en/docs/299/67916#releaseinfo) |\- |Version release information. |

### Field

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |date |Dimension key. |
|name |String |Date |Dimension name. |
|dataType |String |string |Dimension type. |
|aggregate |String |\- |Aggregation method. |

### ReleaseInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|env |String |test |Environment in which the version was released. |
|commit |String |[] |Version\-related commits. |
|release |String |v2.2.123 |Version. |
|create_at |Integer |1668483578 |Version release time. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "chart":{
            "fields":[
                {
                    "id":"date",
                    "dataType":"string",
                    "name":""
                },
                {
                    "id":"count",
                    "dataType":"number",
                    "name":"Action trigger count"
                }
            ],
            "source":[
                [
                    "1665072000",
                    "4"
                ]
            ]
        },
        "info":[
            {
                "id":"count",
                "name":"Action trigger count",
                "count":"14",
                "change":"-0.2632"
            }
        ],
        "extra":{
            "release_info":[
            ]
        }
    },
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
