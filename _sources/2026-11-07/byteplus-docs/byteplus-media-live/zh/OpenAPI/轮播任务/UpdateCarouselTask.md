---
title: "UpdateCarouselTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecarouseltask-zh-CN"
---

调用 `UpdateCarouselTask` API 修改指定轮播任务的配置，调整回放内容、播放规则或时间范围，系统将在更新后按照新的配置执行轮播任务。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多10次查询。

* 保持原有配置：当未传递非必填参数时，当前轮播任务的原有配置将被保留，不会恢复为默认值。

* 仅支持更新运行中的任务：仅支持更新处于 `running` 状态的任务。可调用 `GetCarouselDetail` 和 `ListCarouselTask` API 查询任务状态。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateCarouselTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 除了各自的专用参数外，还必须携带 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateCarouselTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|TaskID |String |是 |`44c5da50318440*********2d62c910b8` |待更新轮播任务的 ID，即任务的唯一标识符。调用 `CreateCarouselTask` 接口创建轮播任务时返回。 |
|播放规则 |[Rule](https://docs.byteplus.com/en/docs/24/107037#rule) 对象 |是 |`-` |轮播播放规则用于指定轮播回放的素材及行为等。 |


<span id="rule"></span>
### 播放规则


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|循环播放 |Integer |否 |`1` |指定该素材连续播放的次数。该字段的值必须大于等于 `0`。如未传递，则保持原有轮播配置。支持的值及含义如下：<br><br><br>* `0`：不循环播放；<br><br>* 其他正整数：按指定次数循环播放。 |
|素材 |[Source](https://docs.byteplus.com/en/docs/24/107037#source) 数组 |是 |`-` |轮播素材列表，用于指定轮播过程中需播放的素材资源。 |
|SeekInfo |[SeekInfo](https://docs.byteplus.com/en/docs/24/107037#seekinfo) 对象 |否 |`-` |用于控制素材更新后回放行为的配置参数。 |


<span id="source"></span>
### 素材


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ID |String |是 |`1` |轮播素材的唯一标识符。同一播放列表中，每个素材的 `ID` 必须唯一，不允许重复。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若素材的 <code>ID</code> 未发生变化（即更新后的 <code>ID</code> 与原素材的 <code>ID</code> 相同），则仅可更新除 <code>Type</code> 和 <code>Url</code> 以外的其他参数。</div><br> |
|Type |String |是 |`vod` |轮播素材的文件类型，用于指定素材的文件来源类型。支持以下值：<br><br><br>* `vod`：点播 MP4 或 FLV 文件；<br><br>* `m3u8`：点播 M3U8 文件。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果素材的<code>ID</code>未发生变化（即更新后的<code>ID</code>与原素材的<code>ID</code>相同），则<code>Type</code>的取值应与原素材保持一致。</div><br> |
|Url |String |是 |`https://live.example.com/video.mp4` |轮播素材的公网可访问地址。请确保所提供的地址能够被公网正常访问，以便正确加载轮播素材内容。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果素材的<code>ID</code>未发生变化（即更新后的<code>ID</code>与原素材的<code>ID</code>相同），则<code>Url</code>的取值应与原素材保持一致。</div><br> |
|Seek |Integer |否 |`10` |用于控制回放当前素材时跳过开头的一段时间。例如跳过片头，单位为秒。该字段仅在素材类型为点播（`type=vod`）时有效。该字段的使用规则如下：<br><br><br>* 如果`Seek`的值小于或等于`0`，或大于视频实际时长，则该字段不生效。<br><br>* 请根据点播素材的实际时长设置合适的值，以实现跳过片头的效果。 |
|Loop |Integer |否 |`1` |用于指定该素材连续回放的次数。该字段的取值必须大于或等于`0`。如未传递，则保持原轮播配置。支持的取值及含义如下：<br><br><br>* `0`：不循环播放；<br><br>* 其他正整数：按指定次数循环播放。 |


<span id="seekinfo"></span>
### SeekInfo


|**参数** |**数据类型** |**必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Immediate |Long |否 |`1` |用于设置素材切换方式，默认值为`0`。支持的取值及含义如下：<br><br><br>* `0`：回放当前素材后切换到下一个素材；<br><br>* `1`：立即切换到指定素材，并从指定播放进度开始回放。 |
|SourceID |String |否 |`1f9f207a55a43f45` |用于回放的更新素材ID，仅在`Immediate=1`时有效。<br><br><br>* 如未填写，则直接从新素材的第一个素材开始回放。<br><br>* 如填写，则从对应的`SourceID`开始回放。 |
|SourceSeek |Long |否 |`10` |切换素材后，素材的回放位置（单位：秒），表示从该位置开始回放，仅在`Immediate=1`时有效。如未填写，则从对应`SourceID`的素材起始位置开始回放。 |


<span id="Response parameters"></span>
## 返回参数

有关 API 专用返回参数，请参见下表。更多详情请参考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Data |[Data](https://docs.byteplus.com/en/docs/24/107037#data)对象 |`-` |包含任务更新相关信息的数据对象。 |


<span id="data"></span>
### 数据


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|OptID |Integer |`2` |当前生效任务配置的序号，用于标识最新的任务修改记录。每次任务配置更新后，该值会递增。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateCarouselTask&Version=2023-01-01
{
    "TaskID": "44c5da50318440*********2d62c910b8",
    "Rule": {
        "Loop": 1,
        "Source": [
            {
                "ID": "1",
                "Type": "vod",
                "Url": "https://live.example.com/video.mp4",
                "Seek": 10,
                "Loop": 1
            }
        ],
        "SeekInfo": {
            "Immediate": 1,
            "SourceID": "1f9f207a55a43f45",
            "SourceSeek": 10
        }
    }
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301532184E885F20A2263C133082",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateCarouselTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": {
            "OptID": 2
        }
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参阅[请求参数](https://docs.byteplus.com/en/docs/24/107037#request-parameters)接口行为以进行检查。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
