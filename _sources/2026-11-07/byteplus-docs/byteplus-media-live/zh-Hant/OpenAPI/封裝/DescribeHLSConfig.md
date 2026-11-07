---
title: "DescribeHLSConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describehlsconfig-zh-TW"
---

調用 `DescribeHLSConfig` API，以查詢特定網域名稱空間的 HLS 配置，包括片段大小、片段數量等。

<span id="Requirements"></span>
## 需求

速率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeHLSConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) 和 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeHLSConfig` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得該網域所屬的網域名稱空間。 |


<span id="Response parameters"></span>
## 回應參數

如需 API 專屬回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|HLSConfigList |[HLSConfigList](https://docs.byteplus.com/en/docs/24/107299#hlsconfiglist) 陣列 |`-` |HLS 配置列表。 |


<span id="hlsconfiglist"></span>
### HLSConfigList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`push.example.com` |網域名稱空間。 |
|App |String |`live` |AppName 欄位。 |
|Interval |Float |`3` |HLS 片段時長（以秒為單位）。 |
|PlaylistLength |Integer |`3` |m3u8 播放列表中的媒體片段數量。 |
|FirstPlaylistLength |Integer |`2` |初始播放列表包含的媒體片段數量。 |
|UpdateTime |String |`2024-04-11 06:30:11` |配置最後更新的時間。 |
|CreateTime |String |`2024-04-11 06:30:11` |配置建立的時間。 |
|PartTargetDuration |Float |`1` |每個媒體片段分割出的部分片段時長。<br><br>以秒為單位。<br><br>0 表示停用低延遲 HLS。 |
|InsertPDT |Boolean |`true` |是否在播放檔案中插入 PDT 時間標籤，值及含義如下。<br><br><br>* `true`：插入；<br><br>* `false`：不插入。 |
|PDTInterval |String |`3` |在播放檔案中插入 PDT（#EXT\-X\-PROGRAM\-DATE\-TIME）時間標籤的間隔（以秒為單位），取值範圍為 [0,3600]，預設值為 0。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若 PDT 間隔設為 0 或小於片段時長，則每個片段都會插入 PDT 標籤。</div><br> |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeHLSConfig&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 範例回應

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
