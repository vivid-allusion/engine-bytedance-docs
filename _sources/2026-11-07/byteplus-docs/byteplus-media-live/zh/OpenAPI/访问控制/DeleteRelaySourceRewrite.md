---
title: "DeleteRelaySourceRewrite"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-3nf0nln2b2-zh-CN"
---

删除回源地址重写规则。回源地址重写功能允许根据预设的匹配规则，从新的地址拉取流。详情请参见[回源地址重写](https://docs.byteplus.com/en/byteplus-media-live/docs/origin-address-rewrite)。

<span id="Requirements"></span>
## 要求

速率限制：每个账号每秒最多 10 次查询。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DeleteRelaySourceRewrite&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用除了特定的 API 参数外，还必须包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DeleteRelaySourceRewrite` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |否 |`example` |域名空间。你可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面，获取该域名所属的域名空间。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">未指定 Vhost 的请求可能会意外匹配并删除域名。因此，强烈建议你指定 Vhost。</div><br> |
|Domain |String |否 |`example.com` |拉流域名。你可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面，获取域名。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于唯一的 API 特定返回调用结果参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Items |[Items](https://docs.byteplus.com/en/docs/24/106967#items)数组 |`-` |已删除的重写规则列表。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DeleteRelaySourceRewrite&Version=2023-01-01
{
    "Domain": "push.example.com",
    "Vhost": "pull.example.com"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DeleteRelaySourceRewrite",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```
