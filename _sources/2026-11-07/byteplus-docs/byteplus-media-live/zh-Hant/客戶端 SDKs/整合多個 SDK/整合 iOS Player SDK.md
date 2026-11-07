---
title: "整合 iOS Player SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios-zh-TW"
---

本主題介紹如何整合 iOS Player SDK。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本指南涵蓋 SDK 1.40.200 及以上版本。若你已整合舊版 SDK，可參考 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-ios-dynamic-library-upgrade-guide">iOS 動態函式庫升級指南</a>，了解升級或從靜態函式庫切換至動態函式庫的操作說明。</div>


<span id="2178b17a"></span>
## 系統需求


* 運行 iOS 11.0 或更高版本的實體裝置

* Xcode 14.1 或更高版本


<span id="43e22af2"></span>
## 先決條件

你已建立 SDK 應用程式並取得 SDK 授權。如需更多資訊，請參閱 [取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-TW)。

<span id="d2f677b3"></span>
## 整合 SDK

你可以透過以下任一方法整合 SDK：


* 自動整合（推薦）：使用 CocoaPods 或 Swift Package Manager（SPM）自動下載 SDK 套件。對於 CocoaPods，你可以選擇整合動態函式庫或靜態函式庫；而 SPM 僅能整合動態函式庫。

* 手動整合：[聯絡你的技術支援](https://console.byteplus.com/workorder/create)以獲得手動整合 SDK 的協助。


本節說明如何自動整合 SDK。


<Tabs>
<Tab zoneid="X7CuwAw3MV" title="使用 CocoaPod">
<TabTitle>使用 CocoaPod</TabTitle>

<span id="e266c047"></span>
### 整合動態函式庫（推薦）

<span id="64362f11"></span>
#### 步驟 1：安裝 CocoaPods

在你的 Mac 上安裝 Ruby，並於終端機執行以下指令以安裝 CocoaPods。

```Ruby
sudo gem install cocoapods
```


<span id="5fb664bc"></span>
#### 步驟 2：建立 Podfile

於專案目錄執行以下指令以建立 Podfile。

```Ruby
pod init
```


<span id="22dee6b4"></span>
#### 步驟 3：新增相依項目

將以下程式碼新增至你的 Podfile。

```Ruby
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
pod 'TTSDKFramework', 'x.x.x.x-premium', :subspecs => ['LivePull']
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">請將 <code>x.x.x.x-premium</code> 替換為具體的 SDK 版本。建議你使用最新版本。如需版本號相關資訊，請參閱 <a href="https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes-zh-TW">iOS 版 Player SDK 發行說明</a>。</div>


* <div data-tips="true" data-tips-type="tip">若要拉取 RTM 協定的串流，請用 <code>'LivePull-RTS'</code> 替代 <code>'LivePull'</code>：<code>pod 'TTSDKFramework', 'x.x.x.x-premium', :subspecs => ['LivePull-RTS']</code>。</div>


* <div data-tips="true" data-tips-type="tip">自 1.51.300.2\-premium 版本起，若需使用超解析度（SR）及影片銳化功能，請在 <code>'LivePull'</code> 外加上 <code>'LivePull-BMF'</code>：<code>pod 'TTSDKFramework', 'x.x.x.x-premium', :subspecs => ['LivePull', 'LivePull-BMF']</code>。</div>



<span id="627e080c"></span>
#### 步驟 4：安裝 SDK

於終端機執行以下指令，以安裝 Podfile 指定的 SDK 相依項目。

```Plain
pod install
```


<span id="cd337301"></span>
### 整合靜態函式庫

若要整合靜態函式庫，請依照動態函式庫的步驟操作，但 pod 名稱請使用 TTSDK 而非 TTSDKFramework。

```Ruby
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
pod 'TTSDK', 'x.x.x.x-premium', :subspecs => ['LivePull']
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">請將 <code>x.x.x.x-premium</code> 替換為具體的 SDK 版本。建議你使用最新版本。如需版本號相關資訊，請參閱 <a href="https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes-zh-TW">iOS 版 Player SDK 發行說明</a>。</div>


* <div data-tips="true" data-tips-type="tip">若要使用 RTM 協定拉流，請使用 <code>'LivePull-RTS'</code> 取代 <code>'LivePull'</code>：<code>pod 'TTSDK', 'x.x.x.x-premium', :subspecs => ['LivePull-RTS']</code>。</div>


* <div data-tips="true" data-tips-type="tip">自 1.51.300.2\-premium 版本起，若要使用超解析度（SR）和影片銳化功能，除了 <code>'LivePull'</code> 外，還需新增 <code>'LivePull-BMF'</code>：<code>pod 'TTSDK', 'x.x.x.x-premium', :subspecs => ['LivePull', 'LivePull-BMF']</code>。</div>



</Tab>
<Tab zoneid="ZE0xs6Sejt" title="使用 SPM">
<TabTitle>使用 SPM</TabTitle>

1. 在你的 Xcode 專案中，於 **Package Dependencies** 標籤下點擊  **+**  按鈕。

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b6519c733fb4d17a41f535fab1039da~tplv-goo7wpa0wc-image.image" width="2516px" />   </div>
   

2. 於彈出視窗右上角輸入 `git@github.com:byteplus-sdk/TTSDK_BytePlus_SPM.git`。然後，輸入你要整合的 SDK 版本，並點擊 **Add Package** 以新增 TTSDK 相依項目。

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f2260bdeb5c41fea0aa4a023aaa4ccf~tplv-goo7wpa0wc-image.image" width="1872px" />   </div>
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">建議您將 <strong>Exact Version</strong> 設為 <strong>Dependency Rule</strong>。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">僅能指定支援 SPM 整合的 SDK 版本。如需瞭解特定版本的更多資訊，請參見 <a href="https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes-zh-TW">iOS 版 Player SDK 發行說明</a>。   </div>
   

3. 選擇所需元件後，點擊 **Add Package**，將其加入你的目標。

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f922aa76e474e02b625c653262b3c3d~tplv-goo7wpa0wc-image.image" width="1312px" />   </div>
   

   你可以為 BytePlus MediaLive SDK 選擇以下元件：

   * `TTSDK_LivePull`：使用 FLV、HLS 或 RTMP 協定拉取直播串流。

   * `TTSDK_LivePull-RTS`：使用 FLV、HLS、RTMP 或 RTM 協定拉取直播串流。


</Tab>
</Tabs>


<span id="bee4f6c1"></span>
## 新增授權檔案

將授權檔案複製到你的專案目錄。你在 SDK 初始化時需要此檔案路徑。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">請確保授權檔案所綁定的 bundle ID 與 app ID 與你的專案一致。否則授權驗證將失敗。</div>
