---
title: "ResourceList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ResourceList"
---

Get static resource list.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ResourceList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ResourceList |The API name. The current API name is `ResourceList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67979#commonparams) |Yes |\- |Public parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67979#timefilter) |Yes |\- |Time range. |
|slow_duration |Long |Yes |3,000 |Slow loading threshold. |
|pgno |Long |Yes |1 |Page number. |
|pgsz |Long |Yes |10 |Number of items per page. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67979#filtercondition) |No |\- |The filter condition. |
|order_by |String |No |count |Sorting fields. Available values are slow_rate, slow_value, count, avg, pct25, pct50, pct70, pct90, and pct99. |

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
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The type of the first level must be "and", and the type of the second must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operators. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Condition values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67979#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ResourceList&Version=2022-10-12
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
    "slow_duration": 3000,
    "pgno": 1,
    "pgsz": 10,
    "order_by": "count,slow_rate,slow_value,avg,pct25,pct50,pct70,pct90,pct99",
    "filter_conditions": {
        "type": "and",
        "field": "pid",
        "children": [
            {
                "type": "and",
                "children": [],
                "values": "[data explore]",
                "field": "pid",
                "groupKey": "context",
                "op": "in"
            }
        ],
        "op": "in",
        "groupKey": "context",
        "values": "[data explore]"
    }
}
```

## Response parameters

|**Parameters** |**type** |**Sample value** |**Description** |
|---|---|---|---|
|error_msg |String |\- |Error message. An empty value indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |
|data |Object of [ResourceListData](https://docs.byteplus.com/en/docs/299/67979#resourcelistdata) |\- |Static resource list. |

### ResourceListData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [ResourceListItem](https://docs.byteplus.com/en/docs/299/67979#resourcelistitem) |\- |Static resource list. |
|total |Long |10 |Total number of static resource clusters. |

### ResourceListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |data:image/svg+xml |Static resource address. |
|type |String |resource |Static resource type. |
|value |String |1,000 |Static resource latency. |
|indicators |Array of [ResourceListItemIndicator](https://docs.byteplus.com/en/docs/299/67979#resourcelistitemindicator) |\- |The overview value of the static resource metric. |

### ResourceListItemIndicator

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Load count. |The metric name. |
|value |Long |1,000 |The metric value. |

## Sample response

```JSON
{
    "error_msg": "",
    "error_no": 0,
    "data": {
        "data": [
            {
                "name": "data:image/svg+xml",
                "value": "1000",
                "indicators": [
                    {
                        "label": "load count",
                        "value": 1000
                    }
                ],
                "type": "resource",
                "from_cache": true
            }
        ],
        "total": 10
    }
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
