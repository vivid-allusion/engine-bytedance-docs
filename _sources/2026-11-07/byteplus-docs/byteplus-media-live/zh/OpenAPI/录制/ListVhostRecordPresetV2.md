---
title: "ListVhostRecordPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023-zh-CN"
---

调用 `ListVhostRecordPresetV2` API 查询指定 Vhost 下的所有录制配置，包括 Vhost、Vhost + 应用、Vhost + 应用 + 流 三个层级的所有配置。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 10 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListVhostRecordPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除需传递 API 专属参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListVhostRecordPresetV2` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可通过调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名空间。 |
|Type |String |否 |`tos` |要查询的存储类型。支持的有效值包括：<br><br><br>* `tos`（默认）：BytePlus TOS。<br><br>* `vod`：BytePlus 视频点播。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于 API 专属返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PresetList |[PresetList](https://docs.byteplus.com/en/docs/24/106962#presetlist) 数组 |`-` |录制配置列表。 |


<span id="presetlist"></span>
### PresetList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|App |String |`live` |AppName 字段。 |
|Stream |String |`example_stream` |StreamName 字段。 |
|SlicePresetV2 |[SlicePresetV2](https://docs.byteplus.com/en/docs/24/106962#slicepresetv2) 对象 |`-` |配置信息。 |


<span id="slicepresetv2"></span>
### SlicePresetV2


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ID |Long |`8` |配置 ID。 |
|Name |String |`RecordPresetexample` |配置名称。 |
|RecordPresetConfig |[RecordPresetConfig](https://docs.byteplus.com/en/docs/24/106962#recordpresetconfig) 对象 |`-` |录制参数。 |


<span id="recordpresetconfig"></span>
### RecordPresetConfig


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TranscodeRecord |Integer |`1` |是否录制转码流。支持的有效值包括：<br><br><br>* `0`（默认）：不录制；<br><br>* `1`：录制所有转码流；<br><br>* `2`：录制由 TranscodeSuffixList 指定的转码流。若转码流后缀列表为空，仍表示录制所有转码流。 |
|TranscodeSuffixList |String 数组 |`['_hd']` |转码流后缀列表。当转码流录制配置根据指定转码流（`TranscodeRecord` 值为 `2`）生效时，`TranscodeSuffixList` 默认配置为空，效果等同于录制所有转码流。 |
|OriginRecord |Integer |`1` |是否录制原始流。支持的有效值包括：<br><br><br>* `0`（默认）：不录制原始流。<br><br>* `1`：录制原始流。 |
|SliceDuration |Integer |`5` |单个 TS 文件的时长（秒）。默认值为 `10`。支持范围：5–30。该参数在录制文件存储为 HLS 格式时生效。 |
|FlvParam |[RecordParam](https://docs.byteplus.com/en/docs/24/106962#recordparam) 对象 |`-` |录制文件存储为 FLV 格式时的录制配置。 |
|HlsParam |[RecordParam](https://docs.byteplus.com/en/docs/24/106962#recordparam) 对象 |`-` |录制文件存储为 HLS 格式时的录制配置。 |
|Mp4Param |[RecordParam](https://docs.byteplus.com/en/docs/24/106962#recordparam) 对象 |`-` |录制文件存储为 MP4 格式时的录制配置。 |


<span id="recordparam"></span>
### RecordParam


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Enable |Boolean |`true` |是否启用当前格式的录制。支持的有效值包括：<br><br><br>* `false`：禁用<br><br>* `true`：启用 |
|时长 |整数 |`7200` |在录制完成后存储录制文件的场景下，录制文件的最大时长及其取值和含义如下。<br><br><br>* `-1`：表示全程录制。录制完成后，生成并存储完整的录制文件。<br><br>* 当取值在 [300, 86400] 范围内时，表示录制文件将按设定时长分段生成。录制完成后，录制文件将一并上传和存储。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该参数仅在录制文件为 HLS 格式，并且需在分段录制与实时存储场景下配置为两种选项之一时生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">录制过程中若发生断流，相应生成的录制文件时长也会相应缩短。</div><br> |
|RealtimeRecordDuration |整数 |`7200` |在分段录制与实时存储场景下，设置分段录制文件的时长，单位为秒。默认值为 1800。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">录制过程中若发生断流，相应生成的录制文件时长也会相应缩短。</div><br> |
|Splice |整数 |`0` |在录制完成后存储录制文件的场景下，用于指定直播流断开时录制内容的合并方式。其取值和含义如下。<br><br><br>* `-1`：合并流片段。无论中间是否有暂停，均合并为一个文件，直到录制达到最大时长。<br><br>* `0`（默认）：生成新文件。每次直播流暂停后恢复，都会重新生成一个录制文件。<br><br>* 大于 0 的任意值：设置生成新文件前的最大等待时间，单位为秒。若在定义的等待时间内暂停并重新开始，则录制会继续写入同一个文件。超过定义的等待时间后恢复，将会分割为新文件。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该参数仅在录制文件为 HLS 格式，并且需在分段录制与实时存储场景下配置为两种选项之一时生效。</div><br> |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/106962#tosparam) 对象 |`-` |TOS 存储配置。 |
|VODParam |[VODParam](https://docs.byteplus.com/en/docs/24/106962#vodparam) 对象 |`-` |视频点播存储配置。 |


<span id="tosparam"></span>
### TOSParam


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Enable |布尔值 |`true` |定义是否将录制文件存储到 TOS 存储中。可选值包括：<br><br><br>* `false`：不将录制文件存储到 TOS。<br><br>* `true`：将录制文件存储到 TOS。 |
|Bucket |字符串 |`live-test-tos-example` |TOS 存储的 bucket。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若 <code>TOSParam</code> 中的 <code>Enable</code> 设置为 <code>true</code>，则必须指定 <code>Bucket</code>。</div><br> |
|StorageDir |字符串 |`live/liveapp` |录制文件在 bucket 中的目录，默认为空。 |
|ExactObject |字符串 |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |录制文件的存储规则。 |


<span id="vodparam"></span>
### VODParam


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Enable |布尔值 |`true` |是否使用视频点播存储录制文件。可选值包括：<br><br><br>* `false`：不使用视频点播存储录制文件。<br><br>* `true`：使用视频点播存储录制文件。 |
|VodRegion |字符串 |`ap-singapore-1` |视频点播区域。可选值：<br><br><br>* `ap-singapore-1`：亚太地区（新加坡）。<br><br>* `ap-southeast-1`：亚太地区（柔佛）。 |
|VodNamespace |字符串 |`SnapShot` |BytePlus 视频点播空间的名称，属于`VodRegion`。你可以登录[BytePlus 视频点播控制台](https://console.byteplus.com/vodpaas/totalOverview/)查询空间名称。 |
|WorkflowID |String |`25524a2d*********891d7daf4b9` |工作流 ID。如果指定工作流 ID，则会将对应的工作流应用于存储在视频点播中的录制文件。你可以登录[BytePlus 视频点播控制台](https://console.byteplus.com/vodpaas/totalOverview/)获取工作流 ID。 |
|ClassificationID |Integer |`12***45` |直播录制文件存储到点播时的视频分类 ID。你可以通过视频点播的[ListVideoClassifications](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listvideoclassifications)接口查询视频分类 ID 等信息。默认值为空。 |
|StorageClass |Integer |`1` |直播录制文件存储到视频点播时的存储类型。默认值为`1`。支持的取值如下。<br><br><br>* `1`：标准存储；<br><br>* `2`：归档存储。 |
|ExactObject |String |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |设置录制文件存储到视频点播时的存储规则。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=ListVhostRecordPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20220726*******************051B513A",
        "Action": "ListVhostRecordPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "PresetList": [
        {
            "Vhost": "push.example.com",
            "App": "live",
            "SlicePresetV2": {
                "ID": 8,
                "Name": "RecordPresetexample",
                "RecordPresetConfig": {
                    "OriginRecord": 1,
                    "HlsParam": {
                        "Enable": "true",
                        "RealtimeRecordDuration": 7200,
                        "Splice": 0,
                        "TOSParam": {
                            "Enable": true,
                            "Bucket": "live-test-tos-example",
                            "StorageDir": "",
                            "RecordObject": "record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}"
                        }
                    }
                }
            }
        }
    ]
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务未开启或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与预设相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
