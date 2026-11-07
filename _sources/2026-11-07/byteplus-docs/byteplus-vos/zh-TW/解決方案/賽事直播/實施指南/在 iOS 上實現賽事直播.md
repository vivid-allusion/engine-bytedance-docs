---
title: "在 iOS 上實現賽事直播"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-live-sport-streaming-for-ios-zh-TW"
---

本指南介紹如何使用 BytePlus MediaLive SDK 在 iOS 上實現賽事直播觀看體驗。您將學習如何初始化直播播放器、透過低延遲協議拉流、切換機位和畫質，以及在播放之上疊加互動功能。

<span id="lsi-env"></span>
## 環境要求


* Xcode 16 或更高版本。我們建議使用最新版本的 Xcode 以獲得最佳效能。

* 一台執行 iOS 13 或更高版本的真機裝置。


<span id="lsi-prereq"></span>
## 前提條件


* 一個已啟用 [BytePlus MediaLive](https://console.byteplus.com/live) 的有效 [BytePlus 帳戶](http://console.byteplus.com/)。

* 完成 [直播的基礎設定](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)：

   * 取得 BytePlus MediaLive SDK 授權。

      * 有關如何取得授權的詳細說明，請參見 [存取您的 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license)。

      * 要瞭解更多如何根據您的需求選擇合適的授權類型，請參考 [SDK 簡介](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)。


<span id="lsi-version"></span>
## 版本要求


* 要使用 **直播拉流** 功能，您必須使用 BytePlus MediaLive SDK。請記得在 [用戶端 SDK 元件](https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination) 頁面選擇正確的 SDK。


<span id="lsi-integrate"></span>
## 整合 SDK

將 `TTSDKFramework` 的 pull subspec 新增到您的 `Podfile` 中：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">要取得最新的版本號，請參見 <a href="https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination">用戶端 SDK 元件</a>。</div>


```Ruby
$TT_SDK_VERSION = '1.50.200.2-premium'
pod 'TTSDKFramework', $TT_SDK_VERSION, :subspecs => ['LivePull-RTS']
```


然後執行 `pod install`。

<span id="lsi-impl"></span>
## 實現

<span id="lsi-player"></span>
### 步驟 1: 建立播放器

使用 BytePlus MediaLive SDK 建立一個直播播放器實例，並設定其 delegate 以接收播放回呼。

```Swift
let player = TVLManager(type: VeLivePlayerTypeOwn)
```


<span id="lsi-pull"></span>
### 步驟 2: 拉流

為選定的機位和畫質設定拉流 URL，然後開始播放。要使用低延遲 FLV，請在播放前啟用低延遲 FLV 選項。

<span id="lsi-switch"></span>
### 步驟 3: 切換機位和畫質

當觀眾選擇不同的機位或畫質檔位時，將播放器重新繫結到相應的拉流 URL。當同一源有多個協議或畫質檔位可用時，請選擇與觀眾選擇相匹配的 URL。

<span id="lsi-interact"></span>
### 步驟 4: 新增互動功能

在播放檢視之上疊加互動 UI（禮物、評論和彈幕、點讚），並提供用於全螢幕觀看的橫螢幕模式。

<span id="lsi-code"></span>
## 範例程式碼

請參考 Demo 原始碼，將此功能整合到您的應用中。


* iOS：[LiveSportStreaming](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/LiveSportStreaming)
