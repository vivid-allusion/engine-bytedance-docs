---
title: "Cloud Recording"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69818"
---

You can record audio and video calls or live streaming processes into one or more files and store them in a specified cloud storage platform for future playback, archiving, secondary processing, or analysis. This article mainly introduces how to quickly use Cloud Recording and related configurations (such as mixed\-stream recording, single\-stream recording, recording file formats, recording file storage, etc.).

The following two recording modes are supported:


* **Mixed\-stream recording**: Mixes multiple audio and video streams into a single stream to generate one audio and video file. You can customize parameters such as the layout, resolution, and bitrate of the final synthesized video.

* **Single\-stream recording**: Records each subscribed audio and video stream separately into individual files without mixing. The resolution of the recorded file remains the same as the original stream.


<span id="5fb67a22"></span>
## Applicable Scenarios


|Industry |Scenario |
|---|---|
|Online Education |Record the entire process of online courses for students to review on demand after class. |
|Video Conference |Record important meeting content to automatically generate meeting minutes or archive as evidence. |
|Financial Industry |Archive for future reference when handling video interviews, remote witnessing, and other businesses. |


<span id="2eb36c9e"></span>
## Billing

Cloud Recording is a paid feature. For billing details, please refer to [Billing of Cloud Recording](https://docs.byteplus.com/docs/byteplus-rtc/docs-1392577).

<span id="f39a033b"></span>
## Quick Start

<span id="5879760b"></span>
### Step 1: Enable Cloud Recording in the Console


1. Go to the [Console](https://console.byteplus.com/rtc/cloudRTC?from=doc).

2. Select your target RTC application from the drop\-down box, go to the **Cloud recording** tab, and click **Enable**.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/83de3c6108214bd194b0be88253c1b9a) </span>

<span id="c5aadab0"></span>
### Step 2 (Recommended): Receive Recording Notifications

Recording tasks are asynchronous. It is recommended to  [Enable Message Notification](https://docs.byteplus.com/docs/byteplus-rtc/docs-75110) to receive real\-time events such as task start, task stop, and file generation.

<span id="a8e09711"></span>
### Step 3: Start a Recording Task

Call `StartRecord` to initiate a single\-stream or mixed\-stream recording task.


<Tabs>
<Tab zoneid="uIQTBbJtyL" title="Mixed-stream Recording">
<TabTitle>Mixed-stream Recording</TabTitle>

<span id="45228d24"></span>
#### Core Parameters


* `RecordMode`: Keep as the default value `0`.

* `Layout`: Configure the video layout (Auto, Vertical, Side\-by\-side, or Custom). For details, see [Mixed-stream Layout Mode](https://docs.byteplus.com/docs/byteplus-rtc/docs-69818#0011a98e).

* `Encode`: Configure audio and video encoding parameters, such as resolution, frame rate, and bitrate.

* `StorageConfig`: **Required**. Configure the storage location for recording files, such as BytePlus VOD or BytePlus TOS.


<span id="62e21f0c"></span>
#### Request Example

```JSON
{
    "AppId": "Your_AppId",
    "RoomId": "Your_RoomId",
    "TaskId": "mixed_record_001",
    "RecordMode": 0,
    "Layout": {}, // Default to Auto layout
    "Encode": {
        "VideoWidth": 1280,
        "VideoHeight": 720,
        "VideoFps": 15,
        "VideoBitrate": 0 // 0 means adaptive bitrate
    },
    "FileFormatConfig": { "FileFormat": ["MP4"] },
    "StorageConfig": {
        "Type": 2, // 2 represents third-party storage platform supporting S3 protocol
        "CustomConfig": {
            "Vendor": 0, // 0 represents Amazon S3
            "Region": 0, // Region list see API reference
            "Bucket": "your-s3-bucket-name",
            "AccessKey": "Your_AccessKey",
            "SecretKey": "Your_SecretKey"
        }
    }
}
```



</Tab>
<Tab zoneid="ktMzj94DcK" title="Single-stream Recording">
<TabTitle>Single-stream Recording</TabTitle>

<span id="a43b8f2c"></span>
#### Core Parameters


* `RecordMode`: Must be set to `1`.

* `TargetStreams`: **Optional**. If not passed, all streams in the room are recorded by default.

* `StorageConfig`: **Required**. Configure the storage location for recording files. You can choose BytePlus VOD or third\-party storage supporting S3 protocol.


<span id="88d292ca"></span>
#### Request Example

The following example demonstrates how to record the streams of user_A and user_B in Room1 and store the recording files in MP4 format to VOD.

```JSON
{
    "AppId": "Your_AppId",
    "RoomId": "Your_RoomId",
    "TaskId": "single_record_002",
    "RecordMode": 1,    // Indicates single-stream recording
    "TargetStreams": {
        "StreamList": [
            { "UserId": "user_A", "StreamType": 0 },
            { "UserId": "user_B", "StreamType": 0 }
        ]
    },
    "FileFormatConfig": { "FileFormat": ["MP4"] },
    "StorageConfig": {
        "Type": 1, // 1 represents BytePlus VOD
        "VodConfig": {
            "AccountId": "Your_AccountId",
            "Space": "your-vod-space-name"
        }
    }
}
```



</Tab>
</Tabs>


<span id="9d4fd0e7"></span>
### Step 4: Update, Query, or Stop a Recording Task


* Call [UpdateRecord](https://docs.byteplus.com/docs/byteplus-rtc/docs-116406) to update the previously set cloud recording configuration parameters.

* When you need to end the recording, call [StopRecord](https://docs.byteplus.com/docs/byteplus-rtc/docs-116407) to stop an ongoing recording task.

* Call [GetRecordTask](https://docs.byteplus.com/docs/byteplus-rtc/docs-116408) to query the status of the mixed\-stream recording task, and you will receive information such as the task start time and task status.


<span id="6ed4de59"></span>
## Advanced Features

<span id="bb69d7ad"></span>
### Auto Recording

You can enable the Auto Recording feature for a specified RTC application in the console. Once enabled, when users meet the conditions enter the room and start publishing audio and video streams, the system will automatically start a single\-stream recording task for them.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>



* <div data-tips="true" data-tips-type="warning">Currently, Auto Recording only supports recording video streams (camera) and does not support screen streams. If a user only publishes screen streams, auto recording will not be triggered.</div>


* <div data-tips="true" data-tips-type="warning">After the room is dissolved or the user stops publishing audio and video and the maximum idle timeout is exceeded, the task will automatically end.</div>


1. Go to the [Console](https://console.byteplus.com/rtc/cloudRTC?from=doc).

2. Select your target RTC application from the drop\-down box, go to the **Cloud recording** tab, and click **Add auto recording**.

3. Configure the recording rules:

   * **Business ID**: You can set different business IDs (`BusinessId`) for different business scenarios.

      * If a business ID is set, auto recording will only be triggered for users who pass the same `BusinessId` via the `StartRecord` API.

      * If no business ID is set, single\-stream recording will be performed by default for all users publishing audio and video in the room.

   * **Storage Location**: Recording files can be stored in BytePlus VOD or BytePlus TOS.


<span id="b0e4fbd1"></span>
### Storage Location

This function allows you to store recordings in a variety of storage platforms. BytePlus VOD, Amazon S3, and Alibaba Cloud Object Storage Service are currently supported.

<span id="0011a98e"></span>
### Mixed\-stream Layout Mode

Mixed\-stream recording provides three preset layout modes. If the preset layouts do not meet your needs, you can customize the layout by setting coordinates through the `CustomLayout` field.

<span id="1a936e5a"></span>
#### Adaptive Mode

Automatically arranged based on the number of people. If the number of people is not full or there are only audio streams, the corresponding positions will display the background color. The video will be automatically cropped to fill the viewport.


* 2 users:

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/2peop.png) </span>

* 4 users:

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/4peopl.png) </span>

* 5~9 / 10~16 users:

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/9peop.png) </span>

* 17 users:

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/17p.png) </span>


Auto layout follows these rules:


* The specific layout is selected based on the number of people, following the schematic diagrams above. When the number of people does not reach the maximum applicable for the layout, the empty windows will display the background color.

* Users who only publish audio will still occupy a window in the overall layout, and the window will display the background color.

* If the aspect ratio of the actual video stream is inconsistent with the viewport's aspect ratio, the video will be automatically cropped to fit the window size.


<span id="03c73f60"></span>
#### Vertical Layout

1 large viewport (user can be specified) + side small viewports (arranged in the order of joining). The large viewport can specify a UserID; otherwise, it displays randomly.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/1-5p.png) </span>

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/8-9.png) </span>

Vertical layout follows these rules:


* For the large window:

   * If no user is specified, the large window will randomly display a user; if the specified user has not entered the channel or has entered but not published a stream, the large window will display the background color.

   * If the aspect ratio of the actual video stream is inconsistent with the window's aspect ratio, the window will crop the video according to the display area's aspect ratio and scale the video proportionally to fill the display area.

* For the small windows:

   * The small viewports are arranged in the order of joining. If a user exits the channel, the subsequent users will move up to occupy the previous user's window in order.

   * If the aspect ratio of the actual video stream is inconsistent with the viewport's aspect ratio, the video will be cropped to fit the viewport size.

   * When the number of people does not reach the maximum applicable for the layout, the empty windows will display the background color.

   * Users who only publish audio will still occupy a window in the overall layout, and the window will display the background color.


<span id="a95b9db0"></span>
#### Side\-by\-side Layout

All screens are divided equally and tiled.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/2user.png) </span>

<span id="be2ec5fe"></span>
### Customize File Name of Recording

By configuring `FileNameConfig`, you can define the storage path (`Prefix`) and filename (`Pattern`) of the recording files for easy archiving and retrieval.

The total length of the filename must not exceed 128 characters. You can use `{}` placeholders in the filename to insert dynamic variables, such as `{RoomId}`, `{UserId}`, etc.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">The custom filename format does not include the file extension (e.g., <code>.mp4</code>). The file format is controlled by the <code>FileFormatConfig</code> parameter.</div>


<span id="e3cdd5e6"></span>
#### Single\-stream Recording


* **Pattern**: `{TaskId}_{RoomId}_{UserId}_{Type}_{StartTime}_{Duration}_{Random}`

* **Fillable Variables**:

   
   |Variable |Description |
   |---|---|
   |`TaskId` |Task ID of cloud recording. |
   |`RoomId` |The unique identifier for a room. |
   |`UserId` |The ID of the user publishing the stream. |
   |`Type` |The type of stream. `C` for camera stream, `S` for screen stream. |
   |`StartTime` |The UTC timestamp in milliseconds (ms) when the recording task starts. |
   |`Duration` |The duration of the recording file in seconds (s). The value is padded with leading zeros to a fixed length of 6 characters (e.g., 000123). |
   |`Random` |An eight\-digit random number to ensure the filename is unique. |
   


<span id="0f54b73d"></span>
#### Mixed\-stream Recording


* **Pattern**: `{TaskId}_{RoomId}_{StartTime}_{Duration}_{Random}`

* **Fillable Variables**:

   
   |Variable |Description |
   |---|---|
   |`TaskId` |Task ID of cloud recording. |
   |`RoomId` |The unique identifier for a room. |
   |`StartTime` |The UTC timestamp in milliseconds (ms) when the recording task starts. |
   |`Duration` |The duration of the recording file in seconds (s). The value is padded with leading zeros to a fixed length of 6 characters (e.g., 000123). |
   |`Random` |An eight\-digit random number to ensure the filename is unique. |
   


<span id="aa53c8db"></span>
#### Auto Recording

Auto recording is single\-stream recording, and its filename format is fixed to the default format: `{TaskId}_{RoomId}_{UserId}_{Type}_{StartTime}_{Duration}_{Random}`.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">In auto recording mode, the value of <code>TaskId</code> is the same as <code>UserId</code>.</div>


<span id="7481d018"></span>
### Record and Upload Simultaneously (HLS)

If you want to start watching the playback while the recording is still in progress to reduce the waiting time for long video recordings, you can set `Control.EnableSyncUpload` to `true` to enable simultaneous recording and uploading.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">This feature is only effective for recording files in <code>HLS</code> format.</div>


<span id="332eb651"></span>
### Recording File Slicing


* **Duration slicing**: Whenever the recording duration reaches approximately 4 hours, the system will automatically create a new recording file (slice). Multiple files are arranged in sequential order. If cloud recording callbacks are configured, information on all recording files can be obtained via the `RecordStopped.RecordFileList` callback.

* **Stream interruption slicing** (single\-stream recording only): When a stream is interrupted:

   * If the interruption time is less than `MaxSilenceSeconds` (default is 3600 seconds), the recording service will add black frames or the last frame of the corresponding duration to the current file.

   * If the interruption time exceeds `MaxSilenceSeconds`, the recording service will end the current file first, and create a new recording file after the video stream recovers.


<span id="14184976"></span>
### Task Control Parameters

In the `StartRecord` request, you can perform finer control over the recording task using the following parameters:


* `MaxIdleTime`: The idle timeout time of the task (seconds), after which the task will automatically terminate. The value range is [10,86400], and the default value is 180.

* `MaxRecordTime`: Maximum recording duration (seconds). The task will automatically stop when this duration is exceeded. Default is `0`, meaning no limit.

* `MaxSilenceSeconds`: (Effective for single\-stream only) The max silence time of the task (seconds). The value range is [60, 3600], with the unit being seconds, and the default value is 3600. When the stream is interrupted, if the interruption time is less than this value, the system will supplement frames; if greater, a new file may be generated.

* `FrameInterpolationMode`: Frame interpolation mode. When the video stream is interrupted, choose to supplement the last frame (`0`) or black frames (`1`).


<span id="96832310"></span>
## Frequently Asked Questions


* Why is the recording file of a screen stream not clear enough in adaptive layout?

   In adaptive layout, server does not set ultra\-high bit rate by default. If you subscribe to the screen stream, we recommend setting a higher bit rate manually. To set video publishing parameters such as bit rate in different scenarios, please refer to [Setting Video Encoder Configuration](https://docs.byteplus.com/docs/byteplus-rtc/docs-70122).

* In single\-stream recording, a black frame is displayed in the first few seconds after the user re\-enters the room.

   In single\-stream recording, if the user only sends audio streams a few seconds after rejoining, the server will fill in a black frame instead of the previous frame.
