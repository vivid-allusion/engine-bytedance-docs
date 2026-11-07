---
title: "GetAppExceptionIssueList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionIssueList"
---

Obtain the list of crash issues for an app.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppExceptionIssueList&Version=2025\-12\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you call this API, specify the required public request parameters (such as <code>x-app-ids</code>). Otherwise, the call fails.</div>



|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppExceptionIssueList |The API name. The API name is `GetAppExceptionIssueList`. |
|Version |String |Yes |2025\-12\-01 |The API version. The API version is `2025-12-01`. |
|Aid |Integer |Yes |123456 |The app ID. |
|StartTime |Integer |Yes |1665417600 |The timestamp of the query start time. Unit: seconds. |
|EndTime |Integer |Yes |1665504000 |The timestamp of the query end time. Unit: seconds. |
|BizType |String |Yes |crash |The exception type. Values:<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* custom_exception: Custom exception |
|Filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67885#condition) |No |\- |The filter condition. |
|IsNew |Integer |No |0 |Whether this is a new issue. Values:<br><br><br>* 0: This is not a new issue.<br><br>* 1: This is a new issue. |
|Token |String |No |keyword |The search keyword. |
|PageNo |Integer |No |1 |The page number. |
|PageSize |Integer |No |10 |The page size. |
|OrderBy |String |No |crash_user_descend |The sorting method. Values:<br><br><br>* crash_user_ascend: User count in ascending order<br><br>* crash_user_descend: User count in descending order<br><br>* crash_count_ascend: Event count in ascending order<br><br>* crash_count_descend: Event count in descending order<br><br>* latest_report_time_ascend: Latest report time in ascending order<br><br>* latest_report_time_descend: Latest report time in descending order |
|From |String |No |startup |The source module. Values:<br><br><br>* startup: Startup analysis module<br><br>* app_page: Page analysis module |
|Status |Array of String |No |["pending","solved"] |The list of issue states. You can configure multiple states simultaneously. Values:<br><br><br>* pending<br><br>* processing<br><br>* ignored<br><br>* solved<br><br>* reopen |
|Managers |Array of Long |No |[] |The IDs of the persons responsible for this issue. |
|Tags |Array of Long |No |[] |The list of tag IDs. |
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
|SubConditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67885#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppExceptionIssueList&Version=2025-12-01
{
    "Aid": 123456,
    "StartTime": 1665417600,
    "EndTime": 1665504000,
    "BizType": "crash",
    "Filters": {
        "Op": "eq",
        "Type": "expression",
        "Value": "1.2.0",
        "MapKey": "",
        "Values": [
            "1.2.0"
        ],
        "Dimension": "app_version",
        "SubConditions": []
    },
    "IsNew": 0,
    "Token": "null pointer exception",
    "PageNo": 1,
    "PageSize": 10,
    "OrderBy": "crash_user_descend",
    "From": "startup",
    "Status": [
        "pending",
        "processing"
    ],
    "Managers": [
        10001,
        10002
    ],
    "Tags": [
        1,
        2
    ],
    "TimeType": "api_time"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Integer |100 |The total number of items. |
|Result |Array of [IssuePageItem](https://docs.byteplus.com/en/docs/299/67885#issuepageitem) |\- |The issue list. |


<span id="issuepageitem"></span>
### IssuePageItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Os |String |Android |The operating system. Values:<br><br><br>* Android<br><br>* iOS |
|Issue |Object of [IssueInfo](https://docs.byteplus.com/en/docs/299/67885#issueinfo) |\- |The issue status information. |
|Stack |Object of [ParsedStack](https://docs.byteplus.com/en/docs/299/67885#parsedstack) |\- |The stack trace information. |
|Title |String |title |The subtitle. |
|IssueId |String |issue_xxx |The issue ID. |
|CrashType |String |java |The crash type. Values:<br><br><br>* java: Java crash<br><br>* launch: Java launch crash<br><br>* native: Native crash<br><br>* anr: ANR<br><br>* crash: Crash<br><br>* watch_dog: Hang<br><br>* oom_crash: OOM crash<br><br>* extension: Extension crash |
|CrashUser |Integer |5 |The number of users affected by the crash. |
|CrashCount |Integer |10 |The crash count. |
|CrashRatio |Double |0.01 |The crash rate. |
|EnsureType |String |custom_error |The user\-defined error information. |
|EventDetail |String |detail |The crash content. |
|CrashLineNum |String |123 |The crash line number. |
|EndAppVersion |String |1.0.1 |The end app version. |
|LatestMessage |String |\- |The latest error message. |
|CrashUserRatio |Double |0.02 |The ratio of users affected by the crash. |
|EarliestEventId |String |event_xxx |The event ID of the earliest crash occurrence. |
|LatestCrashTime |Long |1665504000 |The timestamp of the last occurrence time. Unit: seconds. |
|StartAppVersion |String |1.0.0 |The starting app version. |
|BlockDurationAvg |Long |0 |The average lag duration. |
|CrashUserCompare |Double |0.1 |The rate of change of the number of users affected by the crash. |
|LatestEnsureType |String |custom_error |The latest custom error information. |
|LatestExitReason |String |\- |The last exit reason. |
|LatestReportTime |Long |1665507600 |The latest report time. |
|AvgProcessCpuRate |Long |0 |The average process CPU utilization. |
|CrashCountCompare |Double |0.1 |The rate of change of the crash count. |
|CrashRatioCompare |Double |0.1 |The rate of change of the crash rate. |
|ReportCntPerLanuch |Long |0 |The number of CPU reports per launch. |
|LatestExitSubReason |String |\- |The last exit sub\-reason. |
|EndUpdateVersionCode |String |101 |The end minor version. |
|CrashUserRatioCompare |Double |0.1 |The change rate of the ratio for users affected by the crash. |
|StartUpdateVersionCode |String |100 |The start minor version. |
|BlockDurationAvgCompare |Double |0.0 |The change rate of the average lag duration. |


<span id="issueinfo"></span>
### IssueInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |Long |1112121 |The issue ID in MySQL. |
|Tag |Array of [Tags](https://docs.byteplus.com/en/docs/299/67885#tags) |\- |The tag information. |
|Status |String |processing |The issue status. Values:<br><br><br>* pending<br><br>* processing<br><br>* ignored<br><br>* solved<br><br>* reopen |
|Managers |Array of [IssueManager](https://docs.byteplus.com/en/docs/299/67885#issuemanager) |\- |The list of persons responsible for this issue. |
|FixedVersion |String |v1.1.2 |The fixed version. |


<span id="parsedstack"></span>
### ParsedStack


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Brief |String |Crash due to null object reference |The brief description of the crash. |
|Lines |Array of String |["at package.class.method(SourceFile:line)"] |Each line in the call stack trace. |
|Owner |Integer |12345 |The user ID or identifier of the crash owner. |
|Title |String |NullPointerException |The title of the exception or crash. |
|Detail |String |at com.example.myapp.MainActivity.onCreate |The detailed stack trace information. |
|Reason |String |Attempt to invoke virtual method on a null object reference |The cause of the crash. |
|Gwpasan |Object of [GWPSANBacktrace](https://docs.byteplus.com/en/docs/299/67885#gwpsanbacktrace) |\- |The GWP ASan\-related stack trace information. |
|ErrorMsg |String |retrace error |The error message related to the retrace symbol table. |
|CrashFile |String |MainActivity.java |The file where the crash occurred. |
|SessionId |String |session_xxx |The session ID. |
|CrashClazz |String |MainActivity |The class where the crash occurred. |
|MainThread |Object of [IOSParsedBacktrace](https://docs.byteplus.com/en/docs/299/67885#iosparsedbacktrace) |\- |The parsed backtrace of the iOS main thread. |
|CrashMethod |String |onCreate |The method where the crash occurred. |
|CrashReason |String |Null object reference |The crash cause description. |
|OtherThread |Array of [OtherThreadLines](https://docs.byteplus.com/en/docs/299/67885#otherthreadlines) |\- |Other thread information for the Android ANR crash. |
|UnexistLibs |JSON Map |\- |Missing symbol table information. |
|NativeFrames |Array of [NativeFrame](https://docs.byteplus.com/en/docs/299/67885#nativeframe) |\- |The native crash stack. |
|OtherThreads |Array of [IOSParsedBacktrace](https://docs.byteplus.com/en/docs/299/67885#iosparsedbacktrace) |\- |Parsed backtraces of other threads. |
|StackAnalysis |Array of [AnalysisItem](https://docs.byteplus.com/en/docs/299/67885#analysisitem) |\- |The stack trace analysis information. |
|CrashException |String |java.lang.NullPointerException |The crash exception type. |
|JavaMainFrames |Array of [Frame](https://docs.byteplus.com/en/docs/299/67885#frame) |\- |The main stack trace of a Java crash. |
|CrashLineNumber |String |23 |The line number where the crash occurred. |
|RegisterAnalysis |Array of [AnalysisItem](https://docs.byteplus.com/en/docs/299/67885#analysisitem) |\- |The register analysis information. |
|CustomAddressAnalysis |Array of [AnalysisItem](https://docs.byteplus.com/en/docs/299/67885#analysisitem) |\- |The custom address analysis information. |


<span id="tags"></span>
### Tags


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |Long |301 |The tag ID. |
|Key |String |component |The tag key. |
|Values |Array of [ValueId](https://docs.byteplus.com/en/docs/299/67885#valueid) |\- |The tag value. |


<span id="issuemanager"></span>
### IssueManager


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |test_user |The name of the person responsible for this issue. |
|Email |String |test_user@test.com |The email address of the person responsible for this issue. |
|UserId |Long |12 |The ID of the person responsible for this issue. |


<span id="gwpsanbacktrace"></span>
### GWPSANBacktrace


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Gwpasan |Object of [GWPSANMeta](https://docs.byteplus.com/en/docs/299/67885#gwpsanmeta) |\- |The GWP ASan metadata. |
|Allocate |Object of [IOSParsedBacktrace](https://docs.byteplus.com/en/docs/299/67885#iosparsedbacktrace) |\- |The stack trace that records allocation information for `allocateAddr`. |
|IsSymbol |Integer |0 |Whether it is symbolized. Values:<br><br><br>* 0: It is not symbolized.<br><br>* 1: It is symbolized. |
|Deallocate |Object of [IOSParsedBacktrace](https://docs.byteplus.com/en/docs/299/67885#iosparsedbacktrace) |\- |The stack trace that records deallocation information. |


<span id="iosparsedbacktrace"></span>
### IOSParsedBacktrace


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Num |Long |123 |The number of stack trace frames or records. |
|Reason |String |EXC_BAD_ACCESS (SIGSEGV) |The cause of the crash or issue. |
|Backtrace |Array of [ParsedStackLine](https://docs.byteplus.com/en/docs/299/67885#parsedstackline) |[{"unit": "MyApp", "method": "doSomething", "location": "MyApp.swift:42", "is_sys": false, "wrong": false, "value": "0x0000000102d8c170", "address": "0x0000000102d8c150", "symbol": "*hidden#237*"}] |The list of stack trace lines for iOS devices. |
|MallocSize |Double |1024.5 |The allocated memory size. |
|ThreadName |String |com.apple.main\-thread |The thread name. |


<span id="otherthreadlines"></span>
### OtherThreadLines


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |Integer |1 |The thread identifier. |
|Name |String |background_thread |The thread name. |
|Stack |String |Frame1\nFrame2\nFrame3 |The stack trace information of the thread. |


<span id="unexistlibs"></span>
### UnexistLibs


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |The name of the missing add\-on. |
|value |String |\- |The UUID of the missing add\-on. |


<span id="nativeframe"></span>
### NativeFrame


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|File |String |libexample.so |The native code library file. |
|Method |String |ExampleFunction |The function in the native library. |


<span id="analysisitem"></span>
### AnalysisItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |R0 |The analysis item name. |
|Value |String |0x0 |The value of the analysis item. |
|Symbol |String |\- |The symbol information. |
|Address |String |\- |The address information. |
|MapInfo |String |\- |The Map information. |
|StrValue |String |\- |The value in string format. |
|ImageInfo |String |\- |The image information. |
|ObjectInfo |String |\- |The object information. |


<span id="frame"></span>
### Frame


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Reason |String |Attempt to invoke virtual method on a null object reference |The exception cause. |
|FrameLines |Array of [FrameLine](https://docs.byteplus.com/en/docs/299/67885#frameline) |[{"class": "MainActivity", "method": "onCreate", "file": "MainActivity.java", "line_number": "42"}] |Each line in the stack trace. |
|ExceptionName |String |NullPointerException |The exception name. |


<span id="valueid"></span>
### ValueId


|**Parameters** |**type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |Long |201 |The unique identifier of the value. |
|Value |String |production |The string representation of value. |


<span id="gwpsanmeta"></span>
### GWPSANMeta


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |Integer |0 |The GWPSANBacktrace type. |
|AllocateAddr |Long |0 |The allocation address corresponding to the crash address. |
|AllocateSize |Integer |0 |The allocated memory size. |
|AsanFaultAddr |Long |0 |The crash address. |


<span id="parsedstackline"></span>
### ParsedStackLine


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Unit |String |MyApp |The unit name. |
|IsSys |Boolean |false |Whether it is system code. |
|Value |String |0x0000000102d8c170 |Additional value information. |
|Wrong |Boolean |false |Whether the stack trace line is erroneous. |
|Method |String |doSomething |The method name. |
|Symbol |String |*hidden#237* |The symbol. This can be either a compiled symbol or a function name. |
|Address |String |0x0000000102d8c150 |The memory address. |
|Location |String |MyApp.swift:42 |The location. It is usually the file name and line number. |


<span id="frameline"></span>
### FrameLine


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|File |String |MainActivity.java |The file name. |
|Class |String |MainActivity |The class name. |
|Method |String |onCreate |The method name. |
|LineNumber |String |42 |The line number. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "Action": "GetAppExceptionIssueList",
        "Region": "cn-north-1",
        "Service": "apmplus_openapi",
        "Version": "2025-12-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Total": 100,
        "Result": [
            {
                "Os": "Android",
                "Issue": {
                    "Id": 1112121,
                    "Tag": [],
                    "Status": "processing",
                    "Managers": [],
                    "FixedVersion": "v1.1.2"
                },
                "Stack": {
                    "Brief": "Crash due to null object reference",
                    "Lines": [
                        "at package.class.method(SourceFile:line)"
                    ],
                    "Owner": 12345,
                    "Title": "NullPointerException",
                    "Detail": "at com.example.myapp.MainActivity.onCreate",
                    "Reason": "Attempt to invoke virtual method on a null object reference",
                    "Gwpasan": {
                        "Gwpasan": {
                            "Type": 0,
                            "AllocateAddr": 0,
                            "AllocateSize": 0,
                            "AsanFaultAddr": 0
                        },
                        "Allocate": {
                            "Num": 123,
                            "Reason": "EXC_BAD_ACCESS (SIGSEGV)",
                            "Backtrace": [
                                {
                                    "unit": "MyApp",
                                    "method": "doSomething",
                                    "location": "MyApp.swift:42",
                                    "is_sys": false,
                                    "wrong": false,
                                    "value": "0x0000000102d8c170",
                                    "address": "0x0000000102d8c150",
                                    "symbol": "_hidden#237_"
                                }
                            ],
                            "MallocSize": 1024.5,
                            "ThreadName": "com.apple.main-thread"
                        },
                        "IsSymbol": 0,
                        "Deallocate": {
                            "Num": 123,
                            "Reason": "EXC_BAD_ACCESS (SIGSEGV)",
                            "Backtrace": [
                                {
                                    "unit": "MyApp",
                                    "method": "doSomething",
                                    "location": "MyApp.swift:42",
                                    "is_sys": false,
                                    "wrong": false,
                                    "value": "0x0000000102d8c170",
                                    "address": "0x0000000102d8c150",
                                    "symbol": "_hidden#237_"
                                }
                            ],
                            "MallocSize": 1024.5,
                            "ThreadName": "com.apple.main-thread"
                        }
                    },
                    "ErrorMsg": "retrace error",
                    "CrashFile": "MainActivity.java",
                    "SessionId": "session_xxx",
                    "CrashClazz": "MainActivity",
                    "MainThread": {
                        "Num": 123,
                        "Reason": "EXC_BAD_ACCESS (SIGSEGV)",
                        "Backtrace": [
                            {
                                "unit": "MyApp",
                                "method": "doSomething",
                                "location": "MyApp.swift:42",
                                "is_sys": false,
                                "wrong": false,
                                "value": "0x0000000102d8c170",
                                "address": "0x0000000102d8c150",
                                "symbol": "_hidden#237_"
                            }
                        ],
                        "MallocSize": 1024.5,
                        "ThreadName": "com.apple.main-thread"
                    },
                    "CrashMethod": "onCreate",
                    "CrashReason": "Null object reference",
                    "OtherThread": [],
                    "NativeFrames": [],
                    "OtherThreads": [],
                    "StackAnalysis": [],
                    "CrashException": "java.lang.NullPointerException",
                    "JavaMainFrames": [],
                    "CrashLineNumber": "23",
                    "RegisterAnalysis": [],
                    "CustomAddressAnalysis": []
                },
                "Title": "title",
                "IssueId": "issue_xxx",
                "CrashType": "java",
                "CrashUser": 5,
                "CrashCount": 10,
                "CrashRatio": 0.01,
                "EnsureType": "custom_error",
                "EventDetail": "detail",
                "CrashLineNum": "123",
                "EndAppVersion": "1.0.1",
                "LatestMessage": "-",
                "CrashUserRatio": 0.02,
                "EarliestEventId": "event_xxx",
                "LatestCrashTime": 1665504000,
                "StartAppVersion": "1.0.0",
                "BlockDurationAvg": 0,
                "CrashUserCompare": 0.1,
                "LatestEnsureType": "custom_error",
                "LatestExitReason": "-",
                "LatestReportTime": 1665507600,
                "AvgProcessCpuRate": 0,
                "CrashCountCompare": 0.1,
                "CrashRatioCompare": 0.1,
                "ReportCntPerLanuch": 0,
                "LatestExitSubReason": "-",
                "EndUpdateVersionCode": "101",
                "CrashUserRatioCompare": 0.1,
                "StartUpdateVersionCode": "100",
                "BlockDurationAvgCompare": 0
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
