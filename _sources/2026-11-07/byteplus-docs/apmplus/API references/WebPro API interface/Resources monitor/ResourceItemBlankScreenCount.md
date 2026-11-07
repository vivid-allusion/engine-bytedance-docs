---
title: "ResourceItemBlankScreenCount"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ResourceItemBlankScreenCount"
---

Get the list of white\-screen incidents caused by static resource errors.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ResourceItemBlankScreenCount&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ResourceItemBlankScreenCount |The API name. The current API name is `ResourceItemBlankScreenCount`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|name |String |Yes |data:image/svg+xml |Static resource URL. |
|type |String |Yes |resource |Static resource type. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67983#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67983#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67983#filtercondition) |No |\- |The filter condition. |
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
|granularity |Integer |No |3600 |Aggregation granularity, in seconds. |

### FilterCondition

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The "type" of the first level must be "and", and the "type" of the second level must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67983#filtercondition) |No |\- |If there are further conditions at the lower level, place them here. This parameter is required when the type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ResourceItemBlankScreenCount&Version=2022-10-12
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
    "pgno": 1,
    "pgsz": 10,
    "order_by": "score,client_time",
    "filter_conditions": {
        "type": "and",
        "groupKey": "context",
        "values": "[data explore]",
        "field": "pid",
        "op": "in",
        "children": [
            {
                "type": "and",
                "groupKey": "context",
                "children": [],
                "field": "pid",
                "op": "in",
                "values": "[data explore]"
            }
        ]
    },
    "order": "desc,asc"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ResourceItemBlankScreenResponseData](https://docs.byteplus.com/en/docs/299/67983#resourceitemblankscreenresponsedata) |\- |A list of white\-screen incidents caused by static resource errors. |
|errmsg |String |\- |Error message. Empty indicates success. |
|errno |Integer |0 |Error code. 0 indicates success. |

### ResourceItemBlankScreenResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Long |10 |White\-screen count. |
|result |Array of [ListItem](https://docs.byteplus.com/en/docs/299/67983#listitem) |\- |White\-screen list. |
|user_total |Long |10 |Number of users impacted by white\-screens. |

### ListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|pid |String |path_test |PID of the white\-screen page. |
|url |String |https://www.test.com/path_test?key1=value1 |White\-screen page URL. |
|score |Double |0 |White\-screen score. |
|screenshot |String |data:image/jpeg;base64,/9j/4AAQS |Base64\-encoded value of the white\-screen screenshot captured on site. |
|session_id |String |049437a9 |The session ID associated with the white\-screen. |
|client_time |Long |1667313554658 |Client timestamp when the white\-screen incident occurred. |

## Sample response

```JSON
{
    "data": {
        "result": [
            {
                "url": "https://www.test.com/path_test?key1=value1",
                "score": 706,
                "session_id": "049437a9",
                "client_time": 1667313554658,
                "pid": "path_test",
                "screenshot": "data:image/jpeg;base64,/9j/4AAQS"
            }
        ],
        "user_total": 10,
        "total": 10
    },
    "errmsg": "",
    "errno": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
