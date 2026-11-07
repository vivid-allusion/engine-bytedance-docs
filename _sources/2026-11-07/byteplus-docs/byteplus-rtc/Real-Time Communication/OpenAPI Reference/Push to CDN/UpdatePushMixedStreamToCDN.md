---
title: "UpdatePushMixedStreamToCDN"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69849"
---

If you have started a task, you can call `UpdatePushMixedStreamToCDN` to update the task's parameters.

<span id="usage-scenario"></span>
## Usage scenario

You can call the `UpdatePushMixedStreamToCDN`interface to override the following parameters previously set in `StartPushMixedStreamToCDN`or `UpdatePushMixedStreamToCDN`:


* `TargetStreams`

* `Layout.CustomLayout.Canvas.Background`, `Layout.CustomLayout.Canvas.BackgroundImage` and `Layout.CustomLayout.Regions`

* parameters in `Encode` other than `audioProfile` .


By calling this OpenAPI, you cannot update parameters other than the above parameters. For the above parameters, if you do not pass in corresponding values when calling this API, these values will be updated to the default values.

<span id="requirements"></span>
## Requirements

When calling `StartPushMixedStreamToCDN`, `Layout. LayoutMode` must be 2. That is, some parameters of the `UpdatePushMixedStreamToCDN` update task are supported only in custom layout mode.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=UpdatePushMixedStreamToCDN&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdatePushMixedStreamToCDN` |Interface name. The value of this interface: `UpdatePushMixedStreamToCDN` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|BusinessId |String |No |`Your_****nessId` |The Business identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room |
|TaskId |String |Yes |`Your_TaskId` |Custom an ID for this task.<br><br>It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.<br><br>The `TaskId` is the identifier of the task. Under a RoomId of an AppId, the TaskId is unique. The TaskId can be repeated under different AppId or different RoomId. Therefore, AppId + RoomId + TaskId is the unique identifier of the task, which can be used to identify the running task in a certain room under the specified AppId, so that this task can be updated or stopped during the running of this task. |
|TargetStreams |Object of [Streams](https://docs.byteplus.com/en/docs/12/14224#streams) |No |`-` |You can use this parameter to set streams to be pushed to CDN. |
|Layout |Object of [Layout](https://docs.byteplus.com/en/docs/12/14224#layout) |No |`-` |Layout parameters when multiple streams in the room are mixed into one. |
|Encode |Object of [Encode](https://docs.byteplus.com/en/docs/12/14224#encode) |No |`-` |Encoding parameters of audio and video |
|Control |Object of [Control](https://docs.byteplus.com/en/docs/12/14224#control) |No | |Configuration options |
|IsUpdatePartialParam |Boolean |No |`False` |Whether to update partial parameters. Even after enabling this function, parameters must also be passed in hierarchical order. IF you need to update array\-type parameters,all parameters in the array must be passed in.<br><br><br>* `False`: No.<br><br>* `True`: Yes.<br><br>   The default value is `False`. |
|SequenceNumber |Integer |No |`0` |The sequence number of a request. If you pass in a sequence number, the server will verify it. Please ensure that the sequence number of the last update request is greater than the sequence number of the previous request.<br><br>It's recommended to pass in this parameter when updating partial parameters, so that the server will update parameters according to the latest request. |


<span id="streams"></span>
### Streams


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|StreamList |Array of [Stream](https://docs.byteplus.com/en/docs/12/14224#stream) |No |`-` |A list of `Streams`. It can be empty. When empty, it means subscribing to all streams in the room. In a `StreamList`, `Stream. Index`cannot be duplicated. |


<span id="stream"></span>
### Stream


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Index |Integer |No |`0` |In custom layout, use `Index` to flag the stream. Later in the `Layout.regions.StreamIndex`, you need to use `Index` to specify the layout settings for the corresponding stream. |
|WTNStreamId |String |No |`wtn_live_stream_01` |The ID of the WTN stream to be pushed.<br><br>> Required when pushing WTN streams, and mutually exclusive with `UserId`. |
|UserId |String |No |`Your_UserId` |UserId which represents the user a stream belongs to.<br><br>> Required when pushing RTC audio and video streams and is mutually exclusive with `WTNStreamId`. |
|StreamType |Integer |No |`0` |The type of RTC stream:<br><br><br>* `0` (default): Normal audio & video stream.<br><br>* `1`: Screen stream.<br><br>> It only takes effect when pushing an RTC stream. |


<span id="layout"></span>
### Layout


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|LayoutMode |Integer |No |`0` |Layout mode. The default value is `0`, and the value ranges from `{0, 1, 2, 3}` .<br><br><br>* `0`: Self\-adaptation layout mode.<br><br>* `1`: Vertical layout mode (this mode does not support the screen stream).<br><br>* `2`: Custom layout mode.<br><br>* `3`: Side\-by\-side layout mode.<br><br>   See details in [Mixed-stream Layout Mode](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69818#jFHMzAHT). |
|MainVideoStreamIndex |Integer |No |`-` |This parameter takes effect when the vertical layout mode is used and the `TargetStreams.StreamList` is not empty. At this point, the corresponding `StreamList. Stream. Index` video stream is the main picture stream. If `TargetStreams. StreamList` is null, the main picture stream is a random stream. |
|CustomLayout |Object of [CustomLayout](https://docs.byteplus.com/en/docs/12/14224#customlayout) |No |`-` |Use this parameter for specific settings when using custom layout mode. |


<span id="customlayout"></span>
### CustomLayout


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Canvas |Object of [Canvas](https://docs.byteplus.com/en/docs/12/14224#canvas) |No |`-` |The width and height of the overall screen (canvas) and the background color. |
|Regions |Array of [Region](https://docs.byteplus.com/en/docs/12/14224#region) |No |`-` |In Custom Layout mode, you can use `Regions`to set the picture layout for each video stream. Wherein each `Region`match corresponding video stream. |


<span id="canvas"></span>
### Canvas


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Width |Integer |No |`640` |The width of the overall screen (canvas), in px, in the range `[2,1920]` (must be even). The default value is `640`.If the value is invalid, it is automatically changed to the default value |
|Height |Integer |No |`480` |The overall screen (canvas) height, in px, in the range `[2,1920]` (must be even). The default value is `480`. If the value is invalid, it is automatically changed to the default value. |
|Background |String |No |`#000000` |The background color of the overall screen (canvas) in the format #RGB (hexadecimal). The default value is `#000000` (black), and the range is `#000000~ #ffffff` (both case). If the value is invalid, it is automatically changed to the default value. |
|BackgroundImage |String |No |`无` |The URL of the background image. The maximum length is 1024 bytes. The format of the image that can be uploaded includes: JPG, JPEG, PNG. If the width and height of the background picture are inconsistent with the width and height of the overall screen, the background picture will be adjusted to a full screen. |


<span id="region"></span>
### Region


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|StreamIndex |Integer |Yes |`0` |The identifier of the stream. This flag should correspond to `TargetStreams. StreamList. Stream.Index`. |
|LocationX |Float |No |`0` |The normalized ratio of video stream to the abscissa of the upper left corner corresponding to relative to the overall picture. The value ranges from `[0.0, 1.0)`, and the default value is `0`. If this parameter is passed, the server will verify it. If it is not valid, the server will return the error code `InvalidParameter`.<br><br>The actual coordinates of the upper left corner of the corresponding area of the video stream are obtained by multiplying the picture size and normalized scale and rounding. Suppose, `Canvas. Width = 1920, Region. LocationX = 0.33`, then the abscissa of the upper left corner of the canvas is `634`(1920\*0.33=633.6 rounded). |
|LocationY |Float |No |`0` |The normalized ratio of video stream to the ordinate of the upper left corner corresponding to relative to the overall picture , the value ranges from `[0.0,1.0)`, and the default value is `0`. If this parameter is passed, the server will verify it. If it is not valid, the server will return the error code `InvalidParameter`.<br><br>The actual coordinates of the upper left corner of the corresponding area of the video stream are obtained by multiplying the picture size and normalized scale and rounding. Suppose, `Canvas. Width = 1920, Region. LocationX = 0.33`, then the abscissa of the upper left corner of the canvas is `634`(1920\*0.33=633.6 rounded). |
|WidthProportion |Float |Yes |`0.5` |The normalized ratio of video stream to the width of the region corresponding to relative to the overall picture. The range of values is `(0.0,1.0]`. |
|HeightProportion |Float |Yes |`0.5` |The normalized ratio of video stream to the height of the region corresponding to relative to the overall picture. The range of values is `(0.0,1.0]`. |
|ZOrder |Integer |No |`0` |Use this parameter to set the layer order of the specified picture when the pictures of multiple streams overlap. The value range is `[0,100]`. `0`means that the area image is at the lowest level, and `100`means that the area image is at the top level. The default value is `0`. If the value is invalid, it is automatically changed to the default value. |
|Alpha |Float |No |`1` |The transparency of the picture. The value range is `(0.0, 1.0]`. `0.0`means completely transparent, `1.0` means completely opaque, and the default value is `1.0`. If the value is invalid, it is automatically changed to the default value. |
|RenderMode |Integer |No |`0` |The rendering mode of the stream's picture. The value ranges from `{0,1,2,3}`, and the default value is `0`:<br><br><br>* `0`: Scale directly according to the specified width and height. If the aspect ratio of the input stream is different from the specified aspect ratio, the screen will be distorted.<br><br>* `1`: Crop the video according to the aspect ratio of the display area, and then scale the video proportionally to fill the display area.<br><br>* `2`: Scale the video according to the aspect ratio of the original screen, and displaying it in the center of the display area. If the aspect ratio of the original screen is different from the specified aspect ratio, there will be gaps in the screen, which will be filled with the background color value.<br><br>* `3`: Scale directly according to the specified width and height. If the aspect ratio of the original screen is different from the specified aspect ratio, the screen will be distorted.<br><br>   When the value is invalid, it will automatically adjust to the default value.<br><br>&nbsp;<br><br>   Currently, `0` and `3` are the same mode, but it's recommended to use `3` to achieve the same logic as the client.<br><br>&nbsp;<br><br>   Under different rendering modes, the effects are as follows: <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/Rendermode.png) </span> |
|SourceCrop |Object of [SourceCrop](https://docs.byteplus.com/en/docs/12/14224#sourcecrop) |No |`\-` |The source stream clipping function. Clipping can be done before the source video frame is rendered, that is, rendering after preprocessing |
|AlternateImage |String |No |`\-` |The url of the complement picture. The length does not exceed 1024 strings.<br><br><br>1. If the video stream corresponding to the `Region. StreamIndex` is not published, or suspended, the image corresponding to `AlternateImage` will fill the canvas space corresponding to the `Region`. When the video stream is captured and published, `AlternateImage`does not cause any impact.<br><br>2. The formats that can be uploaded include: JPG, JPEG, PNG.<br><br>3. When the size of the picture and the canvas do not match, the picture will be rendered in the canvas according to the settings of RenderMode. |
|MediaType |Integer |No |`0` |Media type of the stream to be mixed.<br><br><br>* `0`: Audio and Video<br><br>* `1`: Audio<br><br>* `2`: Video<br><br>   The default value is `0`. When the value is invalid, it will automatically adjust to the default value.<br><br>   For example. If the input stream is an audio and video stream, MeidaType = `1`, only video content is mixed. |
|AlternateImageFillMode |Integer |No |`0` |Rendering mode of the placeholder image.<br><br><br>* `0`: Scale according to the ratio of the user's video frame<br><br>* `1`: Maintain the ratio of the placeholder image<br><br>   The default value is `0`. If the value is invalid, it is automatically changed to the default value. |


<span id="sourcecrop"></span>
### SourceCrop


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|LocationX |Float |No |`0` |The normalized ratio of the abscissa of the upper left corner of the video frame obtained after cutting relative to the overall picture before cutting and the value ranges from `[0.0,1.0)`. It defaults to `0.0`. If the value is invalid, it is automatically changed to the default value. |
|LocationY |Float |No |`0` |The normalized ratio of the ordinate of the upper left corner of the video frame obtained after cutting relative to the overall picture before cutting, the value ranges from `[0.0,1.0)`. It defaults to `0.0`. If the value is invalid, it is automatically changed to the default value. |
|WidthProportion |Float |No |`0.5` |The normalized ratio of video stream after cutting to the width of the region corresponding to relative to the overall picture. The value ranges from `(0.0,1.0]`. It defaults to `1.0`. If the value is invalid, it is automatically changed to the default value. |
|HeightProportion |Float |No |`0.5` |The normalized ratio of video stream after cutting to the height of the region corresponding to relative to the overall picture. The value ranged from `(0.0,1.0]`. It defaults to `1.0`. If the value is invalid, it is automatically changed to the default value. |


<span id="encode"></span>
### Encode


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|VideoWidth |Integer |No |`640` |The width of the output picture. The default value is `640`and the range is `[2,1920]`, which must be even. If the value is invalid, it is automatically changed to the default value. This parameter does not take effect when the custom layout mode turns on, and the width of the overall picture complies with `canvas.width`. |
|VideoHeight |Integer |No |`480` |The height of the output picture, and the range is `[2,1920]`, which must be even. The default value is `480`. If the value is invalid, it is automatically changed to the default value. This parameter does not take effect when the custom layout mode turns on, and the hight of the overall picture compile with `canvas.Height`. |
|VideoFps |Integer |No |`15` |Output video frame rate. The default is `15` and the range is `[1,60]`. If the value is invalid, it is automatically changed to the default value. |
|VideoBitrate |Integer |No |`-` |Output video bit rate. Value range is `[1,10000]`, in Kbps. Default value is self\-adaptation. If the value is invalid, it is automatically changed to the default value. When `VideoCodec = 1`, you must set this field. |
|VideoCodec |Integer |No |`0` |Video coding protocol. The default value is `0`. The value can be `0`or `1`. `0`means `H.264`. `1`means`byteVC1`. When `VideoCodec = 1`, you must set the `VideoBitrate`field. |
|VideoGop |Integer |No |`4` |Output video GOP. The default is `4`and the range is `[1, 5]`in seconds. If the value is invalid, it is automatically changed to the default value. |
|AudioCodec |Integer |No |`0` |Audio encoding protocol. The default value is `0`, and the aac encoding protocol is used at this time. Currently only aac is supported. |
|AudioProfile |Integer |No |`0` |Audio profile type, effective when using aac encoding. The default value is `0` and the range is `{0,1,2}`. `0` means LC ;`1` means HE\-V1 specifications;`2` means HE\-V2 specifications.When `AudioProfile`takes `2`, only dual channel is supported. If the value is invalid, it is automatically changed to the default value. |
|AudioBitrate |Integer |No |`\-` |Audio bitrate. The value range is `[32,192]`, with the unit being Kbps.<br><br><br>* If this parameter is not filled in, RTC will generate an audio bitrate value based on `AudioProfile`, `AudioSampleRate` and `AudioChannels`<br><br>* If this parameter is filled in, it will be taken as the standard under normal circumstances. However, due to different settings of `AudioProfile`, `AudioSampleRate`, and `AudioChannels`, the actual upper and lower limits of the audio bitrate will be further dynamically adjusted within the range of [32, 192], and the actual effective bitrate may differ from the entered value. |
|AudioSampleRate |Integer |No |`48000` |Audio sample rate. The default value is `48000`. The value range is `{16000, 32000, 44100, 48000}`, and the unit is Hz. If the value is invalid, it is automatically changed to the default value.<br><br>`16000` only takes effect on cloud recording. |
|AudioChannels |Integer |No |`2` |The number of audio track. The default value is `2`, and the range is `{1,2}`. `2` means dual channel. `1`means mono channel. If the value is invalid, it is automatically changed to the default value. |


<span id="control"></span>
### Control


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|MediaType |Integer |No |`0` |The type of stream that is used to globally control the subscription. `0` means audio & video, and `1` means pure audio. Pure video is not supported. The default value is `0`. For WTN, use default value only. |
|FrameInterpolationMode |Integer |No |`0` |The default value is `0`. Value can take `0`and `1`. `0` is the last frame, and `1`is the black frame. If the value is invalid, it is automatically changed to the default value. In automatic layout mode, there is no logic for adding frame.<br><br>**What is adding frame**: The frame rate of the video is usually fixed when audio & video is recorded or transcoded. However, due to network fluctuations or other reasons, the actual frame rate may not reach the preset frame rate. At this time, it is necessary to add frames to keep the video smooth. Adding the last frame means that the supplementary video frame is the same as the last frame before the interruption, and the picture seen at this time may be temporarily still. Completing black frames means that the supplementary video frames are all black.<br><br>Relationship among Placeholder image, frame Interpolation, keeping last Frame:<br><br>&nbsp;<br><br>You can set the placeholder image in the `Region` by passing the `Alternateimage` field, and set the frame interpolation mode in the `Control` by passing the `FrameInterpolationMode` field. However, the priority of the setting of placeholder image is higher than that of the frame interpolation mode.<br><br><br>* When the video stream corresponding to `Region.StreamIndex` stops publishing, the canvas corresponding to `Region` will be filled with the placeholder image or the image set in interpolation frame mode according to the setting. But when the video stream is a screen stream, the frame interpolation mode does not take effect.<br><br>* When the video stream corresponding to `Region.StreamIndex` stops capturing or pushing, the canvas corresponding to `Region` will be filled with the last frame.<br><br>* When the video stream corresponding to `Region.StreamIndex` is published, the set placeholder image or the frame set in interpolation mode has no effect. |
|MaxIdleTime |Integer |No |`180` |The idle timeout time of the task, after which the task will automatically terminate. The unit is seconds. The value range is `[10,86400]`, and the default value is `180`.<br><br><br>* If the idle time is less than set value, the task will resume and frames will be added according to the set `FrameInterpolationMode` when the task resumes.<br><br>* If the idle time exceeds set value, the task will be automatically terminated. |
|MaxRecordTime |Integer |No |`0` |(Valid for recording only) Maximum recording duration in seconds. Default is `0`. `0`means there is no limit to the recording time. |
|TalkVolume |Integer |No |`30` |(Valid for pushing to CDN only)Effective volume of user. The range is `[0,255]`, and the default value is `30`. |
|SpatialConfig |Object of [SpatialConfig](https://docs.byteplus.com/en/docs/12/14224#spatialconfig) |No | |Configuration of spatial audio. If the audio parameter of pushing to CDN is set to mono channel, this function will be invalid. |
|PushStreamMode |Integer |No |`0` |Pushshing\-stream mode of pushing to CDN, used to control the timing of triggering pushing streams to CDN. The value can take `0` or `1`.<br><br><br>* 0: The stream will be pushed to CDN when a user in the room pushes a RTC stream.<br><br>* 1: After calling the interface, a stream will be pushed to CDN regardless of whether there are a user in the room pushing a RTC stream.<br><br>   When the value is illegal, it will be automatically adjusted to the default value.<br><br>   The logic of timeout remains unchanged. |


<span id="spatialconfig"></span>
### SpatialConfig


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|EnableSpatialRender |Boolean |No |`false` |Whether to enable spatial audio.<br><br><br>* `false`: Disable<br><br>* `true`: Enable |
|AudienceSpatialPosition |Array of Integer |No |`[0,0,0]` |The Three\-dimensional coordinates of the audience's location. The default value is `[0,0,0]`. The length of the array is `3`, and the three values correspond to `X`, `Y`, and `Z` respectively. The range of each value is `[-100, 100]`. |
|AudienceSpatialOrientation |Object of [AudienceSpatialOrientation](https://docs.byteplus.com/en/docs/12/14224#audiencespatialorientation) |No |`-` |Set the orientation of the audience. The vectors are perpendicular to each other, and if the values passed do not guarantee perpendicularity to each other, the default value is automatically assigned. The default values are: `forward` = `[1, 0, 0]`, `right` = `[0, 1, 0]`, `up` = `[0, 0, 1]`. |


<span id="audiencespatialorientation"></span>
### AudienceSpatialOrientation


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Up |Array of Float |No |`[1, 0, 0]` |Upward orientation. |
|Right |Array of Float |No |`[0, -1, 0]` |Right orientation. |
|Forward |Array of Float |No |`[0, 0, 1]` |Front orientation. |


<span id="response-parameters"></span>
## Response parameters

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=UpdatePushMixedStreamToCDN&Version=2020-12-01
{
    "AppId": "You****pId",
    "BusinessId": "Your_****nessId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
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


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "UpdatePushMixedStreamToCDN",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "cn-north-1"
    }
}
```


&nbsp;
