---
title: "CreateCarouselTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcarouseltask-zh-CN"
---

调用 `CreateCarouselTask` API 创建轮播任务。在直播过程中，视频直播服务器会根据任务配置，按照设定顺序循环播放指定的视频内容。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多 10 次查询。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=CreateCarouselTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`CreateCarouselTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Name |String |是 |`## 商品轮播` |轮播任务名称用于标识该任务。支持由中文字符、大小写字母（A\-Z，a\-z）和数字（0\-9）组成。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该名称不能与其他正在运行的任务名称重复。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">已启动的任务不允许使用重复名称。</div><br> |
|规则 |[规则](https://docs.byteplus.com/en/docs/24/106974#rule)对象 |是 |`-` |轮播规则用于指定轮播回放的素材及行为。 |


<span id="rule"></span>
### 规则


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Loop |Integer |是 |`-1` |轮播循环播放次数，用于控制直播循环播放的次数。支持的取值及含义如下：<br><br><br>* `-1`：无限循环播放；<br><br>* `0`：不循环播放；<br><br>* 其他正整数：指定轮播循环播放的具体次数。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">直播循环播放行为同时受 <code>Loop</code> 和 <code>StopTime</code> 字段影响：</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当 <code>Loop</code> 次数达到设定值时，无论是否到达 <code>StopTime</code>，轮播将自动停止。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当到达 <code>StopTime</code> 时，即使 <code>Loop</code> 未完成，轮播也会停止。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若未设置 <code>StopTime</code>，系统默认最大轮播时长为 3 天。</div><br> |
|Mode |Integer |是 |`1` |该字段用于指定轮播素材的拼接模式，决定回放时多个点播素材的连接方式。支持的取值如下：<br><br><br>* `0`：普通模式。前后素材的音视频参数（如分辨率、码率、编码格式等）会进行校验。参数一致时可无缝连接，参数不同则切换时可能出现短暂中断。<br><br>* `1`：转码模式。系统会统一格式化所有点播素材，使其符合相同音视频参数，确保切换时素材始终平滑无缝连接。用户可手动配置目标参数。如未配置，则默认采用第一个素材的参数。 |
|输出 |[Output](https://docs.byteplus.com/en/docs/24/106974#output)对象 |是 |`-` |轮播任务的推流参数，包括视频、音频、推流地址和回调信息。 |
|播放时间 |Long |是 |`1672531200000` |轮播任务的开始时间，以Unix时间戳表示，精度为`ms`。参数要求如下：<br><br><br>* 当值为`0`时，表示立即开始推流；<br><br>* 如设置具体时间，必须为当前时间之后的值。 |
|StopTime |Long |否 |`1672800000000` |轮播任务的结束时间，Unix时间戳，精度为`ms`。设置该字段后，系统会根据该时间点自动关闭任务。最大时间范围为`3天`，默认值为`3天`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">轮播任务的结束时间<code>StopTime</code>必须晚于开始时间<code>PlayTime</code>。</div><br> |
|Source |[Source](https://docs.byteplus.com/en/docs/24/106974#source)数组 |是 |`-` |轮播素材列表，用于指定轮播过程中播放的素材资源。 |


<span id="output"></span>
### 输出


|**参数** |**数据类型** |**必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Video |[Video](https://docs.byteplus.com/en/docs/24/106974#video)对象 |否 |`-` |在转码模式下（即`Rule.Mode = 1`），可选配置推流的视频参数。默认情况下，除GOP外，所有参数均按第一个素材的设置以轮播方式处理。 |
|Audio |[Audio](https://docs.byteplus.com/en/docs/24/106974#audio)对象 |否 |`-` |在转码模式下（即`Rule.Mode = 1`），可用于配置推流的音频参数。 |
|Url |字符串数组 |是 |`[ "rtmp://push.example.com/live/stream1" ]` |用于推流的RTMP或RTMPS地址，支持**multi\-push**（即同一直播内容同时推送到多个推流地址）。地址最少为1个，最多支持8个。 |
|Callback |[Callback](https://docs.byteplus.com/en/docs/24/106974#callback)对象 |否 |`-` |回调函数配置，用于接收任务状态更新等通知。 |


<span id="source"></span>
### Source


|**参数** |**数据类型** |**必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ID |字符串 |是 |`1` |轮播素材的唯一标识。同一播放列表中，每个素材的`ID`必须唯一，不允许重复。 |
|Type |字符串 |是 |`vod` |轮播素材的文件类型，用于指定素材的文件来源类型。支持以下取值：<br><br><br>* `vod`：点播MP4或FLV文件；<br><br>* `m3u8`：点播M3U8文件。 |
|Url |字符串 |是 |`https://live.example.com/video.mp4` |轮播素材的公网可访问地址。请确保所提供地址可被公网正常访问，以正确加载轮播素材内容。 |
|Loop |整数 |否 |`1` |指定该素材连续播放的次数。该字段取值必须大于等于`0`，默认值为`0`。支持的取值及含义如下：<br><br><br>* `0`：不循环播放；<br><br>* 其他正整数：按指定次数循环播放。 |
|Seek |整数 |否 |`10` |用于控制播放当前素材时跳过开头的一段时间。例如跳过片头，单位为秒。仅当素材类型为点播视频（`type=vod`）时，此字段有效。以下是此字段的使用规则：<br><br><br>* 若`Seek`的值小于或等于`0`，或大于视频实际时长，则此字段不生效。<br><br>* 请根据点播素材的实际长度设置合适的值，以实现跳过片头的效果。 |


<span id="video"></span>
### Video


|**参数** |**数据类型** |**必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|BitRate |整数 |否 |`15` |视频的码率，单位为`bit`，且数值需小于或等于`20000`。若指定`Video`对象，则此字段为必填项。 |
|FrameRate |整数 |否 |`30` |视频帧率，取值范围为`[10, 60]`。若指定`Video`对象，则此字段为必填项。 |
|GOP |整数 |否 |`5` |IDR帧的最大间隔，单位为秒。默认值为`2`，取值范围为`[1,10]`。 |
|Preset |字符串 |否 |`faster` |**编码预设**<br><br>此参数用于指定编码速度与压缩率的平衡，支持以下选项（从最快到最慢）：<br><br><br>* **`ultrafast`**：编码速度最快，CPU占用最低，但压缩率最低，文件体积最大。适用于极高实时性要求的场景。<br><br>* **`superfast`**：编码速度非常快，压缩率较低，适用于对延迟敏感但可接受较大文件体积的场景。<br><br>* **`veryfast`**：编码速度较快，适用于高实时性需求的场景。<br><br>* **`faster`**（默认）：编码速度较快，质量与压缩率均衡，适用于大多数直播或短视频场景。<br><br>* **`fast`**：编码速度适中，压缩率较高，适用于对画质和文件体积有一定要求的场景。<br><br>* **`medium`**：编码速度与压缩率均衡，适用于大多数常规视频处理任务。<br><br>* **`slow`**：编码速度较慢，但压缩率更高，视频质量更好，适用于对画质要求较高的场景，如归档或高质量点播内容。 |
|Width |整数 |否 |`1920` |视频宽度，单位为像素。支持的取值范围为`[10, 2160]`。若指定`Video`对象，则此字段为必填项。 |
|Height |整数 |否 |`1080` |视频高度（单位：像素），取值范围为`[10, 2160]`。若指定`Video`对象，则此字段为必填项。 |


<span id="audio"></span>
### Audio


|**参数** |**数据类型** |**必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|BitRate |整数 |否 |`320000` |音频码率的设置范围，支持的取值为`[128000, 640000]`，单位为`bps`。若指定`Audio`对象，则此字段为必填项。 |
|ChannelLayout |字符串 |否 |`立体声` |音频的声道布局。若指定`Audio`对象，则此字段为必填项。支持以下取值：<br><br><br>* `mono`：单声道。<br><br>* `立体声`：立体声。 |
|采样率 |整数 |否 |`48000` |音频的采样率参数。如果指定了`Audio`对象，则该字段为必填项。支持的采样率值包括：<br><br><br>* `22000`<br><br>* `32000`<br><br>* `44100`<br><br>* `48000`<br><br><br>请根据您的业务需求选择合适的采样率进行配置。 |


<span id="callback"></span>
### Callback


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Url |字符串 |是 |`https://callback.example.com/notify` |回调地址。该字段需准确配置，用于接收系统回调信息。 |


<span id="Response parameters"></span>
## 返回参数

有关唯一的 API 专属返回参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Data |[Data](https://docs.byteplus.com/en/docs/24/106974#data)对象 |`-` |轮播任务数据对象。 |


<span id="data"></span>
### 数据


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TaskID |字符串 |`e1fb009334fc5b16` |轮播任务的唯一标识符。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

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


<span id="Sample response"></span>
### 返回示例

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


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](#Request Parameters)说明进行检查。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请联系[技术支持](https://console.volcengine.com/workorder/create?step=2&SubProductID=P00000076)。 |
