---
title: "GetCarouselDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getcarouseldetail"
---

Call the `GetCarouselDetail` API to query the detailed information of the specified carousel task, including the playback status, video list, and current playback progress, to facilitate the management and monitoring of the task execution status.

<span id="requirements"></span>
## Requirements

Rate limit: 10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=GetCarouselDetail&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetCarouselDetail` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|TaskID |String |Yes |`44c5da50318440*********2d62c910b8` |The ID of the carousel task to be queried, which is the unique identifier of the task. It is returned when the `CreateCarouselTask` interface is called to create a carousel task. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Object of [Data](https://docs.byteplus.com/en/docs/24/47071#data) |`-` |The data object containing information related to the carousel task. |


<span id="data"></span>
### Data


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|LastOperationIndex |Integer |`1` |The latest playlist modification sequence number, each time the `UpdateCarouselTask` interface is called to update the task, this value will be incremented by `1`. |
|LastSuccessOperationIndex |Integer |`1` |The currently actually effective playlist sequence number, indicating that the task is currently playing according to the material list of this version. |
|PlayInfo |String |`{"Loop":1,"SourceID":"2","SourceLoop":1,"SourceSeek":910}` |The information of the currently playing or the last played material is returned in the form of a JSON string. This field contains the detailed information of the material, such as the material name, the playback position, etc., which is convenient for the user to obtain the specific data related to the playback. |
|Rule |String |`{"Loop":1,"Mode":1,"Output":{"Audio":{"BitRate":144000,"ChannelLayout":"stereo","SampleRate":44100},"Url":["rtmp://push-rtmp-f5.douyincdn.com/zebraedit/dev-114203018399843854?expire=1729119100&sign=a1b23eb99a26816a5db20a1ec4b314cb&volcSecret=a1b23eb99a26816a5db20a1ec4b314cb&volcTime=1729119100"],"Video":{"BitRate":8000000,"Codec":"h264","FrameRate":30,"GOP":2,"Height":1080,"Preset":"faster","Width":1920}},"PlayTime":1,"Source":[{"ID":"1","Type":"vod","Url":"https://tosv.byted.org/obj/fcdn-engine-001/test/douyin_D_90sTVC_1Mbps.mp4"},{"ID":"2","Type":"vod","Url":"https://tosv.byted.org/obj/fcdn-engine-001/test/111.mp4"}]}` |The playback rules for the carousel task, and the following are some of the key parameters:<br><br><br>* `Loop`: Whether to loop playback and the number of loop times.<br><br>* `Mode`: Playback mode (normal mode/transcoding mode).<br><br>* `Output`: Streaming parameters, including `Audio` (audio parameters), `Video` (video parameters), and `Url` (streaming address).<br><br>* `Source`: Carousel material list, including the `ID`, `Type` (such as `vod`), and `Url` (playback address) of each material. |
|Status |String |`running` |The current status of the task. The following values are supported:<br><br><br>* `pending`: The task is waiting to be scheduled;<br><br>* `prepare`: The task is being initialized;<br><br>* `running`: The task is running;<br><br>* `prestop`: The task is being stopped;<br><br>* `done`: The task has been stopped.<br><br>   This field is used to indicate the current stage in the task life cycle and is typically used for monitoring or querying the progress of task execution. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=GetCarouselDetail&Version=2023-01-01
{
    "TaskID": "44c5da50318440*********2d62c910b8"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301535298CE0D4E0152CAF10A8AC",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetCarouselDetail",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": {
            "LastOperationIndex": 1,
            "LastSuccessOperationIndex": 1,
            "PlayInfo": "{\"Loop\":1,\"SourceID\":\"2\",\"SourceLoop\":1,\"SourceSeek\":910}",
            "Rule": "{\"Loop\":1,\"Mode\":1,\"Output\":{\"Audio\":{\"BitRate\":144000,\"ChannelLayout\":\"stereo\",\"SampleRate\":44100},\"Url\":[\"rtmp://push-rtmp-f5.douyincdn.com/zebraedit/dev-114203018399843854?expire=1729119100&sign=a1b23eb99a26816a5db20a1ec4b314cb&volcSecret=a1b23eb99a26816a5db20a1ec4b314cb&volcTime=1729119100\"],\"Video\":{\"BitRate\":8000000,\"Codec\":\"h264\",\"FrameRate\":30,\"GOP\":2,\"Height\":1080,\"Preset\":\"faster\",\"Width\":1920}},\"PlayTime\":1,\"Source\":[{\"ID\":\"1\",\"Type\":\"vod\",\"Url\":\"https://tosv.byted.org/obj/fcdn-engine-001/test/douyin_D_90sTVC_1Mbps.mp4\"},{\"ID\":\"2\",\"Type\":\"vod\",\"Url\":\"https://tosv.byted.org/obj/fcdn-engine-001/test/111.mp4\"}]}",
            "Status": "running"
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/47071#request-parameters) description for inspection. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |


&nbsp;
