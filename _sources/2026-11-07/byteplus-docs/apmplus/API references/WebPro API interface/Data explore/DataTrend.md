---
title: "DataTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/DataTrend"
---

Get the report trend for a specific type.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=DataTrend&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DataTrend |The API name. The current API name is `DataTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67951#commonparams) |Yes |\- |Common parameter. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67951#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67951#filtercondition) |No |\- |The filter condition. |
|ev_type |String |Yes |session |Report type.<br><br><br>* session<br><br>* view<br><br>* js_error<br><br>* action<br><br>* http<br><br>* resource<br><br>* resource_error<br><br>* custom<br><br>* log<br><br>* performance_longtask<br><br>* blank_screen |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service Type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time, in seconds. |
|end_time |Integer |Yes |1665744613 |End time, in seconds. |
|granularity |Integer |No |3600 |Aggregation time granularity, in seconds. |

### FilterCondition

|**Parameters** |**type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The first level type must be "and", and the second level type must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operators. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Map type field key. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67951#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. This level cannot coexist with field, op, groupkey, and values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=DataTrend&Version=2022-10-12
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
    "ev_type": "session,view,js_error,action,http,resource,resource_error,custom,log,performance_longtask,blank_screen",
    "filter_conditions": {
        "type": "and",
        "values": "[data explore]",
        "children": [
            {
                "type": "and",
                "op": "in",
                "field": "pid",
                "children": [],
                "values": "[data explore]",
                "groupKey": "context"
            }
        ],
        "field": "pid",
        "groupKey": "context",
        "op": "in"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67951#chartdata) |\- |Report trend for a specific type. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### ChartData

|**Parameters** |**type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67951#field) |\- |Line chart/pie chart dimensions, len(fields)=len(source[i]). |
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
                "dataType": "string",
                "aggregate": "",
                "id": "date"
            }
        ]
    },
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
