---
title: "iOS 動態庫升級指南"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ios-dynamic-library-upgrade-guide-zh-TW"
---

要將 iOS Player SDK 的動態庫升級至 1.40.200 或更高版本，請依照以下說明操作。本主題涵蓋從舊版動態庫升級，以及從靜態庫切換至動態庫的操作。

<span id="fd6edce5"></span>
## 新版本的優勢

與 1.39.300 及更早版本相比，動態庫的新版本具有以下優點：


* SDK 套件體積更小。

* 依賴項與靜態庫保持一致，方便動態庫與靜態庫間切換。

* 標頭檔案的導入方式現已與標準系統動態庫一致。


<span id="a71d1f66"></span>
## 從舊版動態庫升級

若已集成 1.39.300 或更早版本的動態庫，可按照以下步驟升級至 1.40.200 及以上版本。


1. 保持原有的 CocoaPods 集成方式。若需減少 SDK 套件體積，可將 subspec 名稱更改為 [Integrating the SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios) 中列出的名稱。例如，集成拉流功能時，可將 `subspecs => ["BasePull"]` 改為 `subspecs => ["LivePull"]`。

2. 為避免升級後標頭檔案導入錯誤，可透過以下兩種方式修改專案程式碼。

   * 方式一：修改標頭檔案的導入方式。

      * 若以 `#import <xxx/xxx.h>` 導入，請全部替換為 `#import <TTSDKFramework/xxx.h>`。

      * 若導入子模組的標頭檔案，如 `#import <TTSDKPUFramework/TTSDKPUFramework.h`，請替換為 `#import <TTSDKFramework/TTSDKFramework.h>`。

   * 方式二：在 Podfile 中新增環境變數 `ENV['TTSDK_FRAMEWORK_MODULE_NAME'] = 'PREVIOUS_FRAMEWORK'`。將 `PREVIOUS_FRAMEWORK` 替換為現有框架的名稱。


<span id="4b65c91c"></span>
## 從靜態庫切換至動態庫

若已集成靜態庫，可依照以下步驟切換至 1.40.200 及以上版本的動態庫：


1. 修改 CocoaPods 集成方式，將 pod 名稱從 `TTSDK` 改為 `TTSDKFramework`。例如，將 `pod 'TTSDK', :subspecs => ['LivePull-RTS']` 改為 `pod 'TTSDKFramework', :subspecs => ['LivePull-RTS']`。

2. 修改標頭檔案的導入方式。

   * 若以 `#import "xxx.h"` 導入，無需修改程式碼。

   * 若以 `#import <TTSDK/xxx.h>` 導入，可透過以下兩種方式修改專案程式碼：

      * 方式一（推薦）：在 Podfile 中新增環境變數設定 `ENV['TTSDK_FRAMEWORK_MODULE_NAME'] = 'TTSDK'`。

      * 方式二：將所有 `#import <TTSDK/xxx.h>` 替換為 `#import <TTSDKFramework/xxx.h>`。
