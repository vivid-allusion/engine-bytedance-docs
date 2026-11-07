---
title: "GetJsErrorListPerAction"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetJsErrorListPerAction"
---

Get the list of JavaScript errors associated with the specified action.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetJsErrorListPerAction&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetJsErrorListPerAction |The API name. The current API name is `GetJsErrorListPerAction`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|action_type |String |Yes |click |Action type. Call the `GetActionOverviewList` API to view available values. |
|pid |String |Yes |Data explore |Page ID. Call the `GetActionOverviewList` API to view available values. |
|action_target_name |String |Yes |Description |Action name. Call the `GetActionOverviewList` API to view available values. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67917#commonparams) |Yes |\- |Common parameter. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67917#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67917#filtercondition) |No |\- |The filter condition. |
|order_by |String |No |count_descend |Sorting order.<br><br><br>* count_ascend: Ascending order<br><br>* count_descend (default): Descending order |
|pgno |Long |No |1 |The page number for a pagination query. |
|pgsz |Long |No |10 |The number of items per page for a pagination query. |

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
|op |String |No |in |Condition operators. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Map type field key. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67917#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. This level cannot coexist with field, op, groupkey, and values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetJsErrorListPerAction&Version=2022-10-12
{
    "common":{
        "aid":12345
    },
    "time_filter":{
        "start_time":1664621845,
        "end_time":1665140253,
        "granularity":86400
    },
    "action_type":"click",
    "pid":"data explore",
    "action_target_name":"description",
    "metric_type":"avg",
    "filter_conditions":{
        "type":"and",
        "children":[
            {
                "op":"in",
                "field":"pid",
                "values":[
                    "data explore"
                ]
            }
        ]
    },
    "pgsz":20,
    "pgno":1,
    "order_by":"count_descend"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_msg |String |"" |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |
|data |Object of [OverviewErrorListResponseData](https://docs.byteplus.com/en/docs/299/67917#overviewerrorlistresponsedata) |\- |List of white screen cases caused by JS errors. |

### OverviewErrorListResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Long |10 |Total number of JS error clusters. |
|result |Array of [ErrorListItem](https://docs.byteplus.com/en/docs/299/67917#errorlistitem) |\- |JS error aggregation list. |

### ErrorListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|message |String |Minified React error |Error message. |
|name |String |Error |Error type. |
|filename |String |12345.js |Error file name. |
|issue_id |String |12345 |Issue status operation |
|issue |Object of [IssueInfo](https://docs.byteplus.com/en/docs/299/67917#issueinfo) |\- |Issue assignment information. |
|meego_issue_url |String |\- |If issue_status is not done, this field is not set. |
|level |String |\- |Start and end time. |
|max_crash_time |Long |1667441262510 |Occurrence time of the latest JS error within the currently selected time range. |
|min_crash_time |Long |1666781177513 |Error and user count. |
|count |Long |10 |Number of errors in the error and user count statistics. |
|count_mini_chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67917#chartdata) |\- |Error count trend. |
|user |Long |10 |Affected user count. |
|user_mini_chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67917#chartdata) |\- |Affected user trend. |

### IssueInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|managers |Array of [IssueManager](https://docs.byteplus.com/en/docs/299/67917#issuemanager) |\- |Issue assignee. |
|status |String |processing |Issue status. |
|fixed_version |String |v1.1.2 |The fixed version. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67917#field) |\- |Line chart/pie chart dimensions. len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of data points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

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
    "err_detail":"",
    "data":{
        "measure_category_meta_list":[
            {
                "key":"pageview",
                "label":"user analysis",
                "type":"simple",
                "measure_meta_list":[
                    {
                        "key":"",
                        "type":"basic",
                        "label":"PV",
                        "short_label":"",
                        "measure_name":"pv_uv.count"
                    },
                    {
                        "key":"",
                        "type":"basic",
                        "label":"UV",
                        "short_label":"",
                        "measure_name":"pv_uv.user"
                    },
                    {
                        "key":"",
                        "type":"basic",
                        "label":"Session count",
                        "short_label":"",
                        "measure_name":"pv_uv.session_count"
                    }
                ]
            }
        ]
    },
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
