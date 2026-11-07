---
title: "ResourceItemDashboard"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ResourceItemDashboard"
---

Get the dashboard for a specified static resource.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ResourceItemDashboard&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ResourceItemDashboard |The API name. The current API name is `ResourceItemDashboard`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|name |String |Yes |data:image/svg+xml |Static resource URL. |
|type |String |Yes |resource |Static resource type. |
|slow_duration |Long |Yes |3,000 |Slow loading threshold. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67977#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67977#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67977#filtercondition) |No |\- |The filter condition. |

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
|op |String |No |in |Condition operators. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Map type field key. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67977#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. This level cannot coexist with field, op, groupkey, and values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ResourceItemDashboard&Version=2022-10-12
{
    "name": "data:image/svg+xml",
    "type": "resource",
    "slow_duration": 3000,
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
        "values": "[data explore]",
        "op": "in",
        "field": "pid",
        "groupKey": "context",
        "children": [
            {
                "type": "and",
                "groupKey": "context",
                "field": "pid",
                "values": "[data explore]",
                "op": "in",
                "children": []
            }
        ]
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ResourceItemDashboardData](https://docs.byteplus.com/en/docs/299/67977#resourceitemdashboarddata) |\- |Request dashboard. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### ResourceItemDashboardData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|sla_trend |Object of [DashBoardChartData](https://docs.byteplus.com/en/docs/299/67977#dashboardchartdata) |\- |Request SLA trend. |
|slow_trend |Object of [DashBoardChartData](https://docs.byteplus.com/en/docs/299/67977#dashboardchartdata) |\- |Slow request percentage trend. |
|sla_dashboard |Object of [DashBoardChartData](https://docs.byteplus.com/en/docs/299/67977#dashboardchartdata) |\- |Request SLA. |
|slow_dashboard |Object of [DashBoardChartData](https://docs.byteplus.com/en/docs/299/67977#dashboardchartdata) |\- |Slow request percentage. |

### DashBoardChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67977#chartdata) |\- |Request dashboard details. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67977#field) |\- |Line chart/pie chart dimensions. len(fields)=len(source[i]). |
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
    "error_msg": "",
    "data": {
        "slow_trend": {
            "extra": {
                "benchmark": 71
            },
            "data": {
                "fields": [
                    {
                        "aggregate": "",
                        "id": "date",
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
            }
        },
        "slow_dashboard": {
            "extra": {
                "benchmark": 183
            },
            "data": {
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
                        "name": "date",
                        "id": "date",
                        "dataType": "string",
                        "aggregate": ""
                    }
                ]
            }
        },
        "sla_dashboard": {
            "extra": {
                "benchmark": 963
            },
            "data": {
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
                        "aggregate": "",
                        "id": "date",
                        "name": "date"
                    }
                ]
            }
        },
        "sla_trend": {
            "data": {
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
                        "id": "date",
                        "dataType": "string",
                        "aggregate": "",
                        "name": "date"
                    }
                ]
            },
            "extra": {
                "benchmark": 365
            }
        }
    },
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
