---
title: "JSErrDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/JSErrDetail"
---

Get JavaScript error details.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=JSErrDetail&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |JSErrDetail |The API name. The API name is `JSErrDetail`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67953#commonparams) |Yes |\- |Public parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67953#timefilter) |Yes |\- |Time range. |
|issue_id |String |Yes |2769ad7223a4eaefffbe9b2f59bb933b |JavaScript error aggregation ID. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67953#filtercondition) |No |\- |The filter condition. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string ("") indicates all environments. |
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
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67953#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupkey, or values at the same level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=JSErrDetail&Version=2022-10-12
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
    "issue_id": "2769ad7223a4eaefffbe9b2f59bb933b"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [JSErrDetail](https://docs.byteplus.com/en/docs/299/67953#jserrdetail) |\- |JavaScript error details. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### JSErrDetail

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |\- |Error name and type. |
|message |String |Error: message test |Error message. |
|filename |String |12345.js |Error file name. |
|user |Long |10 |Error and user count information: Number of users affected by the JavaScript error. |
|count |Long |10 |JavaScript error. |
|issue_id |String |1234567223a4eaefffbe9b2f59bb933b |Issue\-related information: JavaScript error aggregation ID. |
|issue |Object of [IssueInfo](https://docs.byteplus.com/en/docs/299/67953#issueinfo) |\- |Issue status operation and assignment information. |
|min_crash_time |Long |1668561659926 |Occurrence time of the earliest JavaScript error within the selected time interval. |
|max_crash_time |Long |1678561659926 |Occurrence time of the latest JavaScript error within the selected time range. |
|min_crash_release |String |v1.2.3 |Earliest version in which the JS error occurred within the selected time range. |
|max_crash_release |String |v1.2.4 |Latest version in which the JavaScript error occurred within the selected time range. |
|min_crash_pid |String |pid_1 |The page on which the JavaScrip error first occurred within the selected time range. |
|max_crash_pid |String |pid_2 |The page on which the JavaScrip error last occurred within the selected time range. |
|trends |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67953#chartdata) |\- |JavaScript error trend chart. |
|extra |Object of [TrendExtra](https://docs.byteplus.com/en/docs/299/67953#trendextra) |\- |Additional information about JavaScript errors. |
|release_distribution |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67953#chartdata) |\- |Version distribution. |
|pid_distribution |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67953#chartdata) |\- |Page distribution. |
|releases |Array of String |\- |List of versions where JavaScript errors occurred. |

### IssueInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|managers |Array of [IssueManager](https://docs.byteplus.com/en/docs/299/67953#issuemanager) |\- |Issue assignee. |
|status |String |processing |Issue status. |
|fixed_version |String |v1.1.2 |The fixed version. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67953#field) |\- |Dimensions of the line chart or pie chart. len(fields) = len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of data points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

### TrendExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|release_info |Array of [ReleaseInfo](https://docs.byteplus.com/en/docs/299/67953#releaseinfo) |\- |Release status. |

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

### ReleaseInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|env |String |test |Release environment. |
|commit |String |[] |Version\-related commits. |
|release |String |v2.2.123 |Version. |
|create_at |Integer |1668483578 |Release time. |

## Sample response

```JSON
{
    "data": {
        "extra": {
            "release_info": [
                {
                    "commit": "",
                    "create_at": 1668483578,
                    "env": "test",
                    "release": "v2.2.123"
                }
            ]
        },
        "release_distribution": {
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
                    "aggregate": "",
                    "dataType": "string",
                    "id": "date"
                }
            ]
        },
        "releases": [],
        "message": "Error: message test",
        "trends": {
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
                    "aggregate": "",
                    "id": "date",
                    "dataType": "string"
                }
            ]
        },
        "issue": {
            "fixed_version": "v1.1.2",
            "tag": [
                {
                    "key": "",
                    "id": 172,
                    "values": [
                        {
                            "value": "",
                            "id": 346
                        }
                    ]
                }
            ],
            "managers": [
                {
                    "head_url": "",
                    "email": "test_user@test.com",
                    "name": "test_user",
                    "user_id": 12
                }
            ],
            "status": "processing",
            "id": 944
        },
        "max_crash_pid": "pid_2",
        "meego_issue_url": "powerful",
        "issue_id": "1234567223a4eaefffbe9b2f59bb933b",
        "filename": "12345.js",
        "git_issue_url": "I'm",
        "user": 10,
        "count": 10,
        "min_crash_time": 1668561659926,
        "name": "together",
        "pid_distribution": {
            "fields": [
                {
                    "id": "date",
                    "dataType": "string",
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
        "max_crash_release": "v1.2.4",
        "min_crash_release": "v1.2.3",
        "max_crash_time": 1678561659926,
        "min_crash_pid": "pid_1"
    },
    "error_no": 0,
    "error_msg": ""
}
```

## Error codes

There are no specific error codes for this API currently. If the API call returns an error,  see [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes).
