---
title: "GetWebCastTask"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-zq385antnd"
---

After you start a webrecord task, you can call `GetWebCastTask` to specify the `AppId`, `RoomId` and `TaskId` to get the relevant information of the specified Webrecord task.

<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://open.byteplusapi.com?Action=GetWebCastTask&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetWebCastTask` |Interface name. The value of this interface: `GetWebCastTask` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |ID of the target RTC room. It's the identifier of a room. |
|TaskId |String |Yes |`Your_TaskId` |Custom an ID for this task.<br><br>It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.<br><br>The `TaskId` is the identifier of the task. Under a RoomId of an AppId, the TaskId is unique. The TaskId can be repeated under different AppId or different RoomId. Therefore, AppId + RoomId + TaskId is the unique identifier of the task, which can be used to identify the running task in a certain room under the specified AppId, so that this task can be updated or stopped during the running of this task. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|WebCastTask |Object of [WebCastTask](https://docs.byteplus.com/en/docs/12/14273#webcasttask) |`-` |Information about the webrecord task |


<span id="webcasttask"></span>
### WebCastTask


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|StartTime |Long |`1676987478000` |Unix timestamp when the task starts, in ms. |
|EndTime |Long |`1676987489000` |Unix timestamp when the task stops, in ms.`0` means that the task is running. |
|Status |Long |`3` |Status of the task.<br><br><br>* `0`: Unknown exception<br><br>* `1`: Not started<br><br>* `2`: Running<br><br>* `3`: Ended<br><br>* `4`: Task failed |
|StopReason |String |`StopByAPI` |Reason why task stops:<br><br><br>* Empty: the task is not finished<br><br>* `UnknownStopReason`: There is a unknown reason for stopping<br><br>* `StopByAPI`: The user stops the task by calling the API<br><br>* `StartTaskFailed`: The task failed to start<br><br>* `IdleTimeOut`: The idle time has exceeded the set value. |
|UserId |String |`Your_UserId` |Id of user pushing the content of a webpage. |
|SourceURL |String |`https://xxxxx` |The address of the web page that needs to be relayed. This URL can carry custom queryParams for authentication and other needs, and the overall length does not exceed 1024. |
|VideoSolutions |Array of [VideoSolution](https://docs.byteplus.com/en/docs/12/14273#videosolution) |`-` |Output video parameters. Up to 2 channels are supported in the simulcast mode. The receiving end can subscribe according to needs. the web page with the maximum video stream resolution Resolution will be rendered. If the value is empty, a stream will be sent by the default value. |
|MaxRunningTime |Integer |`86400` |Maximum running time. After this time, the task will be terminated automatically. The unit is seconds. The value's range is [10,86400], and the default value is `86400`. It is automatically adjusted to the default value when not filled. |
|MonitorConfig |Object of [MonitorConfig](https://docs.byteplus.com/en/docs/12/14273#monitorconfig) |`-` |Configuration on page Availability Monitor |
|EventNotifyConfig |Object of [EventNotifyConfig](https://docs.byteplus.com/en/docs/12/14273#eventnotifyconfig) |`-` |Configuration of page event notification . This configuration can be enabled if it is necessary to prevent incomplete pages from being collected when the loading is not complete. |


<span id="videosolution"></span>
### VideoSolution


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Width |Integer |`1280` |Video width,in px. Its range is `[50,1920]`, and the default value is `1280`. The value must be an even number, and it will be automatically adjusted to an even number when the value is odd. |
|Height |Integer |`720` |Video height, in px. Its range is `[50,1080]`, and the default value is `720`. The value must be an even number, and it will be automatically adjusted to an even number when the value is odd. |
|FrameRate |Integer |`15` |Sent frame rate, in frame/second, its range is `[1,60]`, and the default value is `15`.It is recommended to refer to [Video Encoder Parameter](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70122) for frame rate and bitrate settings. |
|Bitrate |Integer |`0` |Maximum sending bitrate in Kbps, its range is `[0,10000]`, and the default value is `0`.`0` means adaptive bitrate. |


<span id="monitorconfig"></span>
### MonitorConfig


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|FreezeCheckInterval |Integer |`5` |Interval to check if there is no change in the page content. The value's range is `[2,30]` in seconds. The default value is `0`, which means not enabled.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When there are two consecutive detection hits, the page will be refreshed and <code>Status=4, Reason="PageFreeze"</code> will be called back.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When there are two consecutive detection hits again, the task will be rescheduled and <code>Status=5, Reason="PageFreeze"</code> will be called back.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">No change in the page may be a normal scenario for your business. Please carefully evaluate the actual content of the page before enabling this function to avoid early exit of the task.</div><br> |
|BlankCheckInterval |Integer |`5` |Interval for checking whether the page is blank. The value's range is `[2,30]` in seconds. The default value is `0`, which means not enabled.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When there are two consecutive detection hits, the page will be refreshed and <code>Status=4, Reason="PageBlank"</code> will be called back.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When there are two consecutive detection hits again, the task will be rescheduled, and <code>Status=5, Reason="PageBlank"</code> will be called back.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A completely white page may be a normal scenario for your business, please carefully evaluate the actual content of the page before enabling this function to avoid early exit of the task.</div><br> |
|CrashCheckInterval |Integer |`5` |The detection interval for whether the page's JS thread is crashed/stuck. The value's range is `[0,30]` in seconds. The default value is `0`, which means not enabled.<br><br>When a detection hit occurs, the task will be rescheduled, and `Status=5, Reason="PageCrash"` will be called back. |


<span id="eventnotifyconfig"></span>
### EventNotifyConfig


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|EnableEventNotify |Boolean |`true` |Whether to enable page active event notification. The default value is `false`.<br><br><br>* `true`: Inject two JS functions into the page: `onWebcastStart()` and `onWebcastEnd()`.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the page judges that the resources are loaded and calls <code>onWebcastStart()</code>, the control program will start to collect the page content. When the page judges that the content of this task has been completed, <code>onWebcastEnd()</code> will be called to notify the control program to end this task. The effect of <code>StopWebCast</code> openAPI remains unchanged, and you can end the task ahead of schedule by calling it. Detection of other page content and JS thread (if enabled) will start after <code>onWebcastStart()</code> event is received.   </div><br>   <br><br>* `false`: The collection will start after the page is opened, and the collection will end after receiving the `StopWebCast` openAPI request. |
|StartTimeout |Integer |`2` |Timeout to wait for a start event when page active event notification is enabled. The value range is `[0,60]` in seconds. The default value is `0`, which means not enabled. This parameter is valid only when `EnableEventNotify` is `true` .<br><br><br>* When the start event is received within the timeout period, the collection function is running normally, and the user will receive a `Status=1` callback.<br><br>* When the start event is not received within the timeout period, it will be refreshed, and the waiting time will be reset. The task will be rescheduled after the timeout occurs again.<br><br>   * Callback `Status=4, Reason="StartEventTimeout"` will be called when refreshed.<br><br>   * `Status=5, Reason="StartEventTimeout"` will be called back when rescheduling. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
GET https://open.byteplusapi.com?Action=GetWebCastTask&Version=2020-12-01&AppId=You****pId&RoomId=Your_RoomId&TaskId=Your_TaskId
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": {
        "WebcastTask": {
            "StartTime": 1676987478000,
            "EndTime": 1676987489000,
            "Status": 3,
            "StopReason": "StopByAPI",
            "UserId": "Your_UserId",
            "SourceURL": "https://xxxxx",
            "VideoSolutions": [
                {
                    "Width": 1920,
                    "Height": 1080,
                    "FrameRate": 60,
                    "Bitrate": 10000
                }
            ],
            "MonitorConfig": {
                "BlankCheckInterval": 5,
                "CrashCheckInterval": 5,
                "FreezeCheckInterval": 5
            },
            "EventNotifyConfig": {
                "EnableEventNotify": true,
                "StartTimeout": 2
            },
            "MaxRunningTime": 3600
        }
    },
    "ResponseMetadata": {
        "RequestId": "Your_RequestId",
        "Action": "GetWebCastTask",
        "Version": "2020-12-01"，
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
