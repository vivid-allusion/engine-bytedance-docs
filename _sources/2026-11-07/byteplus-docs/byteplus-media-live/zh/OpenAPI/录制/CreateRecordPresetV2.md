---
title: "CreateRecordPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023-zh-CN"
---

调用 `CreateRecordPresetV2` API 创建录制配置。系统会根据你的录制配置，对符合条件的在线流进行录制。

<span id="Usage scenario"></span>
## 使用场景

`CreateRecordPresetV2` API 支持创建三种配置级别：Vhost（低优先级）、Vhost + 应用（中优先级）、Vhost + 应用 + 流（高优先级）。当存在多个配置级别时，优先级依次递增。例如，如果同时创建了 Vhost 和 Vhost + 应用级别的配置，直播流会优先使用 Vhost + 应用级别。

<span id="Requirements"></span>
## 要求


* 前提条件：

   * 当你选择将录制文件存储在视频点播平台时，请先开通 BytePlus 视频点播服务，并参考 [空间](https://https://docs.byteplus.com/en/docs/byteplus-vod/docs-space-management) 创建空间。

   * 当录制文件存储在 TOS 时，请先开通 TOS 服务，并联系 [support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) 进行授权。

* 计费情况：使用录制和存储功能可能会产生录制费用，详情请参考 [转码](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding_2)。

* 频率限制：单个用户的调用频率限制为每秒 10 次。

* 生效说明：若你新增、更新或删除录制配置，需重新推拉流，并等待 3\-5 分钟后变更才会生效。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=CreateRecordPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除需传递 API 专属参数外，还需传递 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`CreateRecordPresetV2` |API 操作。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取域名所属的域名空间。 |
|应用 |String |否 |`live` |直播流 URL 中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 30 个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当 <code>应用</code> 值为空，且 <code>流</code> 值也为空时，表示录制配置为 Vhost 级别的全局配置。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当 <code>应用</code> 值不为空时，关于流值的含义请参见 <code>流</code> 参数说明。</div><br> |
|流 |String |否 |`stream001` |流名称。该值与直播流 URL 中的 StreamName 字段一致。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 100 个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当 <code>应用</code> 值不为空，且 <code>流</code> 值为空时，表示录制配置为 Vhost + 应用级别的全局配置。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当<code>应用</code>值不为空且<code>流</code>不为空时，表示录制配置为 Vhost + 应用 + 流。</div><br> |
|RecordPresetConfig |[RecordPresetConfig](https://docs.byteplus.com/en/docs/24/107011#recordpresetconfig) 对象 |是 |`-` |直播流录制的详细配置。 |


<span id="recordpresetconfig"></span>
### RecordPresetConfig


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|TranscodeRecord |整数 |否 |`1` |是否录制转码流。支持范围：<br><br><br>* `0`（默认）：不录制；<br><br>* `1`：录制所有转码流；<br><br>* `2`：录制由 TranscodeSuffixList 指定的转码流。如果转码流后缀列表为空，仍会录制所有转码流。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">需选择<code>TranscodeRecord</code>或<code>OriginRecord</code>其中之一进行录制。</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>TranscodeRecord</code> 和 <code>OriginRecord</code> 不能同时为 <code>0</code></div><br> |
|OriginRecord |整数 |否 |`0` |是否录制原始流。支持范围：<br><br><br>* `0`（默认）：不录制原始流。<br><br>* `1`：录制原始流。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">需选择<code>TranscodeRecord</code>或<code>OriginRecord</code>其中之一进行录制。</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>TranscodeRecord</code> 和 <code>OriginRecord</code> 不能同时为 <code>0</code>。</div><br> |
|SliceDuration |整数 |否 |`5` |单个 TS 文件的时长，单位为秒。默认值为 10。支持范围：2–100。当录制文件存储为 HLS 格式时该参数生效。 |
|FlvParam |[RecordParam](https://docs.byteplus.com/en/docs/24/107011#recordparam) 对象 |否 |`-` |录制文件为 FLV 格式时的参数。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须通过设置<code>FlvParam</code>、<code>HlsParam</code>、<code>Mp4Param</code>中的任一参数值，指定至少一种录制格式。</div><br> |
|HlsParam |[RecordParam](https://docs.byteplus.com/en/docs/24/107011#recordparam) 对象 |否 |`-` |录制文件为 HLS 格式时的参数。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须通过设置<code>FlvParam</code>、<code>HlsParam</code>、<code>Mp4Param</code>中的任一参数值，指定至少一种录制格式。</div><br> |
|Mp4Param |[RecordParam](https://docs.byteplus.com/en/docs/24/107011#recordparam) 对象 |否 |`-` |录制文件为 MP4 格式时的参数。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须通过设置<code>FlvParam</code>、<code>HlsParam</code>、<code>Mp4Param</code>中的任一参数值，指定至少一种录制格式。</div><br> |
|TranscodeSuffixList |字符串数组 |否 |`["_hd","_bd"]` |转码流后缀列表。当指定的转码流匹配时（`TranscodeRecord`值为`2`），转码流录制配置生效，`TranscodeSuffixList`的默认配置为空，若为空，则录制所有转码流。 |


<span id="recordparam"></span>
### RecordParam


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Enable |布尔值 |否 |`true` |是否启用当前格式的录制。支持范围：<br><br><br>* `false`（默认）：禁用<br><br>* `true`：启用 |
|时长 |整数 |否 |`7200` |在录制完成后存储录制文件的场景下，单个文件的录制时长，单位为秒，默认值为 7200，取值范围为 \-1 及 300\-86400。<br><br><br>* `-1`：录制时长不限制。录制完成后会生成并存储一个完整的录制文件。<br><br>* 当取值为 [300,86400] 区间时，表示录制文件时长达到后立即生成录制文件，并在录制完成后一并上传。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该参数仅在录制文件为 HLS 格式，且需配合分段录制和实时存储场景的两种配置之一时生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">录制过程中若发生断流，所生成的录制文件时长也会相应缩短。</div><br> |
|Splice |整数 |否 |`0` |在录制完成后存储录制文件的场景下，合并切片时长（单位为秒）默认值为0。其取值及含义如下。<br><br><br>* `-1`：合并流切片。无论是否有暂停，所有内容都合并为一个文件，直到录制达到最大时长。<br><br>* `0`（默认）：不合并流。生成新文件。每次直播流暂停后恢复时都会生成新的录制文件。<br><br>* 大于0的任意值：设置生成新文件前的最大等待时间（单位为秒）。若在设定时间内暂停并重新开始，录制会继续在同一个文件中。在设定等待时间后恢复，将会拆分文件。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该参数仅在录制文件为HLS格式时生效，并需在分段录制实时存储场景下配置为两种选项之一。</div><br> |
|RealtimeRecordDuration |Integer |否 |`300` |在实时存储场景下，单个文件录制时长（单位为秒）默认值为`1800`，取值范围为300\-21600。当录制时长达到设定的单文件录制时长后，录制文件会立即生成并实时上传存储。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">录制过程中若发生断开，生成的录制文件对应时长也会相应缩短。</div><br> |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/107011#tosparam)对象 |否 |`-` |TOS存储配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">只能指定一个位置存储录制文件，即<code>TOSParam</code>或<code>VODParam</code>，不可同时指定。</div><br> |
|VODParam |[VODParam](https://docs.byteplus.com/en/docs/24/107011#vodparam)对象 |否 |`-` |VOD存储配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">只能指定一个位置存储录制文件，即<code>TOSParam</code>或<code>VODParam</code>，不可同时指定。</div><br> |
|ContinueDuration |Integer |否 |`180` |在分段录制实时存储场景下，设置连接中断恢复等待时间（单位为秒），默认值为180，取值范围为[0,3600]。<br><br>若连接中断时长小于该值，录制任务不会停止；若实际连接中断时长大于该值，录制任务会停止，连接恢复后会重新启动新的录制任务。 |


<span id="tosparam"></span>
### TOSParam


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |定义是否将录制文件存储至TOS存储。有效取值：<br><br><br>* `false`（默认）：不在TOS中存储录制文件。<br><br>* `true`：在TOS中存储录制文件。 |
|Bucket |String |否 |`live-test-tos-example` |TOS存储的Bucket。例如，存储位置为live\-test\-tos\-example/live/liveapp时，`Bucket`值为`live-test-tos-example`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若使用TOS存储，即在<code>TOSParam</code>中设置<code>Enable</code>为<code>true</code>，则必须指定<code>Bucket</code>。</div><br> |
|StorageDir |String |否 |`live/liveapp` |TOS存储Bucket的目录。，默认为空。例如，存储位置为live\-test\-tos\-example/live/liveapp时，`StorageDir`的值为`live/liveapp`。 |
|ExactObject |String |否 |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |存储路径。默认值为<br><br>`"record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}"`。<br><br>你可以删除路径中的固定片段，例如`{App}/{Stream}`。<br><br>参数格式要求如下：<br><br><br>* 路径不能以正斜杠`/`或反斜杠`\`开头；<br><br>* 路径不能包含`//`或`/./`；<br><br>* 路径不能包含转义序列，例如`\b`、`\t`、`\n`、`\v`、`\f`、`\r`；<br><br>* 最后一个片段作为文件名，必须符合文件命名规范。例如，不能为`..`。<br><br><br>如果你保留`ExactObject`的默认值，最终存储目录类似于：`record/your_domain_name.com/app1/stream1/1683357987_1683358299.mp4`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果你将ExactObject设置为不能保证存储路径唯一性的自定义值，则存在新录制文件覆盖旧录制文件的风险（如果它们的存储路径相同）。</div><br> |


<span id="vodparam"></span>
### VODParam


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否通过视频点播存储录制文件。有效值：<br><br><br>* `false`（默认）：不通过视频点播存储录制文件。<br><br>* `true`：通过视频点播存储录制文件。 |
|VodRegion |String |否 |`ap-singapore-1` |视频点播区域。有效值：<br><br><br>* `ap-singapore-1`：亚太（新加坡）。<br><br>* `ap-southeast-1`：亚太（柔佛）。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果<code>VODParam</code>中的<code>Enable</code>设置为<code>true</code>，则该参数为必填项。</div><br> |
|VodNamespace |String |否 |`Snapshot` |视频点播空间名称，必须属于指定的`VodRegion`。你可以登录[BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/)查询空间名称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果<code>VODParam</code>中的<code>Enable</code>设置为<code>true</code>，则该参数为必填项。</div><br> |
|WorkflowID |String |否 |`25524a2d891d7daf4b9` |工作流ID。如果指定了工作流ID，则会对存储到视频点播的录制文件应用对应的工作流。你可以登录[BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/)获取工作流ID。默认值为空。 |
|ClassificationID |Integer |否 |`1234` |直播录制文件存储到视频点播时的视频分类ID。你可以通过视频点播的[ListVideoClassifications](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listvideoclassifications)接口查询视频分类ID等信息。默认值为空。 |
|StorageClass |Integer |否 |`1` |直播流录制文件存储到视频点播时的存储类型。默认值为`1`。支持的取值及含义如下：<br><br><br>* `1`：标准存储；<br><br>* `2`：归档存储。 |
|ExactObject |String |否 |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |设置录制文件存储到视频点播时的存储规则。默认值为`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}`。你可以删除路径中的固定片段，例如`{App}/{Stream}`。<br><br><br>* 路径不能以正斜杠`/`或反斜杠`\`开头；<br><br>* 路径不能包含`//`或`/./`；<br><br>* 路径不能包含转义序列，例如`\b`、`\t`、`\n`、`\v`、`\f`、`\r`；<br><br>* 最后一个片段作为文件名，必须符合文件命名规范。例如，不能为`..`。<br><br><br>如果你保留默认值，最终存储目录类似于：`record/your_domain_name/app1/stream1/1683357987_1683358299.mp4`。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PresetName |String |`abcdabcdab` |录制配置ID。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=CreateRecordPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
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
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateRecordPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PresetName": "abc****dab"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107011#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据。 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |由于当前账号下不存在请求的资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.AccountIDNotAllowed |该AccountID无权限访问对应资源，请检查请求参数。 |由于当前账号下不存在请求的资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.BillingStatus |该AccountID的计费情况不可用，请开通服务或充值。 |视频直播流服务未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded.Exist |%s已存在 |请求创建的资源（包括域名空间、域名、应用名称、配置、证书）已存在。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与预设相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
