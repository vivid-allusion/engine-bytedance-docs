---
title: "UpdatePublicStreamParam"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-113681"
---

Call the `UpdatePublicStreamParam` interface to update the parameters of a published WTN stream, such as adjusting the mixing layout, included media streams, and encoding parameters.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=UpdatePublicStreamParam&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdatePublicStreamParam` |Interface name. The value of this interface: `UpdatePublicStreamParam` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|BusinessId |String |No |`Your_****nessId` |The business identifier for your audio & video app |
|PublicStreamId |String |Yes |`Your_PublicStreamId` |The ID of public streams. |
|TranscodeMode |Integer |No |`0` |The processing mode of public streams.<br><br><br>* `0`：Transcoding.<br><br>* `1`：Packaging. When `TranscodeMode`=`1`,<br><br>   * `TargetStreams` can only specify one stream, and the `UserId` of this stream cannot be empty and should be the `UserId` of the corresponding room user.<br><br>   * `ExcludeStreams` must be empty.<br><br>   * The setting of the `Encode.VideoConfig` does not take effect.<br><br>   * The setting of `Layout` does not take effect. |
|TargetStreams |Array of [PublicStream](https://docs.byteplus.com/en/docs/12/14230#publicstream) |Yes |`-` |Specify single or multiple media streams and corresponding parameters for the public stream. It's a Stream array and supports up to 17 streams. |
|ExcludeStreams |Array of [PublicStream](https://docs.byteplus.com/en/docs/12/14230#publicstream) |No |`-` |You can use this parameter to exclude **unnecessary** audio & video streams in the public stream. It is equal to a blacklist. The default parameter is empty. The streams in the blacklist should not exceed 17. The `stream` in this parameter should not be the same with that in `TargetStreams`. |
|Layout |Object of [PublicLayout](https://docs.byteplus.com/en/docs/12/14230#publiclayout) |No |`-` |The layout parameters when multiple media streams merge into one public stream. |
|Encode |Object of [PublicEncode](https://docs.byteplus.com/en/docs/12/14230#publicencode) |No |`-` |Media encoding parameters |
|Control |Object of [PublicControl](https://docs.byteplus.com/en/docs/12/14230#publiccontrol) |No |`-` |Control options. |


<span id="publicstream"></span>
### PublicStream


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|MediaType |Integer |No | |The meida type of streams. The default value is `0`.<br><br><br>* `0`: Audio and Video<br><br>* `1`: Pure Audio<br><br>* `2`: Pure Video |
|StreamType |Integer |No |`0` |The type of stream, the value can take `0` or `1`, and the default value is `0`.<br><br><br>* `0`: audio and video stream<br><br>* `1`: screen stream. |
|Index |Integer |No |`1` |The parameter is required when choosing the custom layout mode.<br><br>It marks different media streams in the same public stream.<br><br>In the same `TargetStreams`, `Stream.Index` is unique. |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room in which user publishing the public stream. |
|UserId |String |No |`Your_UserId` |The user ID of the publisher of the media stream. When UserId is empty, it means subscribing to all streams in the room. UserId must be unique and should not be the same across rooms. |


<span id="publiclayout"></span>
### PublicLayout


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|LayoutMode |Integer |Yes |`0` |Layout mode. The default value is `0`, and the value ranges from `{0, 1, 2, 3}` .<br><br><br>* `0`: Self\-adaptation layout mode.<br><br>* `1`: Vertical layout mode (this mode does not support the screen stream).<br><br>* `2`: Custom layout mode.<br><br>* `3`: Side\-by\-side layout mode.<br><br>   See details in [Mixed-stream Layout Mode](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69818#jFHMzAHT). |
|VerticalLayout |Object of [VerticalLayout](https://docs.byteplus.com/en/docs/12/14230#verticallayout) |No | |Parameters for vertical layout. |
|CustomLayout |Object of [PublicCustomLayout](https://docs.byteplus.com/en/docs/12/14230#publiccustomlayout) |No | |Parameters for custom layout. |


<span id="verticallayout"></span>
### VerticalLayout


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|MainStream |Object of [PublicStream](https://docs.byteplus.com/en/docs/12/14230#publicstream) |No | |Specify the stream and related information to be displayed in the large window.<br><br><br>1. If a user's audio and video are specified in the `TargetStreams` parameter of [StartPushPublicStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-113680), but only the user's audio is specified in `MainStream`, the public stream only contains the user's audio, and the area of the large window is left blank.<br><br>2. If a user's video is specified in the `TargetStreams` parameter of [StartPushPublicStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-113680), but only their audio is specified in `MainStream`, the public stream will exclude both audio and video for that user, leaving the large window area blank.<br><br>3. If the user specified in `MainStream` does not exist, the large window area will remain blank. |


<span id="publiccustomlayout"></span>
### PublicCustomLayout


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Regions |Array of [PublicCustomRegion](https://docs.byteplus.com/en/docs/12/14230#publiccustomregion) |Yes | |In custom layout, configuration for multiple video streams |
|FrameInterpolationMode |Integer |No |`0` |Select frame interpolation mode. Default value is `0`.<br><br><br>* `0` ：Fill in the last frame<br><br>* `1` ：Fill in black frame.<br><br>   There is no frame interpolation in automatic layout mode.<br><br>   **Add frame**: The frame rate of the video is usually fixed when audio & video is recorded or transcoded. However, due to network fluctuations or other reasons, the actual frame rate may not reach the preset frame rate. At this time, it is necessary to add frames to keep the video smooth. Adding the last frame means that the supplementary video frame is the same as the last frame before the interruption, and the picture seen at this time may be temporarily still. Completing black frames means that the supplementary video frames are all black.<br><br>   Relationship among Placeholder image, frame Interpolation, keeping last Frame:<br><br>   You can set the placeholder image in the `Region` by passing the `Alternateimage` field, and set the frame interpolation mode in the `Control` by passing the `FrameInterpolationMode` field. However, the priority of the setting of placeholder image is higher than that of the frame interpolation mode.<br><br>* When the video stream corresponding to `Region.StreamIndex` stops publishing, the canvas corresponding to `Region` will be filled with the placeholder image or the image set in interpolation frame mode according to the setting. But when the video stream is a screen stream, the frame interpolation mode does not take effect.<br><br>* When the video stream corresponding to `Region.StreamIndex` stops capturing or pushing, the canvas corresponding to `Region` will be filled with the last frame.<br><br>* When the video stream corresponding to `Region.StreamIndex` is published, the set placeholder image or the frame set in interpolation mode has no effect. |
|BackgroundColor |String |No |`#000000` |The background color of the entire screen (canvas), in the format of #RGB (hexadecimal), default value is `#000000` (black), range is `#000000 ~ #ffffff` (case insensitive). When the value is invalid, it is automatically adjusted to the default value. If you set a background image, the background image will cover the background color. |
|BackgroundImage |String |No |`http://xxxx.svg` |The URL of the background image. The maximum length is 1024 bytes. The image formats that can be sent include: `JPG`, `JPEG`, `PNG`. If the width and height of the background image are inconsistent with the width and height of the entire screen, the background image will be scaled to fill the screen. If you set a background image, the background image will cover the background color. |


<span id="publiccustomregion"></span>
### PublicCustomRegion


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|StreamIndex |Integer |Yes |`1` |Stream identifier, used to specify which stream the layout settings will be applied to. |
|LocationX |Float |No |`0` |The horizontal coordinate of the upper left corner of the area corresponding to the video stream relative to the whole picture, the value range is [0.0, 1.0). |
|LocationY |Float |No |`0` |The vertical coordinate of the upper left corner of the area corresponding to the video stream relative to the whole picture, the value range is [0.0, 1.0). |
|WidthProportion |Float |Yes |`0.5` |The width of the area corresponding to the video stream relative to the whole picture, the value range is (0.0, 1.0]. |
|HeightProportion |Float |Yes |`0.5` |The height of the area corresponding to the video stream relative to the whole picture, the value range is (0.0, 1.0]. |
|ZOrder |Integer |No | |When the picture overlaps, use this parameter to set the layer order of the specified picture, the value range is [0, 100]: 0 means that the image of this area is at the bottom layer, 100 means that the image of this area is at the top layer, the default value is 0. |
|Alpha |Float |No |`1.0` |The transparency of the picture, the value range is (0.0, 1.0]. `0.0` means completely transparent, `1.0` means completely opaque, the default value is `1.0`. |
|RenderMode |Integer |No |`0` |The rendering mode of the picture, the value range is `{0, 1, 2, 3}`, the default value is 0：<br><br><br>* `0` means to scale directly according to the specified width and height. If the aspect ratio of the original picture is different from the specified aspect ratio, it will cause the picture to deform<br><br>* `1` means to crop the video according to the aspect ratio of the display area, and then stretch or shrink the video proportionally to fill the display area.<br><br>* `2` means to scale the video according to the aspect ratio of the original picture and display it in the center of the display area. If the aspect ratio of the original picture is different from the specified aspect ratio, there will be a gap in the picture filled with background color. When the value is illegal, it is automatically adjusted to the default value.<br><br>* `3` means to scale directly according to the specified width and height. If the aspect ratio of the original picture is different from the specified aspect ratio, it will cause the picture to deform.<br><br>   Currently `0` and `3` are both scaled directly according to the specified width and height, but we recommend you to use `3` to align with the client\-side. |
|AlternateImage |String |No |`https://xx.com/img/1.png` |The url of the placeholder image |
|SourceCrop |Object of [SourceCrop](https://docs.byteplus.com/en/docs/12/14230#sourcecrop) |No |`-` |Source stream cropping function. Under the public stream function, `SourceCrop` does not take effect on `AlternateImage`. |


<span id="sourcecrop"></span>
### SourceCrop


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|LocationX |Float |No |`0` |The normalized ratio of the abscissa of the upper left corner of the video frame obtained after cutting relative to the overall picture before cutting and the value ranges from `[0.0,1.0)`. It defaults to `0.0`. If the value is invalid, it is automatically changed to the default value. |
|LocationY |Float |No |`0` |The normalized ratio of the ordinate of the upper left corner of the video frame obtained after cutting relative to the overall picture before cutting, the value ranges from `[0.0,1.0)`. It defaults to `0.0`. If the value is invalid, it is automatically changed to the default value. |
|WidthProportion |Float |No |`0.5` |The normalized ratio of video stream after cutting to the width of the region corresponding to relative to the overall picture. The value ranges from `(0.0,1.0]`. It defaults to `1.0`. If the value is invalid, it is automatically changed to the default value. |
|HeightProportion |Float |No |`0.5` |The normalized ratio of video stream after cutting to the height of the region corresponding to relative to the overall picture. The value ranged from `(0.0,1.0]`. It defaults to `1.0`. If the value is invalid, it is automatically changed to the default value. |


<span id="publicencode"></span>
### PublicEncode


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|VideoConfig |Object of [VideoConfig](https://docs.byteplus.com/en/docs/12/14230#videoconfig) |No |`-` |Video encoding configuration |


<span id="videoconfig"></span>
### VideoConfig


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Width |Integer |No |`640` |The width of the output picture. The default value is 640, the range is [16, 1920], must be an even number. |
|Height |Integer |No |`480` |The height of the output picture, the default value is 480. The range is [16, 1920], must be an even number. |
|FrameRate |Integer |No |`15` |The frame rate of the output video. The default is `15`. The range is [1,60], in fps. |
|Bitrate |Integer |No |`256` |The highest output video bitrate. The range is [0,10000], in Kbps, the default value is `0`, which means adaptive bitrate. |
|VideoCodec |Integer |No |`0` |Video encoding protocol. The enumeration values are `{0, 5}`, the default value is `0`.<br><br><br>* `0`: `H.264`<br><br>* `5`: `VP8`. If you choose the `VP8` format, please contact BytePlus technical support. |


<span id="publiccontrol"></span>
### PublicControl


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DataMsg |String |No |`-` |Custom information inserted into the public stream, which can be used for stream information synchronization, with a length not exceeding 4 kB.<br><br>The data will be added to the 30 video frames following the current video frame. Only valid when calling `UpdatePublicStreamParam`. |
|MaxIdleTime |Integer |No |`180` |The idle timeout of the task, after which the task automatically terminates. The unit is seconds. The range is [10, 86400], the default value is `180`. Only valid when calling `StartPushPublicStream`. |
|VolumeIndicationMode |Boolean |No |`false` |Whether to enable the volume indication mode.<br><br><br>* `true`: Enable volume indication.<br><br>* `false`: Do not enable volume indication.<br><br>   The default value is `false`. |
|VolumeIndicationInterval |Integer |No |`2000` |The callback interval of volume indication, in milliseconds, the minimum value is `100`, the default value is `2000`. If the value is invalid, it will automatically adjust to the default value. When `VideoConfig.FrameRate` is greater than 10 fps, the callback interval can reach 100ms. |
|UserCaptureStatsMode |Boolean |No |`false` |Whether to enable the callback of room user capture status. After enabling, it will be called back through `onPublicStreamDataMessageReceived`.<br><br><br>* `true`: Enable room user capture status callback.<br><br>* `false`: Do not enable room user capture status callback.<br><br>   The default value is `false`. |
|UserCaptureStatsInterval |Integer |No |`2000` |The callback interval of room user capture status, only triggered in pure audio. The unit is milliseconds, the default value is `2000`, the range is `[1000,2147483647]`. If the value is invalid, it will automatically adjust to the default value. |
|StreamPublishStatsMode |Boolean |No |`false` |Whether to enable the callback of room user publish status, only triggered in pure audio. After enabling, it will be called back through `onPublicStreamDataMessageReceived`.<br><br><br>* `true`: Enable room user publish status callback.<br><br>* `false`: Do not enable room user publish status callback.<br><br>   The default value is false. |
|StreamPublishStatsInterval |Integer |No |`2000` |The callback interval of room user publish status, only triggered in pure audio. The unit is milliseconds, the default value is `2000`, the range is `[1000,2147483647]`. If the value is invalid, it will automatically adjust to the default value. |


<span id="response-parameters"></span>
## Response parameters

The return value `Result` only returns "ok" when the request is successful, and returns an error code and related information when failed.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=UpdatePublicStreamParam&Version=2020-12-01
{
    "AppId": "You****pId",
    "BusinessId": "Your_****nessId",
    "TranscodeMode": 0,
    "TargetStreams": [
        {
            "Index": 0,
            "UserId": "Your_UserId_3",
            "RoomId": "Your_RoomId",
            "StreamType": 1,
            "MediaType": 0
        },
        {
            "Index": 1,
            "UserId": "Your_UserId_3",
            "RoomId": "Your_RoomId",
            "StreamType": 1,
            "MediaType": 0
        }
    ],
    "Encode": {
        "VideoConfig": {
            "Width": 640,
            "Height": 480,
            "FrameRate": 15,
            "Bitrate": 256
        }
    },
    "Layout": {
        "LayoutMode": 2,
        "CustomLayout": {
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
                    "RenderMode": 1,
                    "AlternateImage": "https://xx.com/img/1.jpg",
                    "SourceCrop": {
                        "LocationX": 500,
                        "LocationY": 0,
                        "WidthProportion": 0.5,
                        "HeightProportion": 0.5
                    }
                }
            ],
            "FrameInterpolationMode": 0,
            "BackgroundColor": "#000000",
            "BackgroundImage": "https://xx.com/img/1.jpg"
        }
    },
    "Control": {
        "DataMsg": "CamInfo"
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
        "Action": "UpdatePublicStreamParam",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
