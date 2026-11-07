---
title: "ResourceItemTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ResourceItemTrend"
---

Get the trend for a specified static resource.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ResourceItemTrend&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ResourceItemTrend |The API name. The API name is `ResourceItemTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|name |String |Yes |data:image/svg+xml |Static resource URL. |
|type |String |Yes |resource |Static resource type. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67984#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67984#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67984#filtercondition) |No |\- |The filter condition. |
|pick_type |String |Yes |avg |Aggregation method for total loading duration. Aggregation by avg, pct25, pct50, pct70, pct90, and pct99 is supported. |
|slow_duration |Long |Yes |3,000 |Slow loading threshold. |

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

|**Parameters** |**type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The type of the first level must be "and", and the type of the second level must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values are eq, neq, lt, lte, gt, gte, in, not_in, regex, and not_regex. |
|groupKey |String |No |context |Key of the map\-type field. The set of optional values can be obtained by the `GetFieldKeys` method. |
|values |Array of String |No |[data explore] |Condition values. The set of optional values can be obtained by the `GetFieldValues` method. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67984#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ResourceItemTrend&Version=2022-10-12
{
    "name": "data:image/svg+xml",
    "type": "resource",
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
    "pick_type": "avg,pct25,pct50,pct70,pct90,pct99",
    "slow_duration": 3000,
    "filter_conditions": {
        "type": "and",
        "values": "[data explore]",
        "op": "in",
        "field": "pid",
        "children": [
            {
                "type": "and",
                "children": [],
                "groupKey": "context",
                "field": "pid",
                "values": "[data explore]",
                "op": "in"
            }
        ],
        "groupKey": "context"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ResourceItemTrendData](https://docs.byteplus.com/en/docs/299/67984#resourceitemtrenddata) |\- |Trend of duration for each stage of static resources and distribution of total loading duration. |
|error_msg |String |\- |Error message. If the request was successful, this field is empty. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### ResourceItemTrendData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67984#chartdata) |\- |Duration trends for each stage of the static resource. |
|distribution |Object of [ResourceItemDistributionWithExtra](https://docs.byteplus.com/en/docs/299/67984#resourceitemdistributionwithextra) |\- |Distribution of total load duration of the static resource. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67984#field) |\- |Dimensions of the line chart or pie chart. len(fields) = len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of data points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

### ResourceItemDistributionWithExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|distribution |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67984#chartdata) |\- |Request duration distribution. |

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
    "error_no": 0,
    "data": {
        "distribution": {
            "distribution": {
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
            "extra": {
                "benchmark": 184,
                "value": 723,
                "label": "plankton"
            }
        },
        "trend": {
            "fields": [
                {
                    "name": "date",
                    "aggregate": "",
                    "id": "date",
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
        }
    }
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
