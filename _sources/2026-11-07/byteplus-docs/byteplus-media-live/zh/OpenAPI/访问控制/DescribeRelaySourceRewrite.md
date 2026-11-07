---
title: "DescribeRelaySourceRewrite"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dakt2mfojk-zh-CN"
---

查询回源地址重写规则。回源地址重写功能可根据预设的匹配规则，从新的地址拉取流。详情请参见[回源地址重写](https://docs.byteplus.com/en/byteplus-media-live/docs/origin-address-rewrite)。

<span id="Requirements"></span>
## 要求

速率限制：每个账号每秒最多查询 10 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeRelaySourceRewrite&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除需传递 API 专属参数外，还需传递[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeRelaySourceRewrite` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取该域名所属的域名空间。 |
|Domain |String |否 |`pull.example.com` |拉流域名。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取域名。 |


<span id="Response parameters"></span>
## 返回调用结果参数

如需了解唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|RelaySourceRewriteList |[RelaySourceRewriteList](https://docs.byteplus.com/en/docs/24/106902#relaysourcerewritelist)对象 |`无` |回源地址重写配置 |


<span id="relaysourcerewritelist"></span>
### RelaySourceRewriteList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|Domain |String |`pull.example.com` |域名。 |
|RewriteRule |[RewriteRule](https://docs.byteplus.com/en/docs/24/106902#rewriterule)对象 |`无` |回源地址重写配置。 |


<span id="rewriterule"></span>
### RewriteRule


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Enable |Boolean |`true` |是否已开启回源地址重写。 |
|RewriteRuleList |[RewriteRuleList](https://docs.byteplus.com/en/docs/24/106902#rewriterulelist)数组 |`无` |重写规则列表。 |


<span id="rewriterulelist"></span>
### RewriteRuleList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TargetPath |String |`/app/live/$1` |新路径。 |
|OriginPath |String |`/example/$2` |现有路径。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeRelaySourceRewrite&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeRelaySourceRewrite",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "RelaySourceRewriteList": {
            "Domain": "push.example.com",
            "Vhost": "pull.example.com",
            "RewriteRules": {
                "Enable": true,
                "RewriteRuleList": [
                    {
                        "TargetPath": "/app/live/$1",
                        "OriginPath": "/app/live/$2"
                    }
                ]
            }
        }
    }
}
```
