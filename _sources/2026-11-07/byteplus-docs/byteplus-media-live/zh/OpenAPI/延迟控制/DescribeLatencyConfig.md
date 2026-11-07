---
title: "DescribeLatencyConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelatencyconfig-zh-CN"
---

调用`DescribeLatencyConfig` API 查询 GOP 的服务器缓存配置。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 10 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLatencyConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用除需传递接口专属参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLatencyConfig` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |域名空间。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面，获取域名所属的域名空间。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Vhost</code> 和 <code>Domain</code> 至少需配置一个。</div><br> |
|Domain |String |否 |`pull.example.com` |拉流域名。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面，获取域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Vhost</code> 和 <code>Domain</code> 至少需配置一个。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

关于接口专属的唯一返回调用结果参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|LatencyConfigList |[LatencyConfigList](https://docs.byteplus.com/en/docs/24/106990#latencyconfiglist) 数组 |`-` |延迟配置列表。 |


<span id="latencyconfiglist"></span>
### LatencyConfigList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|Domain |String |`pull.example.com` |域名。 |
|GopCacheSize |String |`2000` |边缘服务器用于临时存储视频内容的缓存大小。缓存大小的单位为毫秒。 |
|CreateTime |String |`2024-03-25T11:20:47Z` |配置创建时的 UTC 时间，格式为 RFC 3339。 |
|UpdateTime |String |`2024-03-25T11:20:47Z` |配置最后更新时间的 UTC 时间，格式为 RFC 3339。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLatencyConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "domain": "pull.example.com"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202404120143108F3D78593F7AFFF41F99",
        "Action": "DescribeLatencyConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "LatencyConfigList": [
            {
                "CreateTime": "2024-03-25T11:20:47Z",
                "Domain": "example.com",
                "GopCacheSize": 2000,
                "UpdateTime": "2024-03-25T11:20:47Z",
                "Vhost": "example"
            }
        ]
    }
}
```
