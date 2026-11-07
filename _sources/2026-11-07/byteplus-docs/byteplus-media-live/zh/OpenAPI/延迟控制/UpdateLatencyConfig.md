---
title: "UpdateLatencyConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/updatelatencyconfig-zh-CN"
---

调用 `UpdateLatencyConfig` API，通过为指定拉流域名下的流配置服务器 GOP 缓存，以降低直播延迟。

<span id="Requirements"></span>
## 要求


* 限制：该功能适用于通过 Flash Video（FLV）和 RTMP 协议进行拉流。

* 频率限制：每个账号每秒最多可查询 10 次。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateLatencyConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除需传递 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateLatencyConfig` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Domain |String |是 |`pull.example.com` |拉流域名。您可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名。 |
|GopCacheSize |Integer |是 |`2000` |边缘服务器的缓存大小指为临时存储图像组（GOP）分配的存储空间。<br><br><br>* 缓存大小以毫秒为单位。<br><br>* 支持范围：500\-20,000。<br><br>* 默认值为 `2000`。 |


<span id="Response parameters"></span>
## 返回调用结果参数

该 API 的返回结果仅包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateLatencyConfig&Version=2023-01-01
{
    "GopCacheSize": 2000,
    "Domain": "pull.example.com"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240412014133DA1BD20A355B07FE66F5",
        "Action": "UpdateLatencyConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```
