---
title: "UpdateSnapshotPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/updatesnapshotpresetv2-zh-CN"
---

更新已添加的截图配置。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多10次请求。

* 生效说明：要使截图配置的变更（包括新增、更新或删除）生效，需在修改后3\-5分钟重新推流。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* 接口地址：https://open.byteplusapi.com/?Action=UpdateSnapshotPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专属参数外，还需携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateSnapshotPresetV2` |API操作名称。 |
|Version |String |是 |`2023-01-01` |该API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名命名空间。可调用[ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2)获取用于更新截图配置的`Vhost`值。 |
|应用 |String |是 |`live` |应用名称。可调用[ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2)获取用于更新截图配置的`应用`值。 |
|Status |Integer |否 |`1` |截图配置是否生效。有效值：<br><br><br>* `1`：生效。<br><br>* `0`：不生效。 |
|SnapshotPresetConfig |[SnapshotPresetConfig](https://docs.byteplus.com/en/docs/24/106924#snapshotpresetconfig)对象 |是 |`-` |截图配置的详细参数。 |
|Preset |String |是 |`preset-123` |截图配置名称。可调用[ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2)获取用于更新截图配置的`Name`值。 |


<span id="snapshotpresetconfig"></span>
### SnapshotPresetConfig


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|JpegParam |[JpegParam](https://docs.byteplus.com/en/docs/24/106924#jpegparam)对象 |否 |`-` |JPEG格式截图的参数，启用JPEG截图时设置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须启用JPEG或JPG截图中的一种，不能同时启用两者。</div><br> |
|JpgParam |[JpgParam](https://docs.byteplus.com/en/docs/24/106924#jpgparam)对象 |否 |`-` |JPG格式截图的参数，启用JPG截图时设置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须启用JPEG或JPG截图中的一种，不能同时启用两者。</div><br> |
|Interval |Integer |否 |`10` |截图间隔时间，单位为秒。默认值：`10`。该值必须为正整数。 |


<span id="jpegparam"></span>
### JpegParam


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否启用当前格式的截图。默认值：`false`。有效值：<br><br><br>* `true`：启用。<br><br>* `false`：禁用。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/106924#tosparam)对象 |否 |`-` |截图存储到TOS的配置。 |


<span id="jpgparam"></span>
### JpgParam


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否启用当前格式的截图。默认值：`false`。有效值：<br><br><br>* `true`：启用。<br><br>* `false`：禁用。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/106924#tosparam)对象 |否 |`-` |截图存储到TOS的配置。 |


<span id="tosparam"></span>
### TOSParam


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否使用TOS进行存储。默认值：`false`。有效值：<br><br><br>* `true`：使用TOS。<br><br>* `false`：不使用TOS。 |
|Bucket |String |否 |`live-test-tos-example` |TOS存储的桶名称。例如，若存储路径为`live-test-tos-example/live/liveapp`，参数值为`live-test-tos-example`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用TOS存储时，该参数为必填项。</div><br> |
|StorageDir |String |否 |`live/liveapp` |TOS存储桶下的存储目录。默认值为空。例如，若存储路径为`live-test-tos-example/live/liveapp`，参数值为`live/liveapp`。 |
|ExactObject |字符串 |否 |`{Domain}/{应用}/{流}/{UnixTimestamp}` |当截图类型为非覆盖时的存储规则。您可以按照 {Domain}/{应用}/{流}/{UnixTimestamp} 格式配置该规则。支持以下字符：<br><br><br>* 小写字母 (a\-z)<br><br>* 大写字母 (A\-Z)<br><br>* 数字 (0\-9)<br><br>* 连字符 (\-)<br><br>* 感叹号 (!)<br><br>* 下划线 (_)<br><br>* 句点 (.)<br><br>* 星号 (\*)<br><br>* 占位符<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">您必须传入 <code>ExactObject</code> 或 <code>OverwriteObject</code>。</div><br> |
|OverwriteObject |字符串 |否 |`{Domain}/{应用}/{流}` |当截图类型为覆盖时的存储规则。您可以按照 {Domain}/{应用}/{流} 格式配置该规则。支持以下字符：<br><br><br>* 小写字母 (a\-z)<br><br>* 大写字母 (A\-Z)<br><br>* 数字 (0\-9)<br><br>* 连字符 (\-)<br><br>* 感叹号 (!)<br><br>* 下划线 (_)<br><br>* 句点 (.)<br><br>* 星号 (\*)<br><br>* 占位符<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">您必须传入 <code>ExactObject</code> 或 <code>OverwriteObject</code>。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

该API仅在返回调用结果中返回[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateSnapshotPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
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
    "Preset": "preset-123"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateSnapshotPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍返回该错误码，请 [联系技术支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考请求参数说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域命名空间、域、应用、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域命名空间、域、应用、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |BytePlus MediaLive 服务未开通或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域命名空间、域、应用、配置和证书）。建议重试。如果仍返回该错误码，请 [联系技术支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到预设 |未找到配置。请检查所提供的配置是否与已创建的配置一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请 [联系技术支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与功能配置相关的内部错误。请 [联系技术支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请 [联系技术支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请 [联系技术支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请 [联系技术支持](https://console.byteplus.com/workorder/create)。 |
