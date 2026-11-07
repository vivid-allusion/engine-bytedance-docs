---
title: "執行 VeLiveQuickStartDemo（適用於 React Native）"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-rn-zh-TW"
---

為了探索 BytePlus MediaLive SDK 的功能，您可以在已整合 React Native SDK 的應用程式上執行 VeLiveQuickStartDemo。本主題中的步驟將協助您成功執行此範例。

<span id="a21722ee"></span>
## 系統需求


* 開發用的配置描述檔

* React Native 0.73.0 及以上版本

* Android

   * Android 5.0（SDK API 等級 21）或更高版本

   * Android Studio 4.0 或更高版本

   * 一台運行 Android 5.0 或更高版本的實體 Android 裝置

   * 請確保 CPU 架構為 armeabi\-v7a 或 arm64\-v8a

* iOS

   * Xcode 14.0 或更高版本

   * CocoaPods 1.11.3 或更高版本

   * 一台運行 iOS 11.0 或更高版本的實體 iOS 裝置


<span id="ed62ded1"></span>
## 先決條件

在開始之前，請完成以下任務：


* 註冊 BytePlus 帳戶。如需詳細操作說明，請參考 [註冊並驗證 BytePlus 帳戶](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account)。

* 啟用 BytePlus MediaLive 服務，並在控制台中新增推流與拉流的域名。詳細操作請參考 [開始使用 BytePlus MediaLive](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-zh-TW)。


<span id="073dc5e5"></span>
## 準備工作

在執行範例前，您需要準備 SDK 授權、App ID 及 token 資訊。

<span id="ba69c964"></span>
### **下載 MediaLive SDK 授權**

請依照 [SDK 管理](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)中的指引建立 SDK 應用，並下載相應的 SDK 授權。請記錄 App ID 與 bundle ID 以備後用。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bea7ca3024e46998c225be78e7dff60~tplv-goo7wpa0wc-image.image) </span>

<span id="ec13e57b"></span>
## 執行範例

本節將介紹設定與執行範例的詳細步驟。

<span id="9dde0df8"></span>
### 下載原始碼

請透過 [提交工單](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)聯繫技術支援以取得範例原始碼。

<span id="bb219e9f"></span>
### 整合 SDK 授權


1. 將下載的 MediaLive SDK 授權檔案重新命名為 `ttsdk.lic`。

2. 將 `ttsdk.lic` 檔案替換至 `android/app/src/main/assets/` 與 `ios` 目錄，使用您自己的 SDK 授權。

   * Android

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_044c1ec77126f9426239e8b66c25c310.jpg) </span>

   * iOS

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_837d406299865f1c08b552e8cdece2ce.jpg) </span>


<span id="0212a64a"></span>
### Gradle 同步


1. 在 Android Studio 中開啟 `Android/VeLiveQuickStartDemo`。

2. 點擊 **Sync Project with Gradle Files**。

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5cc7b8c264de379a8e295f701c75bee2.png) </span>


<span id="80b9feb1"></span>
### 更新 CocoaPods 資料庫


1. 開啟 Terminal，並將目前目錄切換至 `ios`。

2. 執行 `pod install --repo-update`，以更新本地 CocoaPods 資料庫並安裝專案依賴項。


<span id="6e21bd77"></span>
### 配置推流與拉流


* 若您整合推流與拉流，或僅整合推流，請開啟 `src/store/push/pusher.ts` 檔案並進行以下修改。

   ```JavaScript
   // 使用推流或同時使用推流與拉流
   import {initEnv} from '@byteplus/react-native-live-push';
   
   initEnv({
     AppID: 'appId', // App ID，您可以在 MediaLive 控制台的 SDK 管理頁面取得。
     // 請設定 iOS 的 bundle ID 或 Android 的 package name。
     AppName: 'xxx'
     })
   
     // The channel through which to download the app.您也可以使用此參數區分不同環境的應用建置，例如正式、測試與除錯。
     AppChannel: Platform.select({
         android: 'GoogleStore',
         ios: 'AppStore',
         default: ''
     }),
   
     // The version number of your Android app.有效的版本號需包含兩個或以上分隔符，例如「1.3.2」。
     AppVersion: '1.0.0',
     
     // 授權檔案名稱。若您更換授權檔案，需在此處修改檔案名稱。為了快速驗證 SDK，您可以替換原始授權檔案（ttsdk.lic）的內容。
     LicenseUri: {
       android: 'assets:///ttsdk.lic', 
       ios: 'ttsdk.lic'
     },
     UserUniqueID: 'VeLiveQuickStartDemo',
   });
   ```
   

* 若您僅整合拉流，請開啟 `src/store/pull/player.ts` 檔案並進行以下修改。

   ```JavaScript
   // 僅使用拉流
   import {initEnv} from '@byteplus/react-native-live-pull';
   
   initEnv({
     AppID: 'appId', // App ID，你可以在 MediaLive 控制台的 SDK 管理頁面取得。
     // 請設定 iOS 的 bundle ID 或 Android 的 package name。
     AppName: Platform.select({
         android: 'xxx', 
         ios: 'xxx'
     })
   
     // The channel through which to download the app.你也可以使用此參數來區分不同環境的應用程式建置，例如正式環境、測試環境與除錯環境。
     AppChannel: Platform.select({
         android: 'GoogleStore',
         ios: 'AppStore',
         default: ''
     }),
   
     // The version number of your Android app.有效的版本號應包含兩個或以上的分隔符號，例如「1.3.2」。
     AppVersion: '1.0.0',
     
     // 授權檔案名稱。若更換授權檔案，需在此修改檔案名稱。為快速驗證 SDK，你可以替換原始授權檔案（ttsdk.lic）的內容。
     LicenseUri: {
       android: 'assets:///ttsdk.lic', 
       ios: 'ttsdk.lic'
     },
     UserUniqueID: 'VeLiveQuickStartDemo',
   });
   ```
   


<span id="266db972"></span>
### 編譯範例

請參考 [React Native 文件](https://reactnative.dev/docs/running-on-device)。
