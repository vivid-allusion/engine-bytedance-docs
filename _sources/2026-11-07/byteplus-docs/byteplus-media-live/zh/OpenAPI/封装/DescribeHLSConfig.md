---
title: "DescribeHLSConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describehlsconfig-zh-CN"
---

调用 `DescribeHLSConfig` API 查询指定域名空间的 HLS 配置，包括分片大小、分片数量等。

<span id="Requirements"></span>
## 要求

速率限制：每个账号每秒最多查询 10 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeHLSConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeHLSConfig` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取该域名所属的域名空间。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|HLSConfigList |[HLSConfigList](https://docs.byteplus.com/en/docs/24/107010#hlsconfiglist) 数组 |`-` |HLS 配置列表。 |


<span id="hlsconfiglist"></span>
### HLSConfigList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|App |String |`live` |AppName 字段。 |
|Interval |Float |`3` |HLS 分片时长，单位为秒。 |
|PlaylistLength |Integer |`3` |m3u8 播放列表中的媒体分片数量。 |
|FirstPlaylistLength |Integer |`2` |初始播放列表包含的媒体分片数量。 |
|UpdateTime |String |`2024-04-11 06:30:11` |配置最后一次更新时间。 |
|CreateTime |String |`2024-04-11 06:30:11` |配置创建时间。 |
|PartTargetDuration |Float |`1` |每个媒体分片拆分出的部分分片时长。<br><br>单位为秒。<br><br>0 表示关闭低延迟 HLS。 |
|InsertPDT |Boolean |`true` |是否在回放文件中插入 PDT 时间标签，值及含义如下。<br><br><br>* `true`：插入；<br><br>* `false`：不插入。 |
|PDTInterval |String |`3` |在回放文件中插入 PDT（#EXT\-X\-PROGRAM\-DATE\-TIME）时间标签的间隔，单位为秒，取值范围为 [0,3600]，默认值为 0。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若 PDT 间隔设置为 0 或小于分片时长，则每个分片都会插入 PDT 标签。</div><br> |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeHLSConfig&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202404120105366DB1CC6291C10149B0EE",
        "Action": "DescribeHLSConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "HLSConfigList": [
            {
                "Vhost": "example.com",
                "App": "",
                "FirstPlaylistLength": 2,
                "Interval": 3,
                "PartTargetDuration": 1,
                "PlaylistLength": 3,
                "CreateTime": "2024-04-11 06:30:11",
                "UpdateTime": "2024-04-11 06:30:11"
            }
        ]
    }
}
```
