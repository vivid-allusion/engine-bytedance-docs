---
title: "GetCarouselDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getcarouseldetail-zh-CN"
---

调用 `GetCarouselDetail` API 查询指定轮播任务的详细信息，包括回放状态、视频列表和当前播放进度，便于管理和监控任务执行状态。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 10 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=GetCarouselDetail&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetCarouselDetail` |API 操作。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|TaskID |String |是 |`44c5da50318440*********2d62c910b8` |待查询轮播任务的 ID，即任务的唯一标识。该参数在调用 `CreateCarouselTask` 接口创建轮播任务时返回。 |


<span id="Response parameters"></span>
## 返回参数

唯一的 API 专属返回参数请参见下表。更多详情请参考 [请求与响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Data |[Data](https://docs.byteplus.com/en/docs/24/107028#data) 对象 |`-` |包含与轮播任务相关信息的数据对象。 |


<span id="data"></span>
### 数据


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|LastOperationIndex |Integer |`1` |最新播放列表修改序号，每次调用 `UpdateCarouselTask` 接口更新任务时，该值每次增加 `1`。 |
|LastSuccessOperationIndex |Integer |`1` |当前生效的播放列表序号，表示任务当前按照该版本的素材列表进行播放。 |
|PlayInfo |String |`{"Loop":1,"SourceID":"2","SourceLoop":1,"SourceSeek":910}` |当前正在播放或最后一次播放的素材信息以 JSON 字符串形式返回。该字段包含素材的详细信息，如素材名称、播放位置等，便于用户获取与回放相关的具体数据。 |
|Rule |String |`{"Loop":1,"Mode":1,"Output":{"Audio":{"BitRate":144000,"ChannelLayout":"stereo","SampleRate":44100},"Url":["rtmp://push-rtmp-f5.douyincdn.com/zebraedit/dev-114203018399843854?expire=1729119100&sign=a1b23eb99a26816a5db20a1ec4b314cb&volcSecret=a1b23eb99a26816a5db20a1ec4b314cb&volcTime=1729119100"],"Video":{"BitRate":8000000,"Codec":"h264","FrameRate":30,"GOP":2,"Height":1080,"Preset":"faster","Width":1920}},"PlayTime":1,"Source":[{"ID":"1","Type":"vod","Url":"https://tosv.byted.org/obj/fcdn-engine-001/test/douyin_D_90sTVC_1Mbps.mp4"},{"ID":"2","Type":"vod","Url":"https://tosv.byted.org/obj/fcdn-engine-001/test/111.mp4"}]}` |轮播任务的播放规则，以下为部分关键参数：<br><br><br>* `Loop`：是否循环播放及循环次数。<br><br>* `Mode`：播放模式（普通模式/转码模式）。<br><br>* `Output`：流参数，包括 `音频参数`、`视频参数` 和 `Url`（流地址）。<br><br>* `Source`：轮播素材列表，包括每个素材的 `ID`、`Type`（如 `vod`）和 `Url`（播放地址）。 |
|Status |String |`running` |当前任务状态。支持以下取值：<br><br><br>* `pending`：任务等待调度；<br><br>* `prepare`：任务初始化中；<br><br>* `running`：任务运行中；<br><br>* `prestop`：任务停止中；<br><br>* `done`：任务已停止。<br><br><br>该字段用于指示任务当前所处的生命周期阶段，通常用于监控或查询任务执行进度。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=GetCarouselDetail&Version=2023-01-01
{
    "TaskID": "44c5da50318440*********2d62c910b8"
}
```


<span id="Sample response"></span>
### 返回示例

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


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 常见错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/107028#request-parameters)说明进行检查。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
