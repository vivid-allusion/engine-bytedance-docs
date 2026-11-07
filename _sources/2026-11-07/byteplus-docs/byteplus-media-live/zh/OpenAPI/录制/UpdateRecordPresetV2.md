---
title: "UpdateRecordPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023-zh-CN"
---

调用 `UpdateRecordPresetV2` API 以更新已创建的录制配置。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多 10 次查询。

* 接口行为：在新增、更新和删除录制配置后，需要重新推拉流（3\-5 分钟）以使用变更后的配置。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateRecordPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateRecordPresetV2` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 获取待更新配置的域名空间。 |
|应用 |String |否 |`live` |AppName 字段。可调用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 获取待更新配置的 AppName 字段。 |
|流 |String |否 |`example_stream` |StreamName 字段。可调用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 获取待更新配置的 StreamName 字段。 |
|Preset |String |是 |`liverecord` |配置名称。可调用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 获取待更新配置的名称。 |
|RecordPresetConfig |[RecordPresetConfig](https://docs.byteplus.com/en/docs/24/106991#recordpresetconfig) 对象 |否 |`-` |录制详细配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">以下参数如未传值，则表示与更新前配置一致。</div><br> |


<span id="recordpresetconfig"></span>
### RecordPresetConfig


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|TranscodeRecord |Integer |否 |`1` |是否录制转码流。支持范围：<br><br><br>* `0`（默认）：不录制；<br><br>* `1`：录制所有转码流；<br><br>* `2`：录制由 TranscodeSuffixList 指定的转码流。若转码流后缀列表为空，仍录制所有转码流。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">需选择 <code>TranscodeRecord</code> 或 <code>OriginRecord</code> 进行录制。</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>TranscodeRecord</code> 和 <code>OriginRecord</code> 不可同时为 <code>0</code>。</div><br> |
|OriginRecord |Integer |否 |`1` |是否录制原始流。支持范围：<br><br><br>* `0`（默认）：不录制；<br><br>* `1`：录制原始流。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">需选择 <code>TranscodeRecord</code> 或 <code>OriginRecord</code> 进行录制。</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>TranscodeRecord</code> 和 <code>OriginRecord</code> 不可同时为 <code>0</code>。</div><br> |
|SliceDuration |Integer |否 |`5` |单个 TS 文件的时长（秒）。默认值为 `10`。支持范围：5–30。该参数在录制文件存储为 HLS 格式时生效。 |
|FlvParam |[RecordParam](https://docs.byteplus.com/en/docs/24/106991#recordparam) 对象 |否 |`-` |录制文件存储为 FLV 格式时的录制配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须通过设置 <code>FlvParam</code>、<code>HlsParam</code> 或 <code>Mp4Param</code> 中至少一个参数值指定录制格式。</div><br> |
|HlsParam |[RecordParam](https://docs.byteplus.com/en/docs/24/106991#recordparam) 对象 |否 |`-` |录制文件存储为 HLS 格式时的录制配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须通过设置 <code>FlvParam</code>、<code>HlsParam</code> 或 <code>Mp4Param</code> 中至少一个参数值指定录制格式。</div><br> |
|Mp4Param |[RecordParam](https://docs.byteplus.com/en/docs/24/106991#recordparam) 对象 |否 |`-` |在将录制文件以 MP4 格式存储时的录制配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须通过设置<code>FlvParam</code>、<code>HlsParam</code>和<code>Mp4Param</code>中的一个参数值，指定至少一种录制格式。</div><br> |
|转码流后缀列表 |字符串数组 |否 |`["_hd"]` |转码流后缀列表。当指定的转码流匹配时（`TranscodeRecord`值为`2`），转码流录制配置生效，`TranscodeSuffixList`的默认配置为空，若为空，则录制所有转码流。 |


<span id="recordparam"></span>
### RecordParam


|**参数** |**数据类型** |**必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|启用 |布尔型 |否 |`true` |是否启用当前格式的录制。有效值：<br><br><br>* `false`（默认）：禁用<br><br>* `true`：启用 |
|时长 |整数 |否 |`7200` |在录制完成后存储录制文件的场景下，单个文件的录制时长（单位：秒）默认值为 7200，取值范围为 \-1 和 300\-86400。<br><br><br>* `-1`：录制时长无限制。录制完成后，生成并存储完整的录制文件。<br><br>* 当取值在 [300,86400] 之间时，表示录制文件时长达到设定值后立即生成录制文件，并在录制完成后统一上传。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该参数仅在录制文件为 HLS 格式时生效，并需在分段录制和实时存储场景下配置为两种选项之一。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">录制过程中若发生断开，生成的录制文件的时长也会相应缩短。</div><br> |
|拼接 |整数 |否 |`0` |在录制完成后存储录制文件的场景下，合并拼接时长（单位：秒）默认值为 0。其取值及含义如下。<br><br><br>* `-1`：合并流片段。无论是否有暂停，所有内容都合并为一个文件，直到录制达到最大时长。<br><br>* `0`（默认）：不合并流。生成新文件。每次直播流暂停后恢复，都会重新录制生成新文件。<br><br>* 大于 0 的任意值：设置生成新文件前的最大等待时间（单位：秒）。若在定义的时间内暂停并重启，录制会继续在同一个文件中。在定义的等待时间后恢复，将会拆分文件。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该参数仅在录制文件为 HLS 格式时生效，并需在分段录制和实时存储场景下配置为两种选项之一。</div><br> |
|实时录制时长 |整数 |否 |`7200` |在分段录制和实时存储场景下，设置分段录制文件的时长（单位：秒）。默认值为 1800，取值范围为`300-21600`。当录制时长达到设定的单文件录制时长时，录制文件会立即生成并实时上传存储。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">录制过程中若发生断开，生成的录制文件的时长也会相应缩短。</div><br> |
|续录时长 |整数 |否 |`180` |在分段录制实时存储场景下，设置连接中断恢复等待时间（单位：秒），默认值为180，取值范围为[0,3600]。<br><br>如果连接中断时长小于该值，录制任务不会停止；如果实际连接中断时长大于该值，录制任务将停止，并在连接恢复后重新启动新的录制任务。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/106991#tosparam)对象 |否 |`-` |TOS存储配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">只能指定一个存储录制文件的位置，要么是<code>TOSParam</code>，要么是<code>VODParam</code>，不可同时指定。</div><br> |
|VODParam |[VODParam](https://docs.byteplus.com/en/docs/24/106991#vodparam)对象 |否 |`-` |视频点播存储配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">只能指定一个存储录制文件的位置，要么是<code>TOSParam</code>，要么是<code>VODParam</code>，不可同时指定。</div><br> |


<span id="tosparam"></span>
### TOSParam


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |定义是否将录制文件存储到TOS存储。有效值：<br><br><br>* `false`：不在TOS中存储录制文件。<br><br>* `true`：在TOS中存储录制文件。 |
|Bucket |String |否 |`live-test-tos-example` |BytePlus TOS存储的bucket。例如，当存储位置为live\-test\-tos\-example/live/liveapp时，`Bucket`的值为`live-test-tos-example`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果使用TOS存储，即在<code>TOSParam</code>中设置<code>Enable</code>为<code>true</code>，则必须指定<code>Bucket</code>。</div><br> |
|StorageDir |String |否 |`live/liveapp` |TOS存储的Bucket目录，默认情况下为空。例如，当存储位置为live\-test\-tos\-example/live/liveapp时，`StorageDir`的值为`live/liveapp`。 |
|ExactObject |String |否 |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |存储路径。默认值为<br><br>`"record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}"`。<br><br>可以删除路径中的固定片段，例如`{App}/{Stream}`。<br><br>参数格式要求如下：<br><br><br>* 路径不能以正斜杠`/`或反斜杠`\`开头；<br><br>* 路径不能包含`//`或`/./`；<br><br>* 路径不能包含转义序列，如`\b`、`\t`、`\n`、`\v`、`\f`、`\r`；<br><br>* 最后一个片段作为文件名，必须遵循文件命名规范。例如，不能为`..`。<br><br><br>如果保持`ExactObject`的默认值，最终存储目录类似于：`record/your_domain_name.com/app1/stream1/1683357987_1683358299.mp4`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果将ExactObject设置为自定义值且无法保证存储路径唯一性，则存在新录制文件覆盖旧文件的风险（若存储路径相同）。</div><br> |


<span id="vodparam"></span>
### VODParam


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否使用BytePlus视频点播存储录制文件。有效值：<br><br><br>* `false`：不使用BytePlus视频点播存储录制文件。<br><br>* `true`：使用BytePlus视频点播存储录制文件。 |
|VodRegion |String |否 |`ap-singapore-1` |视频点播区域。有效值：<br><br><br>* `ap-singapore-1`：亚太（新加坡）。<br><br>* `ap-southeast-1`：亚太（柔佛）。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果<code>Enable</code>在<code>VODParam</code>中设置为<code>true</code>，则该参数为必填项。</div><br> |
|VodNamespace |String |否 |`Snapshot` |BytePlus视频点播空间名称，必须属于指定的`VodRegion`。可登录[BytePlus VOD控制台](https://console.byteplus.com/vodpaas/totalOverview/)查询空间名称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果<code>Enable</code>在<code>VODParam</code>中设置为<code>true</code>，则该参数为必填项。</div><br> |
|WorkflowID |字符串 |否 |`25524a2d*********891d7daf4b9` |工作流 ID。如果指定了工作流 ID，则会对存储在视频点播中的录制文件应用对应的工作流。你可以登录[BytePlus 视频点播控制台](https://console.byteplus.com/vodpaas/totalOverview/)获取工作流 ID。默认值为空。 |
|ClassificationID |整数 |否 |`12**34` |直播录制文件存储到点播时的视频分类 ID。你可以通过视频点播的[ListVideoClassifications](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listvideoclassifications)接口查询视频分类 ID 等信息。默认值为空。 |
|StorageClass |整数 |否 |`1` |直播录制文件存储到视频点播时的存储类型。默认值为`1`。支持的取值及含义如下。<br><br><br>* `1`：标准存储；<br><br>* `2`：归档存储。 |
|ExactObject |字符串 |否 |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |设置录制文件存储到视频点播时的存储规则。默认值为`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}`。你可以删除路径中的固定片段，例如`{App}/{Stream}`。<br><br><br>* 路径不能以正斜杠`/`或反斜杠`\`开头；<br><br>* 路径不能包含`//`或`/./`；<br><br>* 路径不能包含转义字符，例如`\b`、`\t`、`\n`、`\v`、`\f`、`\r`；<br><br>* 最后一个片段作为文件名，必须符合文件命名规范。例如，不能为`..`。<br><br><br>如果保持默认值，最终的存储目录类似于：`record/your_domain_name/app1/stream1/1683357987_1683358299.mp4`。 |


<span id="Response parameters"></span>
## 返回调用结果参数

该 API 仅在返回调用结果中返回 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateRecordPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Preset": "liverecord",
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
        "RequestId": "20220726*******************051B513A",
        "Action": "UpdateRecordPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106991#request-parameters)说明进行排查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求的资源（资源包括域名空间、域名、应用名、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下无请求的资源（资源包括域名空间、域名、应用名、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 未开通计费情况，请开通服务或充值。 |视频直播服务未开通或账号欠费，导致计费情况不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到预设 |未找到配置。请检查传入的配置是否与已创建的配置一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生了与预设相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生了内部错误，请联系管理员。 |发生了内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生了内部错误，请联系管理员。 |发生了内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务已超时。请联系管理员。 |内部服务已超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
