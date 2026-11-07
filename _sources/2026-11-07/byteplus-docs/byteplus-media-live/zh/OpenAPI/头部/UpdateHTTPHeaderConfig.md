---
title: "UpdateHTTPHeaderConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatehttpheaderconfig-zh-CN"
---

调用`UpdateHTTPHeaderConfig` API，可在边缘服务器返回给客户端的返回调用结果中添加额外的 HTTP 头部，或在回源任务中向第三方源站发送的请求中添加额外的 HTTP 头部。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多 10 次请求。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateHTTPHeaderConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 除了需传递各自的专有参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必选** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateHTTPHeaderConfig` |API 操作名。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必选** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名所属的域名空间。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的[域名](https://console.byteplus.com/live/main/domain/list)页面获取该信息。 |
|Domain |String |否 |`pull.example.com` |拉流域名。如不指定，则该配置应用于域名空间下所有拉流域名。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的[域名](https://console.byteplus.com/live/main/domain/list)页面获取域名。 |
|Phase |Integer |是 |`0` |需更新的 HTTP 头部类型：<br><br><br>* `0`：边缘服务器返回给客户端的返回调用结果中；<br><br>* `1`：回源任务中向第三方源站发送的请求中。 |
|HeaderConfigList |[HeaderConfigList](https://docs.byteplus.com/en/docs/24/106941#headerconfiglist) 数组 |是 |`无` |需添加的 HTTP 头部列表。<br><br>最多可添加 20 个头部。 |
|BlockOriginal |Integer |否 |`0` |是否移除原有头部。<br><br><br>* `0`：保留；<br><br>* `1`：移除。 |
|Enable |Boolean |是 |`true` |是否启用该域名的配置。<br><br><br>* `true`：启用；<br><br>* `false`：停用。 |


<span id="headerconfiglist"></span>
### HeaderConfigList


|**参数** |**数据类型** |**是否必选** |**示例值** |**接口行为** |
|---|---|---|---|---|
|HeaderKey |String |否 |`Content-Type` |头部名称，需唯一，且不超过 1024 个字符。 |
|HeaderValue |String |否 |`text/plain` |头部值。可指定常量或变量作为头部值。<br><br>对于返回调用结果中的头部，头部值可为以下变量：<br><br><br>* `${domain}`：客户端请求中的域名。示例：`example.com`<br><br>* `${uri}`：客户端请求的路径（不含查询参数）。如客户端请求被重写，则该变量表示重写后的路径。示例：`/dir/sample.php`<br><br>* `${args}`：客户端请求中的查询参数。如客户端请求被重写，则该变量表示重写后的参数。示例：`color=red&n=10`<br><br>* `${remote_addr}`：发起请求的客户端 IP 地址。示例：`10.10.10.10`<br><br>* `${server_addr}`：响应客户端请求的边缘服务器 IP 地址。示例：`10.10.10.10`<br><br><br>对于请求中的头部，头部值可为以下变量：<br><br><br>* `${upstream_host}`：回源请求中的域名。示例：`example.com`<br><br>* `${upstream_uri}`：回源请求的路径（不含查询参数）。如果请求被重写，该变量表示重写后的路径。示例：`/dir/sample.php`<br><br>* `${upstream_args}`：源站拉流请求中的查询参数。如果请求被重写，该变量表示重写后的参数。示例：`color=red&n=10`<br><br>* `${remote_addr}`：发送请求的客户端 IP 地址。示例：`10.10.10.10` |
|HeaderFieldType |Integer |必填 |`0` |请求头值的类型：<br><br><br>* `0`：常量；<br><br>* `1`：变量。 |


<span id="Response parameters"></span>
## 返回参数

该 API 的返回调用结果仅包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateHTTPHeaderConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "Phase": 0,
    "HeaderConfigList": [
        {
            "HeaderKey": "Content-Type",
            "HeaderValue": "text/plain",
            "HeaderFieldType": 0
        }
    ],
    "BlockOriginal": 0,
    "Enable": true
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "UpdateHTTPHeaderConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为本操作相关的错误码。其他错误码请参见[BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106941#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |由于当前账号下不存在请求的资源（资源包括域名空间、域名、应用、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |由于当前账号下不存在请求的资源（资源包括域名空间、域名、应用、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置和证书）。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |未找到域名 |未找到域名（Domain）。请检查传入的域名是否与实际使用的域名一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
