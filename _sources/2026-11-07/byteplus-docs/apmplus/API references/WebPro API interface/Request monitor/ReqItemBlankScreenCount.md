---
title: "ReqItemBlankScreenCount"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ReqItemBlankScreenCount"
---

Get the list of white screens caused by request errors.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ReqItemBlankScreenCount&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ReqItemBlankScreenCount |The API name. The current API name is `ReqItemBlankScreenCount`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|domain |String |No |www.test.com |Request domain. |
|path |String |No |\- |Request path. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67971#commonparams) |Yes |\- |Common parameter. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67971#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67971#filtercondition) |No |\- |The filter condition. |
|order_by |String |No |score,client_time |Sorting dimension. |
|order |String |No |desc,asc |Ascending or descending order. |
|pgno |Long |Yes |1 |Page number. |
|pgsz |Long |Yes |10 |Number of items per page. |

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
|groupKey |String |No |context |Key of the map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67971#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. This level cannot coexist with field, op, groupkey, and values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ReqItemBlankScreenCount&Version=2022-10-12
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
    "pgno": 1,
    "pgsz": 10,
    "domain": "www.test.com",
    "order_by": "score,client_time",
    "order": "desc,asc",
    "path": "",
    "filter_conditions": {
        "type": "and",
        "values": "[data explore]",
        "op": "in",
        "groupKey": "context",
        "field": "pid",
        "children": [
            {
                "type": "and",
                "values": "[data explore]",
                "children": [],
                "groupKey": "context",
                "field": "pid",
                "op": "in"
            }
        ]
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ReqItemBlankScreenResponseData](https://docs.byteplus.com/en/docs/299/67971#reqitemblankscreenresponsedata) |\- |List of white screens caused by request errors. |
|errmsg |String |\- |Error message. Empty indicates success. |
|errno |Integer |0 |Error code. 0 indicates success. |

### ReqItemBlankScreenResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Long |10 |Blank screen count. |
|result |Array of [ListItem](https://docs.byteplus.com/en/docs/299/67971#listitem) |\- |White\-screen list. |
|user_total |Long |10 |Number of users affected by white screens. |

### ListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|pid |String |path_test |White\-screen page PID. |
|url |String |https://www.test.com/path_test?key1=value1 |White\-screen page URL. |
|score |Double |0 |White\-screen score. |
|screenshot |String |data:image/jpeg;base64,/9j/4AAQS |Base64\-encoded value of the white\-screen screenshot captured on site.. |
|session_id |String |049437a9 |The session ID associated with the white screen. |
|client_time |Long |1667313554658 |Client time when the white screen occurred. |

## Sample response

```JSON
{
    "errno": 0,
    "data": {
        "result": [
            {
                "client_time": 1667313554658,
                "session_id": "049437a9",
                "pid": "path_test",
                "screenshot": "data:image/jpeg;base64,/9j/4AAQS",
                "url": "https://www.test.com/path_test?key1=value1",
                "score": -20
            }
        ],
        "user_total": 10,
        "total": 10
    },
    "errmsg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
