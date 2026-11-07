---
title: "GetPushMixedStreamToCDNTask"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-w5q4dtjbde"
---

After you start a mixed\-stream task to push to CDN, you can use this interface to query the task.

<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://open.byteplusapi.com?Action=GetPushMixedStreamToCDNTask&Version=2020\-12\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="Query"></span>
### Query


|**Parameter**  |**Data Type**  |**Required**  |**Sample Value**  |**Description**  |
|---|---|---|---|---|
|Action |String |Yes |`GetPushMixedStreamToCDNTask` |Interface name. The value of this interface: `GetPushMixedStreamToCDNTask` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |
|AppId |String |Yes |`661e7ae5543cf` |The only identifier for your audio & video app. See [get the AppId](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid). |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. |
|TaskId |String |No |`Your_TaskId` |Custom an ID for this task.<br><br>It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.<br><br>The `TaskId` is the identifier of the task. Under a RoomId of an AppId, the TaskId is unique. The TaskId can be repeated under different AppId or different RoomId. Therefore, AppId + RoomId + TaskId is the unique identifier of the task, which can be used to identify the running task in a certain room under the specified AppId, so that this task can be updated or stopped during the running of this task. |
|UserId |String |No |`Your_UserId` |The user ID of the client that initiates the live streaming relay task.<br><br>If you start more than two tasks, when calling this interface to query:<br><br><br>* The first task. `UserId` can be passed in by Id of user initiating the task, `TaskId` can be passed in by `Null` or Id of user initiating the task.<br><br>* Other tasks. `UserId` can be passed in by Id of user initiating the task, `TaskId` can be passed in by Id of mixing\-stream task. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|PushMixedStreamToCDNTask |Object of [PushMixedStreamToCDNTask](https://docs.byteplus.com/en/docs/12/14226#pushmixedstreamtocdntask) |`-` |Information about the mixed\-stream task. |


<span id="pushmixedstreamtocdntask"></span>
### PushMixedStreamToCDNTask


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|StartTime |Long |`1624873773000` |Start time of a task, Unix timestamp, in milliseconds |
|EndTime |Long |`1624874235000` |End time of a task, Unix timestamp, in milliseconds. `0` means the task is not finished |
|Status |Long |`3` |Task status:<br><br><br>* `0`: Unknown exception status<br><br>* `1`: Not started<br><br>* `2`: Running<br><br>* `3`: Ended<br><br>* `4`: Task failed |
|StopReason |String |`StopByAPI` |The reason why the mixed stream push task stopped. The possible values are as follows:<br><br><br>* Empty string: The task is not finished.<br><br>* `UnknownStopReason`: Unknown stop reason.<br><br>* `StopByAPI`: The user actively called the server\-side OpenAPI to stop the task.<br><br>* `StartTaskFailed`: Task failed to start.<br><br>* `IdleTimeOut`: The task exceeded the maximum idle time.<br><br>* `UserDisconnect`: The client user actively left the room or called the stop push interface. |
|PushStreamState |Integer |`6` |Status of pushing the stream<br><br><br>* `0`: Failed to get the status of task. It's recommended to make a query again later.<br><br>* `1`: Not started<br><br>* `2`: First time to connect CDN service<br><br>* `3`: Reconnecting to CDN service<br><br>* `4`: Succeeded to connect CDN service, and trying to pushing the stream.<br><br>* `5`: Succeeded to connect CDN service and push the stream<br><br>* `6`: Stopped to push the stream.<br><br><br>Only when `Status`=`2`，`PushStreamState` is meaningful；When`Status`=`3`，`PushStreamState`=`6`; when `status` returns other values，`PushStreamState` =`0`. |
|TargetStreams |Object of [Streams](https://docs.byteplus.com/en/docs/12/14226#streams) |`-` |The audio & video stream that needs to be mixed in the room. |
|ExcludeStreams |Object of [Streams](https://docs.byteplus.com/en/docs/12/14226#streams) |`-` |The audio & video stream that needs to be excluded. |
|PushURL |String |`rtmp://xxxxxx` |Push stream address. Only rtmp and rtmps protocols are supported. The rtmps protocol only supports internal business. |
|Encode |Object of [Encode](https://docs.byteplus.com/en/docs/12/14226#encode) |`-` |Encoding parameters of audio and video. |
|Layout |Object of [Layout](https://docs.byteplus.com/en/docs/12/14226#layout) |`-` |Layout parameters when multiple streams in the room are mixed into one. |
|Control |Object of [Control](https://docs.byteplus.com/en/docs/12/14226#control) | |Configuration options. |


<span id="streams"></span>
### Streams


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|StreamList |Array of [Stream](https://docs.byteplus.com/en/docs/12/14226#stream) |`-` |A list of `Streams`. It can be empty. When empty, it means subscribing to all streams in the room. In a `StreamList`, `Stream. Index`cannot be duplicated. |


<span id="stream"></span>
### Stream


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|Index |Integer |`0` |In custom layout, use `Index` to flag the stream. Later in the `Layout.regions.StreamIndex`, you need to use `Index` to specify the layout settings for the corresponding stream. |
|WTNStreamId |String |`wtn_live_stream_01` |The ID of the WTN stream to be pushed.<br><br>> Required when pushing WTN streams, and mutually exclusive with `UserId`. |
|UserId |String |`Your_UserId` |UserId which represents the user a stream belongs to.<br><br>> Required when pushing RTC audio and video streams and is mutually exclusive with `WTNStreamId`. |
|StreamType |Integer |`0` |The type of RTC stream:<br><br><br>* `0` (default): Normal audio & video stream.<br><br>* `1`: Screen stream.<br><br><br>> It only takes effect when pushing an RTC stream. |


<span id="encode"></span>
### Encode


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|VideoWidth |Integer |`640` |The width of the output picture. The default value is `640`and the range is `[2,1920]`, which must be even. If the value is invalid, it is automatically changed to the default value. This parameter does not take effect when the custom layout mode turns on, and the width of the overall picture complies with `canvas.width`. |
|VideoHeight |Integer |`480` |The height of the output picture, and the range is `[2,1920]`, which must be even. The default value is `480`. If the value is invalid, it is automatically changed to the default value. This parameter does not take effect when the custom layout mode turns on, and the hight of the overall picture compile with `canvas.Height`. |
|VideoFps |Integer |`15` |Output video frame rate. The default is `15` and the range is `[1,60]`. If the value is invalid, it is automatically changed to the default value. |
|VideoBitrate |Integer |`-` |Output video bit rate. Value range is `[1,10000]`, in Kbps. Default value is self\-adaptation. If the value is invalid, it is automatically changed to the default value. When `VideoCodec = 1`, you must set this field. |
|VideoCodec |Integer |`0` |Video coding protocol. The default value is `0`. The value can be `0`or `1`. `0`means `H.264`. `1`means`byteVC1`. When `VideoCodec = 1`, you must set the `VideoBitrate`field. |
|VideoGop |Integer |`4` |Output video GOP. The default is `4`and the range is `[1, 5]`in seconds. If the value is invalid, it is automatically changed to the default value. |
|AudioCodec |Integer |`0` |Audio encoding protocol. The default value is `0`, and the aac encoding protocol is used at this time. Currently only aac is supported. |
|AudioProfile |Integer |`0` |Audio profile type, effective when using aac encoding. The default value is `0` and the range is `{0,1,2}`. `0` means LC ;`1` means HE\-V1 specifications;`2` means HE\-V2 specifications.When `AudioProfile`takes `2`, only dual channel is supported. If the value is invalid, it is automatically changed to the default value. |
|AudioBitrate |Integer |`\-` |Audio bitrate. The value range is `[32,192]`, with the unit being Kbps.<br><br><br>* If this parameter is not filled in, RTC will generate an audio bitrate value based on `AudioProfile`, `AudioSampleRate` and `AudioChannels`<br><br>* If this parameter is filled in, it will be taken as the standard under normal circumstances. However, due to different settings of `AudioProfile`, `AudioSampleRate`, and `AudioChannels`, the actual upper and lower limits of the audio bitrate will be further dynamically adjusted within the range of [32, 192], and the actual effective bitrate may differ from the entered value. |
|AudioSampleRate |Integer |`48000` |Audio sample rate. The default value is `48000`. The value range is `{16000, 32000, 44100, 48000}`, and the unit is Hz. If the value is invalid, it is automatically changed to the default value.<br><br>`16000` only takes effect on cloud recording. |
|AudioChannels |Integer |`2` |The number of audio track. The default value is `2`, and the range is `{1,2}`. `2` means dual channel. `1`means mono channel. If the value is invalid, it is automatically changed to the default value. |


<span id="layout"></span>
### Layout


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|LayoutMode |Integer |`0` |Layout mode. The default value is `0`, and the value ranges from `{0, 1, 2, 3}` .<br><br><br>* `0`: Self\-adaptation layout mode.<br><br>* `1`: Vertical layout mode (this mode does not support the screen stream).<br><br>* `2`: Custom layout mode.<br><br>* `3`: Side\-by\-side layout mode.<br><br><br>See details in [Mixed-stream Layout Mode](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69818#jFHMzAHT). |
|MainVideoStreamIndex |Integer |`-` |This parameter takes effect when the vertical layout mode is used and the `TargetStreams.StreamList` is not empty. At this point, the corresponding `StreamList. Stream. Index` video stream is the main picture stream. If `TargetStreams. StreamList` is null, the main picture stream is a random stream. |
|CustomLayout |Object of [CustomLayout](https://docs.byteplus.com/en/docs/12/14226#customlayout) |`-` |Use this parameter for specific settings when using custom layout mode. |


<span id="customlayout"></span>
### CustomLayout


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|Canvas |Object of [Canvas](https://docs.byteplus.com/en/docs/12/14226#canvas) |`-` |The width and height of the overall screen (canvas) and the background color. |
|Regions |Array of [Region](https://docs.byteplus.com/en/docs/12/14226#region) |`-` |In Custom Layout mode, you can use `Regions`to set the picture layout for each video stream. Wherein each `Region`match corresponding video stream. |


<span id="canvas"></span>
### Canvas


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|Width |Integer |`640` |The width of the overall screen (canvas), in px, in the range `[2,1920]` (must be even). The default value is `640`.If the value is invalid, it is automatically changed to the default value |
|Height |Integer |`480` |The overall screen (canvas) height, in px, in the range `[2,1920]` (must be even). The default value is `480`. If the value is invalid, it is automatically changed to the default value. |
|Background |String |`#000000` |The background color of the overall screen (canvas) in the format #RGB (hexadecimal). The default value is `#000000` (black), and the range is `#000000~ #ffffff` (both case). If the value is invalid, it is automatically changed to the default value. |
|BackgroundImage |String |`无` |The URL of the background image. The maximum length is 1024 bytes. The format of the image that can be uploaded includes: JPG, JPEG, PNG. If the width and height of the background picture are inconsistent with the width and height of the overall screen, the background picture will be adjusted to a full screen. |


<span id="region"></span>
### Region


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|StreamIndex |Integer |`0` |The identifier of the stream. This flag should correspond to `TargetStreams. StreamList. Stream.Index`. |
|LocationX |Float |`0` |The normalized ratio of video stream to the abscissa of the upper left corner corresponding to relative to the overall picture. The value ranges from `[0.0, 1.0)`, and the default value is `0`. If this parameter is passed, the server will verify it. If it is not valid, the server will return the error code `InvalidParameter`.<br><br>The actual coordinates of the upper left corner of the corresponding area of the video stream are obtained by multiplying the picture size and normalized scale and rounding. Suppose, `Canvas. Width = 1920, Region. LocationX = 0.33`, then the abscissa of the upper left corner of the canvas is `634`(1920\*0.33=633.6 rounded). |
|LocationY |Float |`0` |The normalized ratio of video stream to the ordinate of the upper left corner corresponding to relative to the overall picture , the value ranges from `[0.0,1.0)`, and the default value is `0`. If this parameter is passed, the server will verify it. If it is not valid, the server will return the error code `InvalidParameter`.<br><br>The actual coordinates of the upper left corner of the corresponding area of the video stream are obtained by multiplying the picture size and normalized scale and rounding. Suppose, `Canvas. Width = 1920, Region. LocationX = 0.33`, then the abscissa of the upper left corner of the canvas is `634`(1920\*0.33=633.6 rounded). |
|WidthProportion |Float |`0.5` |The normalized ratio of video stream to the width of the region corresponding to relative to the overall picture. The range of values is `(0.0,1.0]`. |
|HeightProportion |Float |`0.5` |The normalized ratio of video stream to the height of the region corresponding to relative to the overall picture. The range of values is `(0.0,1.0]`. |
|ZOrder |Integer |`0` |Use this parameter to set the layer order of the specified picture when the pictures of multiple streams overlap. The value range is `[0,100]`. `0`means that the area image is at the lowest level, and `100`means that the area image is at the top level. The default value is `0`. If the value is invalid, it is automatically changed to the default value. |
|Alpha |Float |`1` |The transparency of the picture. The value range is `(0.0, 1.0]`. `0.0`means completely transparent, `1.0` means completely opaque, and the default value is `1.0`. If the value is invalid, it is automatically changed to the default value. |
|RenderMode |Integer |`0` |The rendering mode of the stream's picture. The value ranges from `{0,1,2,3}`, and the default value is `0`:<br><br><br>* `0`: Scale directly according to the specified width and height. If the aspect ratio of the input stream is different from the specified aspect ratio, the screen will be distorted.<br><br>* `1`: Crop the video according to the aspect ratio of the display area, and then scale the video proportionally to fill the display area.<br><br>* `2`: Scale the video according to the aspect ratio of the original screen, and displaying it in the center of the display area. If the aspect ratio of the original screen is different from the specified aspect ratio, there will be gaps in the screen, which will be filled with the background color value.<br><br>* `3`: Scale directly according to the specified width and height. If the aspect ratio of the original screen is different from the specified aspect ratio, the screen will be distorted.<br><br><br>When the value is invalid, it will automatically adjust to the default value.<br><br>&nbsp;<br><br>Currently, `0` and `3` are the same mode, but it's recommended to use `3` to achieve the same logic as the client.<br><br>&nbsp;<br><br>Under different rendering modes, the effects are as follows: <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/Rendermode.png) </span> |
|SourceCrop |Object of [SourceCrop](https://docs.byteplus.com/en/docs/12/14226#sourcecrop) |`\-` |The source stream clipping function. Clipping can be done before the source video frame is rendered, that is, rendering after preprocessing |
|AlternateImage |String |`\-` |The url of the complement picture. The length does not exceed 1024 strings.<br><br><br>1. If the video stream corresponding to the `Region. StreamIndex` is not published, or suspended, the image corresponding to `AlternateImage` will fill the canvas space corresponding to the `Region`. When the video stream is captured and published, `AlternateImage`does not cause any impact.<br><br>2. The formats that can be uploaded include: JPG, JPEG, PNG.<br><br>3. When the size of the picture and the canvas do not match, the picture will be rendered in the canvas according to the settings of RenderMode. |
|MediaType |Integer |`0` |Media type of the stream to be mixed.<br><br><br>* `0`: Audio and Video<br><br>* `1`: Audio<br><br>* `2`: Video<br><br><br>The default value is `0`. When the value is invalid, it will automatically adjust to the default value.<br><br>For example. If the input stream is an audio and video stream, MeidaType = `1`, only video content is mixed. |
|AlternateImageFillMode |Integer |`0` |Rendering mode of the placeholder image.<br><br><br>* `0`: Scale according to the ratio of the user's video frame<br><br>* `1`: Maintain the ratio of the placeholder image<br><br><br>The default value is `0`. If the value is invalid, it is automatically changed to the default value. |


<span id="sourcecrop"></span>
### SourceCrop


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|LocationX |Float |`0` |The normalized ratio of the abscissa of the upper left corner of the video frame obtained after cutting relative to the overall picture before cutting and the value ranges from `[0.0,1.0)`. It defaults to `0.0`. If the value is invalid, it is automatically changed to the default value. |
|LocationY |Float |`0` |The normalized ratio of the ordinate of the upper left corner of the video frame obtained after cutting relative to the overall picture before cutting, the value ranges from `[0.0,1.0)`. It defaults to `0.0`. If the value is invalid, it is automatically changed to the default value. |
|WidthProportion |Float |`0.5` |The normalized ratio of video stream after cutting to the width of the region corresponding to relative to the overall picture. The value ranges from `(0.0,1.0]`. It defaults to `1.0`. If the value is invalid, it is automatically changed to the default value. |
|HeightProportion |Float |`0.5` |The normalized ratio of video stream after cutting to the height of the region corresponding to relative to the overall picture. The value ranged from `(0.0,1.0]`. It defaults to `1.0`. If the value is invalid, it is automatically changed to the default value. |


<span id="control"></span>
### Control


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|MediaType |Integer |`0` |The type of stream that is used to globally control the subscription. `0` means audio & video, and `1` means pure audio. Pure video is not supported. The default value is `0`. For WTN, use default value only. |
|FrameInterpolationMode |Integer |`0` |The default value is `0`. Value can take `0`and `1`. `0` is the last frame, and `1`is the black frame. If the value is invalid, it is automatically changed to the default value. In automatic layout mode, there is no logic for adding frame.<br><br>**What is adding frame**: The frame rate of the video is usually fixed when audio & video is recorded or transcoded. However, due to network fluctuations or other reasons, the actual frame rate may not reach the preset frame rate. At this time, it is necessary to add frames to keep the video smooth. Adding the last frame means that the supplementary video frame is the same as the last frame before the interruption, and the picture seen at this time may be temporarily still. Completing black frames means that the supplementary video frames are all black.<br><br>Relationship among Placeholder image, frame Interpolation, keeping last Frame:<br><br>&nbsp;<br><br>You can set the placeholder image in the `Region` by passing the `Alternateimage` field, and set the frame interpolation mode in the `Control` by passing the `FrameInterpolationMode` field. However, the priority of the setting of placeholder image is higher than that of the frame interpolation mode.<br><br><br>* When the video stream corresponding to `Region.StreamIndex` stops publishing, the canvas corresponding to `Region` will be filled with the placeholder image or the image set in interpolation frame mode according to the setting. But when the video stream is a screen stream, the frame interpolation mode does not take effect.<br><br>* When the video stream corresponding to `Region.StreamIndex` stops capturing or pushing, the canvas corresponding to `Region` will be filled with the last frame.<br><br>* When the video stream corresponding to `Region.StreamIndex` is published, the set placeholder image or the frame set in interpolation mode has no effect. |
|MaxIdleTime |Integer |`180` |The idle timeout time of the task, after which the task will automatically terminate. The unit is seconds. The value range is `[10,86400]`, and the default value is `180`.<br><br><br>* If the idle time is less than set value, the task will resume and frames will be added according to the set `FrameInterpolationMode` when the task resumes.<br><br>* If the idle time exceeds set value, the task will be automatically terminated. |
|MaxRecordTime |Integer |`0` |(Valid for recording only) Maximum recording duration in seconds. Default is `0`. `0`means there is no limit to the recording time. |
|TalkVolume |Integer |`30` |(Valid for pushing to CDN only)Effective volume of user. The range is `[0,255]`, and the default value is `30`. |
|SpatialConfig |Object of [SpatialConfig](https://docs.byteplus.com/en/docs/12/14226#spatialconfig) | |Configuration of spatial audio. If the audio parameter of pushing to CDN is set to mono channel, this function will be invalid. |
|PushStreamMode |Integer |`0` |Pushshing\-stream mode of pushing to CDN, used to control the timing of triggering pushing streams to CDN. The value can take `0` or `1`.<br><br><br>* 0: The stream will be pushed to CDN when a user in the room pushes a RTC stream.<br><br>* 1: After calling the interface, a stream will be pushed to CDN regardless of whether there are a user in the room pushing a RTC stream.<br><br><br>When the value is illegal, it will be automatically adjusted to the default value.<br><br>The logic of timeout remains unchanged. |


<span id="spatialconfig"></span>
### SpatialConfig


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|EnableSpatialRender |Boolean |`false` |Whether to enable spatial audio.<br><br><br>* `false`: Disable<br><br>* `true`: Enable |
|AudienceSpatialPosition |Array of Integer |`[0,0,0]` |The Three\-dimensional coordinates of the audience's location. The default value is `[0,0,0]`. The length of the array is `3`, and the three values correspond to `X`, `Y`, and `Z` respectively. The range of each value is `[-100, 100]`. |
|AudienceSpatialOrientation |Object of [AudienceSpatialOrientation](https://docs.byteplus.com/en/docs/12/14226#audiencespatialorientation) |`-` |Set the orientation of the audience. The vectors are perpendicular to each other, and if the values passed do not guarantee perpendicularity to each other, the default value is automatically assigned. The default values are: `forward` = `[1, 0, 0]`, `right` = `[0, 1, 0]`, `up` = `[0, 0, 1]`. |


<span id="audiencespatialorientation"></span>
### AudienceSpatialOrientation


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|Up |Array of Float |`[1, 0, 0]` |前方朝向 |
|Right |Array of Float |`[0, -1, 0]` |右边朝向 |
|Forward |Array of Float |`[0, 0, 1]` |头顶朝向 |


<span id="sample-request"></span>
### Sample request

```json
GET https://open.byteplusapi.com?Action=GetPushMixedStreamToCDNTask&Version=2020-12-01&AppId=661e****543cf&RoomId=Your_RoomId&TaskId=Your_TaskId&UserId=Your_UserId
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": {
        "PushMixedStreamToCDNTask": {
            "StartTime": 1677237518000,
            "EndTime": 1677239022000,
            "Status": 3,
            "StopReason": "StopByAPI",
            "PushStreamState": "6",
            "TargetStreams": {
                "StreamList": [
                    {
                        "Index": 1,
                        "UserId": "user1",
                        "StreamType": 0
                    }
                ]
            },
            "ExcludeStreams": {
                "StreamList": [
                    {
                        "Index": 3,
                        "UserId": "user3",
                        "StreamType": 1
                    }
                ]
            },
            "PushURL": "rtmp://xxxxxx",
            "Layout": {
                "LayoutMode": 2,
                "CustomLayout": {
                    "Canvas": {
                        "Width": 1280,
                        "Height": 720,
                        "Background": "#303342",
                        "BackgroundImage": "http://xxxxxx"
                    },
                    "Regions": [
                        {
                            "StreamIndex": 1,
                            "LocationX": 0,
                            "LocationY": 0.2,
                            "WidthProportion": 0.5,
                            "HeightProportion": 0.4,
                            "ZOrder": 0,
                            "Alpha": 1,
                            "CornerRadius": 0,
                            "RenderMode": 0,
                            "SourceCrop": {
                                "LocationX": 0.5,
                                "LocationY": 0.5,
                                "WidthProportion": 0.4,
                                "HeightProportion": 0.4
                            },
                            "AlternateImage": "http://xxxxx",
                            "SpatialPosition": [
                                1,
                                1,
                                1
                            ]
                        }
                    ]
                }
            },
            "Encode": {
                "VideoCodec": 0,
                "VideoBitrate": 1600,
                "VideoWidth": 1280,
                "VideoHeight": 720,
                "VideoFps": 15,
                "VideoGop": 4,
                "AudioCodec": 0,
                "AudioProfile": 0,
                "AudioBitrate": 128,
                "AudioSampleRate": 48000,
                "AudioChannels": 2
            },
            "Control": {
                "MediaType": 0,
                "FrameInterpolationMode": 0,
                "MaxIdleTime": 180,
                "VolumeIndicationInterval": 2,
                "VolumeIndicationMode": false,
                "TalkVolume": 0,
                "SpatialConfig": {
                    "AudienceSpatialPosition": [
                        0,
                        0,
                        0
                    ]
                },
                "PushStreamMode": 0
            }
        }
    },
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "GetPushMixedStreamToCDNTask",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "cn-north-1"
    }
}
```
