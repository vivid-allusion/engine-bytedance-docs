---
title: "ImprovedPerf"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ImprovedPerf"
---

Get the list of top 5 pages with optimized performance.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ImprovedPerf&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ImprovedPerf |The API name. The API name is `ImprovedPerf`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67965#timefilter) |Yes |\- |Time range. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67965#commonparams) |Yes |\- |Public parameters. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67965#filtercondition) |No |\- |The filter condition. |
|metric |String |Yes |fp |The key of the performance metric used for sorting. Supported values are fp, fcp, fmp, tti, load, and lcp. |
|type |String |No |avg |The aggregation method for the performance metric used for sorting. Supported aggregation methods are avg, pct50, pct75, pct90, and pct95. |
|min_count |Integer |No |1 |Sample size threshold. Pages below the threshold are excluded from the calculation. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time, in seconds. |
|end_time |Integer |Yes |1665744613 |End time, in seconds. |
|granularity |Integer |No |3600 |Aggregation granularity, in seconds. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

### FilterCondition

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The first level type must be "and", and the second level type must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, and not_regex. |
|groupKey |String |No |context |The key of the map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[data explore] |Condition values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67965#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ImprovedPerf&Version=2022-10-12
{
    "time_filter": {
        "start_time": 1665485413,
        "end_time": 1665744613,
        "granularity": 3600
    },
    "common": {
        "aid": 12345,
        "site_type": "web",
        "env": "online",
        "user": "test_user",
        "os": "webpro"
    },
    "metric": "fp，fcp,fmp,tti,load,lcp",
    "min_count": 1,
    "filter_conditions": {
        "type": "and",
        "op": "in",
        "values": "[data explore]",
        "field": "pid",
        "groupKey": "context",
        "children": [
            {
                "type": "and",
                "op": "in",
                "children": [],
                "field": "pid",
                "groupKey": "context",
                "values": "[data explore]"
            }
        ]
    },
    "type": "avg,pct50,pct75,pct90,pct95"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [PerfChangeItem](https://docs.byteplus.com/en/docs/299/67965#perfchangeitem) |\- |List of top 5 pages for performance optimization/deterioration. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### PerfChangeItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|to |Long |2345 |Performance metric value for the second half of the selected time range. |
|pid |String |path_test |Page ID. |
|from |Long |1234 |Performance metric value for the first half of the selected time range. |
|extra |Object of [TrendExtra](https://docs.byteplus.com/en/docs/299/67965#trendextra) |\- |Version release status within the selected time range. |
|trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67965#chartdata) |\- |Performance metric change trend. |

### TrendExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|release_info |Array of [ReleaseInfo](https://docs.byteplus.com/en/docs/299/67965#releaseinfo) |\- |Version release information. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67965#field) |\- |Dimensions of the line chart or pie chart. len(fields) = len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of data points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

### ReleaseInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|env |String |test |Version release environment. |
|commit |String |[] |Version\-related commit. |
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
    "data": [
        {
            "trend": {
                "fields": [
                    {
                        "id": "date",
                        "dataType": "string",
                        "aggregate": "",
                        "name": "date"
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
            "from": 1234,
            "pid": "path_test",
            "extra": {
                "release_info": [
                    {
                        "env": "test",
                        "release": "v2.2.123",
                        "create_at": 1668483578,
                        "commit": ""
                    }
                ]
            },
            "to": 2345
        }
    ],
    "error_no": 0,
    "error_msg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
