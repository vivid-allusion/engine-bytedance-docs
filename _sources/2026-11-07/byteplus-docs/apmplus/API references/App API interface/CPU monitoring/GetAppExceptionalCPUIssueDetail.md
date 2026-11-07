---
title: "GetAppExceptionalCPUIssueDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalCPUIssueDetail"
---

Get CPU issue details.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppExceptionalCPUIssueDetail&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppExceptionalCPUIssueDetail |The API name. The current API name is `GetAppExceptionalCPUIssueDetail`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|aid |Integer |No |123456 |Unique identifier of the app. |
|os |String |No |Android |The operating system.<br><br><br>* Android<br><br>* iOS |
|start_time |Integer |No |1665417600 |Query start time (Unix timestamp). |
|end_time |Integer |No |1665504000 |Query end time (Unix timestamp). |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67896#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|issue_id |String |No |issue_12345 |Issue identifier. |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67896#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppExceptionalCPUIssueDetail&Version=2022-10-12
{
    "aid": 123456,
    "os": "Android",
    "start_time": 1665417600,
    "end_time": 1665504000,
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
    "issue_id": "issue_12345"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [IssueDetailResponseData](https://docs.byteplus.com/en/docs/299/67896#issuedetailresponsedata) |\- |Returned data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="issuedetailresponsedata"></span>
### IssueDetailResponseData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|os |String |android |The operating system.<br><br><br>* Android<br><br>* iOS |
|issue |Object of [IssueInfo](https://docs.byteplus.com/en/docs/299/67896#issueinfo) |\- |The issue status information. |
|stack |Object of [ParsedStack](https://docs.byteplus.com/en/docs/299/67896#parsedstack) |\- |Stack trace information. |
|event_id |String |event_54321 |Event ID. |
|issue_id |String |issue_98765 |The issue ID. |
|crash_user |Integer |17 |The number of users affected by the crash. |
|crash_count |Integer |42 |The crash count. |
|crash_ratio |Double |0.002 |The crash rate. |
|cpu_exception |Object of [CPUException](https://docs.byteplus.com/en/docs/299/67896#cpuexception) |\- |CPU anomaly information with detailed data. |
|end_app_version |String |1.0.3 |The end app version. |
|crash_user_ratio |Double |0.001 |The ratio of users affected by the crash. |
|latest_crash_time |Long |1622140800 |The latest crash time. |
|start_app_version |String |1.0.0 |The starting app version. |
|crash_user_compare |Double |\-0.05 |The rate of change of the number of users affected by the crash. |
|latest_report_time |Long |1622227200 |The latest crash report time. |
|crash_count_compare |Double |0.1 |The rate of change of the crash count. |
|earliest_crash_time |Long |1619539200 |First crash time. |


<span id="issueinfo"></span>
### IssueInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |1112121 |The issue ID in MySQL. It is different from issue_id. |
|tag |Array of [Tags](https://docs.byteplus.com/en/docs/299/67896#tags) |\- |Label. |
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


<span id="cpuexception"></span>
### CPUException


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|average_speed |Double |50.0 |Android average process usage speed rate. |
|average_usage |Double |25.0 |iOS average process utilization. |
|count_per_user |Double |1.5 |Report count per launch. |
|average_speed_compare |Double |0.1 |Android average process utilization change rate. |
|average_usage_compare |Double |\-0.5 |iOS average process utilization change rate. |
|count_per_user_compare |Double |0.2 |Change rate of report count per launch. |


<span id="tags"></span>
### Tags


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |301 |The tag ID. |
|key |String |component |The tag key. |
|values |Array of [ValueId](https://docs.byteplus.com/en/docs/299/67896#valueid) |[{"id": 202, "value": "backend"}, {"id": 203, "value": "frontend"}] |The tag value. |


<span id="unexistlibs"></span>
### UnexistLibs


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |libssl.so |The name of the missing add\-on. |
|value |String |a1b2xxx\-xxx\-xxx7890 |The UUID of the missing add\-on. |


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
        "os": "android",
        "issue": "",
        "stack": "",
        "event_id": "event_54321",
        "issue_id": "issue_98765",
        "crash_user": 17,
        "crash_count": 42,
        "crash_ratio": 0.002,
        "cpu_exception": "",
        "end_app_version": "1.0.3",
        "crash_user_ratio": 0.001,
        "latest_crash_time": 1622140800,
        "start_app_version": "1.0.0",
        "crash_user_compare": -0.05,
        "latest_report_time": 1622227200,
        "crash_count_compare": 0.1,
        "earliest_crash_time": 1619539200
    },
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) codes for troubleshooting.
