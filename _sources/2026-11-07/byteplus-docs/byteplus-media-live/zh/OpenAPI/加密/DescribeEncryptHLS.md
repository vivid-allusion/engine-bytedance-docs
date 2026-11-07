---
title: "DescribeEncryptHLS"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeencrypthls-zh-CN"
---

调用 `DescribeEncryptHLS` API，查询用于 HLS 标准加密的自主管理密钥管理服务地址及密钥更新周期。

<span id="Requirements"></span>
## 要求

请求频率限制：每个账号每秒最多 1 次查询。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeEncryptHLS&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除 API 专属参数外，还需携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeEncryptHLS` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|URL |String |`http://example.kms.com/get_key?` |客户端搭建自主管理密钥管理服务后，请求该地址以从密钥管理服务获取密钥。 |
|CycleTime |Float |`60` |流媒体服务器生成密钥的更新周期，单位为秒，取值范围为 [60,604800]。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeEncryptHLS",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "URL": "http://example.kms.com/get_key?",
        "CycleTime": 60
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/106906#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无所请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无所请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。若仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持人员](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
