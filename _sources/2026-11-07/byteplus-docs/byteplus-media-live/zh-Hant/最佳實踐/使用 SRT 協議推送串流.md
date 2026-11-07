---
title: "使用 SRT 協議推送串流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/PushWithSRT-zh-TW"
---

要推送低延遲的直播視頻串流，可以搭配 MediaLive 使用安全可靠傳輸（SRT）協議。本主題說明 SRT 是什麼、其限制，並提供取得推流地址及配置串流軟體（如 OBS）的逐步操作指引。

<span id="5f710556"></span>
## 背景

SRT 協議是一種開源低延遲視頻傳輸協議。它支援在如網際網路等不可預測的網路上優化串流媒體效能，並實現安全、可靠的高畫質視頻傳輸與分發。

SRT 協議基於 UDT 協議（一種基於 UDP 的傳輸協議），並保留 UDT 的核心理念與機制。它提供強大的丟包重傳能力。SRT 支援自動重傳請求（ARQ）與前向錯誤更正（FEC），協助資料恢復。

<span id="458950f1"></span>
## 限制


* MediaLive 支援兩種 SRT 協議推流方式：RTMP over SRT 與 TS over SRT。

   * TS over SRT 功能使用 UDP 9000 埠口；

   * RTMP over SRT 功能使用 UDP 1999 埠口。

* MediaLive 支援推送 H.264 或 H.265 視訊編碼的直播串流，以及 AAC 編碼且僅有單一音軌的純音訊串流。

* 使用 SRT 協議推流後，支援以 RTMP、FLV、RTM 格式拉流與播放。目前不支援使用 SRT 協議拉流。

* MediaLive 預設支援使用 SRT 協議推流。使用 SRT 協議推流所產生的流量，將依 **Standard** 價格階層計費。


<span id="9bf6edca"></span>
## 操作流程

<span id="30d88731"></span>
### 取得 SRT 推流地址

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">建議使用 <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-address-generator">address generator</a> 快速生成 SRT 串流地址。</div>


你也可以依 SRT 推流地址規則手動組建推流地址。規則如下。


* TS over SRT

   ```Plain
   srt://push.example.com:9000?streamid=#!::h=push.example.com,r=AppName/StreamName,m=publish,volcTime=1648717***,volcSecret=xxx
   ```
   

   格式說明如下表所示。

   
   |參數 |說明 |
   |---|---|
   |`streamid` |需以 `#!::` 開頭，並遵循 YAML 語法。 |
   |`h` |值為推流網域名稱。 |
   |`r` |值為 `{AppName}/{StreamName}`。 |
   |`m` |值為 `publish`，表示推流操作。 |
   

* RTMP over SRT

   ```Plain
   rtmp://push.example.com:1999/AppName/StreamName?volcTime=1648717***&volcSecret=***
   ```
   


<span id="98c74f75"></span>
### 使用 SRT 協議推送串流

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本節範例使用最新版 OBS 示範串流操作。你可以使用任何支援 SRT 協議的串流軟體進行直播。</div>



1. 開啟 OBS 串流軟體。

2. 在 **Controls** 區域點擊 **Settings**。

3. 於左側導覽窗格選擇 **Stream**。在 **Service** 欄位選擇 **Custom**。於 **Server** 欄位輸入 SRT 串流地址，然後點擊 **OK**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cacc6f1015b34b968ec5ceadecc166cb~tplv-goo7wpa0wc-image.image) </span>

4. 在 **Controls** 區域點擊 **Start Streaming**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ebe665e26154792bbfb8d1ba089e011~tplv-goo7wpa0wc-image.image) </span>
