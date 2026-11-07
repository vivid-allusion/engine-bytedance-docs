---
title: "DeleteHLSConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/deletehlsconfig-zh-CN"
---

调用`DeleteHLSConfig` API，可将指定域名空间的 HLS 配置恢复为默认设置，包括分片大小、分片数量等。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多 10 次请求

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DeleteHLSConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 除了需要传递 API 专属参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DeleteHLSConfig` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或在 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取域名所属的域名空间。 |
|应用 |String |否 |`live` |直播流 URL 中的 AppName 字段。需与添加配置时填写的值保持一致。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点号（.），长度为 1~30 个字符。 |


<span id="Response parameters"></span>
## 返回调用结果参数

该 API 的返回调用结果中仅包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DeleteHLSConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202404120112128186EFFADE3658DF0DB2",
        "Action": "DeleteHLSConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```
