---
title: "CreateSnapshotPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/createsnapshotpresetv2-zh-CN"
---

添加截图配置，用于在直播流处于截图配置的有效范围内时，对直播流进行截图并保存。

<span id="Usage scenario"></span>
## 使用场景

截图配置根据`Vhost`和`应用`指定适用的直播流范围。当直播流使用的域名属于已配置的`Vhost`，且直播流的`AppName`字段与`应用`配置一致时，将对该直播流进行截图并保存。

<span id="Requirements"></span>
## 要求


* 前提条件：若选择将截图文件存储至TOS，需先开通TOS服务并联系[技术支持](https://console.byteplus.com/workorder/create)进行授权。

* 计费情况：直播流截图功能需付费。更多信息，请参见[截图采集](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-screenshot-capturing)。

* 限速：每个账号每秒最多10次请求。

* 生效方式：无论是新增、更新还是删除截图配置，需在修改后3\-5分钟重新推流，配置才会生效。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=CreateSnapshotPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专属参数外，还需包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`CreateSnapshotPresetV2` |API操作名称。 |
|Version |String |是 |`2023-01-01` |本API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名命名空间，即直播流地址的域名所属的命名空间。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023)或访问**Domains**页面的[BytePlus MediaLive控制台](https://console.byteplus.com/live/main/domain/list)，以查询直播流使用的域名所属的命名空间。 |
|应用 |String |是 |`live` |应用名称，与直播流地址中的`AppName`字段值一致。名称长度需为1\-30个字符，可包含以下字符：<br><br><br>* 大写字母（A\-Z）<br><br>* 小写字母（a\-z）<br><br>* 数字（0\-9）<br><br>* 下划线（_）<br><br>* 连字符（\-）<br><br>* 点（.） |
|Status |Integer |否 |`1` |截图配置是否生效。默认值：`1`。可选值：<br><br><br>* `1`：生效。<br><br>* `0`：不生效。 |
|SnapshotPresetConfig |[SnapshotPresetConfig](https://docs.byteplus.com/en/docs/24/106957#snapshotpresetconfig)对象 |是 |`-` |截图配置详细参数。 |


<span id="snapshotpresetconfig"></span>
### SnapshotPresetConfig


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|JpegParam |[JpegParam](https://docs.byteplus.com/en/docs/24/106957#jpegparam)对象 |否 |`-` |JPEG格式截图参数，启用JPEG截图时设置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须启用JPEG或JPG截图，不能同时启用两者。</div><br> |
|JpgParam |[JpgParam](https://docs.byteplus.com/en/docs/24/106957#jpgparam)对象 |否 |`-` |JPG格式截图参数，启用JPG截图时设置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须启用JPEG或JPG截图，不能同时启用两者。</div><br> |
|Interval |Integer |否 |`10` |截图间隔时间，单位为秒。默认值：`10`。该值必须为正整数。 |


<span id="jpegparam"></span>
### JpegParam


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否启用当前格式的截图。默认值：`false`。有效值：<br><br><br>* `true`：启用。<br><br>* `false`：禁用。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/106957#tosparam)对象 |否 |`-` |用于在TOS中存储截图的配置。 |


<span id="jpgparam"></span>
### JpgParam


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Enable |Boolean |否 |`false` |是否启用当前格式的截图。默认值：`false`。有效值：<br><br><br>* `true`：启用。<br><br>* `false`：禁用。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/106957#tosparam)对象 |否 |`-` |用于在TOS中存储截图的配置。 |


<span id="tosparam"></span>
### TOSParam


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否使用TOS进行存储。默认值：`false`。有效值：<br><br><br>* `true`：使用TOS。<br><br>* `false`：不使用TOS。 |
|Bucket |String |否 |`live-test-tos-example` |TOS存储的bucket。例如，若存储路径为`live-test-tos-example/live/liveapp`，参数值为`live-test-tos-example`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用TOS存储时，该参数为必填项。</div><br> |
|StorageDir |String |否 |`live/liveapp` |TOS存储bucket下的存储目录。默认情况下，该值为空。例如，若存储路径为`live-test-tos-example/live/liveapp`，参数值为`live/liveapp`。 |
|ExactObject |String |否 |`{Domain}/App/{流}/{UnixTimestamp}` |截图类型为非覆盖时的存储规则。可按{Domain}/App/{流}/{UnixTimestamp}格式配置规则。支持以下字符：<br><br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 数字（0\-9）<br><br>* 连字符（\-）<br><br>* 感叹号（!）<br><br>* 下划线（_）<br><br>* 句点（.）<br><br>* 星号（\*）<br><br>* 占位符<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须传入<code>ExactObject</code>或<code>OverwriteObject</code>。</div><br> |
|OverwriteObject |String |否 |`{Domain}/App/{流}` |截图类型为覆盖时的存储规则。可按{Domain}/App/{流}格式配置规则。支持以下字符：<br><br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 数字（0\-9）<br><br>* 连字符（\-）<br><br>* 感叹号（!）<br><br>* 下划线（_）<br><br>* 句点（.）<br><br>* 星号（\*）<br><br>* 占位符<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须传入<code>ExactObject</code>或<code>OverwriteObject</code>。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

如需了解API专属返回调用结果参数，请参见下表。更多详情，请参考[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PresetName |String |`preset-123` |截图配置名称。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=CreateSnapshotPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Status": 1,
    "SnapshotPresetConfig": {
        "JpegParam": {
            "Enable": true,
            "TOSParam": {
                "Enable": true,
                "Bucket": "live-test-tos-example",
                "StorageDir": " live/liveapp",
                "ExactObject": "{Domain}/{App}/{Stream}/{UnixTimestamp}"
            }
        },
        "Interval": 10
    }
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSnapshotPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PresetName": "preset-123"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码，请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回错误码，请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考请求参数说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |因当前账号下无请求资源（资源包括域名空间、域名、应用、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.AccountIDNotAllowed |该AccountID无权限访问对应资源，请检查请求参数 |因当前账号下无请求资源（资源包括域名空间、域名、应用、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.BillingStatus |该AccountID计费情况不可用，请开通服务或充值。 |BytePlus MediaLive服务未开通或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置和证书）。建议重试。若仍返回错误码，请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded.Exist |%s已存在 |您请求创建的资源（包括域命名空间、域、应用、配置和证书）已存在。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与功能配置相关的内部错误。请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系技术支持](https://console.byteplus.com/workorder/create)。 |
