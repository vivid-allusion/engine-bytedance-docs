---
title: "StartSnapshot"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-155125"
---

Starts a snapshot task to capture images from video streams in a specific room at set intervals. These snapshots are typically used for content moderation (identifying illegal information), archiving, or generating highlights.

<span id="usage-scenario"></span>
## Usage scenario

By calling `StartSnapshot`, you can capture frames from one or more video streams within a room under your AppId.


* **Storage**: Results are uploaded to your specified cloud storage platform.

* **Callbacks**: For every snapshot generated, a metadata notification is sent to your configured [callback address](https://console.byteplus.com/rtc/cloudRTC?tab=callback). For more information on the callback data structure, see [SnapshotRealTimeData](https://docs.byteplus.com/en/docs/12/docs-75125#snapshotrealtimedata).


<span id="restrictions"></span>
## Restrictions


* Before using the function, you need to go to [console](https://console.byteplus.com/rtc) to enable Snapshot service.

* QPS must not exceed 150.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=StartSnapshot&Version=2022\-06\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`StartSnapshot` |Interface name. The value of this API: `StartSnapshot` |
|Version |String |Yes |`2022-06-01` |OpenAPI version. The value of this interface: `2022-06-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The unique identifier of your RTC application. |
|BusinessId |String |No |`Your_****nessId` |The Business identifier for your audio & video app. |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room where snapshots will be taken. |
|TaskId |String |Yes |`Your_TaskId` |Custom an ID for this task.<br><br>&nbsp;<br><br>The combination of `AppId + RoomId + TaskId` uniquely identifies a running task. Used to update or stop the task later. For naming rules for TaskId and other fields above, see [ID](https://docs.byteplus.com/en/docs/12/docs-115995#id). |
|TargetStreams |Object |No |`/` |Streams that require snapshotting in the room.<br><br>&nbsp;<br><br>If multiple streams are specified when snapshot are turned on, each stream will be snapshotted. However, if the publisher of a stream turns off the camera, no snapshot will be generated. |
|StreamList |Object[] |No |`-` |A list of `Streams`. It can be empty. When empty, it means subscribing to all streams in the room. In a `StreamList`, `Stream. Index`cannot be duplicated. |
|Index |Integer |No |`0` |In custom layout, use `Index` to flag the stream. Later in the `Layout.regions.StreamIndex`, you need to use `Index` to specify the layout settings for the corresponding stream. |
|UserId |String |Yes |`Your_UserId` |UserId which represents the user a stream belongs to. |
|StreamType |Integer |No |`0` |The type of stream. The value can be `0` or `1`, and the default value is `0`. `0`means normal audio & video stream, `1` means screen stream. You don't need to specify `StreamType` for WTN. |
|MaxIdleTime |Integer |No |`180` |The max idle time for the task. If all streams subscribed to by a task have stopped publishing, then the task will automatically stop after the idle time exceeds the set value. The range of values is [1,86400] in second. The default value is `180`. If the value is not valid, it is automatically adjusted to the default value. |
|ImageConfig |Object |No |`/` |configuration of image: format, size and the interval of snapshot.<br><br>&nbsp;<br><br>If the size of the stream (length and width) is inconsistent with the set value of screenshot size (length and width) when snapshotting, then the original picture of the video stream will be scaled to the set size. |
|Format |Integer |No |`0` |The format of the image.<br><br><br>* `0` ( default): `JPEG`<br><br>* `1`: `PNG`.<br><br><br>When the value is invalid, it is automatically adjusted to the default value. |
|Width |Integer |No |`0` |The actual width of the video frame used in px, and the value range is `[0,1920]`. The default value is `0`, and in this case, it is the same as the actual width of the video stream. If the value is invalid, it will be automatically adjusted to the default value. |
|Height |Integer |No |`0` |The actual height of the video frame in px, and the value range is `[0,1080]` . The default value is `0`. And in this case, it is the same as the actual height of the video stream. If the value is illegal, it will be automatically adjusted to the default value. |
|Interval |Float |No |`2.0` |The interval between consecutive screenshots, in seconds. Floating\-point values are supported with millisecond precision (0.001s).<br><br><br>* **Valid range**: `[0.1, 600]`<br><br>* **Default**: `2.0`<br><br>* Values with more than 3 decimal places will be truncated. |
|StorageConfig |Object |Yes |`/` |Configuration of storage platform. |
|Type |Integer |No |`0` |Storage platform<br><br>&nbsp;<br><br>`0`: BytePlus TOS<br><br>&nbsp;<br><br>`2`: Third\-party storage platform supporting S3 protocol |
|CustomConfig |Object |No |`-` |When Type = `2`, you need to set the value of CustomConfig correctly, otherwise the request will report an error |
|Vendor |Integer |No |`0` |Third\-party cloud storage platform.<br><br><br>* 0: Amazon S3. By default.<br><br>* 1: Aliyun object Storage Service OSS<br><br>* 2: HUAWEI CLOUD OBS<br><br>* 3: Tencent Cloud COS<br><br>* 4: Qiniu Cloud Kodo.<br><br>* 5: Google Cloud Storage |
|Region |Integer |No |`0` |Different storage platforms support different regions, see [Region list](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-115995#region-list)<br><br>&nbsp;<br><br>The default value is `0`. |
|Bucket |String |Yes |`You****cket` |The name of the bucket. |
|AccessKey |String |Yes |`Your_****ssKey` |The AccessKey of the third\-party storage platform account. Make sure this account has writing permission to the bucket.<br><br>&nbsp;<br><br>It's not recommended to enable reading permission. |
|SecretKey |String |Yes |`Your_****etKey` |The SecretKey of the third\-party storage platform account |
|TosConfig |Object |No |`-` |When Type = `0`, the value of TosConfig needs to be set correctly, otherwise the request will report an error. |
|AccountId |String |Yes |`30****000` |BytePlus AccountId.You can find it by licking the account icon in the top\-right corner.<br><br>&nbsp;<br><br>Even if you use the AK and SK of a sub\-user during the OpenAPI authentication process, the AccountId must be of the main account ID. |
|Bucket |String |Yes |`You****cket` |Name of bucket you created on TOS platform. |
|Region |Integer |No |`0` |Supported regions:<br><br><br>* `0` (default): ap\-southeast\-1<br><br>* `1`: cn\-hongkong<br><br>* `2`: ap\-southeast\-3 |
|FileNameConfig |Object |No | |Defines the naming rules and directory paths for snapshot files.<br><br>The final file path and name are constructed as follows: `{Prefix} + {Pattern} + Random Number`.<br><br>**Example**:<br><br>If Prefix is `snapshots/v1/` and Pattern is `{TaskId}_{StartTime}`, the result will be `snapshots/v1/Your_TaskId_16457**26_c46***1.jpg`<br><br>warning<br><br><br>* To prevent data loss, ensure your pattern is unique or enable bucket versioning to support duplicate filenames.<br><br>* The file extension (e.g., .jpg, .png) is appended automatically based on your `ImageConfig` settings. |
|Prefix |String[] |No |`["dir1", "dir2"]` |Define the directory path (prefix) for snapshot files. It takes effect for TosConfig and CustomConfig.<br><br>For example, ["dir1", "dir2"] creates the path `dir1/dir2/`.<br><br>**Constraints**:<br><br><br>* **Maximum Length:**   128 characters (including delimiters).<br><br>* **Allowed Characters:**   Alphanumeric only (a\-z, A\-Z, 0\-9).<br><br>* **Restrictions:**  No symbols (e.g., slashes, underscores, parentheses) allowed within individual strings. |
|Pattern |String |No |`{TaskId} *{RoomId}* ` |Custom filename template using variables in `{}`.<br><br><br>* **Available variables** (vary by recording mode):<br><br>   * **Single\-stream**: {TaskId}, {RoomId}, {UserId}, {Type}, {StartTime}, and {Duration}.<br><br>   * **Mixing\-stream**: {TaskId}, {RoomId}, {StartTime}, and {Duration}.<br><br>* **Constraints**: Max 128 characters; do not include file extensions (e.g., .mp4).<br><br><br>If left empty, default patterns apply based on the recording mode. For the full list and default values, see [Custom Recording Name](https://docs.byteplus.com/en/docs/12/docs-106873). |


<span id="response-parameters"></span>
## Response parameters

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=StartSnapshot&Version=2022-06-01
{
    "AppId": "You****pId",
    "BusinessId": "Your_****nessId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "TargetStreams": "/",
    "MaxIdleTime": 180,
    "ImageConfig": "/",
    "StorageConfig": "/",
    "FileNameConfig": {
        "Prefix": [
            "dir1",
            "dir2"
        ],
        "Pattern": "{TaskId}_{RoomId}_{StartTime}"
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "StartSnapshot",
        "Version": "2022-06-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
