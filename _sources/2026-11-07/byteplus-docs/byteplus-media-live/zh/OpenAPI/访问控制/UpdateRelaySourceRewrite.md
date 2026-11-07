---
title: "UpdateRelaySourceRewrite"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcerewrite-zh-CN"
---

配置回源地址重写规则。回源地址重写功能可根据预设的匹配规则，从新的地址拉取流。详情请参见[回源地址重写](https://docs.byteplus.com/en/docs/24/origin-address-rewrite)。

<span id="Requirements"></span>
## 要求


* 前提条件：仅适用于按需回源拉流任务和使用 FLV、HLS、RTMP 协议的流。

* 限制：最多可配置 50 条重写规则。

* 频率限制：每个账号每秒最多 10 次查询。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateRelaySourceRewrite&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 除了需传入各自的专用参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateRelaySourceRewrite` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |本次 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取域名所属的域名空间。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">未指定 Vhost 可能导致域名被意外修改。因此，强烈建议您指定 Vhost。</div><br> |
|Domain |String |否 |`pull.example.com` |拉流域名。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取域名。 |
|RewriteRule |[RewriteRule](https://docs.byteplus.com/en/docs/24/106986#rewriterule)对象 |否 |`N/A` |回源地址重写配置 |


<span id="rewriterule"></span>
### RewriteRule


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Enable |Boolean |是 |`true` |是否启用回源地址重写<br><br><br>* `true`：启用<br><br>* `false`：禁用 |
|RewriteRuleList |[RewriteRuleList](https://docs.byteplus.com/en/docs/24/106986#rewriterulelist)数组 |是 |`N/A` |重写规则列表 |


<span id="rewriterulelist"></span>
### RewriteRuleList


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|TargetPath |String |否 |`/app/live/$1` |新路径。可使用`${1}`、`${2}`、`${3}`、`${4}`和`${5}`分别表示第 1 至第 5 个通配符匹配的内容。路径需满足以下要求：<br><br><br>* 路径不能包含协议和域名，例如`http://example.domain.com`。<br><br>* 路径必须以`/`开头。<br><br>* 路径长度最多为 1,024 个字符。<br><br>* 路径不能包含连续两个星号，即`**`。<br><br>* 路径不能包含连续两个`${`，即`${${`。 |
|OriginPath |String |否 |`/example/(.\*) \|原有路径。路径最多可包含 5 个通配符。但请勿使用通配符表示查询参数。路径需满足以下要求： \| |* 路径不能包含协议和域名，例如`http://example.domain.com`。<br><br>* 路径必须以`/`开头。<br><br>* 路径长度最多为 1,024 个字符。<br><br>* 路径不能包含连续两个星号，即`**`。<br><br>* 路径不能包含连续两个 ${，即`${${`。 |
|IncludeParams |Boolean |否 |`true` |是否将原路径的查询参数包含在新路径中。<br><br><br>* `true`：包含<br><br>* `false`：不包含 |


<span id="Response parameters"></span>
## 返回参数

该 API 的返回调用结果仅包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateRelaySourceRewrite&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "RewriteRules": {
        "Enable": true,
        "RewriteRuleList": [
            {
                "TargetPath": "/app/live/$1",
                "OriginPath": "/example/(.*)$",
                "IncludeParams": true
            }
        ]
    }
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "UpdateRelaySourceRewrite",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```
