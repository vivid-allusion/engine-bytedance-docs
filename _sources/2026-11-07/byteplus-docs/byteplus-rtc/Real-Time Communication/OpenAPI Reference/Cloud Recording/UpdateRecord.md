---
title: "UpdateRecord"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-116406"
---

After you enable Cloud Recording and make a custom layout in mixing\-stream recording mode, you can update configuration parameters relevant to recording. You can use the `UpdateRecord` OpenAPI to do this.

For information on how to enable cloud recording, see [StartRecord](https://docs.byteplus.com/en/docs/12/docs-115526).

<span id="usage-scenario"></span>
## Usage scenario

You can call the `UpdateRecord` to override the following parameters previously set in `StartRecord` or `UpdateRecord`:


* `TargetStreams`

* `Layout.CustomLayout.Canvas.Background` and `Layout.CustomLayout.Canvas.BackgroundImage`

* `Layout.CustomLayout.Regions`


<span id="requirements"></span>
## Requirements

You must have enabled cloud recording and use mixing\-stream mode. About starting cloud recording, see [StartRecord](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-115526) .

Only `RecordMode = 0`and `Layout. LayoutMode = 2` when you call `StartRecord`, this interface can only be called, that is, task parameters can only be updated in the custom layout mode of mixing\-stream recording.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=UpdateRecord&Version=2022\-06\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateRecord` |Interface name. The value of this interface: `UpdateRecord` |
|Version |String |Yes |`2022-06-01` |OpenAPI version. The value of this interface: `2022-06-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`661e****543cf` |The only identifier for your audio & video app. |
|BusinessId |String |No |`Your_****nessId` |The Business identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room |
|TaskId |String |Yes |`Your_TaskId` |Task ID. |
|TargetStreams |Object of [Streams](https://docs.byteplus.com/en/docs/12/14218#streams) |No |`-` |You can use this parameter to set the audio & video stream to be recorded. When this value is null, all streams in the room will be recorded. The maximum number of people recorded is 17, whether it is mixing stream or a single stream recording. |
|Layout |Object of [Layout](https://docs.byteplus.com/en/docs/12/14218#layout) |No |`-` |Layout parameters. |


<span id="streams"></span>
### Streams


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|StreamList |Array of [Stream](https://docs.byteplus.com/en/docs/12/14218#stream) |No |`-` |A list of `Streams`. It can be empty. When empty, it means subscribing to all streams in the room. In a `StreamList`, `Stream. Index`cannot be duplicated. |


<span id="stream"></span>
### Stream


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Index |Integer |No |`0` |In custom layout, use `Index` to flag the stream. Later in the `Layout.regions.StreamIndex`, you need to use `Index` to specify the layout settings for the corresponding stream. |
|UserId |String |Yes |`Your_UserId` |UserId which represents the user a stream belongs to. |
|StreamType |Integer |No |`0` |The type of stream. The value can be `0` or `1`, and the default value is `0`. `0`means normal audio & video stream, `1` means screen stream. You don't need to specify `StreamType` for WTN. |


<span id="layout"></span>
### Layout


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|LayoutMode |Integer |No |`0` |Layout mode. The default value is `0`, and the value ranges from `{0, 1, 2, 3}` .<br><br><br>* `0`: Self\-adaptation layout mode.<br><br>* `1`: Vertical layout mode (this mode does not support the screen stream).<br><br>* `2`: Custom layout mode.<br><br>* `3`: Side\-by\-side layout mode.<br><br>   See details in [Mixed-stream Layout Mode](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69818#jFHMzAHT). |
|CustomLayout |Object of [CustomLayout](https://docs.byteplus.com/en/docs/12/14218#customlayout) |No |`-` |Use this parameter for specific settings when using custom layout mode. |
|MainVideoStream |Object of [Stream](https://docs.byteplus.com/en/docs/12/14218#stream) |No |`-` |Effective and required in vertical layout mode (when `LayoutMode` is set to 1), this setting dictates the attributes of the main video stream. |


<span id="customlayout"></span>
### CustomLayout


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Canvas |Object of [Canvas](https://docs.byteplus.com/en/docs/12/14218#canvas) |No |`-` |The width and height of the overall screen (canvas) and the background color. |
|Regions |Array of [Region](https://docs.byteplus.com/en/docs/12/14218#region) |No |`-` |In Custom Layout mode, you can use `Regions` to set the picture layout for each video stream. Wherein each `Region` match corresponding video stream. |


<span id="canvas"></span>
### Canvas


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Width |Integer |No |`640` |The width of the overall screen (canvas), in px, in the range `[2, 4096]`(must be even). The default value is `640` .If the value is invalid, it is automatically changed to the default value. |
|Height |Integer |No |`480` |The overall screen (canvas) height, in px, in the range `[2, 2160]`(must be even). The default value is `480`. If the value is invalid, it is automatically changed to the default value. |
|Background |String |No |`#000000` |The background color of the overall screen (canvas) in the format #RGB (hexadecimal). The default value is `#000000`(black), and the range is `#000000~ #ffffff`(both case). If the value is invalid, it is automatically changed to the default value. |
|BackgroundImage |String |No |`\-` |The URL of the background image. The maximum length is 1024 bytes. The format of the image that can be uploaded includes: JPG, JPEG, PNG. If the width and height of the background picture are inconsistent with the width and height of the overall screen, the background picture will be adjusted to a full screen. |


<span id="region"></span>
### Region


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|StreamIndex |Integer |Yes |`0` |The identifier of the stream. This flag should correspond to `TargetStreams. StreamList. Stream.Index`. |
|LocationX |Float |No |`0` |The normalized ratio of video stream to the abscissa of the upper left corner corresponding to relative to the overall picture. The value ranges from `[0.0, 1.0)`, and the default value is `0.0`. If this parameter is passed, the server will verify it.<br><br>The actual coordinates of the upper left corner of the corresponding area of the video stream are obtained by multiplying the picture size and normalized scale and rounding. Suppose, `Canvas. Width = 1920, Region. LocationX = 0.33`, then the abscissa of the upper left corner of the canvas is `634`(1920\*0.33=633.6 rounded). |
|LocationY |Float |No |`0` |The normalized ratio of video stream to the ordinate of the upper left corner corresponding to relative to the overall picture , the value ranges from `[0.0,1.0)`, and the default value is `0.0`. If this parameter is passed, the server will verify it. |
|WidthProportion |Float |Yes |`0.5` |The normalized ratio of video stream to the width of the region corresponding to relative to the overall picture. The range of values is `(0.0,1.0]`. |
|HeightProportion |Float |Yes |`0.5` |The normalized ratio of video stream to the height of the region corresponding to relative to the overall picture. The range of values is `(0.0,1.0]`. |
|ZOrder |Integer |No |`0` |Use this parameter to set the layer order of the specified picture when the pictures of multiple streams overlap. The value range is `[0,100]`. `0`means that the area image is at the lowest level, and `100`means that the area image is at the top level. The default value is `0`. If the value is invalid, it is automatically changed to the default value. |
|Alpha |Float |No |`1` |The transparency of the picture. The value range is `(0.0, 1.0]`. `0.0`means completely transparent, `1.0` means completely opaque, and the default value is `1.0`. If the value is invalid, it is automatically changed to the default value. |
|RenderMode |Integer |No |`0` |The rendering mode of the stream's picture. The value ranges from `{0,1,2,3}`, and the default value is `0`:<br><br><br>* `0`: Scale directly according to the specified width and height. If the aspect ratio of the input stream is different from the specified aspect ratio, the screen will be distorted.<br><br>* `1`: Crop the video according to the aspect ratio of the display area, and then scale the video proportionally to fill the display area.<br><br>* `2`: Scale the video according to the aspect ratio of the original screen, and displaying it in the center of the display area. If the aspect ratio of the original screen is different from the specified aspect ratio, there will be gaps in the screen, which will be filled with the background color value.<br><br>* `3`: Scale directly according to the specified width and height. If the aspect ratio of the original screen is different from the specified aspect ratio, the screen will be distorted.<br><br>   When the value is invalid, it will automatically adjust to the default value.<br><br>   Currently, `0` and `3` are the same mode, but it's recommended to use `3` to achieve the same logic as the client.<br><br>   Under different rendering modes, the effects are as follows: <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/Rendermode.png) </span> |
|SourceCrop |Object of [SourceCrop](https://docs.byteplus.com/en/docs/12/14218#sourcecrop) |No |`\-` |The source stream clipping function. Clipping can be done before the source video frame is rendered, that is, rendering after preprocessing. |
|AlternateImage |String |No |`\-` |The url of the complement picture. The length does not exceed 1024 strings.<br><br><br>* If the video stream corresponding to the `Region. StreamIndex` is not published, or suspended, the image corresponding to `AlternateImage`will fill the canvas space corresponding to the `Region`. When the video stream is captured and published, `AlternateImage`does not cause any impact.<br><br>* The formats that can be uploaded include: JPG, JPEG, PNG.<br><br>* When the size of the picture and the canvas do not match, the picture will be rendered in the canvas according to the settings of RenderMode. |
|MediaType |Integer |No |`0` |Media type of the stream to be mixed.<br><br><br>* `0`: Audio and Video<br><br>* `1`: Audio<br><br>* `2`: Video<br><br>   The default value is `0`. When the value is invalid, it will automatically adjust to the default value.<br><br>   For example. If the input stream is an audio and video stream, MeidaType = `1`, only video content is mixed. |
|AlternateImageFillMode |Integer |No |`0` |Rendering mode of the placeholder image.<br><br><br>* `0`: Scale according to the ratio of the user's video frame.<br><br>* `1`: Maintain the ratio of the placeholder image.<br><br>   The default value is `0`. If the value is invalid, it is automatically changed to the default value. |


<span id="sourcecrop"></span>
### SourceCrop


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|LocationX |Float |No |`0` |The normalized ratio of the abscissa of the upper left corner of the video frame obtained after cutting relative to the overall picture before cutting and the value ranges from `[0.0,1.0)`. It defaults to `0.0`. If the value is invalid, it is automatically changed to the default value. |
|LocationY |Float |No |`0` |The normalized ratio of the ordinate of the upper left corner of the video frame obtained after cutting relative to the overall picture before cutting, the value ranges from `[0.0,1.0)`. It defaults to `0.0`. If the value is invalid, it is automatically changed to the default value. |
|WidthProportion |Float |No |`0.5` |The normalized ratio of video stream after cutting to the width of the region corresponding to relative to the overall picture. The value ranges from `(0.0,1.0]`. It defaults to `1.0`. If the value is invalid, it is automatically changed to the default value. |
|HeightProportion |Float |No |`0.5` |The normalized ratio of video stream after cutting to the height of the region corresponding to relative to the overall picture. The value ranged from `(0.0,1.0]`. It defaults to `1.0`. If the value is invalid, it is automatically changed to the default value. |


<span id="response-parameters"></span>
## Response parameters

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=UpdateRecord&Version=2022-06-01
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "UpdateRecord",
        "Version": "2022-06-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
