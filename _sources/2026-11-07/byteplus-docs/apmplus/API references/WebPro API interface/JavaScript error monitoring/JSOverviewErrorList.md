---
title: "JSOverviewErrorList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/JSOverviewErrorList"
---

Get JS error aggregation list.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=JSOverviewErrorList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |JSOverviewErrorList |The API name. The current API name is `JSOverviewErrorList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67954#commonparams) |Yes |\- |Public parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67954#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67954#filtercondition) |No |\- |The filter condition. |
|order_by |String |No |time_ascend |The sorting method.<br><br><br>* time_ascend<br><br>* time_descend<br><br>* count_ascend<br><br>* count_descend<br><br>* user_ascend<br><br>* user_descend |
|pgno |Long |No |1 |Page number. |
|pgsz |Long |No |10 |Number of items per page. |

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
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The first level type must be "and", and the second level type must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operators. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67954#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=JSOverviewErrorList&Version=2022-10-12
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
    "status": [],
    "pgno": 1,
    "filter_conditions": {
        "type": "and",
        "children": [
            {
                "type": "and",
                "values": "[data explore]",
                "children": [],
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
    "managers": [],
    "pgsz": 10
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |
|data |Object of [OverviewErrorListResponseData](https://docs.byteplus.com/en/docs/299/67954#overviewerrorlistresponsedata) |\- |JS error aggregation list. |

### OverviewErrorListResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Long |10 |Total number of JS error aggregation types. |
|result |Array of [ErrorListItem](https://docs.byteplus.com/en/docs/299/67954#errorlistitem) |\- |JS error aggregation list. |

### ErrorListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|message |String |Minified React error |Error message. |
|name |String |Error |Error type. |
|filename |String |12345.js |Error file name. |
|issue_id |String |12345 |Issue status operation |
|issue |Object of [IssueInfo](https://docs.byteplus.com/en/docs/299/67954#issueinfo) |\- |Issue assignment information. |
|meego_issue_url |String |\- |If issue_status is not done, this field is not set. |
|level |String |\- |Start and end time. |
|max_crash_time |Long |1667441262510 |Occurrence time of the latest JS error within the currently selected time range. |
|min_crash_time |Long |1666781177513 |Error and user count. |
|count |Long |10 |Errors and number of user count errors. |
|count_mini_chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67954#chartdata) |\- |Error count trend. |
|user |Long |10 |Affected user count. |
|user_mini_chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67954#chartdata) |\- |Affected user trend. |

### IssueInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|managers |Array of [IssueManager](https://docs.byteplus.com/en/docs/299/67954#issuemanager) |\- |Issue assignee. |
|status |String |processing |Issue status. |
|fixed_version |String |v1.1.2 |The fixed version. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67954#field) |\- |Line chart/pie chart dimensions, len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of specific points in the trend chart. len(source) is the number of points in the line chart or the number of blocks in the pie chart. |

### IssueManager

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |test_user |Assignee name. |
|email |String |test_user@test.com |Assignee email. |
|user_id |Long |12 |Assignee ID. |

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

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
