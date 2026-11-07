---
title: "ReqSlowList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ReqSlowList"
---

Get the top 10 slow requests.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ReqSlowList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ReqSlowList |The API name. The current API name is `ReqSlowList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67975#commonparams) |Yes |\- |Common parameter. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67975#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67975#filtercondition) |No |\- |The filter condition. |
|slow_duration |Long |Yes |2,000 |Slow request threshold, in milliseconds. |
|order_by |String |No |slow_rate |The sorting method. Supports sorting by slow_rate, slow_value, count, avg, pct25, pct50, pct70, pct90, and pct99. |
|type |String |No |avg |Request latency aggregation method. Supports aggregation by avg, pct25, pct50, pct70, pct90, pct95, and pct99. |

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
|groupKey |String |No |context |Map type field key. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67975#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ReqSlowList&Version=2022-10-12
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
    "slow_duration": 2000,
    "type": "avg,pct25,pct50,pct70,pct90,pct95,pct99",
    "filter_conditions": {
        "type": "and",
        "children": [
            {
                "type": "and",
                "op": "in",
                "groupKey": "context",
                "children": [],
                "values": "[data explore]",
                "field": "pid"
            }
        ],
        "values": "[data explore]",
        "groupKey": "context",
        "field": "pid",
        "op": "in"
    },
    "order_by": "slow_rate,slow_value,count,avg,pct25,pct50,pct70,pct90,pct99"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [ReqSlowListItem](https://docs.byteplus.com/en/docs/299/67975#reqslowlistitem) |\- |Top 10 slow requests. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### ReqSlowListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|path |String |path_test |Request path. |
|domain |String |www.test.com |Request domain. |
|duration |Long |1200 |Request latency, in milliseconds. |
|slow_rate |String |0.12 |Slow request rate. |
|user_rate |String |0.12 |Rate of users affected by slow requests. |
|rate_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67975#chartdata) |\- |Slow request rate trend. |
|user_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67975#chartdata) |\- |Trend in the rate of users affected by slow requests. |
|duration_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67975#chartdata) |\- |Request latency trend. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67975#field) |\- |Line chart/pie chart dimensions. len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of specific points in the trend chart. len(source) is the number of points in the line chart or the number of blocks in the pie chart. |

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
    "error_msg": "",
    "data": [
        {
            "domain": "www.test.com",
            "user_trend": {
                "fields": [
                    {
                        "dataType": "string",
                        "aggregate": "",
                        "id": "date",
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
            "duration": 1200,
            "user_rate": "0.12",
            "duration_trend": {
                "fields": [
                    {
                        "name": "date",
                        "id": "date",
                        "aggregate": "",
                        "dataType": "string"
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
            "slow_rate": "0.12",
            "rate_trend": {
                "fields": [
                    {
                        "dataType": "string",
                        "name": "date",
                        "aggregate": "",
                        "id": "date"
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
            "path": "path_test"
        }
    ],
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
