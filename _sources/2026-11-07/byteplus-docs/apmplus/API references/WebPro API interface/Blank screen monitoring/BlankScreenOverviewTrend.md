---
title: "BlankScreenOverviewTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/BlankScreenOverviewTrend"
---

Get the white\-screen overview trend and attribution distribution.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=BlankScreenOverviewTrend&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |BlankScreenOverviewTrend |The API name. The API name is `BlankScreenOverviewTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67939#commonparams) |Yes |\- |Common parameter. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67939#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67939#filtercondition) |No |\- |The filter condition. |

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
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67939#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=BlankScreenOverviewTrend&Version=2022-10-12
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
        "op": "in",
        "values": "[data explore]",
        "children": [
            {
                "type": "and",
                "children": [
                    {
                        "type": "and",
                        "values": "[data explore]",
                        "op": "in",
                        "groupKey": "context",
                        "field": "pid",
                        "children": []
                    }
                ],
                "op": "in",
                "groupKey": "context",
                "values": "[data explore]",
                "field": "pid"
            }
        ],
        "field": "pid",
        "groupKey": "context"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [OverviewTrendResponseData](https://docs.byteplus.com/en/docs/299/67939#overviewtrendresponsedata) |\- |White\-screen overview trend and distribution by attribution type. |
|error_no |Integer |0 |Error code. 0 indicates success. |
|error_msg |String |"" |Error message. Empty indicates success. |

### OverviewTrendResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|info |Array of [OverviewTrendInfoItem](https://docs.byteplus.com/en/docs/299/67939#overviewtrendinfoitem) |\- |Overview of the white\-screen count, white\-screen impacted users, and their period\-over\-period changes. |
|extra |Object of [TrendExtra](https://docs.byteplus.com/en/docs/299/67939#trendextra) |\- |Additional white\-screen information. |
|user_chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67939#chartdata) |\- |Trend in white\-screen impacted users. |
|count_chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67939#chartdata) |\- |White\-screen count trend. |
|user_pie_chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67939#chartdata) |\- |Distribution of white\-screen impacted users by attribution type. |
|count_pie_chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67939#chartdata) |\- |Distribution of white\-screen values by attribution type. |

### OverviewTrendInfoItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |count |Aggregated value key. |
|name |String |Blank screen count |Aggregated value name. |
|unit |String |ms |Aggregation unit. |
|count |String |1 |Aggregated value. |
|change |String |1.0 |Period\-over\-period. |

### TrendExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|release_info |Array of [ReleaseInfo](https://docs.byteplus.com/en/docs/299/67939#releaseinfo) |\- |Version release information. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67939#field) |\- |Line chart/pie chart dimensions. len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of specific points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

### ReleaseInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|env |String |test |Release environment. |
|commit |String |[] |Version\-related commits. |
|release |String |v2.2.123 |Version. |
|create_at |Integer |1668483578 |Version release time. |

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
    "data": {
        "info": [
            {
                "id": "count",
                "name": "blank screen count",
                "unit": "ms",
                "count": "1",
                "change": "1.0"
            }
        ],
        "extra": {
            "release_info": [
                {
                    "env": "test",
                    "commit": "[]",
                    "release": "v2.2.123",
                    "create_at": 1668483578
                }
            ]
        },
        "user_chart": {
            "fields": [
                {
                    "id": "date",
                    "name": "date",
                    "dataType": "string",
                    "aggregate": "-"
                }
            ],
            "source": [
                [
                    "1668355200",
                    "js_error",
                    "0",
                    "0"
                ]
            ]
        },
        "count_chart": {
            "fields": [
                {
                    "id": "date",
                    "name": "date",
                    "dataType": "string",
                    "aggregate": "-"
                }
            ],
            "source": [
                [
                    "1668355200",
                    "js_error",
                    "0",
                    "0"
                ]
            ]
        },
        "user_pie_chart": {
            "fields": [
                {
                    "id": "date",
                    "name": "date",
                    "dataType": "string",
                    "aggregate": "-"
                }
            ],
            "source": [
                [
                    "1668355200",
                    "js_error",
                    "0",
                    "0"
                ]
            ]
        },
        "count_pie_chart": {
            "fields": [
                {
                    "id": "date",
                    "name": "date",
                    "dataType": "string",
                    "aggregate": "-"
                }
            ],
            "source": [
                [
                    "1668355200",
                    "js_error",
                    "0",
                    "0"
                ]
            ]
        }
    },
    "error_no": 0,
    "error_msg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
