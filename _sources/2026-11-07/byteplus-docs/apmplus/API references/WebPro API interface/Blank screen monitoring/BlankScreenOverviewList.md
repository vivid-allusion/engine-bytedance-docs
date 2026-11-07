---
title: "BlankScreenOverviewList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/BlankScreenOverviewList"
---

Get the blank screen list for different attribution types.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=BlankScreenOverviewList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |BlankScreenOverviewList |The API name. The current API name is `BlankScreenOverviewList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67940#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67940#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67940#filtercondition) |No |\- |The filter condition. |
|order_by |String |No |score |Sorting dimension.<br><br><br>* score<br><br>* client_time<br><br>* time<br><br>* count<br><br>* user |
|order |String |No |desc |The sorting method.<br><br><br>* desc<br><br>* asc |
|pgno |Long |Yes |1 |Page number. |
|pgsz |Long |Yes |10 |Number of items per page. |
|type |String |Yes |js_error |Attribution type.<br><br><br>* js_error<br><br>* resource_error<br><br>* http_error<br><br>* unclassified |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, **minipro**. |
|user |String |No |test_user |Username. |

### TimeFilter

|**Parameters** |**type** |**Required** |**Sample value** |**Description** |
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
|groupKey |String |No |context |Map type field key. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67940#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. This level cannot coexist with field, op, groupkey, and values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=BlankScreenOverviewList&Version=2022-10-12
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
    "type": "js_error, resource_error, http_error, unclassified",
    "order_by": "score,client_time,time,count,user",
    "filter_conditions": {
        "type": "and",
        "children": [
            {
                "type": "and",
                "children": [],
                "groupKey": "context",
                "field": "pid",
                "values": "[data explore]",
                "op": "in"
            }
        ],
        "values": "[data explore",
        "groupKey": "context",
        "field": "pid",
        "op": "in"
    },
    "order": "desc,asc"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|errno |Integer |0 |Error code. 0 indicates success. |
|errmsg |String |\- |Error message. Empty indicates success. |
|data |Object of [OverviewListResponseDataV2](https://docs.byteplus.com/en/docs/299/67940#overviewlistresponsedatav2) |\- |Blank\-screen attribution aggregation list. |

### OverviewListResponseDataV2

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|js_error |Object of [OverviewErrorListResponseData](https://docs.byteplus.com/en/docs/299/67940#overviewerrorlistresponsedata) |\- |List of white screen cases caused by JS errors. |
|http_error |Object of [ReqErrorResponseData](https://docs.byteplus.com/en/docs/299/67940#reqerrorresponsedata) |\- |List of blank screens caused by request errors. |
|unclassified |Object of [OverviewListResponseData](https://docs.byteplus.com/en/docs/299/67940#overviewlistresponsedata) |\- |List of unattributable blank screens. |
|resource_error |Object of [ResourceErrorResponseData](https://docs.byteplus.com/en/docs/299/67940#resourceerrorresponsedata) |\- |List of blank screens caused by static resource errors. |

### OverviewErrorListResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Long |10 |Total number of JS error aggregation types. |
|result |Array of [ErrorListItem](https://docs.byteplus.com/en/docs/299/67940#errorlistitem) |\- |JS error aggregation list. |

### ReqErrorResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Long |10 |Total number of request error clusters causing blank screens. |
|result |Array of [ReqErrorListItem](https://docs.byteplus.com/en/docs/299/67940#reqerrorlistitem) |\- |Aggregation list of request errors causing blank screens. |

### OverviewListResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Long |10 |Unattributable blank screen count. |
|result |Array of [ListItem](https://docs.byteplus.com/en/docs/299/67940#listitem) |\- |List of unattributable blank screens. |

### ResourceErrorResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Long |10 |Total number of static resource error clusters causing blank screens. |
|result |Array of [ResourceErrorListItem](https://docs.byteplus.com/en/docs/299/67940#resourceerrorlistitem) |\- |Aggregation list of static resource errors causing blank screens. |

### ErrorListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|message |String |Minified React error |Error message. |
|name |String |Error |Error type. |
|filename |String |12345.js |Error file name. |
|issue_id |String |12345 |Issue status operation |
|issue |Object of [IssueInfo](https://docs.byteplus.com/en/docs/299/67940#issueinfo) |\- |Issue assignment information. |
|meego_issue_url |String |\- |If issue_status is not done, this field is not set. |
|level |String |\- |Start and end time. |
|max_crash_time |Long |1667441262510 |Occurrence time of the latest JS error within the currently selected time range. |
|min_crash_time |Long |1666781177513 |Error and user count. |
|count |Long |10 |Errors and number of user count errors. |
|count_mini_chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67940#chartdata) |\- |Error count trend. |
|user |Long |10 |Affected user count. |
|user_mini_chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67940#chartdata) |\- |Affected user trend. |

### ReqErrorListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|path |String |path_test |Request error path. |
|user |Long |10 |Number of users affected by request errors. |
|count |Long |10 |Request error count. |
|domain |String |www.test.com |Request error domain. |
|user_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67940#chartdata) |\- |Trend of the number of users affected by request errors. |
|count_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67940#chartdata) |\- |Request error trend. |
|distribution |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67940#chartdata) |\- |Distribution of request error status codes. |

### ListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|pid |String |path_test |Blank screen page PID. |
|url |String |https://www.test.com/path_test?key1=value1 |Blank screen page URL. |
|score |Double |0 |Blank screen score. |
|screenshot |String |data:image/jpeg;base64,/9j/4AAQS |Base64\-encoded value of the blank screen on\-site screenshot. |
|session_id |String |049437a9 |session_id associated with the blank screen. |
|client_time |Long |1667313554658 |Client time when the blank screen occurred. |

### ResourceErrorListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|url |String |\- |Static resource error URL. |
|path |String |path_test |Static resource error path. |
|type |String |resource |Static resource error type. |
|user |Long |10 |Number of users affected by static resource errors. |
|count |Long |10 |Static resource error count. |
|domain |String |www.test.com |Static resource error domain. |
|user_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67940#chartdata) |\- |Trend of the number of users affected by static resource errors. |
|count_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67940#chartdata) |\- |Trend of static resource error count. |

### IssueInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|managers |Array of [IssueManager](https://docs.byteplus.com/en/docs/299/67940#issuemanager) |\- |Issue assignee. |
|status |String |processing |Issue status. |
|fixed_version |String |v1.1.2 |The fixed version. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67940#field) |\- |Line chart/pie chart dimensions. len(fields)=len(source[i]). |
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
    "errmsg": "",
    "data": {
        "http_error": {
            "result": [
                {
                    "user": 10,
                    "domain": "www.test.com",
                    "path": "path_test",
                    "distribution": {
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
                                "id": "date",
                                "name": "date",
                                "aggregate": "Sheet"
                            }
                        ]
                    },
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
                                "id": "date",
                                "name": "date",
                                "aggregate": "clubbing",
                                "dataType": "string"
                            }
                        ]
                    },
                    "count": 10,
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
                                "name": "date",
                                "dataType": "string",
                                "aggregate": ""
                            }
                        ]
                    }
                }
            ],
            "total": 10
        },
        "unclassified": {
            "result": [
                {
                    "url": "https://www.test.com/path_test?key1=value1",
                    "client_time": 1667313554658,
                    "session_id": "049437a9",
                    "score": 51,
                    "screenshot": "data:image/jpeg;base64,/9j/4AAQS",
                    "pid": "path_test"
                }
            ],
            "total": 10
        },
        "resource_error": {
            "result": [
                {
                    "path": "path_test",
                    "domain": "www.test.com",
                    "url": "reflection",
                    "count": 10,
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
                                "name": "date",
                                "dataType": "string",
                                "aggregate": ""
                            }
                        ]
                    },
                    "user": 10,
                    "type": "resource",
                    "count_trend": {
                        "fields": [
                            {
                                "name": "date",
                                "id": "date",
                                "aggregate": "virtue",
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
                    }
                }
            ],
            "total": 10
        },
        "js_error": {
            "result": [
                {
                    "user": 10,
                    "min_crash_time": 1666781177513,
                    "user_mini_chart": {
                        "fields": [
                            {
                                "dataType": "string",
                                "id": "date",
                                "name": "date",
                                "aggregate": "wildly"
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
                    "name": "Error",
                    "done_release": "percent",
                    "filename": "12345.js",
                    "count": 10,
                    "level": "disappear",
                    "max_crash_time": 1667441262510,
                    "issue_id": "12345",
                    "git_issue_url": "",
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
                                "aggregate": "",
                                "dataType": "string",
                                "name": "date",
                                "id": "date"
                            }
                        ]
                    },
                    "issue": {
                        "managers": [
                            {
                                "email": "test_user@test.com",
                                "name": "test_user",
                                "head_url": "",
                                "user_id": 12
                            }
                        ],
                        "id": 886,
                        "fixed_version": "v1.1.2",
                        "tag": [
                            {
                                "key": "",
                                "values": [
                                    {
                                        "value": "",
                                        "id": 419
                                    }
                                ],
                                "id": 401
                            }
                        ],
                        "status": "processing"
                    },
                    "message": "Minified React error",
                    "meego_issue_url": "beyond"
                }
            ],
            "total": 10
        }
    },
    "errno": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
