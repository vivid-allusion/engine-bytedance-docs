---
title: "GetSegmentTask"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-zixcxrzfsy"
---

After you start a segment task, you can call `GetSegmentTask` to specify the `AppId`,`RoomId` and `TaskId` to get the relevant information of the specified segment task.

> The interface can query the task started within 72 hours.


<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://open.byteplusapi.com?Action=GetSegmentTask&Version=2022\-06\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetSegmentTask` |Interface name. The value of this API: `GetSegmentTask` |
|Version |String |Yes |`2022-06-01` |OpenAPI version. The value of this interface: `2022-06-01` |
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |Room Id. It's the identifier of a room. |
|TaskId |String |Yes |`Your_TaskId` |Custom an ID for this task.<br><br>It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.<br><br>The `TaskId` is the identifier of the task. Under a RoomId of an AppId, the TaskId is unique. The TaskId can be repeated under different AppId or different RoomId. Therefore, AppId + RoomId + TaskId is the unique identifier of the task, which can be used to identify the running task in a certain room under the specified AppId, so that this task can be updated or stopped during the running of this task. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SegmentTask |Object of [SegmentTask](https://docs.byteplus.com/en/docs/12/14254#segmenttask) |`-` |Audio Slicing Task Information |


<span id="segmenttask"></span>
### SegmentTask


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|StartTime |Long |`1677477732000` |Unix timestamp when the task starts, in ms. |
|EndTime |Long |`0` |Unix timestamp when the task stops, in ms.`0` means that the task is running. |
|Status |Long |`2` |Status of the task.<br><br><br>* `0`: Unknown exception<br><br>* `1`: Not started<br><br>* `2`: Running<br><br>* `3`: Ended<br><br>* `4`: Task failed |
|StopReason |String | |Reason why task stops:<br><br><br>* `Null`: the task is not finished<br><br>* `UnknownStopReason`: There is a unknown reason for stopping<br><br>* `StopByAPI`: The user stops the task by calling the API<br><br>* `StartTaskFailed`: The task failed to start<br><br>* `IdleTimeOut`: the idle time has exceeded the set value. |
|MaxIdleTime |Integer |`600` |The max idle time for the task. |
|TargetStreams |Object of [Streams](https://docs.byteplus.com/en/docs/12/14254#streams) |`-` |The audio & video stream that needs to be segmented in the room. |
|Duration |Integer |`40` |The duration of every segment file in seconds. |
|StorageConfig |Object of [StorageConfig](https://docs.byteplus.com/en/docs/12/14254#storageconfig) |`-` |Configuration about storage. AK and SK won't be returned. |
|Control |Object of [ControlForSegment](https://docs.byteplus.com/en/docs/12/14254#controlforsegment) |`-` |Advanced features of segment |
|Identifier |String |`getsegmenttask` |Prefix of customized filename. |
|Handle |Boolean |`true` |Whether to start segmenting immediately when this function is turned on. |


<span id="streams"></span>
### Streams


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|StreamList |Array of [Stream](https://docs.byteplus.com/en/docs/12/14254#stream) |`-` |A list of `Streams`. It can be empty. When empty, it means subscribing to all streams in the room. In a `StreamList`, `Stream. Index`cannot be duplicated. |


<span id="stream"></span>
### Stream


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Index |Integer |`0` |In custom layout, use `Index` to flag the stream. Later in the `Layout.regions.StreamIndex`, you need to use `Index` to specify the layout settings for the corresponding stream. |
|UserId |String |`Your_UserId` |UserId which represents the user a stream belongs to. |
|StreamType |Integer |`0` |The type of stream. The value can be `0` or `1`, and the default value is `0`. `0`means normal audio & video stream, `1` means screen stream. You don't need to specify `StreamType` for WTN. |


<span id="storageconfig"></span>
### StorageConfig


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Type |Integer |`0` |Storage platform<br><br>`0`: BytePlus TOS<br><br>`2`: Third\-party storage platform supporting S3 protocol |
|TosConfig |Object of [TosConfig](https://docs.byteplus.com/en/docs/12/14254#tosconfig) |`-` |When Type = `0`, the value of TosConfig needs to be set correctly, otherwise the request will report an error. |
|VodConfig |Object of [VodConfig](https://docs.byteplus.com/en/docs/12/14254#vodconfig) |`-` |When Type = `1`, the value of VodConfig needs to be set correctly, otherwise the request will report an error |
|CustomConfig |Object of [CustomConfig](https://docs.byteplus.com/en/docs/12/14254#customconfig) |`-` |When Type = `2`, you need to set the value of CustomConfig correctly, otherwise the request will report an error |


<span id="tosconfig"></span>
### TosConfig


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AccountId |String |`30****000` |BytePlus AccountId.You can find it by clicking the account icon in the top\-right corner.<br><br>Even if you use the AK and SK of a sub\-user during the OpenAPI authentication process, the AccountId must be of the main account ID. |
|Bucket |String |`You****cket` |Name of bucket you created on TOS platform. |
|Region |Integer |`0` |Supported regions:<br><br><br>* `0` (default): ap\-southeast\-1<br><br>* `1`: cn\-hongkong<br><br>* `2`: ap\-southeast\-3 |


<span id="vodconfig"></span>
### VodConfig


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AccountId |String |`Your_****untId` |Console account ID, such as `200000000`.<br><br><br>* To find the AccountID: Console \-\> My Account \-\> Account ID<br><br>   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/image.png) </span><br><br>* This `AccountID` must be the main account's `AccountID`.<br><br>* Even if AK and SK used to authenticate is from sub\-account, the `AccountID`must be the main account's `AccountID`. |
|Region |Integer |`-` |Only support `0` (ap\-southeast\-1). |
|Space |String |`Your_Space` |Vod space name. |


<span id="customconfig"></span>
### CustomConfig


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vendor |Integer |`0` |Third\-party cloud storage platform.<br><br><br>* 0: Amazon S3. By default.<br><br>* 1: Aliyun object Storage Service OSS<br><br>* 2: HUAWEI CLOUD OBS<br><br>* 3: Tencent Cloud COS<br><br>* 4: Qiniu Cloud Kodo.<br><br>* 5: Google Cloud Storage |
|Region |Integer |`0` |Different storage platforms support different regions, see [Region list](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-115995#region-list)<br><br>The default value is `0`. |
|Bucket |String |`You****cket` |The name of the bucket. |
|AccessKey |String |`Your_****ssKey` |The AccessKey of the third\-party storage platform account. Make sure this account has writing permission to the bucket.<br><br>It's not recommended to enable reading permission. |
|SecretKey |String |`Your_****etKey` |The SecretKey of the third\-party storage platform account |


<span id="controlforsegment"></span>
### ControlForSegment


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Align |Boolean |`false` |Whether to enable slice alignment.<br><br>`Align`is the switch to enable alignment, whose default value is `False`. You can use this function to align the starttime and endtime of each user's segmented file.<br><br>&nbsp;<br><br>When `Align = False`, this function is turned off. In the duration of a segment, if the user publish audio streams, a segment will be generated. If the user does not publish streams in a part of the time during the duration, the duration of a file will be less than the duration set. Starttime of all files may be not the same.<br><br>&nbsp;<br><br>When `Align = True`, this function is turned on. In the duration of a segment, if the user publish audio streams, a segment will be generated. The duration of a file is equal to the set value, and the starttime of all files are the same. If the user does not publish streams in a part of the time during the duration, and the duration of a file remains the same, silent part will be included in the file. However, if the user does not publish audio during the whole duration, no file will be generated. |
|Mixed |Boolean |`false` |Whether to enable mix\-streaming segment.<br><br>'Mixed' is a switch to enable mixing\-stream segment, whose default value is `False`.<br><br><br>* When `Mixed = False`, only the audio streams specified in `TargetStreams` will be segmented separately.<br><br>* When `Mixed = True`, the audio streams specified in `TargetStreams` will be segmented separately, and the specified audio streams will also be mixed to generate a file, and the username of the mixing\-stream file is `mixed`. After the task is created, the mixing\-stream segment will continue to be called back regardless of whether someone is on the mic or not.<br><br>   For callbacks on different platforms, see: |
|IgnoreSilence |Boolean |`false` |Whether to ignore silent segmented file |
|RedundantDuration |Integer |`2` |Duration of redundant segment, in seconds.<br><br>Redundant segment The server segments by the fixed `Duration`, so there may be cases where sensitive words are truncated or unrecognized. In such cases, you can add a redundant segment which is the end of the previous segment, and the duration of the segment will be `RedundantDuration`+ `Duration`.<br><br>For example, when `Duration`= `20` and `RedundantDuration`= `3`, the duration of final output files are: [0\-20], [17\-40], [37\-60]. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://open.byteplusapi.com?Action=GetSegmentTask&Version=2022-06-01&AppId=You****pId&RoomId=Your_RoomId&TaskId=Your_TaskId
```


<span id="sample-response"></span>
### Sample response

```json
{
  "Result": {
    "SegmentTask": {
      "StartTime": 1677477732000,
      "EndTime": 0,
      "Status": 2,
      "StopReason": "",
      "TargetStreams": {
        "StreamList": [
          {
            "Index": 0,
            "UserId": "user0",
            "StreamType": 0
          },
          {
            "Index": 1,
            "UserId": "user1",
            "StreamType": 0
          }
        ]
      },
      "Handle": true,
      "Identifier": "getsegmenttask",
      "MaxIdleTime": 600,
      "Duration": 40,
      "Control": {
        "Align": true,
        "Mixed": true,
        "RedundantDuration": 3,
        "IgnoreSilence": true
      },
      "StorageConfig": {
        "Type": 1,
        "VodConfig": {
          "AccountId": 200000000,
          "Region": 0,
          "Space": "Your_Space"
        }
      }
    }
  },
  "ResponseMetadata": {
    "RequestId": "Your_RequestId",
    "Action": "GetSegmentTask",
    "Version": "2022-06-01",
    "Service": "rtc",
    "Region": "ap-singapore-1"
  }
}
```


&nbsp;
