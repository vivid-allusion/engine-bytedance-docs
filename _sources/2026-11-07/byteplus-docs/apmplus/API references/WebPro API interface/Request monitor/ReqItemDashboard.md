---
title: "ReqItemDashboard"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ReqItemDashboard"
---

Get the dashboard for a specific request.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ReqItemDashboard&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ReqItemDashboard |The API name. The current API name is `ReqItemDashboard`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|slow_duration |Long |Yes |3,000 |Slow request threshold. Unit: ms. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67974#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67974#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67974#filtercondition) |No |\- |The filter condition. |
|name |String |Yes |data:image/svg+xml |Static resource URL. |
|type |String |Yes |resource |Static resource type |

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
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67974#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. This level cannot coexist with field, op, groupkey, and values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ReqItemDashboard&Version=2022-10-12
{
    "domain": "www.test.com",
    "path": "",
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
        "op": "in",
        "groupKey": "context",
        "field": "pid",
        "children": [
            {
                "type": "and",
                "children": [],
                "field": "pid",
                "values": "[data explore]",
                "op": "in",
                "groupKey": "context"
            }
        ],
        "values": "[data explore]"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ReqItemDashboardData](https://docs.byteplus.com/en/docs/299/67974#reqitemdashboarddata) |\- |Request dashboard. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### ReqItemDashboardData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|sla_trend |Object of [DashBoardChartData](https://docs.byteplus.com/en/docs/299/67974#dashboardchartdata) |\- |Request SLA trend. |
|slow_trend |Object of [DashBoardChartData](https://docs.byteplus.com/en/docs/299/67974#dashboardchartdata) |\- |Slow request percentage trend. |
|sla_dashboard |Object of [DashBoardChartData](https://docs.byteplus.com/en/docs/299/67974#dashboardchartdata) |\- |Request SLA. |
|slow_dashboard |Object of [DashBoardChartData](https://docs.byteplus.com/en/docs/299/67974#dashboardchartdata) |\- |Slow request percentage. |

### DashBoardChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67974#chartdata) |\- |Request dashboard details. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67974#field) |\- |Line chart/pie chart dimensions, len(fields)=len(source[i]). |
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
        "slow_dashboard": {
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
                        "name": "date",
                        "dataType": "string",
                        "aggregate": ""
                    }
                ]
            },
            "extra": {
                "benchmark": 129
            }
        },
        "slow_trend": {
            "data": {
                "fields": [
                    {
                        "aggregate": "",
                        "name": "date",
                        "dataType": "string",
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
            "extra": {
                "benchmark": -79
            }
        },
        "sla_dashboard": {
            "data": {
                "fields": [
                    {
                        "aggregate": "",
                        "name": "date",
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
            },
            "extra": {
                "benchmark": 510
            }
        },
        "sla_trend": {
            "data": {
                "fields": [
                    {
                        "name": "date",
                        "id": "date",
                        "dataType": "string",
                        "aggregate": ""
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
                "benchmark": 115
            }
        }
    },
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
