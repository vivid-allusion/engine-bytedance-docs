---
title: "StartRecord"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-115526"
---

In an audio and video application, you can use cloud recording to record audio or video files.

You can use `StartRecord` as an OpenAPI to do this.

<span id="usage-scenario"></span>
## Usage scenario

You can call the `StartRecord` interface to record according to your configuration, including setting single\-stream or mixing\-stream recording mode, layout, and parameters of audio or video files.

You can choose either single\-stream or mixing\-stream recording as the recording mode.


* Single\-stream recording: You can record each stream separately as an audio or video file. In this mode, you cannot set the layout, and the resolution of the recorded file is determined by the original video and can't be modified. The height of the recorded file is the ever\-biggest height resolution of the original video, and so is the width. For example, if resolution of the original video changes from `1920*1080` to `1080*1920` during recording, the resolution of the recorded file is `1920*1920`.

* Mixing\-stream recording: You can mix the specified streams and record in an audio or video file. In this mode, you can set the video layout, resolution, frame rate, bit rate, etc.

> You can only record up to 17 streams in single\-stream recording or mixing stream recording.


You need to configure the storage space in the interface to store the recording results on a storage platform. Now BytePlus VOD, Amazon S3, Alibaba Cloud, HUAWEI CLOUD OBS, Tencent Cloud COS and Qiniu Cloud Kodo are supported. You can also configure storage space and file format on the [Console](https://console.byteplus.com/rtc/workplaceRTC).

If you have enabled the message notification for starting recording, you can receive relevant callback notifications when cloud recording starts. For message notification service, see [Enable Message Notification](https://docs.byteplus.com/en/docs/12/docs-75110).

<span id="requirements"></span>
## Requirements

Before starting recording, you must enable this function on [RTC console](https://console.byteplus.com/rtc/cloudRTC).

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=StartRecord&Version=2022\-06\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`StartRecord` |Interface name. The value of this interface: `StartRecord` |
|Version |String |Yes |`2022-06-01` |OpenAPI version. The value of this interface: `2022-06-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`661e****543cf` |The only identifier for your audio & video app. |
|BusinessId |String |No |`Your_****nessId` |The Business identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room |
|TaskId |String |Yes |`Your_TaskId` |Task ID of cloud recording. You must set the TaskId for each task.<br><br><br>* `TaskId` in a room under an `AppId` is unique, and in different rooms or `AppIds` can be repeated, so `AppId` + `RoomId` + `TaskId` is the unique identifier of a task. You can use `AppId` + `RoomId` + `TaskId` to flag a task running in a room under an `AppId`, so that it can be updated or stopped during running with this combination.<br><br>* For naming rules for TaskId and other fields above.<br><br>   ID should comply with the following naming rules: `[a-zA-Z0-9_@\-\.]{1,128}`. |
|RecordMode |Integer |No |`0` |Use this parameter to set the recording mode: Single\-stream or mixing\-stream recording.<br><br>&nbsp;<br><br>`0`: mixing\-stream recording,<br><br>&nbsp;<br><br>`1`: single\-stream recording.<br><br>&nbsp;<br><br>The default value is `0`. |
|TargetStreams |Object |No |`-` |You can use this parameter to set streams to be recorded. When this value is null, all streams in the room will be recorded. The maximum number of streams recorded is 17 in mixing\-stream or single\-stream recording. The streams set in this parameter must not duplicate those in `ExcludeStreams`. |
|StreamList |Object[] |No |`-` |A list of `Streams`. It can be empty. When empty, it means subscribing to all streams in the room. In a `StreamList`, `Stream. Index`cannot be duplicated. |
|Index |Integer |No |`0` |In custom layout, use `Index` to flag the stream. Later in the `Layout.regions.StreamIndex`, you need to use `Index` to specify the layout settings for the corresponding stream. |
|UserId |String |Yes |`Your_UserId` |UserId which represents the user a stream belongs to. |
|StreamType |Integer |No |`0` |The type of stream. The value can be `0` or `1`, and the default value is `0`. `0`means normal audio & video stream, `1` means screen stream. You don't need to specify `StreamType` for WTN. |
|ExcludeStreams |Object |No |`-` |You can use this parameter to set streams that **do not** need to be recorded, that is, the blocklist of streams. The parameter is empty by default. There are no more than 17 streams in the blocklist. Adding a screen stream to the blocklist is not supported. The streams set in this parameter must not duplicate those in `TargetStreams`. |
|StreamList |Object[] |No |`-` |A list of `Streams`. It can be empty. When empty, it means subscribing to all streams in the room. In a `StreamList`, `Stream. Index`cannot be duplicated. |
|Index |Integer |No |`0` |In custom layout, use `Index` to flag the stream. Later in the `Layout.regions.StreamIndex`, you need to use `Index` to specify the layout settings for the corresponding stream. |
|UserId |String |Yes |`Your_UserId` |UserId which represents the user a stream belongs to. |
|StreamType |Integer |No |`0` |The type of stream. The value can be `0` or `1`, and the default value is `0`. `0`means normal audio & video stream, `1` means screen stream. You don't need to specify `StreamType` for WTN. |
|Encode |Object |No |`-` |Audio & video encoding parameters.<br><br>&nbsp;<br><br>For single\-stream recording, you can set `VideoFps`,`VideoBitrate` and audio parameters.<br><br>&nbsp;<br><br>For mixing stream recording, you can set `VideoWidth`, `VideoHeight`, `VideoFps`, `VideoBitrate` and audio parameters. |
|VideoWidth |Integer |No |`640` |The width of the output picture. The default value is `640`and the range is `[2, 4096]`, which must be even. If the value is invalid, it is automatically changed to the default value. This parameter does not take effect when the custom layout mode turns on, and the width of the overall picture complies with `canvas.width`. |
|VideoHeight |Integer |No |`480` |The height of the output picture, and the range is `[2, 2160]`, which must be even. The default value is `480`. If the value is invalid, it is automatically changed to the default value. This parameter does not take effect when the custom layout mode turns on, and the height of the overall picture complies with `canvas.Height`. |
|VideoFps |Integer |No |`15` |Output video frame rate. The default is `15` and the range is `[1,60]`. If the value is invalid, it is automatically changed to the default value. |
|VideoBitrate |Integer |No |`-` |Output video bit rate. Value range is `[1,10000]`, in Kbps. Default value is self\-adaptation. If the value is invalid, it is automatically changed to the default value. When `VideoCodec = 1`, you must set this field. |
|VideoCodec |Integer |No |`0` |Video coding protocol. The default value is `0`. The value can be `0`or `1`. `0`means `H.264`. `1`means`byteVC1`. When `VideoCodec = 1`, you must set the `VideoBitrate`field. |
|VideoGop |Integer |No |`4` |Output video GOP. The default is `4`and the range is `[1, 5]`in seconds. If the value is invalid, it is automatically changed to the default value. |
|AudioCodec |Integer |No |`0` |Audio encoding protocol. The default value is `0`, and the aac encoding protocol is used at this time. Currently only aac is supported. |
|AudioProfile |Integer |No |`0` |Audio profile type, effective when using aac encoding. The default value is `0` and the range is `{0,1,2}`. `0` means LC ;`1` means HE\-V1 specifications;`2` means HE\-V2 specifications.When `AudioProfile`takes `2`, only dual channel is supported. If the value is invalid, it is automatically changed to the default value. |
|AudioBitrate |Integer |No |`-` |Audio bitrate. The value range is `[32,192]`, with the unit being Kbps.<br><br><br>* If this parameter is not filled in, RTC will generate an audio bitrate value based on `AudioProfile`, `AudioSampleRate` and `AudioChannels`<br><br>* If this parameter is filled in, it will be taken as the standard under normal circumstances. However, due to different settings of `AudioProfile`, `AudioSampleRate`, and `AudioChannels`, the actual upper and lower limits of the audio bitrate will be further dynamically adjusted within the range of [32, 192], and the actual effective bitrate may differ from the entered value. |
|AudioSampleRate |Integer |No |`48000` |Audio sample rate. The default value is `48000`. The value range is `{16000, 32000, 44100, 48000}`, and the unit is Hz. If the value is invalid, it is automatically changed to the default value.<br><br>&nbsp;<br><br>`16000` only takes effect on cloud recording. |
|AudioChannels |Integer |No |`2` |The number of audio track. The default value is `2`, and the range is `{1,2}`. `2` means dual channel. `1`means mono channel. If the value is invalid, it is automatically changed to the default value. |
|Layout |Object |No |`-` |Layout parameters. It's valid only in mixing\-stream mode. |
|LayoutMode |Integer |No |`0` |Layout mode. The default value is `0`, and the range of values is `{0, 1, 2, 3}`.<br><br><br>* 0: [self-adaptation layout](https://docs.byteplus.com/en/docs/12/docs-1167930#self-adaptation-mode).<br><br>* 1: [vertical layout](https://docs.byteplus.com/en/docs/12/docs-1167930#vertical-layout-mode) (not support the screen stream).<br><br>* 2: custom layout mode.<br><br>* 3: [side-by-side layout](https://docs.byteplus.com/en/docs/12/docs-1167930#side-by-side-layout-mode). |
|CustomLayout |Object |No |`-` |Use this parameter for specific settings when using custom layout mode. |
|Canvas |Object |No |`-` |The width and height of the overall screen (canvas) and the background color. |
|Width |Integer |No |`640` |The width of the overall screen (canvas), in px, in the range `[2, 4096]`(must be even). The default value is `640` .If the value is invalid, it is automatically changed to the default value. |
|Height |Integer |No |`480` |The overall screen (canvas) height, in px, in the range `[2, 2160]`(must be even). The default value is `480`. If the value is invalid, it is automatically changed to the default value. |
|Background |String |No |`#000000` |The background color of the overall screen (canvas) in the format #RGB (hexadecimal). The default value is `#000000`(black), and the range is `#000000~ #ffffff`(both case). If the value is invalid, it is automatically changed to the default value. |
|BackgroundImage |String |No |`-` |The URL of the background image. The maximum length is 1024 bytes. The format of the image that can be uploaded includes: JPG, JPEG, PNG. If the width and height of the background picture are inconsistent with the width and height of the overall screen, the background picture will be adjusted to a full screen. |
|Regions |Object[] |No |`-` |In Custom Layout mode, you can use `Regions` to set the picture layout for each video stream. Wherein each `Region` match corresponding video stream. |
|StreamIndex |Integer |Yes |`0` |The identifier of the stream. This flag should correspond to `TargetStreams. StreamList. Stream.Index`. |
|LocationX |Float |No |`0` |The normalized ratio of video stream to the abscissa of the upper left corner corresponding to relative to the overall picture. The value ranges from `[0.0, 1.0)`, and the default value is `0.0`. If this parameter is passed, the server will verify it.<br><br>&nbsp;<br><br>The actual coordinates of the upper left corner of the corresponding area of the video stream are obtained by multiplying the picture size and normalized scale and rounding. Suppose, `Canvas. Width = 1920, Region. LocationX = 0.33`, then the abscissa of the upper left corner of the canvas is `634`(1920\*0.33=633.6 rounded). |
|LocationY |Float |No |`0` |The normalized ratio of video stream to the ordinate of the upper left corner corresponding to relative to the overall picture , the value ranges from `[0.0,1.0)`, and the default value is `0.0`. If this parameter is passed, the server will verify it. |
|WidthProportion |Float |Yes |`0.5` |The normalized ratio of video stream to the width of the region corresponding to relative to the overall picture. The range of values is `(0.0,1.0]`. |
|HeightProportion |Float |Yes |`0.5` |The normalized ratio of video stream to the height of the region corresponding to relative to the overall picture. The range of values is `(0.0,1.0]`. |
|ZOrder |Integer |No |`0` |Use this parameter to set the layer order of the specified picture when the pictures of multiple streams overlap. The value range is `[0,100]`. `0`means that the area image is at the lowest level, and `100`means that the area image is at the top level. The default value is `0`. If the value is invalid, it is automatically changed to the default value. |
|Alpha |Float |No |`1` |The transparency of the picture. The value range is `(0.0, 1.0]`. `0.0`means completely transparent, `1.0` means completely opaque, and the default value is `1.0`. If the value is invalid, it is automatically changed to the default value. |
|RenderMode |Integer |No |`0` |The rendering mode of the stream's picture. The value ranges from `{0,1,2,3}`, and the default value is `0`:<br><br><br>* `0`: Scale directly according to the specified width and height. If the aspect ratio of the input stream is different from the specified aspect ratio, the screen will be distorted.<br><br>* `1`: Crop the video according to the aspect ratio of the display area, and then scale the video proportionally to fill the display area.<br><br>* `2`: Scale the video according to the aspect ratio of the original screen, and displaying it in the center of the display area. If the aspect ratio of the original screen is different from the specified aspect ratio, there will be gaps in the screen, which will be filled with the background color value.<br><br>* `3`: Scale directly according to the specified width and height. If the aspect ratio of the original screen is different from the specified aspect ratio, the screen will be distorted.<br><br><br>When the value is invalid, it will automatically adjust to the default value.<br><br>Currently, `0` and `3` are the same mode, but it's recommended to use `3` to achieve the same logic as the client.<br><br>Under different rendering modes, the effects are as follows: <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/Rendermode.png) </span> |
|SourceCrop |Object |No |`-` |The source stream clipping function. Clipping can be done before the source video frame is rendered, that is, rendering after preprocessing. |
|LocationX |Float |No |`0` |The normalized ratio of the abscissa of the upper left corner of the video frame obtained after cutting relative to the overall picture before cutting and the value ranges from `[0.0,1.0)`. It defaults to `0.0`. If the value is invalid, it is automatically changed to the default value. |
|LocationY |Float |No |`0` |The normalized ratio of the ordinate of the upper left corner of the video frame obtained after cutting relative to the overall picture before cutting, the value ranges from `[0.0,1.0)`. It defaults to `0.0`. If the value is invalid, it is automatically changed to the default value. |
|WidthProportion |Float |No |`0.5` |The normalized ratio of video stream after cutting to the width of the region corresponding to relative to the overall picture. The value ranges from `(0.0,1.0]`. It defaults to `1.0`. If the value is invalid, it is automatically changed to the default value. |
|HeightProportion |Float |No |`0.5` |The normalized ratio of video stream after cutting to the height of the region corresponding to relative to the overall picture. The value ranged from `(0.0,1.0]`. It defaults to `1.0`. If the value is invalid, it is automatically changed to the default value. |
|AlternateImage |String |No |`-` |The url of the complement picture. The length does not exceed 1024 strings.<br><br><br>* If the video stream corresponding to the `Region. StreamIndex` is not published, or suspended, the image corresponding to `AlternateImage`will fill the canvas space corresponding to the `Region`. When the video stream is captured and published, `AlternateImage`does not cause any impact.<br><br>* The formats that can be uploaded include: JPG, JPEG, PNG.<br><br>* When the size of the picture and the canvas do not match, the picture will be rendered in the canvas according to the settings of RenderMode. |
|MediaType |Integer |No |`0` |Media type of the stream to be mixed.<br><br><br>* `0`: Audio and Video<br><br>* `1`: Audio<br><br>* `2`: Video<br><br><br>The default value is `0`. When the value is invalid, it will automatically adjust to the default value.<br><br>For example. If the input stream is an audio and video stream, MediaType = `1`, only video content is mixed. |
|AlternateImageFillMode |Integer |No |`0` |Rendering mode of the placeholder image.<br><br><br>* `0`: Scale according to the ratio of the user's video frame.<br><br>* `1`: Maintain the ratio of the placeholder image.<br><br><br>The default value is `0`. If the value is invalid, it is automatically changed to the default value. |
|MainVideoStream |Object |No |`-` |Effective and required in vertical layout mode (when `LayoutMode` is set to 1), this setting dictates the attributes of the main video stream. |
|Index |Integer |No |`0` |In custom layout, use `Index` to flag the stream. Later in the `Layout.regions.StreamIndex`, you need to use `Index` to specify the layout settings for the corresponding stream. |
|UserId |String |Yes |`Your_UserId` |UserId which represents the user a stream belongs to. |
|StreamType |Integer |No |`0` |The type of stream. The value can be `0` or `1`, and the default value is `0`. `0`means normal audio & video stream, `1` means screen stream. You don't need to specify `StreamType` for WTN. |
|Control |Object |No | |Configuration Options. |
|MediaType |Integer |No |`0` |The type of stream that is used to globally control the subscription. `0` means audio & video, and `1` means pure audio. Pure video is not supported. The default value is `0`. For WTN, use default value only. |
|FrameInterpolationMode |Integer |No |`0` |The default value is `0`. Value can take `0`and `1`. `0` is the last frame, and `1`is the black frame. If the value is invalid, it is automatically changed to the default value.<br><br>&nbsp;<br><br>In automatic layout mode, there is no logic for adding frame.<br><br>&nbsp;<br><br>**What is adding frame**:<br><br>&nbsp;<br><br>The frame rate of the video is usually fixed when audio & video is recorded or transcoded. However, due to network fluctuations or other reasons, the actual frame rate may not reach the preset frame rate. At this time, it is necessary to add frames to keep the video smooth. Adding the last frame means that the supplementary video frame is the same as the last frame before the interruption, and the picture seen at this time may be temporarily still. Completing black frames means that the supplementary video frames are all black. |
|MaxSilenceSeconds |Integer |No |`180` |The max silence time of the task, effective only for single\-stream recording. The value range is [60, 3600], with the unit being seconds, and the default value is 3600.<br><br><br>* If the silence time is less than set value, frames will be added according to the set `FrameInterpolationMode`.<br><br>* If the silence time is greater than set value but less than the idle timeout time, a new file will be generated when the task resumes. |
|MaxIdleTime |Integer |No |`180` |The idle timeout time of the task, after which the task will automatically terminate. The unit is seconds. The value range is `[10,86400]`, and the default value is `180`.<br><br><br>* If the idle time is less than set value, the task will resume and frames will be added according to the set `FrameInterpolationMode` when the task resumes.<br><br>* If the idle time exceeds set value, the task will be automatically terminated. |
|MaxRecordTime |Integer |No |`0` |(Valid for recording only) Maximum recording duration in seconds. Default is `0`. `0`means there is no limit to the recording time. |
|EnableSyncUpload |Boolean |No |`0` |Whether to enable the feature of "recording and uploading simultaneously".<br><br><br>* `false`: Disabled<br><br>* `true`: Enabled.<br><br>   The default value is False.<br><br>   This feature only takes effect for files stored in HLS format, that is: the value of `FileFormatConfig.FileFormat` must include HLS. If the `HLS` format file name contains the Duration fillable variable, with this feature enabled, the value of Duration is always set to 0. |
|FileFormatConfig |Object |No | |Configuration about the format of recording file. |
|FileFormat |String[] |No |`["HLS"]` |Storage file format. It can take MP4, HLS, FLV, MP3, AAC , M4A. Multiple formats can be selected at the same time.<br><br>&nbsp;<br><br>MP3, AAC, and M4A are only valid when encoding pure audio. |
|FileNameConfig |Object |No |`directory1/directory2/Your_TaskId_Your_RoomId_1645769481126_000030_c4694fa1.mp4` |Configuration about the name of recording file.<br><br>**The rule of the file name：** <br><br>The name of the file name is jointly determined by `StorageConfig.Type` and `FileNameConfig`.<br><br><br>* When `StorageConfig.Type` is equal to `1`, the file will be stored in the Vod platform. The file name consists of `FilenameConfig.Pattern` + random number.<br><br>* When the `StorageConfig.Type` is equal to `2`, the file will be stored on a third\-party storage platform. The file name consists of `FilenameConfig.Prefix` + `FilenameConfig.Pattern` + random number.<br><br><br>For example, when `StorageConfig.Type` is equal to `1`, `FilenameConfig.Pattern` is set to `{TaskId}_{RoomId}_{StartTime}_{Duration}`,<br><br>`TaskId` = `Your_TaskId`, `RoomId` = `Your_RoomId`, `StartTime` = `1645769481126`, `Duration` = `30s`, and the random number is `c4694fa1`, the file name is: `Your_TaskId_Your_RoomId_1645769481126_000030_c4694fa1.mp4`.<br><br>When `StorageConfig.Type` is equal to `2`, `FilenameConfig.Prefix` is set to `directory1/directory2/`, `FilenameConfig.Pattern` is set to `{TaskId}_{RoomId}_{StartTime}_{Duration}`,<br><br>`TaskId` = `Your_TaskId`, `RoomId` = `Your_RoomId`, `StartTime` = `1645769481126`, `Duration` = `30s`, and the random number is `c4694fa1`, the file name is: `directory1/directory2/Your_TaskId_Your_RoomId_1645769481126_000030_c4694fa1.mp4`.<br><br>If you set `Pattern`, you need to ensure the uniqueness of the output file's name, or files with the same name will be overwritten. You can also enable version control for your bucket to support duplicate file names. |
|Prefix |String[] |No |`-` |Prefix of the filename, which takes effect for TosConfig and CustomConfig.<br><br>It is an array composed of multiple strings, which can be used to specify the folder on the third\-party storage platform supporting S3. For example: `Prefix`= `[" directory1 "," directory2 "]`, the prefix `directory1/directory2/`will be prefixed before the recording file name. The length of the prefix (including slashes) must not exceed 128 characters. Symbol characters such as slashes, underscores, and parentheses must not appear in 'Prefix'. Only the following characters are supported:<br><br><br>* 26 lowercase letters a\-z<br><br>* 26 uppercase letters A\-Z<br><br>* 10 numbers 0\-9 |
|Pattern |String |No |`-` |Filename pattern, see [Custom Recording Name](https://docs.byteplus.com/en/docs/12/docs-106873). |
|StorageConfig |Object |Yes | |Configuration about storage platform. Now BytePlus TOS, BytePlus VOD, Amazon S3, Alibaba Cloud, HUAWEI CLOUD OBS, Tencent Cloud COS, Qiniu Cloud Kodo and Google Cloud Storage are supported. |
|Type |Integer |No |`0` |Storage platform<br><br>&nbsp;<br><br>`0`: BytePlus TOS<br><br>&nbsp;<br><br>`1`: BytePlus Vod<br><br>&nbsp;<br><br>`2`: Third\-party storage platform supporting S3 protocol |
|TosConfig |Object |No |`-` |When Type = `0`, the value of TosConfig needs to be set correctly, otherwise the request will report an error. |
|AccountId |String |Yes |`30****000` |BytePlus AccountId.You can find it by licking the account icon in the top\-right corner.<br><br>&nbsp;<br><br>Even if you use the AK and SK of a sub\-user during the OpenAPI authentication process, the AccountId must be of the main account ID. |
|Bucket |String |Yes |`You****cket` |Name of bucket you created on TOS platform. |
|Region |Integer |No |`0` |Different storage platforms support different regions, see [Region list](https://docs.byteplus.com/en/docs/12/docs-115995#region-list).<br><br>&nbsp;<br><br>The default value is `0`. |
|VodConfig |Object |No |`-` |When Type = `1`, the value of VodConfig needs to be set correctly, otherwise the request will report an error. |
|AccountId |String |Yes |`Your_****untId` |Console account ID, such as `200000000`.<br><br><br>* To find the AccountID: Console \-\> My Account \-\> Account ID<br><br>   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/image.png) </span><br><br>* This `AccountID` must be the main account's `AccountID`.<br><br>* Even if AK and SK used to authenticate is from sub\-account, the `AccountID`must be the main account's `AccountID`. |
|Region |Integer |No |`-` |Different storage platforms support different regions, see [Region list](https://docs.byteplus.com/en/docs/12/docs-115995#region-list).<br><br>&nbsp;<br><br>The default value is `0`. |
|Space |String |Yes |`Your_Space` |Vod space name. |
|CustomConfig |Object |No | |When Type = `2`, you need to set the value of CustomConfig correctly, otherwise the request will report an error. |
|Vendor |Integer |No |`0` |Third\-party cloud storage platform.<br><br><br>* 0: Amazon S3. By default.<br><br>* 1: Aliyun object Storage Service OSS<br><br>* 2: HUAWEI CLOUD OBS<br><br>* 3: Tencent Cloud COS<br><br>* 4: Qiniu Cloud Kodo.<br><br>* 5: Google Cloud Storage<br><br><br>The default value is 0. |
|Region |Integer |No |`0` |Different storage platforms support different regions, see [Region list](https://docs.byteplus.com/en/docs/12/docs-115995#region-list).<br><br>&nbsp;<br><br>The default value is `0`. |
|Bucket |String |Yes |`You****cket` |Bucket name. |
|AccessKey |String |Yes |`Your_****ssKey` |The AccessKey of the third\-party storage platform account. Make sure this account has writing permission to the bucket.<br><br>&nbsp;<br><br>It's not recommended to enable reading permission. |
|SecretKey |String |Yes |`Your_****etKey` |The SecretKey of the third\-party storage platform account. |
|SecurityToken |String |No |`Your_SecurityToken` |A temporary security token for third\-party cloud storage. This token is issued by the cloud service provider's Security Token Service (STS) with an expiration date. Once the validity period expires, the token becomes invalid, thereby reducing the security risks associated with credential leaks.<br><br><br>* **Validity period**：The validity period of the SecurityToken must be longer than the recording duration, with at least an additional 1 hour reserved for failure retry. Otherwise, there is a risk of losing some data.<br><br>* **Unsupported cloud service providers**: Kodo of Qiniu Cloud is currently not supported. |


<span id="response-parameters"></span>
## Response parameters

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="samples"></span>
## Samples

<span id="sample-request-1"></span>
### Sample request 1

Automatic layout mode:

```json
POST https://open.byteplusapi.com?Action=StartRecord&Version=2022-06-01
{
    "AppId": "You****pId",
    "BusinessId": "Your_****nessId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "RecordMode": 0,
    "FileFormatConfig": {
        "FileFormat": [
            "HLS",
            "FLV"
        ]
    },
    "FileNameConfig": {
        "Prefix": [
            "directory1",
            "directory2"
        ],
        "Pattern": ""
    },
    "StorageConfig": {
        "Type": 1,
        "VodConfig": {
            "AccountId": "Your_****untId",
            "Region": 0,
            "Space": "Your_Space"
        }
    }
}
```


<span id="sample-response-1"></span>
### Sample response 1

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "StartRecord",
        "Version": "2022-06-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```


<span id="sample-request-2"></span>
### Sample request 2

Custom layout mode:

```json
POST https://open.byteplusapi.com?Action=StartRecord&Version=2022-06-01
{
    "AppId": "Your_AppId",
    "BusinessId" : "Your_BusinessId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "RecordMode": 0,
    "FileFormatConfig": {
        "FileFormat": ["HLS", "FLV"]
    },
    "FileNameConfig": {
        "Prefix": ["directory1", "directory2"],
        "Pattern": ""
    },
    "StorageConfig": {
        "Type": 1,
        "VodConfig": {
            "AccountId": "Your_AccountId",
            "Region": 0,
            "Space": "Your_Space"
        }
    },
    "TargetStreams": {
        "StreamList": [
            {
                "Index": 0,
                "UserId": "Your_UserId_3"
            },
            {
                "Index": 1,
                "UserId": "Your_UserId_4",
                "StreamType": 1
            }
        ]
    },
    "Layout": {
        "LayoutMode": 2,
        "CustomLayout": {
            "Canvas": {
                "Width": 860,
                "Height": 340,
                "Background": "#303342"
            },
            "Regions": [
                {
                    "StreamIndex": 0,
                    "LocationX": 0,
                    "LocationY": 0,
                    "WidthProportion": 0.5,
                    "HeightProportion": 1,
                    "ZOrder": 0,
                    "Alpha": 1,
                    "RenderMode": 0
                },
                {
                    "StreamIndex": 1,
                    "LocationX": 0.5,
                    "LocationY": 0,
                    "WidthProportion": 0.5,
                    "HeightProportion": 1,
                    "ZOrder": 1,
                    "Alpha": 1,
                    "RenderMode": 1
                }
            ]
        }
    }
}
```


<span id="sample-response-2"></span>
### Sample response 2

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "StartRecord",
        "Version": "2022-06-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
