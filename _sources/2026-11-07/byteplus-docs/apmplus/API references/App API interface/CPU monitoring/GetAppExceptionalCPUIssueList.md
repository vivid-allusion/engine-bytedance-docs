---
title: "GetAppExceptionalCPUIssueList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalCPUIssueList"
---

Get the CPU issue list.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppExceptionalCPUIssueList&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppExceptionalCPUIssueList |The API name. The current API name is `GetAppExceptionalCPUIssueList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |No |1619827200 |Query start time (Unix timestamp). |
|end_time |Integer |No |1619913600 |Query end time (Unix timestamp). |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67897#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|page_no |Integer |No |1 |Requested page number. |
|page_size |Integer |No |10 |Number of issues requested per page. |
|order_by |String |No |crash_count_compare_ascend |Sorting fields and directions.<br><br><br>* crash_count_compare_ascend: Sort by crash count in ascending order<br><br>* crash_count_compare_descend: Sort by crash count in descending order<br><br>* crash_user_compare_ascend: Sort by crash\-affected user count in ascending order<br><br>* crash_user_compare_descend: Sort by crash\-affected user count in descending order<br><br>* count_per_user_compare_ascend: Sort by crash user rate in ascending order<br><br>* count_per_user_compare_descend: Sort by crash user rate in descending order<br><br>* average_usage_compare_ascend: Sort by average utilization in ascending order<br><br>* average_usage_compare_descend: Sort by average utilization in descending order<br><br>* average_speed_compare_ascend: Sort by average speed in ascending order<br><br>* average_speed_compare_descend: Sort by average speed in descending order |
|is_new |Integer |No |1 |Whether the issue is new.<br><br><br>* 1: Only show new issues<br><br>* 0: All issues |
|token |String |No |keyword |Keyword or token for search. |
|status |Array of String |No |["reopen", "solved"] |Filter issues by specific status.<br><br><br>* pending<br><br>* processing<br><br>* ignored<br><br>* solved<br><br>* reopen |
|tags |Array of Long |No |[123, 456] |Tag filtering, providing the ID of each tag in a list format. |
|managers |Array of Long |No |[123456789] |Filter issues by a specific owner ID. |


<span id="condition"></span>
### Condition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |The operator.<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|type |String |No |expression |The type of the filter condition.<br><br><br>* expression: The current condition is an expression.<br><br>* and: The current condition is a compound expression, and multiple sub\-conditions are in an AND logical relationship.<br><br>* or: The current condition is a compound expression, and multiple sub\-conditions are in an OR logical relationship.<br><br>* map: The current condition is of map type. |
|value |String |No |123456 |The filter value. |
|values |Array of String |No |[123456] |The filter value. Multiple filter values are supported. |
|map_key |String |No |key_1 |The key of the map type. It is required when the type is set to map. |
|dimension |String |No |aid |The name of the condition. |
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67897#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppExceptionalCPUIssueList&Version=2022-10-12
{
    "start_time": 1619827200,
    "end_time": 1619913600,
    "filters": {
        "type": "and",
        "sub_conditions": [
            {
                "dimension": "apm_version",
                "type": "expression",
                "op": "in",
                "values": [
                    "1.4.5"
                ]
            },
            {
                "dimension": "device_model",
                "type": "expression",
                "op": "in",
                "values": [
                    "MI 5X"
                ]
            }
        ]
    },
    "page_no": 1,
    "page_size": 10,
    "order_by": "crash_count_compare_ascend",
    "is_new": 1,
    "token": "keyword",
    "status": [
        "reopen",
        "solved"
    ],
    "tags": [
        123,
        456
    ],
    "managers": [
        123456789
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_no |Integer |0 |Error code. |
|error_msg |String |\- |Error message. |
|data |Object of [IssueListData](https://docs.byteplus.com/en/docs/299/67897#issuelistdata) |\- |Returned data. |


<span id="issuelistdata"></span>
### IssueListData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Integer |3 |Total number of items in the list. |
|result |Array of [IssueItem](https://docs.byteplus.com/en/docs/299/67897#issueitem) |\- |List details. |


<span id="issueitem"></span>
### IssueItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|os |String |android |The operating system.<br><br><br>* Android<br><br>* iOS |
|issue |Object of [IssueInfo](https://docs.byteplus.com/en/docs/299/67897#issueinfo) |\- |Tag and issue status, and information about handler issue status, currently including owner and status. |
|title |String |Out of memory error |Issue title. |
|issue_id |String |issue_12345 |Issue identifier. |
|crash_user |Long |50 |Number of crash\-affected users. |
|crash_count |Long |100 |The crash count. |
|crash_ratio |Double |0.05 |The crash rate. |
|event_detail |String |This error occurred in the home page module... |Detailed issue description. |
|average_speed |Double |1.5 |Android average process usage speed rate. |
|average_usage |Double |30.0 |iOS average process utilization. |
|count_per_user |Long |5 |Average number of reports per user launch. |
|end_app_version |String |1.0.1 |End app version. |
|earliest_event_id |String |event_123 |Earliest event ID. |
|latest_crash_time |Long |1619827200 |Timestamp of the most recent crash. |
|start_app_version |String |1.0.0 |Initial app version. |
|crash_user_compare |Double |0.2 |Change rate of crash\-affected user count compared to the previous period. |
|latest_report_time |Long |1619830800 |Timestamp of the latest report. |
|crash_count_compare |Double |0.1 |Crash count change rate compared to the previous period. |
|average_speed_compare |Double |0.1 |Android average process utilization change rate. |
|average_usage_compare |Double |0.05 |iOS average process utilization change rate. |
|count_per_user_compare |Double |0.1 |Change rate of the average number of reports per user launch. |
|end_update_version_code |String |1.0.1 |End app minor version |
|start_update_version_code |String |1.0.1 |Initial app minor version |


<span id="issueinfo"></span>
### IssueInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |1112121 |The issue ID in MySQL. It is different from issue_id. |
|tag |Array of [Tags](https://docs.byteplus.com/en/docs/299/67897#tags) |\- |Label. |
|status |String |processing |Issue status.<br><br><br>* pending<br><br>* processing<br><br>* ignored<br><br>* solved<br><br>* reopen |
|fixed_version |String |v1.1.2 |The fixed version. |


<span id="tags"></span>
### Tags


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |301 |The tag ID. |
|key |String |component |The tag key. |
|values |Array of [ValueId](https://docs.byteplus.com/en/docs/299/67897#valueid) |[{"id": 202, "value": "backend"}, {"id": 203, "value": "frontend"}] |The tag value. |


<span id="valueid"></span>
### ValueId


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |201 |tag valueID。 |
|value |String |production |The tag value. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "error_no": 0,
    "error_msg": "",
    "data": {
        "total": 3,
        "result": [
            {
                "os": "android",
                "issue": {
                    "id": 1112121,
                    "tag": [
                        {
                            "id": 301,
                            "key": "component",
                            "values": [
                                {
                                    "id": 201,
                                    "value": "production"
                                }
                            ]
                        }
                    ],
                    "status": "processing",
                    "fixed_version": "v1.1.2"
                },
                "title": "Memory overflow error",
                "issue_id": "issue_12345",
                "crash_user": 50,
                "crash_count": 100,
                "crash_ratio": 0.05,
                "event_detail": "This error occurred in the home page module...",
                "average_speed": 1.5,
                "average_usage": 30,
                "count_per_user": 5,
                "end_app_version": "1.0.1",
                "earliest_event_id": "event_123",
                "latest_crash_time": 1619827200,
                "start_app_version": "1.0.0",
                "crash_user_compare": 0.2,
                "latest_report_time": 1619830800,
                "crash_count_compare": 0.1,
                "average_speed_compare": 0.1,
                "average_usage_compare": 0.05,
                "count_per_user_compare": 0.1
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
