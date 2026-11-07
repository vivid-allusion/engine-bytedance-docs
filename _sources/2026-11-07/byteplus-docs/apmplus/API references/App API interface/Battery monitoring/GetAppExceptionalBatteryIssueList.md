---
title: "GetAppExceptionalBatteryIssueList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatteryIssueList"
---

Get the list of app battery anomalies.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppExceptionalBatteryIssueList&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppExceptionalBatteryIssueList |The API name. The current API name is `GetAppExceptionalBatteryIssueList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |No |1619827200 |Query start time (Unix timestamp). |
|end_time |Integer |No |1619913600 |Query end time (Unix timestamp). |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67911#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|is_new |Integer |No |0 |Whether it is a new issue.<br><br><br>* 0: Not a new issue<br><br>* 1: New issue |
|page_no |Integer |No |1 |Page number. |
|page_size |Integer |No |20 |Page size. |
|status |Array of String |No |pending |Processing state.<br><br><br>* pending<br><br>* processing<br><br>* ignored<br><br>* solved<br><br>* reopen |
|managers |Array of Long |No |[123456, 789012] |Filter by manager. Pass a list of user IDs. |
|tags |Array of Long |No |[111, 222] |Pass a list of custom tag IDs. |
|token |String |No |keyword |The search keyword. |
|order_by |String |No |trace_cnt_desc |Sorting fields and methods. |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67911#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppExceptionalBatteryIssueList&Version=2022-10-12
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
    "is_new": 0,
    "page_no": 1,
    "page_size": 20,
    "status": [
        "pending"
    ],
    "managers": [
        123456,
        789012
    ],
    "tags": [
        111,
        222
    ],
    "token": "keyword",
    "order_by": "trace_cnt_desc"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [BatteryTraceIssueData](https://docs.byteplus.com/en/docs/299/67911#batterytraceissuedata) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="batterytraceissuedata"></span>
### BatteryTraceIssueData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Integer |10 |Total number of items in the list. |
|result |Array of [IssuePageItem](https://docs.byteplus.com/en/docs/299/67911#issuepageitem) |\- |List details. |


<span id="issuepageitem"></span>
### IssuePageItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|issue |Object of [IssueInfo](https://docs.byteplus.com/en/docs/299/67911#issueinfo) |\- |Issue status information, currently including owner and status. |
|stack |Object of [ParsedStack](https://docs.byteplus.com/en/docs/299/67911#parsedstack) |\- |Stack trace information. |
|issue_id |String |issue_12345 |The issue ID. |
|trace_cnt |Integer |100 |Occurrence count. |
|trace_type |Integer |1 |Tracking type. |
|trace_user |Integer |50 |Affected user count. |
|end_app_version |String |1.0.5 |The end app version. |
|first_event_time |Integer |1619820000 |First event time. |
|last_report_time |Integer |1619900000 |Time of the last report. |
|start_app_version |String |1.0.0 |The starting app version. |
|trace_cnt_compare |Double |0.1 |Occurrence count change rate. |
|trace_user_compare |Double |0.2 |Affected user count change rate. |
|end_update_version_code |String |1.0.5 |End app minor version |
|start_update_version_code |String |1.0.0 |Initial app minor version |


<span id="issueinfo"></span>
### IssueInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |1112121 |The issue ID in MySQL. It is different from issue_id. |
|tag |Array of [Tags](https://docs.byteplus.com/en/docs/299/67911#tags) |\- |Label. |
|status |String |processing |Issue status.<br><br><br>* pending<br><br>* processing<br><br>* ignored<br><br>* solved<br><br>* reopen |
|fixed_version |String |v1.1.2 |The fixed version. |


<span id="parsedstack"></span>
### ParsedStack


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|brief |String |Crash due to null object reference |Brief description of the stack trace. |
|title |String |NullPointerException |Stack trace title. |
|detail |String |at com.example.myapp.MainActivity.onCreate |Stack trace details. |
|error_msg |String |retrace error |Retrace symbol table error. A prompt for users. |
|unexist_libs |JSON Map | |Missing symbol table information, key: add\-on name, value: UUID. |


<span id="tags"></span>
### Tags


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |301 |The tag ID. |
|key |String |component |The tag key. |
|values |Array of [ValueId](https://docs.byteplus.com/en/docs/299/67911#valueid) |[{"id": 202, "value": "backend"}, {"id": 203, "value": "frontend"}] |The tag value. |


<span id="unexistlibs"></span>
### UnexistLibs


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |The name of the missing add\-on. |
|value |String |\- |The UUID of the missing add\-on. |


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
    "data": {
        "total": 10,
        "result": [
            {
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
                "stack": {
                    "brief": "Crash due to null object reference",
                    "title": "NullPointerException",
                    "detail": "at com.example.myapp.MainActivity.onCreate"
                },
                "issue_id": "issue_12345",
                "trace_cnt": 100,
                "trace_type": 1,
                "trace_user": 50,
                "end_app_version": "1.0.5",
                "first_event_time": 1619820000,
                "last_report_time": 1619900000,
                "start_app_version": "1.0.0",
                "trace_cnt_compare": 0.1,
                "trace_user_compare": 0.2
            }
        ]
    },
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
