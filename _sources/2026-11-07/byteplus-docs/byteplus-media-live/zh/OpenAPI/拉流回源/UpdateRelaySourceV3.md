---
title: "UpdateRelaySourceV3"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023-zh-CN"
---

调用 `UpdateRelaySourceV3` API，以新增或更新按播放触发的回源配置。按播放触发的回源指的是仅在有观众观看时才触发回源，这可以节省源服务器的带宽资源，并提升系统整体效率。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多10次查询。

<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateRelaySourceV3&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除了API专属参数外，还必须包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateRelaySourceV3` |API操作。 |
|Version |String |是 |`2023-01-01` |该API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |该域名所属的域名空间。可通过调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API或在BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取域名空间。 |
|应用 |String |否 |`live` |直播流URL中的AppName字段。如未指定，则配置将应用于所有AppName。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到30个字符。 |
|GroupDetails |[GroupDetails](https://docs.byteplus.com/en/docs/24/106968#groupdetails)数组 |是 |`-` |回源配置组列表。若某个配置组返回错误，系统会按数组顺序自动切换到下一个配置组。 |


<span id="groupdetails"></span>
### GroupDetails


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Group |String |是 |`relay1` |回源配置组名称。 |
|Servers |[Servers](https://docs.byteplus.com/en/docs/24/106968#servers)数组 |是 |`-` |回源配置列表。若某个回源地址返回错误，系统会按数组顺序自动切换到下一个地址。 |


<span id="servers"></span>
### Servers


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|RelaySourceDomain |String |是 |`example.org` |直播源服务器地址，支持填写源服务器的域名或IP地址。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当源服务器使用非默认端口时，支持在回源地址中以<code>域名:端口</code>或<code>IP:端口</code>的形式配置端口。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">最多可添加10个回源地址。回源失败时，将按你添加的地址顺序循环尝试。</div><br> |
|RelaySourceProtocol |String |是 |`rtmp` |流协议。支持的取值包括：<br><br><br>* `rtmp`<br><br>* `flv`<br><br>* `hls`<br><br>* `dash` |
|RelaySourceParams |JSON Map |否 |`{"key1": "value1", "key2": "value2"}` |自定义回源参数。该参数默认为空。格式为`"Key":"Value"`，例如`"domain":"live.push.net"`。 |


<span id="Response parameters"></span>
## 返回参数

该API的返回调用结果仅包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateRelaySourceV3&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "GroupDetails": [
        {
            "Group": "relay1",
            "Servers": [
                {
                    "RelaySourceProtocol": "rtmp",
                    "RelaySourceDomain": "example.org",
                    "RelaySourceParams": {
                        "key1": "value1",
                        "key2": "value2"
                    }
                }
            ]
        }
    ]
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "Service": "live",
        "Region": "ap-singapore-1",
        "Version": "2023-01-01",
        "Action": "UpdateRelaySourceV3_1h0pbmhmb",
        "RequestId": "202306041104200100100232280022D31"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参阅[请求参数](https://docs.byteplus.com/en/docs/24/106968#request-parameters)的接口行为说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据。 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |由于当前账号下不存在请求的资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.AccountIDNotAllow |该AccountID无权限访问对应资源，请检查请求参数。 |由于当前账号下不存在请求的资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.BillingStatus |该AccountID的计费情况不可用，请开通服务或充值。 |视频直播流服务未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded.Exist |%s已存在 |请求创建的资源（包括域名空间、域名、应用名称、配置、证书）已存在。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
