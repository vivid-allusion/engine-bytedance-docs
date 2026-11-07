---
title: "CSAI 整合概述"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/csai-integration-overview-zh-TW"
---

本指南全面介紹了基於 VideoOne 的短劇應用的客戶端廣告插入（CSAI）解決方案。透過整合 BytePlus MediaAds SDK 和 Google IMA SDK，您可以透過片中廣告實現內容變現，既可選擇與付費牆/解鎖模式互為替代，也可單獨使用。

<span id="fb9bc419"></span>
## 主要特性


* **多樣化廣告格式**：支援片頭、片中和片尾廣告。

* **靈活排期**：可透過 VAST 標籤 URL 和精確時間偏移配置廣告。

* **播放器無關**：相容 `TTVideoEngine` 及透過 `ContentPlayer` 介面的自定義播放器。

* **無縫體驗**：自動管理內容的暫停/恢復及廣告跳過邏輯。

* **防跳過**：當使用者快進越過一個或多個廣告點時，自動播放最近一次錯過的廣告，防止有意跳過廣告。

* **頻次控制**：確保每個片中廣告位在每次會話中僅觸發一次，最佳化使用者體驗。


<span id="aa76cfc7"></span>
## 變現規則


* **劇集級別**：單個劇集可選擇 **付費牆/解鎖**模式 **或**片中廣告模式，但不可同時使用。

* **應用級別**：您可以在同一應用內為不同劇集配置不同的變現模式。


<span id="43918d44"></span>
## 體驗演示

下載最新版 [VideoOne Demo](https://docs.byteplus.com/docs/byteplus-vos/docs-byteplus-videoone-demo-app-1-zh-TW)（v5.4.0 及以上），親身體驗片中廣告能力。

<span id="e2257056"></span>
## 整合指南

請選擇您的平臺以開始整合：


* [Android 平臺 CSAI 整合](https://docs.byteplus.com/docs/byteplus-vos/csai-integration-for-android-zh-TW)

* [iOS 平臺的 CSAI 整合](https://docs.byteplus.com/docs/byteplus-vos/csai-integration-for-ios-zh-TW)
