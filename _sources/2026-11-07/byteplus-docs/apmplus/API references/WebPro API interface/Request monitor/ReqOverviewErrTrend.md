---
title: "ReqOverviewErrTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ReqOverviewErrTrend"
---

Get the overall trend of request errors.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ReqOverviewErrTrend&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ReqOverviewErrTrend |The API name. The current API name is `ReqOverviewErrTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67976#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67976#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67976#filtercondition) |No |\- |The filter condition. |

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
|type |String |Yes |and |Filter condition type. Available values are and and rule. Only two levels are supported. The type of the first level must be "and", and the type of the second level must be "rule". |
|field |String |No |pid |The key of the condition field. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, and not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Condition values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67976#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ReqOverviewErrTrend&Version=2022-10-12
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
                "field": "pid",
                "children": [],
                "values": "[data explore]",
                "op": "in",
                "groupKey": "context"
            }
        ],
        "groupKey": "context",
        "field": "pid",
        "values": "[data explore]",
        "op": "in"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [OverviewTrendResponseData](https://docs.byteplus.com/en/docs/299/67976#overviewtrendresponsedata) |\- |Overall trend. |
|error_no |Integer |0 |Error code. 0 indicates success. |
|error_msg |String |\- |Error message. It is empty if the request succeeds. |

### OverviewTrendResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|info |Array of [OverviewTrendInfoItem](https://docs.byteplus.com/en/docs/299/67976#overviewtrendinfoitem) |\- |Custom event overview value. |
|chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67976#chartdata) |\- |Custom event reporting trend. |
|extra |Object of [TrendExtra](https://docs.byteplus.com/en/docs/299/67976#trendextra) |\- |Custom event extra information. |

### OverviewTrendInfoItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |count |Aggregate value key. |
|name |String |Blank screen count |Aggregated value name. |
|unit |String |ms |Aggregation unit. |
|count |String |1 |Aggregated value. |
|change |String |1.0 |Period\-over\-period change. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67976#field) |\- |Line chart/pie chart dimensions. len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of specific points in the trend chart. len(source) is the number of points in the line chart or the number of blocks in the pie chart. |

### TrendExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|release_info |Array of [ReleaseInfo](https://docs.byteplus.com/en/docs/299/67976#releaseinfo) |\- |Version release status. |

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
|env |String |test |Version release environment. |
|commit |String |[] |Version\-related commit. |
|release |String |v2.2.123 |Version. |
|create_at |Integer |1668483578 |Version release time. |

## Sample response

```JSON
{
    "error_msg": "",
    "data": {
        "extra": {
            "release_info": [
                {
                    "release": "v2.2.123",
                    "env": "test",
                    "commit": "",
                    "create_at": 1668483578
                }
            ]
        },
        "chart": {
            "source": [
                [
                    "1668355200",
                    "js_error",
                    "0",
                    "0"
                ]
            ],
            "fields": [
                {
                    "aggregate": "powerful",
                    "id": "date",
                    "dataType": "string",
                    "name": "date"
                }
            ]
        },
        "info": [
            {
                "count": "1",
                "name": "blank screen count",
                "id": "count",
                "unit": "ms",
                "change": "1"
            }
        ]
    },
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
