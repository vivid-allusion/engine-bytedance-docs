---
title: "GetAppMemoryDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppMemoryDetail"
---

Get the summary of a single memory event.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppMemoryDetail&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppMemoryDetail |The API name. The current API name is `GetAppMemoryDetail`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|os |String |No |android |Operating system type.<br><br><br>* Android<br><br>* iOS |
|memory_type |String |No |leaked |Memory issue type.<br><br><br>* leaked: Leak<br><br>* large_object: Large object |
|issue_id |String |No |issue123 |The unique identifier of the issue. |
|start_time |Integer |No |1665417600 |Start time (Unix timestamp). |
|end_time |Integer |No |1665504000 |End time (Unix timestamp). |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67890#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|token |String |No |error |Search keyword or token used to query specific information. |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67890#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppMemoryDetail&Version=2022-10-12
{
    "os": "android",
    "memory_type": "leaked",
    "issue_id": "issue123",
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
    "token": "error"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [DetailResponseData](https://docs.byteplus.com/en/docs/299/67890#detailresponsedata) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="detailresponsedata"></span>
### DetailResponseData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|user |Integer |50 |Affected user count. |
|count |Integer |100 |Error count. |
|issue |Object of [IssueInfo](https://docs.byteplus.com/en/docs/299/67890#issueinfo) |\- |Issue status information, currently including owner and status. |
|title |String |android.graphics.Bitmap |Issue details. |
|sub_title |String |thread com.apm.insight.runtime.u$c.contextClassLoader |Information about the thread with issues. |
|user_rate |Double |0.05 |Affected user rate. |
|count_rate |Double |0.02 |Error rate. |
|user_compare |Double |20 |Affected user count in the previous statistical period. |
|count_compare |Double |1 |Error count in the previous statistical period. |
|latest_event_time |Long |1665504000 |The latest error occurrence time (Unix timestamp). |
|user_rate_compare |Double |0.02 |Change rate of affected user rate. |
|count_rate_compare |Double |\-0.01 |Change rate of error rate. |
|latest_report_time |Long |1665580400 |The latest error report time (Unix timestamp). |
|earliest_event_time |Long |1665417600 |The earliest error occurrence time (Unix timestamp). |


<span id="issueinfo"></span>
### IssueInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |1112121 |The issue ID in MySQL. It is different from issue_id. |
|tag |Array of [Tags](https://docs.byteplus.com/en/docs/299/67890#tags) |\- |Label. |
|status |String |processing |Issue status.<br><br><br>* pending<br><br>* processing<br><br>* ignored<br><br>* solved<br><br>* reopen |
|fixed_version |String |v1.1.2 |The fixed version. |


<span id="tags"></span>
### Tags


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |301 |The tag ID. |
|key |String |component |The tag key. |
|values |Array of [ValueId](https://docs.byteplus.com/en/docs/299/67890#valueid) |[{"id": 202, "value": "backend"}, {"id": 203, "value": "frontend"}] |The tag value. |


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
        "user": 50,
        "count": 100,
        "issue": "",
        "title": "android.graphics.Bitmap",
        "sub_title": "thread com.apm.insight.runtime.u$c.contextClassLoader",
        "user_rate": 0.05,
        "count_rate": 0.02,
        "user_compare": 20,
        "count_compare": 1,
        "latest_event_time": 1665504000,
        "user_rate_compare": 0.02,
        "count_rate_compare": -0.01,
        "latest_report_time": 1665580400,
        "earliest_event_time": 1665417600
    },
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
