---
title: "GetTraceLog"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetTraceLog"
---

Get trace details.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetTraceLog&Version=2025\-12\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you call this API, specify the required public request parameters (such as <code>x-app-ids</code>). Otherwise, the call fails.</div>



|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetTraceLog |The API name. The current API name is `GetTraceLog`. |
|Version |String |Yes |2025\-12\-01 |The API version. The API version is `2025-12-01`. |
|Aid |Integer |Yes |12345 |The app ID. |
|Os |String |Yes |os |The operating system. |
|IdType |String |Yes |uuid |Trace ID type. Values:<br><br><br>* bddid: Device ID<br><br>* ssid：session ID<br><br>* user_id: User ID |
|IdValue |String |Yes |12345 |Trace ID. |
|StartTime |Long |Yes |1668415078 |Timestamp of the Trace start time, in seconds. |
|EndTime |Long |Yes |16684156778 |Timestamp of the trace end time, in seconds. |
|FlagType |Integer |Yes |1 |Value is 0, 1, 2. all = 0, up = 1 (ascending), down = 2 (descending) |
|LogTypes |Array of Integer |Yes |log_types |Query log type. Values:<br><br><br>* 1: Crash log<br><br>* 4: Lag log<br><br>* 6: Launch log<br><br>* 15: Event log |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetTraceLog&Version=2025-12-01
{
    "Aid": 12345,
    "Os": "os",
    "IdType": "uuid",
    "IdValue": "12345",
    "StartTime": 1668415078,
    "EndTime": 16684156778,
    "FlagType": 1,
    "LogTypes": [
        32
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Control |Object of [Control](https://docs.byteplus.com/en/docs/299/67874#control) |control |Start information for the next trace. |
|TraceLogs |Array of [Log](https://docs.byteplus.com/en/docs/299/67874#log) |trace_logs |Trace log. |


<span id="control"></span>
### Control


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|NextTimestamp |Long |1668415078000 |Timestamp of the next load. |


<span id="log"></span>
### Log


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Os |String |os |The operating system. |
|Biz |String |biz |For traffic anomalies only. |
|Tag |JSON Map |tag |tag |
|Data |String |data |Log content. May be text or a JSON object |
|Type |String |crash |Log type. |
|Label |String |Native crash |Log tag. |
|Header |JSON Map |header |Log header. |
|EventId |String |event_id |The event ID. |
|IssueId |String |issue_id |The issue ID. |
|CrashType |String |crash_type |The crash type. |
|RawLogKey |String |raw_log_key |Log key. |
|DumpTosKey |String |dump_tos_key |Jump key. |
|EventTimestamp |Long |1668443877607 |Microsecond timestamp of event occurrence. |
|ServerTimestamp |Long |1668606448000 |Microsecond timestamp when the server received the log. |


<span id="tag"></span>
### Tag


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |The key defined by the label.  |
|value |String |\- |The value defined by the label.  |


<span id="header"></span>
### Header


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |The key of the log header. |
|value |String |\- |The value of the log header. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "Action": "GetTraceLog",
        "Region": "cn-north-1",
        "Service": "apmplus_openapi",
        "Version": "2025-12-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Control": "control",
        "TraceLogs": [
            {
                "Os": "os",
                "Biz": "biz",
                "Data": "data",
                "Type": "crash",
                "Label": "native crash",
                "EventId": "event_id",
                "IssueId": "issue_id",
                "CrashType": "crash_type",
                "RawLogKey": "raw_log_key",
                "DumpTosKey": "dump_tos_key",
                "EventTimestamp": 1668443877607,
                "ServerTimestamp": 1668606448000
            }
        ]
    },
    "error_msg": "fail",
    "error_no": "0",
    "data": {
        "Control": "control",
        "TraceLogs": [
            {
                "Os": "os",
                "Biz": "biz",
                "Data": "data",
                "Type": "crash",
                "Label": "native crash",
                "EventId": "event_id",
                "IssueId": "issue_id",
                "CrashType": "crash_type",
                "RawLogKey": "raw_log_key",
                "DumpTosKey": "dump_tos_key",
                "EventTimestamp": 1668443877607,
                "ServerTimestamp": 1668606448000
            }
        ]
    }
}
```


<span id="YrTTTvWl"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
