---
title: "ReqItemTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ReqItemTrend"
---

Get the latency trend for a specific request.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ReqItemTrend&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ReqItemTrend |The API name. The API name is `ReqItemTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67968#commonparams) |Yes |\- |Common parameter. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67968#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67968#filtercondition) |No |\- |The filter condition. |
|type |String |Yes |avg |Request latency aggregation method. Supports aggregation by avg, pct25, pct50, pct70, pct90, pct95, and pct99. |
|slow_duration |Long |Yes |3,000 |Slow request threshold. |
|name |String |Yes |data:image/svg+xml |Static resource URL. |
|pick_type |String |Yes |avg |Aggregation method for total loading duration. Supports aggregation by avg, pct25, pct50, pct70, pct90, pct95, and pct99. |

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
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The type of the first level must be "and", and the type of the second level must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, and not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Condition values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67968#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ReqItemTrend&Version=2022-10-12
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
    "type": "avg,pct25,pct50,pct70,pct90,pct95,pct99",
    "slow_duration": 3000,
    "filter_conditions": {
        "type": "and",
        "op": "in",
        "groupKey": "context",
        "field": "pid",
        "values": "[data explore]",
        "children": [
            {
                "type": "and",
                "groupKey": "context",
                "values": "[data explore]",
                "children": [],
                "op": "in",
                "field": "pid"
            }
        ]
    },
    "path": "",
    "domain": "www.test.com"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ReqItemTrendData](https://docs.byteplus.com/en/docs/299/67968#reqitemtrenddata) |\- |Request latency trend and distribution. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### ReqItemTrendData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67968#chartdata) |\- |Request latency trend. |
|distribution |Object of [ReqItemDistributionWithExtra](https://docs.byteplus.com/en/docs/299/67968#reqitemdistributionwithextra) |\- |Request latency distribution. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67968#field) |\- |Dimensions of the line chart or pie chart. len(fields) = len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of data points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

### ReqItemDistributionWithExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|distribution |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67968#chartdata) |\- |Request latency distribution. |

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
        "trend": {
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
        "distribution": {
            "distribution": {
                "fields": [
                    {
                        "id": "date",
                        "aggregate": "",
                        "dataType": "string",
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
            "extra": {
                "label": "",
                "value": 330,
                "benchmark": 991
            }
        }
    },
    "error_no": 0,
    "error_msg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
