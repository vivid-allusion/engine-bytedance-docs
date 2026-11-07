---
title: "DescribeCMAFConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describecmafconfig-zh-CN"
---

调用 `DescribeCMAFConfig` API，查询指定域名空间下流媒体的时长和分段数设置。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 10 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeCMAFConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除需传递 API 专属参数外，还需传递 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeCMAFConfig` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取该域所属的域名空间。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|CMAFConfigList |[CMAFConfigList](https://docs.byteplus.com/en/docs/24/107004#cmafconfiglist) 数组 |`-` |CMAF 配置列表。 |


<span id="cmafconfiglist"></span>
### CMAFConfigList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`Arctic` |域名空间。 |
|应用 |String |`Far` |AppName 字段。 |
|Interval |Float |`2.6` |CMAF 分段时长，范围为 1 到 60。 |
|PlaylistLength |Integer |`6` |播放列表中包含的媒体分段数量。整数范围为 3 到 10。 |
|DisableLowLatency |Boolean |`true` |是否未开启低延迟 DASH。低延迟 DASH 扩展协议，可在保持可扩展性的同时实现低延迟视频流。<br><br><br>* `true`：未开启；<br><br>* `false`：开启。 |
|CreateTime |String |`2024-02-23T07:51:15Z` |配置创建时的 UTC 时间，格式为 RFC 3339。 |
|UpdateTime |String |`2024-02-23T07:51:15Z` |配置最后一次更新时的 UTC 时间，格式为 RFC 3339。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeCMAFConfig&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240411060546FAFDB99137DFD66F1D02",
        "Action": "DescribeCMAFConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CMAFConfigList": [
            {
                "Vhost": "example.com",
                "App": "",
                "DefaultLatency": 3,
                "DisableLowLatency": false,
                "Interval": 2,
                "PlaylistLength": 3,
                "CreateTime": "2024-03-18T05:47:44Z",
                "UpdateTime": "2024-03-18T05:47:44Z"
            }
        ]
    }
}
```
