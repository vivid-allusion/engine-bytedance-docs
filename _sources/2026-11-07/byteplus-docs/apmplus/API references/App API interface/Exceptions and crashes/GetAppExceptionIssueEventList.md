---
title: "GetAppExceptionIssueEventList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionIssueEventList"
---

Obtain the detailed event list for a specified app crash issue.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppExceptionIssueEventList&Version=2025\-12\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you call this API, specify the required public request parameters (such as <code>x-app-ids</code>). Otherwise, the call fails.</div>



|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppExceptionIssueEventList |The API name. The name of the current API is `GetAppExceptionIssueEventList`. |
|Version |String |Yes |2025\-12\-01 |The API version. The API version is `2025-12-01`. |
|Aid |Integer |Yes |123456 |The app ID. |
|Os |String |Yes |Android |The operating system. Values:<br><br><br>* Android<br><br>* iOS |
|CrashType |String |Yes |java |The crash type. Values:<br><br><br>* java: Java crash<br><br>* launch: Java launch crash<br><br>* native: Native crash<br><br>* anr: ANR<br><br>* crash: Crash<br><br>* watch_dog: Hang<br><br>* oom_crash: OOM crash<br><br>* extension: Extension crash |
|IssueId |String |Yes |issue_xxx |The issue ID. |
|StartTime |Integer |Yes |1665417600 |The timestamp of the start time. Unit: seconds. |
|EndTime |Integer |Yes |1665504000 |The timestamp of the end time. Unit: seconds. |
|BizType |String |Yes |crash |The exception type. Values:<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* custom_exception: Custom exception<br><br>* metric_kit：MetricKit |
|Filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67884#condition) |No |{} |The filter condition. |
|EventId |String |No |event_xxx |The event ID. |
|PageNo |Integer |Yes |1 |The page number. |
|PageSize |Integer |Yes |10 |The page size. |
|IsNew |Integer |No |0 |Whether this is a new issue. Values:<br><br><br>* 0: This is not a new issue.<br><br>* 1: This is a new issue. |
|Token |String |No |keyword |The search keyword. |
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
|SubConditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67884#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppExceptionIssueEventList&Version=2025-12-01
{
    "Aid": 123456,
    "Os": "Android",
    "CrashType": "java",
    "IssueId": "issue_xxx",
    "StartTime": 1665417600,
    "EndTime": 1665504000,
    "BizType": "crash",
    "Filters": {},
    "EventId": "event_xxx",
    "PageNo": 1,
    "PageSize": 10,
    "IsNew": 0,
    "Token": "keyword",
    "TimeType": "api_time"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Integer |100 |The total number of items. |
|Result |Array of [IssueEvent](https://docs.byteplus.com/en/docs/299/67884#issueevent) |\- |The event list. |


<span id="issueevent"></span>
### IssueEvent


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Aid |Integer |123456 |The app ID. |
|Rom |String |iOS |The ROM information. |
|Bddid |String |bddid_xxx |The device ID. |
|Brief |String |\- |The summary. |
|Stack |Object of [ParsedStack](https://docs.byteplus.com/en/docs/299/67884#parsedstack) |\- |The crash stack trace. |
|Title |String |\- |The title. |
|Reason |String |\- |The cause. |
|Region |String |cn |The region. |
|UserId |String |user_xxx |The user ID. |
|AlogUrl |Array of String |\- |The alog file address list. |
|ApiTime |Long |1665417600 |The report time. |
|Channel |String |app_store |The channel. |
|EventId |String |event_xxx |The event ID. It is the identifier of a single crash. |
|Filters |JSON Map |\- |The custom tag. |
|IssueId |String |issue_xxx |The issue ID. |
|Message |String |\- |The additional message. |
|FileList |Array of [FileInfo](https://docs.byteplus.com/en/docs/299/67884#fileinfo) |\- |The file list. |
|IsParsed |Integer |1 |Whether parsing is successful. |
|CrashFile |String |\- |The crash file. |
|EventTime |Long |1665417600 |The client occurrence time. |
|HprofInfo |Object of [HprofInfo](https://docs.byteplus.com/en/docs/299/67884#hprofinfo) |\- |The hprof information. |
|InAppTime |Long |10 |The usage duration. |
|OsVersion |String |16.0 |The operating system version. |
|RawLogKey |String |raw_log_key_xxx |The original log key. |
|SessionId |String |\- |The session ID. |
|AppVersion |String |1.0.0 |The app version. |
|CrashClazz |String |\- |The crash class name. |
|DumpLogKey |String |dump_log_key_xxx |The dump log key. |
|EnsureType |String |custom_error |The custom error type. |
|ExitReason |String |\- |The exit cause. |
|IsUserExit |Integer |0 |Whether the user actively exited. |
|SdkVersion |String |1.0.0 |The SDK version. It is valid only for SDK monitoring. |
|CrashMethod |String |\- |The crash method. |
|CrashReason |String |\- |The cause of the crash. |
|DeviceModel |String |iPhone 13 |The device model. |
|GwpasanType |String |Unknown |The GWPASan type. |
|NpthVersion |String |1.0.0 |The APM SDK version. |
|ProcessName |String |main |The crash process name. |
|IsBackground |Integer |0 |Whether the app is running in the background. |
|IsJailbroken |Integer |0 |Whether the device is jailbroken. Values:<br><br><br>* 0: It is not jailbroken.<br><br>* 1: It is jailbroken.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required if Os is set to iOS.</div><br> |
|OtherThreads |Array of JSON Map |\- |Other thread information. |
|ExitSubReason |String |\- |The exit sub\-reason. |
|IsLaunchCrash |Integer |0 |Whether it is a startup crash. Values:<br><br><br>* 0: It is not a startup crash.<br><br>* 1: It is a startup crash. |
|StackAnalysis |Array of [AnalysisItem](https://docs.byteplus.com/en/docs/299/67884#analysisitem) |\- |Stack trace analysis. |
|AppDisplayName |String |AppName |The app display name. |
|CrashException |String |\- |The crash exception. |
|CrashLineNumber |String |\- |The crash line number. |
|SdkMinorVersion |String |1.0.0\-hotfix |The SDK minor version. |
|RegisterAnalysis |Array of [AnalysisItem](https://docs.byteplus.com/en/docs/299/67884#analysisitem) |\- |The register analysis information. |
|UpdateVersionCode |String |100 |The minor version. |
|CustomAddressAnalysis |Array of [AnalysisItem](https://docs.byteplus.com/en/docs/299/67884#analysisitem) |\- |The custom address analysis. |


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
|Gwpasan |Object of [GWPSANBacktrace](https://docs.byteplus.com/en/docs/299/67884#gwpsanbacktrace) |\- |The GWP ASan\-related stack trace information. |
|ErrorMsg |String |retrace error |The error message related to the retrace symbol table. |
|CrashFile |String |MainActivity.java |The file where the crash occurred. |
|SessionId |String |session_xxx |The session ID. |
|CrashClazz |String |MainActivity |The class where the crash occurred. |
|MainThread |Object of [IOSParsedBacktrace](https://docs.byteplus.com/en/docs/299/67884#iosparsedbacktrace) |\- |The parsed backtrace of the iOS main thread. |
|CrashMethod |String |onCreate |The method where the crash occurred. |
|CrashReason |String |Null object reference |The crash cause description. |
|OtherThread |Array of [OtherThreadLines](https://docs.byteplus.com/en/docs/299/67884#otherthreadlines) |\- |Other thread information for the Android ANR crash. |
|UnexistLibs |JSON Map |\- |Missing symbol table information. |
|NativeFrames |Array of [NativeFrame](https://docs.byteplus.com/en/docs/299/67884#nativeframe) |\- |The native crash stack. |
|OtherThreads |Array of [IOSParsedBacktrace](https://docs.byteplus.com/en/docs/299/67884#iosparsedbacktrace) |\- |Parsed backtraces of other threads. |
|StackAnalysis |Array of [AnalysisItem](https://docs.byteplus.com/en/docs/299/67884#analysisitem) |\- |The stack trace analysis information. |
|CrashException |String |java.lang.NullPointerException |The crash exception type. |
|JavaMainFrames |Array of [Frame](https://docs.byteplus.com/en/docs/299/67884#frame) |\- |The main stack trace of a Java crash. |
|CrashLineNumber |String |23 |The line number where the crash occurred. |
|RegisterAnalysis |Array of [AnalysisItem](https://docs.byteplus.com/en/docs/299/67884#analysisitem) |\- |The register analysis information. |
|CustomAddressAnalysis |Array of [AnalysisItem](https://docs.byteplus.com/en/docs/299/67884#analysisitem) |\- |The custom address analysis information. |


<span id="filters"></span>
### Filters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |The key of custom data definition. |
|value |String |\- |The value of custom data definition. |


<span id="fileinfo"></span>
### FileInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TosUrl |String |tos://path |The file address. |
|LogType |String |hprof |The file type. |
|FileName |String |log.txt |The file name. |
|FileSize |Long |1024 |The file size. |
|UploadTime |Long |1665417600 |The upload time. |


<span id="hprofinfo"></span>
### HprofInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ApiTime |Long |1665417600 |The timestamp of the report time. Unit: seconds. |
|HasHprof |Integer |0 |Whether hprof exists. Values:<br><br><br>* 0: Does not exist.<br><br>* 1: Exists. |


<span id="otherthreads"></span>
### OtherThreads


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |The thread information. |
|value |String |\- |The value for the thread information. |


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


<span id="gwpsanbacktrace"></span>
### GWPSANBacktrace


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Gwpasan |Object of [GWPSANMeta](https://docs.byteplus.com/en/docs/299/67884#gwpsanmeta) |\- |The GWP ASan metadata. |
|Allocate |Object of [IOSParsedBacktrace](https://docs.byteplus.com/en/docs/299/67884#iosparsedbacktrace) |\- |The stack trace that records allocation information for `allocateAddr`. |
|IsSymbol |Integer |0 |Whether it is symbolized. Values:<br><br><br>* 0: It is not symbolized.<br><br>* 1: It is symbolized. |
|Deallocate |Object of [IOSParsedBacktrace](https://docs.byteplus.com/en/docs/299/67884#iosparsedbacktrace) |\- |The stack trace that records deallocation information. |


<span id="iosparsedbacktrace"></span>
### IOSParsedBacktrace


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Num |Long |123 |The number of stack trace frames or records. |
|Reason |String |EXC_BAD_ACCESS (SIGSEGV) |The cause of the crash or issue. |
|Backtrace |Array of [ParsedStackLine](https://docs.byteplus.com/en/docs/299/67884#parsedstackline) |[{"unit": "MyApp", "method": "doSomething", "location": "MyApp.swift:42", "is_sys": false, "wrong": false, "value": "0x0000000102d8c170", "address": "0x0000000102d8c150", "symbol": "*hidden#237*"}] |The list of stack trace lines for iOS devices. |
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


<span id="frame"></span>
### Frame


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Reason |String |Attempt to invoke virtual method on a null object reference |The exception cause. |
|FrameLines |Array of [FrameLine](https://docs.byteplus.com/en/docs/299/67884#frameline) |[{"class": "MainActivity", "method": "onCreate", "file": "MainActivity.java", "line_number": "42"}] |Each line in the stack trace. |
|ExceptionName |String |NullPointerException |The exception name. |


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
        "Action": "GetAppExceptionIssueEventList",
        "Region": "cn-north-1",
        "Service": "apmplus_openapi",
        "Version": "2025-12-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Total": 100,
        "Result": [
            {
                "Aid": 123456,
                "Rom": "iOS",
                "Bddid": "bddid_xxx",
                "Brief": "-",
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
                    "OtherThread": [
                        {
                            "Id": 1,
                            "Name": "background_thread",
                            "Stack": "Frame1\\nFrame2\\nFrame3"
                        }
                    ],
                    "NativeFrames": [
                        {
                            "File": "libexample.so",
                            "Method": "ExampleFunction"
                        }
                    ],
                    "OtherThreads": [
                        {
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
                    ],
                    "StackAnalysis": [
                        {
                            "Name": "R0",
                            "Value": "0x0",
                            "Symbol": "-",
                            "Address": "-",
                            "MapInfo": "-",
                            "StrValue": "-",
                            "ImageInfo": "-",
                            "ObjectInfo": "-"
                        }
                    ],
                    "CrashException": "java.lang.NullPointerException",
                    "JavaMainFrames": [
                        {
                            "Reason": "Attempt to invoke virtual method on a null object reference",
                            "FrameLines": [
                                {
                                    "class": "MainActivity",
                                    "method": "onCreate",
                                    "file": "MainActivity.java",
                                    "line_number": "42"
                                }
                            ],
                            "ExceptionName": "NullPointerException"
                        }
                    ],
                    "CrashLineNumber": "23",
                    "RegisterAnalysis": [
                        {
                            "Name": "R0",
                            "Value": "0x0",
                            "Symbol": "-",
                            "Address": "-",
                            "MapInfo": "-",
                            "StrValue": "-",
                            "ImageInfo": "-",
                            "ObjectInfo": "-"
                        }
                    ],
                    "CustomAddressAnalysis": [
                        {
                            "Name": "R0",
                            "Value": "0x0",
                            "Symbol": "-",
                            "Address": "-",
                            "MapInfo": "-",
                            "StrValue": "-",
                            "ImageInfo": "-",
                            "ObjectInfo": "-"
                        }
                    ]
                },
                "Title": "-",
                "Reason": "-",
                "Region": "cn",
                "UserId": "user_xxx",
                "AlogUrl": [
                    ""
                ],
                "ApiTime": 1665417600,
                "Channel": "app_store",
                "EventId": "event_xxx",
                "IssueId": "issue_xxx",
                "Message": "-",
                "FileList": [
                    {
                        "TosUrl": "tos://path",
                        "LogType": "hprof",
                        "FileName": "log.txt",
                        "FileSize": 1024,
                        "UploadTime": 1665417600
                    }
                ],
                "IsParsed": 1,
                "CrashFile": "-",
                "EventTime": 1665417600,
                "HprofInfo": {
                    "ApiTime": 1665417600,
                    "HasHprof": 0
                },
                "InAppTime": 10,
                "OsVersion": "16.0",
                "RawLogKey": "raw_log_key_xxx",
                "SessionId": "-",
                "AppVersion": "1.0.0",
                "CrashClazz": "-",
                "DumpLogKey": "dump_log_key_xxx",
                "EnsureType": "custom_error",
                "ExitReason": "-",
                "IsUserExit": 0,
                "SdkVersion": "1.0.0",
                "CrashMethod": "-",
                "CrashReason": "-",
                "DeviceModel": "iPhone 13",
                "GwpasanType": "Unknown",
                "NpthVersion": "1.0.0",
                "ProcessName": "main",
                "IsBackground": 0,
                "IsJailbroken": 0,
                "OtherThreads": [],
                "ExitSubReason": "-",
                "IsLaunchCrash": 0,
                "StackAnalysis": [
                    {
                        "Name": "R0",
                        "Value": "0x0",
                        "Symbol": "-",
                        "Address": "-",
                        "MapInfo": "-",
                        "StrValue": "-",
                        "ImageInfo": "-",
                        "ObjectInfo": "-"
                    }
                ],
                "AppDisplayName": "AppName",
                "CrashException": "-",
                "CrashLineNumber": "-",
                "SdkMinorVersion": "1.0.0-hotfix",
                "RegisterAnalysis": [
                    {
                        "Name": "R0",
                        "Value": "0x0",
                        "Symbol": "-",
                        "Address": "-",
                        "MapInfo": "-",
                        "StrValue": "-",
                        "ImageInfo": "-",
                        "ObjectInfo": "-"
                    }
                ],
                "UpdateVersionCode": "100",
                "CustomAddressAnalysis": [
                    {
                        "Name": "R0",
                        "Value": "0x0",
                        "Symbol": "-",
                        "Address": "-",
                        "MapInfo": "-",
                        "StrValue": "-",
                        "ImageInfo": "-",
                        "ObjectInfo": "-"
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
