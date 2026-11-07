---
title: "RTC API 示例"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/doc-rtc-api-examples-zh-TW"
---

本文件簡要介紹 VideoOne 如何利用 BytePlus RTC SDK 實現高階功能。旨在幫助使用者高效配置 RTC 的高階功能。

<span id="a361cd61"></span>
# RTC 整合指南

<span id="586de8d7"></span>
## 前提條件

已開通 [BytePlus RTC ](https://console.byteplus.com/rtc/workplaceRTC)服務的有效 BytePlus 賬號。請參閱 [使用 RTC 服務前 ](https://docs.byteplus.com/en/byteplus-rtc/docs/69865)獲取詳細操作說明。

<span id="11630b9b"></span>
## 功能實現

VideoOne 展示如何使用 BytePlus RTC SDK 實現高階功能。目前支援以下類別：核心功能、房間管理、音影片傳輸、音訊管理、影片管理、訊息管理及其他元件。有關這些功能實現的更多細節，請參考以下文件：


|**類別** |**功能** |**參考文件** |
|---|---|---|
|核心功能 |快速開始 |[BytePlus RTC：快速開始指南](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70123) |
|房間管理 |多房間 |[BytePlus RTC：加入多個 RTC 房間](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-196844) |
|音影片傳輸 |跨房間對戰 |[BytePlus RTC：跨房間轉發媒體流](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104398) |
|音訊管理 |原始音訊資料 |[BytePlus RTC：獲取原始音訊資料](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1178324) |
||音效混音 |[BytePlus RTC：播放音效檔案](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1178326) |
||音樂混音 |[BytePlus RTC：播放音樂檔案](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70141) |
||音效 |[BytePlus RTC：音效與降噪](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1178327) |
|影片管理 |畫中畫 |[BytePlus RTC：支援移動端前臺多工](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1178325) |
||影片配置 |[BytePlus RTC：設定影片編碼配置](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70122) |
||影片旋轉 |[BytePlus RTC：影片旋轉](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-106458) |
|其他元件 |BytePlus Effects |[BytePlus RTC：影片特效（付費功能）](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717) |
||推流至 CDN |[BytePlus RTC：推流至 CDN](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69817) |
|訊息管理 |SEI 訊息 |[BytePlus RTC：補充增強資訊（SEI）](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70140) |
||訊息與幀同步 ||


參考開原始碼，將這些功能整合到您的應用：


* [iOS：RTCAPIExample](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample)

* [Android：RTCAPIExample](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/rtc-api-example)
