---
title: "CreatePullToPushGroup"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushgroup-2023-zh-CN"
---

调用 `CreatePullToPushGroup` API 创建拉流转推任务组并绑定到项目，通过配置该组可以基于项目管理子账号权限。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 10 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=CreatePullToPushGroup&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`CreatePullToPushGroup` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Name |String |是 |`group001` |任务组名称。可包含中文字符、大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9），长度为 1\-20 个字符。 |
|ProjectName |String |是 |`default` |默认情况下为空，表示属于 'default' 项目。<br><br>任务组名称与项目关联后，可按项目管理资源使用和计费情况。任务组名称创建后，项目设置不可更改。如需管理项目，请访问 BytePlus 控制台的 [Project](https://console.byteplus.com/iam/resourcemanage/project) 页面。 |


<span id="Response parameters"></span>
## 返回调用结果参数

该 API 仅在返回调用结果中返回 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=CreatePullToPushGroup&Version=2023-01-01
{
    "Name": "RelayGroup001",
    "ProjectName": "default"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreatePullToPushGroup",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/107042#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParameter.Tags.Key |指定的参数 Tags.Key 无效。 |参数 `Tags.Key` 未通过校验。请检查参数是否正确。 |
|400 |InvalidParameter.Tags.Value |指定的参数 Tags.Value 无效。 |参数 `Tags.Value` 未通过校验。请检查参数是否正确。 |
|400 |InvalidParameter.Tags |指定的参数 Tags 无效。 |参数 `Tags` 校验失败。请检查参数是否正确。 |
|400 |Duplicate.Tags.Key |指定的 tags 对象包含重复的 key。 |参数 `Tags.Key` 的值重复。请检查参数是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无请求资源（域名空间、域名、应用、配置模版、证书）。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded.Exist |请求创建的资源已存在，请重命名 |请求创建的资源（包括域名空间、域名、应用名称、配置、证书）已存在。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
