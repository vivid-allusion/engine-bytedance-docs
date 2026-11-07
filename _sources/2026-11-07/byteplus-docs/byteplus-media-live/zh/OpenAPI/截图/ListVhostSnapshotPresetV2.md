---
title: "ListVhostSnapshotPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2-zh-CN"
---

获取指定域名命名空间下的所有截图配置信息。

<span id="Requirements"></span>
## 要求

限速：每个账号每秒最多10次请求。

<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListVhostSnapshotPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除了API专属参数外，还必须包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListVhostSnapshotPresetV2` |API操作。 |
|Version |String |是 |`2023-01-01` |本API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名命名空间，即直播流地址所属的域名命名空间。你可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023)或访问**Domains**页面的[BytePlus MediaLive控制台](https://console.byteplus.com/live/main/domain/list)，以查看直播流使用的域名所属的命名空间。 |
|Type |String |否 |`tos` |截图配置中截图文件的存储位置。默认情况下，截图配置不会按存储位置进行筛选。目前只能设置为`tos`，表示截图存储在TOS。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关API专属返回调用结果参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PresetList |[PresetList](https://docs.byteplus.com/en/docs/24/107021#presetlist)数组 |`-` |截图配置列表。 |


<span id="presetlist"></span>
### PresetList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名命名空间。 |
|应用 |String |`live` |应用名称。 |
|SlicePresetV2 |[SlicePresetV2](https://docs.byteplus.com/en/docs/24/107021#slicepresetv2)对象 |`-` |截图配置的基本信息。 |


<span id="slicepresetv2"></span>
### SlicePresetV2


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|SnapshotPresetConfig |[SnapshotPresetConfig](https://docs.byteplus.com/en/docs/24/107021#snapshotpresetconfig)对象 |`-` |截图配置的详细信息。 |
|Name |String |`preset-123` |截图配置名称。 |
|Status |Integer |`1` |截图配置是否生效。有效值：<br><br><br>* `1`：生效。<br><br>* `0`：不生效。 |


<span id="snapshotpresetconfig"></span>
### SnapshotPresetConfig


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|JpegParam |[JpegParam](https://docs.byteplus.com/en/docs/24/107021#jpegparam)对象 |`-` |JPEG格式截图参数。 |
|JpgParam |[JpgParam](https://docs.byteplus.com/en/docs/24/107021#jpgparam)对象 |`-` |JPG格式截图参数。 |
|Interval |Integer |`10` |截图间隔时间，单位为秒。 |


<span id="jpegparam"></span>
### JpegParam


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Enable |Boolean |`true` |当前格式截图是否已开启。有效值：<br><br><br>* `true`：已开启。<br><br>* `false`：未开启。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/107021#tosparam)对象 |`-` |截图存储到TOS的配置。 |


<span id="jpgparam"></span>
### JpgParam


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Enable |Boolean |`false` |当前格式截图是否已开启。有效值：<br><br><br>* `true`：已开启。<br><br>* `false`：未开启。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/107021#tosparam)对象 |`-` |截图存储到TOS的配置。 |


<span id="tosparam"></span>
### TOSParam


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Enable |Boolean |`true` |是否使用TOS存储。有效值：<br><br><br>* `true`：已使用。<br><br>* `false`：未使用。 |
|Bucket |String |`live-test-tos-example` |TOS存储桶。例如，存储路径为`live-test-tos-example/live/liveapp`时，参数值为`live-test-tos-example`。 |
|StorageDir |String |`live/liveapp` |TOS存储桶下的存储目录。例如，存储路径为`live-test-tos-example/live/liveapp`时，参数值为`live/liveapp`。 |
|ExactObject |String |`{Domain}/{App}/{Stream}/{UnixTimestamp}` |截图类型为非覆盖时的存储规则。您可以按照 {Domain}/{应用}/{流}/{UnixTimestamp} 的格式配置规则。支持以下字符：<br><br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 数字（0\-9）<br><br>* 连字符（\-）<br><br>* 感叹号（!）<br><br>* 下划线（_）<br><br>* 句点（.）<br><br>* 星号（\*）<br><br>* 占位符 |
|OverwriteObject |字符串 |`{Domain}/{应用}/{流}` |当截图类型为覆盖时的存储规则。您可以按照 {Domain}/{应用}/{流} 的格式配置规则。支持以下字符：<br><br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 数字（0\-9）<br><br>* 连字符（\-）<br><br>* 感叹号（!）<br><br>* 下划线（_）<br><br>* 句点（.）<br><br>* 星号（\*）<br><br>* 占位符 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=ListVhostSnapshotPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Type": "tos"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListVhostSnapshotPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PresetList": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "SlicePreset": {
                    "SnapshotPresetConfig": {
                        "JpegParam": {
                            "Enable": true,
                            "TOSParam": {
                                "Enable": true,
                                "Bucket": "live-test-tos-example",
                                "StorageDir": "live/liveapp",
                                "ExactObject": "{Domain}/{App}/{Stream}/{UnixTimestamp}"
                            }
                        },
                        "Interval": 10
                    },
                    "Name": "preset-123",
                    "Status": "1"
                }
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍然返回该错误码，请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考请求参数说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域命名空间、域、应用、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域命名空间、域、应用、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |BytePlus MediaLive 服务未开通或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域命名空间、域、应用、配置和证书）。建议重试。如果仍然返回该错误码，请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与功能配置相关的内部错误。请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
