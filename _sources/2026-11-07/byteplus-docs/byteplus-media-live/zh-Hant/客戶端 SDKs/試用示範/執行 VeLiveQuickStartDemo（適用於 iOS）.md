---
title: "執行 VeLiveQuickStartDemo（適用於 iOS）"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-ios-zh-TW"
---

若要探索 BytePlus MediaLive SDK 的功能，您可以在 iOS 裝置上執行 VeLiveQuickStartDemo。本主題中的步驟將協助您成功編譯並啟動此示範程式，展示基本的推流與拉流、進階功能如自適應碼率，以及互動功能例如與觀眾連麥和主播 PK 對戰。

VeLiveQuickStartDemo 包含三種類型的功能：


* 基本功能，包括推流與拉流。

* 進階功能，包括：

   * 自適應碼率

   * 推送外部音訊與視訊來源

   * H.265 硬體編碼

   * 子母畫面（PiP）

* 互動直播功能，包括與觀眾連麥及主播 PK 對戰。


<span id="208fe723"></span>
## 系統需求


* Xcode 14.0 或以上版本

* CocoaPods 1.11.3 或以上版本

* 運行 iOS 11.0 或以上版本的實體 iOS 裝置

* 開發用的簽發描述檔


<span id="4cff3e13"></span>
## 先決條件


* 註冊 BytePlus 帳號。詳細操作請參考 [註冊並驗證 BytePlus 帳號](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account)。

* 啟用 BytePlus MediaLive 服務，並在控制台新增推流與拉流的網域名稱。詳細操作請參考 [開始使用 BytePlus MediaLive](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-zh-TW)。

* 若要體驗互動直播功能，您還需啟用 BytePlus RTC 服務。詳細操作請參考 [啟用 RTC 服務](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865)。


<span id="66cf45e9"></span>
## 準備工作

在執行示範程式前，請取得 SDK 授權、App ID 及 Token 資訊。

<span id="96bcd67f"></span>
### 加速網域的配置


1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左側導覽窗格中，點擊 **網域名稱**。

3. 新增推流與拉流的網域名稱。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0dec0195bac047c384081882dfec2e64~tplv-goo7wpa0wc-image.image) </span>

<span id="9dacd3e8"></span>
### **下載 MediaLive 授權**

依照 [SDK 管理](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)中的指引建立 SDK 應用，並下載對應的 SDK 授權。請記錄 App ID 與 Bundle ID 以便後續使用。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bea7ca3024e46998c225be78e7dff60~tplv-goo7wpa0wc-image.image) </span>

<span id="9377cabf"></span>
### **取得 RTC App ID 與 App Key**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若你不打算測試互動直播功能，可略過此章節。</div>



1. 登入 [BytePlus RTC 控制台](https://console.byteplus.com/rtc/workplaceRTC)。

2. 在左側導覽窗格中，點擊 **應用管理**。

3. 點擊 **建立應用**，並在彈出的對話框中輸入您的應用名稱。將 **所屬專案**欄位維持預設值。

4. 點擊 **確定**以儲存設定。

5. 在應用列表中找到您的應用，並記錄 App ID 與 App Key。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b565075eda70420d85d70cc7cc950223~tplv-goo7wpa0wc-image.image) </span>


<span id="abc77f0b"></span>
## 執行示範程式

本節將介紹設定與執行示範程式的詳細步驟。

<span id="619e2c8e"></span>
### 下載原始碼


1. 前往 GitHub 並複製 [VeLiveQuickStartDemo](https://github.com/byteplus-sdk/VeLiveQuickStartDemo.git) 儲存庫。

2. 示範程式的目錄結構如下：

   ```Bash
   iOS/VeLiveQuickStartDemo
   └── VeLiveQuickStartDemo
       ├── App // Entry point of the demo app
       ├── Features // Features
       │   ├── Basic // Basic features
       │   │   ├── PullStream // Stream pulling
       │   │   └── PushCamera // Video capture and stream pushing
       │   ├── Advanced // Advanced features
       │   │   ├── PullRTM // Pulling an RTM stream
       │   │   ├── PushAutoBitrate // Adaptive bitrate
       │   │   ├── PushBeauty // Beauty AR and special effects
       │   │   ├── PushCustom // Pushing external audio and video sources
       │   │   ├── PushH265Codec // H.265 hardware encoding
       │   │   ├── PictureInPicture // PiP
       │   │   └── ScreenCapture // Screen recording and streaming
       │   └── Interact // Interactive live features
       │       ├── Link // Co-hosting with audience members
       │       ├── Manager // Common host and audience activities
       │       └── PK // Host PK battle
       ├── Helper // Utilities, such as SDK initialization and external video capture
   ```
   


<span id="6febb740"></span>
### 整合 SDK 授權


1. 將您下載的 MediaLive SDK 授權重新命名為 `ttsdk.lic`。

2. 將 `iOS/VeLiveQuickStartDemo/VeLiveQuickStartDemo/Resource/` 目錄下原有的 `ttsdk.lic` 檔案替換為您自己的 SDK 授權。


<span id="055049ad"></span>
### 更新 Cocoapods 倉庫


1. 開啟 Terminal，並切換目前目錄至 `iOS/VeLiveQuickStartDemo`。

2. 執行 `pod install --repo-update`，以更新本地 Cocoapods 倉庫並安裝專案依賴項。


<span id="817a8f22"></span>
### 推流與拉流的配置


1. 在專案根目錄下，於 Xcode 中開啟 `VeLiveQuickStartDemo.xcworkspace` 檔案。

2. 於專案樹狀視圖中，定位至 `VeLiveQuickStartDemo/Helper`，並開啟 `VeLiveSDKHelper.h` 檔案。

3. 完成以下配置。

   ```Java
   // The app ID
   #define TTSDK_APP_ID @"53**10"
   
   // 授權檔案名稱。若你更換授權檔案，需在此修改檔案名稱。為快速驗證 SDK，你可以替換原始授權檔案（ttsdk.lic）的內容。
   #define TTSDK_LICENSE_NAME @"ttsdk.lic"
   
   // 設定 AccessKey ID 與 AccessKey secret，用於 API 請求驗證。
   #define ACCESS_KEY_ID @""
   #define SECRET_ACCESS_KEY @""
   
   // 域名空間
   #define LIVE_VHOST @"push.example.com"
   
   /* 
   * 推流與拉流地址範例 ：https://{DomainName}/{AppName}/{StreamName}.flv
   * 推流與拉流地址中的 AppName 支援大小寫字母、數字、底線</a> (_)、連字號 (-)，最長 30 字元。例如 live
   */
   #define LIVE_APP_NAME @"live"
   
   // 設定推流用的域名g
   #define LIVE_PUSH_DOMAIN @"push.example.com"
   
   // 設定拉流用的域名g
   #define LIVE_PULL_DOMAIN @"pull.example.com"
   ```
   


<span id="ca1f9885"></span>
### 多人連麥與主播 PK 對戰的配置


1. 於 Xcode 中開啟 `VeLiveQuickStartDemo/Helper/VeLiveSDKHelper.h` 檔案。

2. 輸入 RTC App ID 與 App Key。


```Java
// The RTC app ID
#define RTC_APPID @""

// The RTC app key
#define RTC_APPKEY @""
```


<span id="fa7c2a86"></span>
### 專案配置


1. 在 Xcode 的專案編輯器中選擇目標。

2. 點擊 **簽名與功能**。

3. 將 **Bundle Identifier** 設為你在 [Downloading a MediaLive license](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-ios#9dacd3e8) 章節中準備的值。

4. 選擇開發用的 Provisioning Profile。


<span id="36503b02"></span>
### 設定 bundle ID


1. 開啟 `VeLiveQuickStartDemo/VeLiveQuickStartDemo.xcworkspace`。

2. 修改配置檔 Podfile，以啟用或停用螢幕錄製與串流功能。若你修改此變數，必須重新執行 pod install。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/797eb2573d214d16b54cd219d1c99b98~tplv-goo7wpa0wc-image.image) </span>

3. 修改主專案 App 及螢幕錄製與串流 extension 的 Bundle Identifier 與 GroupID 設定。

   1. 將主專案 App 的 Bundle Identifier 修改為建立 BytePlus MediaLive 應用時指定的 bundle ID。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0db405f62f804ed09064860e242007dd~tplv-goo7wpa0wc-image.image) </span>

   2. 修改螢幕錄製與串流 extension 的 Bundle Identifier。此 Bundle Identifier 必須以 App 的 Bundle Identifier 為前綴。若已停用螢幕錄製與串流功能，可略過此步驟。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b20ab98536c44e79fba177d165090ef~tplv-goo7wpa0wc-image.image) </span>

   3. 修改 GroupID 設定。若未啟用螢幕錄製與串流功能，可略過此步驟。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6bee18d237a4a36b128947b50b1ff63~tplv-goo7wpa0wc-image.image) </span>

4. 選擇主專案的開發簽名檔（Provisioning Profile）。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27fb2efe3b704291bdb9f9cfde43c237~tplv-goo7wpa0wc-image.image) </span>

5. 選擇螢幕錄製與串流 extension 的開發簽名檔（Provisioning Profile）。若未啟用螢幕錄製與串流功能，可略過此步驟。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b590d748ec32437a9d8b55203e108af4~tplv-goo7wpa0wc-image.image) </span>


<span id="6e1c77df"></span>
### 編譯 demo


1. 將你在 [Prerequisites](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-ios#4cff3e13) 章節準備的實體 iOS 裝置連接至電腦，並於 Xcode 設定為目標裝置。

2. 點擊 **Run** 以開始編譯流程。


若編譯流程無錯誤完成，demo app 將安裝於已連接的行動裝置。
