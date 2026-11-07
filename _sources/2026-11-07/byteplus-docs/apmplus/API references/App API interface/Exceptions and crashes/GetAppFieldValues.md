---
title: "GetAppFieldValues"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppFieldValues"
---

Obtain the available values for app filter conditions.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppFieldValues&Version=2025\-12\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you call this API, specify the required public request parameters (such as <code>x-app-ids</code>). Otherwise, the call fails.</div>



|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppFieldValues |The API name. The API name is `GetAppFieldValues`. |
|Version |String |Yes |2025\-12\-01 |The API version. The API version is `2025-12-01`. |
|Aid |Integer |Yes |123456 |The app ID. |
|StartTime |Integer |Yes |1665417600 |The timestamp of the start time. Unit: seconds. |
|EndTime |Integer |Yes |1665504000 |The timestamp of the end time. Unit: seconds. |
|BizType |String |Yes |crash |The exception type. Values:<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* custom_exception: Custom exception |
|CrashType |String |No |java |The crash type. Values:<br><br><br>* java: Java crash<br><br>* launch: Java launch crash<br><br>* native: Native crash<br><br>* anr: ANR<br><br>* crash: Crash<br><br>* watch_dog: Hang<br><br>* oom_crash: OOM crash<br><br>* extension: Extension crash |
|Os |String |No |Android |The operating system. Values:<br><br><br>* Android<br><br>* iOS |
|IssueId |String |No |issue_xxx |The issue ID. |
|Keyword |String |No |keyword |The search keyword. |
|Field |String |Yes |os_version |The field key. Sample value:<br><br><br>* os_version: OS version<br><br>* device_model: Device model<br><br>* app_version: App version<br><br>* update_version_code: App minor version<br><br>* npth_version: APM SDK version<br><br>* channel: Download channel<br><br>* rom: ROM information<br><br>* province: Province<br><br>* process_name: Process name<br><br>* device_manufacturer: Manufacturer<br><br>* last_scene: App page |
|Limit |Integer |Yes |100 |The number of returned data entries. |
|Filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67888#condition) |No |\- |The filter condition. |
|TimeType |String |No |api_time |The time type. Values:<br><br><br>* api_time: Report time (default)<br><br>* event_time: Occurrence time |


<span id="condition"></span>
### Condition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Op |String |No |in |The operator. Values:<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|Type |String |No |expression |The type of the filter condition. Sample value:<br><br><br>* expression: The current condition is a single expression.<br><br>* and: The current condition is a compound expression, and the sub\-conditions in `SubConditions` are in a logical AND relationship.<br><br>* or: The current condition is a compound expression, and the sub\-conditions in `SubConditions` are in a logical OR relationship.<br><br>* map: The current condition is of the map type. |
|Value |String |No |123456 |The filter value. |
|MapKey |String |No |key_1 |The key of the map type.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>type</code> is set to map.</div><br> |
|Values |Array of String |No |[123456] |The filter values. You can configure multiple values simultaneously. |
|Dimension |String |No |aid |The name of the condition. |
|SubConditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67888#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppFieldValues&Version=2025-12-01
{
    "Aid": 123456,
    "StartTime": 1665417600,
    "EndTime": 1665504000,
    "BizType": "crash",
    "CrashType": "java",
    "Os": "Android",
    "IssueId": "issue_xxx",
    "Keyword": "keyword",
    "Field": "os_version",
    "Limit": 100,
    "Filters": {},
    "TimeType": "api_time"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Label |String |iOS 13 |The display name of the field value. |
|Value |String |13.0 |The field value. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "Action": "GetAppFieldValues",
        "Region": "cn-north-1",
        "Service": "apmplus_openapi",
        "Version": "2025-12-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": [
        {
            "Label": "Android",
            "Value": "android"
        },
        {
            "Label": "iOS",
            "Value": "ios"
        },
        {
            "Label": "iOS 15",
            "Value": "15.0"
        },
        {
            "Label": "iOS 16",
            "Value": "16.0"
        }    ]
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
