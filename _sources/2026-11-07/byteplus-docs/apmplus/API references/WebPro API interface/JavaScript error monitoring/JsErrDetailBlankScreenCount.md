---
title: "JsErrDetailBlankScreenCount"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/JsErrDetailBlankScreenCount"
---

Get the list of blank screens caused by JavaScript errors.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=JsErrDetailBlankScreenCount&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |JsErrDetailBlankScreenCount |The API name. The API name is `JsErrDetailBlankScreenCount`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67956#commonparams) |Yes |\- |Public parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67956#timefilter) |Yes |\- |Time range. |
|pgno |Long |Yes |1 |Page number. |
|pgsz |Long |Yes |10 |Number of items per page. |
|error_message |String |No |error message |JavaScript error message. |
|order_by |String |No |score,client_time |Sorting dimension. |
|order |String |No |desc,asc |Ascending or descending order. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67956#filtercondition) |No |\- |The filter condition. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string ("") indicates all environments.. |
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
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The type of the first level must be "and", and the type of the second level must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, and not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[data explore] |Condition values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67956#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=JsErrDetailBlankScreenCount&Version=2022-10-12
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
    "issue_id": "Terrace",
    "pgno": 1,
    "pgsz": 10,
    "error_message": "error message",
    "order_by": "score,client_time",
    "order": "desc,asc"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [OverallListResponseData](https://docs.byteplus.com/en/docs/299/67956#overalllistresponsedata) |\- |A list of white\-screen events. |
|errmsg |String |\- |Error message. If the request was successful, this field is empty. |
|errno |Integer |\- |Error code. 0 indicates success. |

### OverallListResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Long |10 |White\-screen count. |
|result |Array of [ListItem](https://docs.byteplus.com/en/docs/299/67956#listitem) |\- |A list of white\-screen events. |
|user_total |Long |10 |Number of users affected by white screens. |

### ListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|pid |String |path_test |PID associated with the white\-screen event. |
|url |String |https://www.test.com/path_test?key_1=value_1 |URL of the page where the white\-screen event occurred.. |
|score |Double |0 |White\-screen score. |
|screenshot |String |data:image/jpeg;base64,/9j |Base64\-encoded screenshot of the white screen page. |
|session_id |String |12345acd\-6400\-451a\-846c\-e1d5622a11fe |Session ID associated with the white\-screen event. |
|client_time |Long |12345678 |Client time when the blank screen occurred. |

## Sample response

```JSON
{
    "data": {
        "result": [
            {
                "session_id": "12345acd-6400-451a-846c-e1d5622a11fe",
                "screenshot": "data:image/jpeg;base64,/9j",
                "pid": "path_test",
                "client_time": 12345678,
                "score": 363,
                "url": "https://www.test.com/path_test?key_1=value_1"
            }
        ],
        "total": 10,
        "user_total": 10
    },
    "errmsg": "",
    "errno": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
