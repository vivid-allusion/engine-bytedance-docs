---
title: "GetAppMemoryEventList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppMemoryEventList"
---

Obtain the memory event list.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppMemoryEventList&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppMemoryEventList |The API name. The current API name is `GetAppMemoryEventList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|os |String |No |android |The operating system.<br><br><br>* Android<br><br>* iOS |
|memory_type |String |No |leaked |Memory issue type.<br><br><br>* leaked: Leak<br><br>* large_object: Large object |
|issue_id |String |No |issue_12345 |The issue ID. |
|start_time |Integer |No |1617122400 |Query start time (Unix timestamp). |
|end_time |Integer |No |1617208800 |Query end time (Unix timestamp). |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67891#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|event_id |String |No |event_12345 |Event ID. |
|page_no |Integer |No |1 |Page number being viewed. |
|page_size |Integer |No |10 |Page size. |
|token |String |No |crash |Keyword or token used to query specific information. |
|is_new |Integer |No |1 |Whether the issue is new.<br><br><br>* 1: Only show new issues<br><br>* 0: All issues |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67891#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppMemoryEventList&Version=2022-10-12
{
    "os": "android",
    "memory_type": "leaked",
    "issue_id": "issue_12345",
    "start_time": 1617122400,
    "end_time": 1617208800,
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
    "event_id": "event_12345",
    "page_no": 1,
    "page_size": 10,
    "token": "crash",
    "is_new": 1
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [IssueEventListResponseData](https://docs.byteplus.com/en/docs/299/67891#issueeventlistresponsedata) |\- |Returned data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="issueeventlistresponsedata"></span>
### IssueEventListResponseData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Integer |10 |Total number of items in the list. |
|result |Array of [IssueEvent](https://docs.byteplus.com/en/docs/299/67891#issueevent) |\- |List details. |


<span id="issueevent"></span>
### IssueEvent


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|aid |Integer |12345 |Unique identifier of the app. |
|rom |String |stock |ROM type or version. |
|region |String |us\-west |The region where the device is located. |
|channel |String |official |Application distribution channel. |
|filters |JSON Map |{"tag1": "value1", "tag2": "value2"} |The custom tag. |
|tos_key |String |tos_key_example |Key of the TOS key object in the TOS storage system. |
|user_id |String |user123 |Unique identifier of the user. |
|api_time |Long |1665417600 |Report time (Unix timestamp). |
|event_id |String |event_123456789 |Unique identifier of this crash. |
|issue_id |String |issue_123 |Unique identifier of the issue associated with this event. |
|device_id |String |abcdef123456 |Unique identifier of the device. |
|launch_id |String |launch_123 |Unique identifier of the app launch. |
|event_time |Long |1665417600 |Client event occurrence time (Unix timestamp). |
|os_version |String |Android 11 |The operating system version. |
|app_version |String |1.0.0 |Current version of the app. |
|in_app_time |Long |3600 |App usage duration before the event was triggered. |
|object_name |String |LeakedClass |Name of the object that may cause memory leaks. |
|object_size |String |64 |Size of the reported object. Unit: Bytes. |
|raw_log_key |String |raw_log_123456789 |The storage Key of the raw log. |
|device_model |String |Pixel 4XL |The device model. |
|dump_log_key |String |dump_log_123456789 |Storage Key of the dump log. |
|object_count |String |1 |Total count of reported objects. |
|process_name |String |com.example.app |Name of the process where the issue occurred at runtime. |
|is_background |Integer |0 |Indicates whether the app is running in the background. |
|is_jailbroken |Integer |0 |Indicates whether the device is jailbroken. |
|is_launch_crash |Integer |1 |Indicates whether this crash occurred at launch. |
|large_object_type |Integer |1 |Type identifier of large object memory. |
|update_version_code |String |100200300 |Minor version number of the app. |


<span id="filters"></span>
### Filters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |tag1 |Custom key. |
|value |String |value1 |Custom value. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": {
        "total": 10,
        "result": [
            {
                "aid": 12345,
                "rom": "stock",
                "region": "us-west",
                "channel": "official",
                "filters": {
                    "tag1": "value1",
                    "tag2": "value2"
                },
                "tos_key": "tos_key_example",
                "user_id": "user123",
                "api_time": 1665417600,
                "event_id": "event_123456789",
                "issue_id": "issue_123",
                "device_id": "abcdef123456",
                "launch_id": "launch_123",
                "event_time": 1665417600,
                "os_version": "Android 11",
                "app_version": "1.0.0",
                "in_app_time": 3600,
                "object_name": "LeakedClass",
                "object_size": "64",
                "raw_log_key": "raw_log_123456789",
                "device_model": "Pixel 4XL",
                "dump_log_key": "dump_log_123456789",
                "object_count": "1",
                "process_name": "com.example.app",
                "is_background": 0,
                "is_jailbroken": 0,
                "is_launch_crash": 1,
                "large_object_type": 1,
                "update_version_code": "100200300"
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
