---
title: "JSOverviewTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/JSOverviewTrend"
---

Get JavaScript error overview metrics and trends.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=JSOverviewTrend&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |JSOverviewTrend |The API name. The API name is `JSOverviewTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67958#commonparams) |Yes |\- |Public parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67958#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67958#filtercondition) |No |\- |The filter condition. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string ("") indicates all environments. |
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
|op |String |No |in |Condition operators. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67958#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=JSOverviewTrend&Version=2022-10-12
{
    "common": {
        "aid": 12345,
        "site_type": "web",
        "env": "online",
        "os": "webpro",
        "user": "test_user"
    },
    "time_filter": {
        "start_time": 1665485413,
        "end_time": 1665744613,
        "granularity": 3600
    },
    "filter_conditions": {
        "type": "and",
        "op": "in",
        "children": [
            {
                "type": "and",
                "children": [
                    {
                        "type": "and",
                        "values": "[data explore]",
                        "field": "pid",
                        "groupKey": "context",
                        "op": "in",
                        "children": []
                    }
                ],
                "op": "in",
                "field": "pid",
                "values": "[data explore]",
                "groupKey": "context"
            }
        ],
        "field": "pid",
        "groupKey": "context",
        "values": "[data explore]"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [OverviewTrendResponseData](https://docs.byteplus.com/en/docs/299/67958#overviewtrendresponsedata) |\- |Overall trend. |
|error_no |Integer |0 |Error code. 0 indicates success. |
|error_msg |String |\- |Error message. Empty indicates success. |

### OverviewTrendResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|info |Array of [OverviewTrendInfoItem](https://docs.byteplus.com/en/docs/299/67958#overviewtrendinfoitem) |\- |Custom event overview value. |
|chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67958#chartdata) |\- |Custom event reporting trend. |
|extra |Object of [TrendExtra](https://docs.byteplus.com/en/docs/299/67958#trendextra) |\- |Custom event extra information. |

### OverviewTrendInfoItem

|**Parameters** |**type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |count |Aggregated value key. |
|name |String |Blank screen count |Aggregated value name. |
|unit |String |ms |Aggregation unit. |
|count |String |1 |Aggregated value. |
|change |String |1.0 |Period\-over\-period. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67958#field) |\- |Line chart/pie chart dimensions. len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of data points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

### TrendExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|release_info |Array of [ReleaseInfo](https://docs.byteplus.com/en/docs/299/67958#releaseinfo) |\- |Version release information. |

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
|env |String |test |Release environment. |
|commit |String |[] |Version\-related commit. |
|release |String |v2.2.123 |Version. |
|create_at |Integer |1668483578 |Version release time. |

## Sample response

```JSON
{
    "error_msg": "",
    "error_no": 0,
    "data": {
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
                    "dataType": "string",
                    "name": "date",
                    "aggregate": "",
                    "id": "date"
                }
            ]
        },
        "extra": {
            "release_info": [
                {
                    "env": "test",
                    "create_at": 1668483578,
                    "release": "v2.2.123",
                    "commit": ""
                }
            ]
        },
        "info": [
            {
                "count": "1",
                "unit": "ms",
                "id": "count",
                "name": "blank screen count",
                "change": "1"
            }
        ]
    }
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
