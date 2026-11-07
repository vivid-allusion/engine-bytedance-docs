---
title: "ReqList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ReqList"
---

Get request list.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ReqList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ReqList |The API name. The current API name is `ReqList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67973#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67973#timefilter) |Yes |\- |Time range. |
|slow_duration |Long |Yes |3,000 |Slow request threshold. Unit: ms. |
|pgno |Long |Yes |1 |Page number. |
|pgsz |Long |Yes |10 |Number of items per page. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67973#filtercondition) |No |\- |The filter condition. |
|order_by |String |No |slow_value |The sorting method. Available values are slow_rate, slow_value, count, avg, pct25, pct50, pct70, pct90, and pct99. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, **minipro**. |
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
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The type of the first level must be "and", and the type of the second must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operators. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Map type field key. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67973#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ReqList&Version=2022-10-12
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
    "filter_conditions": {
        "type": "and",
        "op": "in",
        "values": "[data explore]",
        "field": "pid",
        "groupKey": "context",
        "children": [
            {
                "type": "and",
                "groupKey": "context",
                "children": [],
                "op": "in",
                "field": "pid",
                "values": "[data explore]"
            }
        ]
    },
    "order_by": "slow_value, slow_rate, count, avg, pct25,pct50,pct70,pct90,pct99"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |
|data |Object of [ReqListData](https://docs.byteplus.com/en/docs/299/67973#reqlistdata) |\- |Request list. |

### ReqListData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [ReqListItem](https://docs.byteplus.com/en/docs/299/67973#reqlistitem) |\- |Request list. |
|total |Long |\- |Total number of request aggregation types. |

### ReqListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|path |String |\- |Request path. |
|value |String |2,000 |Request latency. |
|domain |String |www.test.com |Request domain. |
|method |String |POST |Request method. |
|indicators |Array of [ReqListItemIndicator](https://docs.byteplus.com/en/docs/299/67973#reqlistitemindicator) |\- |The overview value of the request metric. |

### ReqListItemIndicator

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Slow request count |Request metric name. |
|value |Long |1,000 |Request metric name. |

## Sample response

```JSON
{
    "data": {
        "data": [
            {
                "value": "2000",
                "domain": "www.test.com",
                "indicators": [
                    {
                        "value": 1000,
                        "label": "slow request count"
                    }
                ],
                "method": "POST",
                "path": "",
                "from_cache": false
            }
        ],
        "total": 606
    },
    "error_msg": "",
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
