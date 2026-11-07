---
title: "EventList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/EventList"
---

Get the custom event list.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=EventList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |EventList |The API name. The current API name is `EventList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67941#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67941#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67941#filtercondition) |Yes |\- |The filter condition. |
|search_text |String |No |event_test |Fuzzy search by event name. If this parameter is empty, all events are returned. |
|pgno |Integer |Yes |10 |Page number of the event list. |
|pgsz |Integer |Yes |10 |Number of items per page. |
|order_by |String |No |count_trend |Sorting dimension.<br><br><br>* count_trend<br><br>* user_trend |
|order |String |No |desc,asc |The sorting method.<br><br><br>* desc<br><br>* asc |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. If this parameter is empty, all environments are included. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, **minipro**. |
|user |String |No |test_user |Username. |

### TimeFilter

|**Parameters** |**type** |**Required** |**Sample value** |**Description** |
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
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67941#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=EventList&Version=2022-10-12
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
                "field": "pid",
                "values": "[data explore]",
                "op": "in",
                "children": [],
                "groupKey": "context"
            }
        ],
        "op": "in",
        "values": "[data explore]",
        "field": "pid",
        "groupKey": "context"
    },
    "pgno": 10,
    "pgsz": 10,
    "order": "desc,asc",
    "order_by": "count_trend，user_trend",
    "search_text": "event_test"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_no |Integer |0 |Error code. 0 indicates success. |
|error_msg |String |\- |Error message. Empty indicates success. |
|data |Object of [EventListData](https://docs.byteplus.com/en/docs/299/67941#eventlistdata) |\- |The event list. |

### EventListData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Integer |10 |Total number of custom events. |
|event_list |Array of [EventListItem](https://docs.byteplus.com/en/docs/299/67941#eventlistitem) |\- |The event list. |

### EventListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|event_name |String |event_test |Custom event name. |
|user_total |Integer |10 |Number of users reporting custom events. |
|user_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67941#chartdata) |\- |Trend of the count of users reporting custom events. |
|count_total |Integer |10 |Number of custom event reports. |
|count_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67941#chartdata) |\- |Custom event reporting trend. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67941#field) |\- |Dimensions of the line or pie chart. len(fields) = len(source[i]). |
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
    "data": {
        "event_list": [
            {
                "count_trend": {
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
                            "name": "date",
                            "id": "date"
                        }
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
                            "id": "date",
                            "aggregate": "",
                            "name": "date",
                            "dataType": "string"
                        }
                    ]
                },
                "user_total": 10,
                "event_name": "event_test",
                "count_total": 10
            }
        ],
        "total": 10
    },
    "error_no": 0,
    "error_msg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
