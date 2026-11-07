---
title: "ResourceErrorList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ResourceErrorList"
---

Get the static resource error list.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ResourceErrorList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ResourceErrorList |The API name. The current API name is `ResourceErrorList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67980#commonparams) |Yes |\- |Common parameter. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67980#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67980#filtercondition) |No |\- |The filter condition. |
|order_by |String |No |count,user |Sorting fields. |

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
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The first level type must be "and", and the second level type must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Condition values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67980#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ResourceErrorList&Version=2022-10-12
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
        "children": [
            {
                "type": "and",
                "values": "[data explore]",
                "op": "in",
                "groupKey": "context",
                "children": [],
                "field": "pid"
            }
        ],
        "op": "in",
        "groupKey": "context",
        "field": "pid",
        "values": "[data explore]"
    },
    "order_by": "count,user"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [ResourceErrorListItem](https://docs.byteplus.com/en/docs/299/67980#resourceerrorlistitem) |\- |Static resource error list. |
|error_no |Integer |0 |Error code. 0 indicates success. |
|error_msg |String |\- |Error message. An empty value indicates success. |

### ResourceErrorListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|url |String |\- |Static resource error URL. |
|path |String |path_test |Static resource error path. |
|type |String |resource |Static resource error type. |
|user |Long |10 |Number of users affected by static resource errors. |
|count |Long |10 |Static resource error count. |
|domain |String |www.test.com |Static resource error domain. |
|user_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67980#chartdata) |\- |Trend of the number of users affected by static resource errors. |
|count_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67980#chartdata) |\- |Trend of static resource error count. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67980#field) |\- |Dimensions of the line chart or pie chart. len(fields) = len(source[i]). |
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
    "error_no": 0,
    "data": [
        {
            "path": "",
            "count": 554,
            "user": 689,
            "type": "drum",
            "count_trend": {
                "fields": [
                    {
                        "name": "date",
                        "aggregate": "How",
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
            "user_trend": {
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
                        "dataType": "string",
                        "id": "date",
                        "aggregate": "sun"
                    }
                ]
            },
            "domain": "sets"
        }
    ]
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
