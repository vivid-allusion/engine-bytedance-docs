---
title: "CreateCarouselTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcarouseltask"
---

Call the `CreateCarouselTask` API to create a carousel task. During the live broadcast, the video live broadcast server will play the specified video content in a loop in the set order according to the task configuration.

<span id="requirements"></span>
## Requirements

Rate limit: 10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=CreateCarouselTask&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateCarouselTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Name |String |Yes |`## Commodity Carousel` |The name of the carousel task is used to identify the task. It supports being composed of Chinese characters, uppercase and lowercase letters (A\-Z, a\-z), and numbers (0\-9).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This name cannot be repeated with the names of other running tasks.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Launched tasks are not allowed to use duplicate names.</div><br> |
|Rule |Object of [Rule](https://docs.byteplus.com/en/docs/24/47075#rule) |Yes |`-` |Carousel rules are used to specify the materials and behaviors of carousel playback. |


<span id="rule"></span>
### Rule


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Loop |Integer |Yes |`-1` |The number of carousel loops, used to control the number of times the live broadcast is looped. The supported values and their meanings are as follows:<br><br><br>* `-1`: Infinite loop;<br><br>* `0`: Do not loop;<br><br>* Other positive integers: Specify the specific number of carousel loops.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The behavior of the live broadcast loop is affected by both the <code>Loop</code> and <code>StopTime</code> fields:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the <code>Loop</code> count reaches the set value, the carousel will stop automatically, regardless of whether the <code>StopTime</code> has been reached.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the <code>StopTime</code> is reached, the carousel will also stop, even if the <code>Loop</code> has not been completed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the <code>StopTime</code> is not set, the system default maximum carousel duration is 3 days.</div><br> |
|Mode |Integer |Yes |`1` |This field is used to specify the splicing mode of carousel materials, which determines the connection method of multiple on\-demand materials during playback. The supported values are as follows:<br><br><br>* `0`: Normal mode. The audio and video parameters (such as resolution, bit rate, encoding format, etc.) of the front and back materials will be checked. If the parameters match, the materials can be seamlessly connected; if the parameters are different, a short interruption may occur during the switching.<br><br>* `1`: Transcoding mode. The system will format all on\-demand materials to make them conform to the same audio and video parameters to ensure that the materials are always smoothly and seamlessly connected during switching. The user can manually configure the target parameters. If not configured, the parameters of the first material will be used by default. |
|Output |Object of [Output](https://docs.byteplus.com/en/docs/24/47075#output) |Yes |`-` |The push stream parameters of the carousel task, including video, audio, push stream address and callback information. |
|PlayTime |Long |Yes |`1672531200000` |The start time of the carousel task, represented by a Unix timestamp with a precision of `ms`. The parameter requirements are as follows:<br><br><br>* When the value is `0`, it means to start streaming immediately;<br><br>* If a specific time is set, it must be a value later than the current time. |
|StopTime |Long |No |`1672800000000` |The stop time of the carousel task, Unix timestamp, with the precision of `ms`. After setting this field, the system will automatically close the task according to this time point. The maximum time range is `3 days`, and the default value is `3 days`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The end time <code>StopTime</code> of the carousel task must be later than the start time <code>PlayTime</code>.</div><br> |
|Source |Array of [Source](https://docs.byteplus.com/en/docs/24/47075#source) |Yes |`-` |Carousel material list, used to specify the material resources played in the carousel process. |


<span id="output"></span>
### Output


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Video |Object of [Video](https://docs.byteplus.com/en/docs/24/47075#video) |No |`-` |It takes effect in the transcoding mode (i.e., `Rule.Mode = 1`), and the video parameters of the push stream can be optionally configured. By default, all parameters (except GOP) are processed in a carousel manner according to the settings of the first material. |
|Audio |Object of [Audio](https://docs.byteplus.com/en/docs/24/47075#audio) |No |`-` |It takes effect in the transcoding mode (i.e., `Rule.Mode = 1`), and can be used to configure the audio parameters of the push stream. |
|Url |Array of String |Yes |`[ "rtmp://push.example.com/live/stream1" ]` |The RTMP or RTMPS address for streaming, supporting **multi\-push** (i.e., pushing the same live content to multiple streaming addresses simultaneously). The minimum number of addresses is 1, and a maximum of 8 addresses are supported. |
|Callback |Object of [Callback](https://docs.byteplus.com/en/docs/24/47075#callback) |No |`-` |Callback function configuration to receive notifications such as task status updates. |


<span id="source"></span>
### Source


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ID |String |Yes |`1` |The unique identifier of the carousel material. In the same playlist, the `ID` of each material must be unique and duplication is not allowed. |
|Type |String |Yes |`vod` |The file type of carousel material is used to specify the file source type of the material. The following values are supported:<br><br><br>* `vod`: On\-demand MP4 or FLV file;<br><br>* `m3u8`: On\-demand M3U8 file. |
|Url |String |Yes |`https://live.example.com/video.mp4` |The publicly accessible address of the carousel material. Ensure that the provided address can be normally accessed by the public network to correctly load the carousel material content. |
|Loop |Integer |No |`1` |Specify the number of times this material is continuously played. The value of this field must be greater than or equal to `0`, and the default value is `0`. The supported values and their meanings are as follows:<br><br><br>* `0`: Do not loop playback;<br><br>* Other positive integers: Loop playback according to the specified number of times. |
|Seek |Integer |No |`10` |Used to control skipping a period of time at the beginning when playing the current material. For example, skipping the opening credits, with the unit being seconds. This field is only valid when the material type is video on demand (`type=vod`). The following are the usage rules for this field:<br><br><br>* If the value of `Seek` is less than or equal to `0` or greater than the actual duration of the video, then this field will not take effect.<br><br>* Ensure that an appropriate value is set according to the actual length of the on\-demand material to achieve the effect of skipping the opening credits. |


<span id="video"></span>
### Video


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|BitRate |Integer |No |`15` |The bit rate of the video, with the unit of `bit`, and the value must be less than or equal to `20000`. If the `Video` object is specified, this field is required. |
|FrameRate |Integer |No |`30` |Video frame rate, with a value range of `[10, 60]`. If the `Video` object is specified, this field is required. |
|GOP |Integer |No |`5` |The maximum interval between IDR frames, in seconds. The default value is `2` and the value range is `[1,10]`. |
|Preset |String |No |`faster` |**Encoding Preset**<br><br>This parameter is used to specify the balance between encoding speed and compression rate, and supports the following options (from fastest to slowest):<br><br><br>* **`ultrafast`**: The encoding speed is the fastest, the CPU usage is the lowest, but the compression rate is the lowest and the file size is the largest. It is suitable for scenarios with extremely high real\-time requirements.<br><br>* **`superfast`**: The encoding speed is very fast and the compression rate is low, suitable for scenarios that are sensitive to latency but can accept larger file sizes.<br><br>* **`veryfast`**: The encoding speed is relatively fast and is suitable for scenarios with high real\-time requirements.<br><br>* **`faster`** (default): The encoding speed is relatively fast, with a balanced quality and compression rate, suitable for most live or short video scenarios.<br><br>* **`fast`**: The encoding speed is moderate and the compression rate is relatively high, suitable for scenarios with certain requirements for image quality and file size.<br><br>* **`medium`**: The encoding speed and compression rate are balanced, suitable for most regular video processing tasks.<br><br>* **`slow`**: The encoding speed is slower, but the compression rate is higher and the video quality is better, suitable for scenarios with high requirements for image quality, such as archiving or high\-quality on\-demand content. |
|Width |Integer |No |`1920` |The width of the video, in pixels. The supported range of values is `[10, 2160]`. If the `Video` object is specified, this field is required. |
|Height |Integer |No |`1080` |The height of the video (unit: pixel), with a value range of `[10, 2160]`. If the `Video` object is specified, this field is required. |


<span id="audio"></span>
### Audio


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|BitRate |Integer |No |`320000` |The setting range of the audio bit rate, the supported values are `[128000, 640000]`, and the unit is `bps`. If the `Audio` object is specified, this field is a required item. |
|ChannelLayout |String |No |`stereo` |The channel layout of the audio. If the `Audio` object is specified, this field is required. The following values are supported:<br><br><br>* `mono`: Mono.<br><br>* `stereo`: Stereo. |
|SampleRate |Integer |No |`48000` |The sampling rate parameter of the audio. If the `Audio` object is specified, this field is required. The supported sampling rate values include:<br><br><br>* `22000`<br><br>* `32000`<br><br>* `44100`<br><br>* `48000`<br><br>   Please select the sampling rate that suits your business needs for configuration. |


<span id="callback"></span>
### Callback


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Url |String |Yes |`https://callback.example.com/notify` |Callback address. This field needs to be accurately configured and is used to receive system callback information. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Object of [Data](https://docs.byteplus.com/en/docs/24/47075#data) |`-` |Carousel task data object. |


<span id="data"></span>
### Data


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TaskID |String |`e1fb009334fc5b16` |The unique identifier of the carousel task. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=CreateCarouselTask&Version=2023-01-01
{
    "Name": "Commodity Carousel",
    "Rule": {
        "Loop": -1,
        "Mode": 1,
        "Output": {
            "Video": {
                "BitRate": 15,
                "FrameRate": 30,
                "GOP": 5,
                "Preset": "faster",
                "Width": 1920,
                "Height": 1080
            },
            "Audio": {
                "BitRate": 320000,
                "ChannelLayout": "stereo",
                "SampleRate": 48000
            },
            "Url": [
                "rtmp://push.example.com/live/stream1"
            ],
            "Callback": {
                "Url": "https://callback.example.com/notify"
            }
        },
        "PlayTime": 1672531200000,
        "Source": [
            {
                "ID": "1",
                "Type": "vod",
                "Url": "https://live.example.com/video.mp4",
                "Loop": 1,
                "Seek": 10
            }
        ],
        "StopTime": 1672800000000
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301432037DE157BFBC968410056C",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateCarouselTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": {
            "TaskID": "e1fb009334fc5b16"
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](#Request Parameters) description for inspection. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please contact [Technical Support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980&_vtm_=a78999.b69280.0_0.0_0.0.1752_7654053815712695861). |


&nbsp;
