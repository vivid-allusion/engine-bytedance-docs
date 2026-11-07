---
title: "GetAppExceptionalBatteryIssueDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatteryIssueDetail"
---

Get app battery anomaly details.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppExceptionalBatteryIssueDetail&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppExceptionalBatteryIssueDetail |The API name. The current API name is `GetAppExceptionalBatteryIssueDetail`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |No |1619827200 |Query start time (Unix timestamp). |
|end_time |Integer |No |1619913600 |Query end time (Unix timestamp). |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67906#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|is_new |Integer |No |1 |New issue.<br><br><br>* 1: New issue<br><br>* 0: Not a new issue |
|issue_id |String |No |issue_12345 |Issue ID. |
|token |String |No |keyword |The search keyword. |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67906#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppExceptionalBatteryIssueDetail&Version=2022-10-12
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
    "is_new": 1,
    "issue_id": "issue_12345",
    "token": "keyword"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [BatteryTraceIssueDetailData](https://docs.byteplus.com/en/docs/299/67906#batterytraceissuedetaildata) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="batterytraceissuedetaildata"></span>
### BatteryTraceIssueDetailData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|issue |Object of [IssueInfo](https://docs.byteplus.com/en/docs/299/67906#issueinfo) |\- |Information on the issue status, including the responsible person and current status. |
|stack |Object of [ParsedStack](https://docs.byteplus.com/en/docs/299/67906#parsedstack) |\- |Stack trace information. |
|trace_cnt |Integer |100 |Error count. |
|trace_user |Integer |50 |Affected user count. |
|trace_ratio |Double |0.05 |Error rate. |
|last_event_time |Integer |1619895600 |The latest event time (Unix timestamp). |
|first_event_time |Integer |1619823600 |First event time (Unix timestamp). |
|last_report_time |Integer |1619899200 |The latest report time (Unix timestamp). |
|trace_user_ratio |Double |0.025 |Affected user rate. |
|trace_cnt_compare |Double |0.1 |Error count change rate. |
|trace_user_compare |Double |0.2 |Change rate of affected user count. |
|trace_ratio_compare |Double |0.01 |Change rate of error rate. |
|trace_user_ratio_compare |Double |0.005 |Change rate of affected user rate. |


<span id="issueinfo"></span>
### IssueInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |1112121 |The issue ID in MySQL. It is different from issue_id. |
|tag |Array of [Tags](https://docs.byteplus.com/en/docs/299/67906#tags) |\- |Label. |
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
|unexist_libs |JSON Map |\- |Missing symbol table information, key: add\-on name, value: UUID. |


<span id="tags"></span>
### Tags


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |301 |The tag ID. |
|key |String |component |The tag key. |
|values |Array of [ValueId](https://docs.byteplus.com/en/docs/299/67906#valueid) |[{"id": 202, "value": "backend"}, {"id": 203, "value": "frontend"}] |The tag value. |


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
|id |Long |201 |tag valueID. |
|value |String |production |The tag value. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": {
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
        "trace_cnt": 100,
        "trace_user": 50,
        "trace_ratio": 0.05,
        "last_event_time": 1619895600,
        "first_event_time": 1619823600,
        "last_report_time": 1619899200,
        "trace_user_ratio": 0.025,
        "trace_cnt_compare": 0.1,
        "trace_user_compare": 0.2,
        "trace_ratio_compare": 0.01,
        "trace_user_ratio_compare": 0.005
    },
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
