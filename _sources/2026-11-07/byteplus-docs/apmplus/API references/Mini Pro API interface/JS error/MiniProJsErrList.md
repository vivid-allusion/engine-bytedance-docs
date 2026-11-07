---
title: "MiniProJsErrList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProJsErrList"
---

View the JavaScript issue list.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProJsErrList&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProJsErrList |The API name. The current API name is `MiniProJsErrList`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68006#common) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/68006#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterConditions](https://docs.byteplus.com/en/docs/299/68006#filterconditions) |No |\- |The filter condition. |
|order_by |String |No |time_ascend |The sorting method.<br><br><br>* time_ascend<br><br>* time_descend<br><br>* count_ascend<br><br>* count_descend<br><br>* user_ascend<br><br>* user_descend |
|pgno |Long |No |1 |Page number. |
|pgsz |Long |No |10 |Number of items per page. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string ("") indicates all environments. |
|os |String |No |minipro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time. Unit: s. |
|granularity |Integer |No |3600 |Aggregation time granularity. Unit: s. |
|end_time |Integer |Yes |1665744613 |End time. Unit: s. |

### FilterConditions

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |The type of the filter condition.<br><br><br>* and: The conditions in children are in an "AND" relationship.<br><br>* rule (default): The condition is atomic.<br><br>   Only two levels are supported. The "type" of the first level must be "and", and the "type" of the second level must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operators. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Map type field key. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Condition values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of String |No |\- |If there are further conditions at the lower level, place them here. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProJsErrList&Version=2024-03-12
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
    "status": [
    ],
    "pgno": 1,
    "filter_conditions": {
        "type": "and",
        "children": [
            {
                "type": "and",
                "values": "[data explore]",
                "children": [
                ],
                "op": "in",
                "field": "pid",
                "groupKey": "context"
            }
        ],
        "field": "pid",
        "values": "[data explore]",
        "groupKey": "context",
        "op": "in"
    },
    "order_by": "time_ascend,time_descend,count_ascend,count_descend,user_ascend,user_descend",
    "managers": [
    ],
    "pgsz": 10
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_no |Integer |0 |Error message. 0 indicates a successful request. |
|error_msg |String |\- |Error message. It is empty if the request succeeds. |
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68006#data) |\- |JavaScript error aggregation list. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|result |Array of [Result](https://docs.byteplus.com/en/docs/299/68006#result) |\- |JavaScript error aggregation list. |
|total |Long |10 |Total number of JS error clusters. |

### Result

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|message |String |Minified React error |Error message. |
|name |String |Error |Error type. |
|filename |String |12345.js |Error file name. |
|issue_id |String |12345 |JavaScript error aggregation ID. |
|issue |Object of [Issue](https://docs.byteplus.com/en/docs/299/68006#issue) |\- |Issue assignment information. |
|level |String |\- |Error level. |
|max_crash_time |Long |1667441262510 |Occurrence time of the latest JavaScript error within the currently selected time range. |
|min_crash_time |Long |1666781177513 |Occurrence time of the earliest JavaScript error within the currently selected time range. |
|count |Long |10 |Errors and number of user count errors. |
|count_mini_chart |Object of [CountMiniChart](https://docs.byteplus.com/en/docs/299/68006#countminichart) |\- |Error count trend. |
|user |Long |10 |Number of impacted users. |
|user_mini_chart |Object of [UserMiniChart](https://docs.byteplus.com/en/docs/299/68006#userminichart) |\- |Impacted user count trend. |

### Issue

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |\- |The issue ID in MySQL. It is different from issue_id. |
|managers |Array of [Managers](https://docs.byteplus.com/en/docs/299/68006#managers) |\- |Issue assignee. |
|status |String |processing |Issue status. |
|fixed_version |String |v1.1.2 |Fixed version. |

### CountMiniChart

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Fields](https://docs.byteplus.com/en/docs/299/68006#fields) |\- |Dimensions of the line chart or pie chart. len(fields) = len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of data points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

### UserMiniChart

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Fields](https://docs.byteplus.com/en/docs/299/68006#fields) |\- |Dimensions of the line chart or pie chart. len(fields) = len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of data points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

### Managers

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |test_user |Assignee name. |
|user_id |Long |12 |Assignee ID. |
|email |String |test_user@test.com |Assignee email. |

### Fields

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |date |Dimension key. |
|dataType |String |string |Dimension type. |
|name |String |Date |Dimension name. |
|aggregate |String |\- |Aggregation method. |

## Sample response

```JSON
{
    "data": {
        "total": 10,
        "result": [
            {
                "issue": {
                    "fixed_version": "v1.1.2",
                    "managers": [
                        {
                            "head_url": "industry",
                            "user_id": 12,
                            "email": "test_user@test.com",
                            "name": "test_user"
                        }
                    ],
                    "status": "processing",
                    "tag": [
                        {
                            "values": [
                                {
                                    "id": 502,
                                    "value": "bladder"
                                }
                            ],
                            "id": 148,
                            "key": ""
                        }
                    ],
                    "id": 418
                },
                "user_mini_chart": {
                    "fields": [
                        {
                            "dataType": "string",
                            "id": "date",
                            "name": "date",
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
                "issue_id": "12345",
                "user": 10,
                "filename": "12345.js",
                "max_crash_time": 1667441262510,
                "done_release": "Out",
                "meego_issue_url": "",
                "git_issue_url": "",
                "name": "Error",
                "count": 10,
                "count_mini_chart": {
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
                            "aggregate": "warming",
                            "name": "date",
                            "id": "date"
                        }
                    ]
                },
                "min_crash_time": 1666781177513,
                "level": "",
                "message": "Minified React error"
            }
        ]
    },
    "error_no": 0,
    "error_msg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
