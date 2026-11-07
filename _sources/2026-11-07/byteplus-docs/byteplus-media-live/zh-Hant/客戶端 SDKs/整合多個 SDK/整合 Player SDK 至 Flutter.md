---
title: "整合 Player SDK 至 Flutter"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter-zh-TW"
---

本主題說明如何將 Player SDK for Flutter 整合至您的應用程式。

<span id="c8bc54ac"></span>
## 開發環境需求


* Flutter 版本：Flutter stable channel 3.0.0 或以上

* Dart 版本：Dart 2.17.0 或以上

* 系統版本：

   * 運行 iOS 11.0 或以上的實體裝置

   * 運行 Android 5.0（minSdkVersion: 21）或以上的實體裝置

* 開發工具：Visual Studio Code 或 Android Studio（建議使用最新版本）


<span id="bcda95b5"></span>
## 先決條件

您已建立 SDK 應用程式並取得 SDK 授權。如需更多資訊，請參閱 [取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-TW)。

<span id="addbcbfe"></span>
## 整合步驟

<span id="950f7a4d"></span>
### 步驟 1：新增相依性


1. 在 `pubspec.yaml` 檔案中，新增 `byteplus_live` 相依性如下：

   ```YAML
   dependencies:
     flutter:
       sdk: flutter
     byteplus_live: x.x.x
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">請將 <code>x.x.x</code> 替換為具體的 SDK 版本。建議您使用最新版本。如需版本號相關資訊，請參閱 <a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-release-notes-zh-TW">Player SDK for Flutter 發行說明</a>。   </div>
   

2. 開啟終端機視窗並執行 `cd` 指令，切換至您的 Flutter 專案目錄。執行 `flutter pub get` 指令以取得所有所需的專案相依性，並確保成功編譯與執行。


<span id="0de5bfe2"></span>
### 步驟 2：平台設定

設定 Android 與 iOS 的相關設定。

<span id="22c08d7f"></span>
#### Android


1. 開啟 `AndroidManifest.xml` 檔案（位於 `app` 目錄），宣告 SDK 所需的權限。

   ```XML
   <!-- Camera -->
   <uses-permission android:name="android.permission.CAMERA" />
   <!-- Recording --> 
   <uses-permission android:name="android.permission.RECORD_AUDIO" />
   <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
   <!-- Network status -->
   <uses-permission android:name="android.permission.INTERNET" />
   ```
   

2. 開啟 `proguard-rules.pro` 檔案（位於 `app` 目錄），新增以下混淆規則。

   ```XML
   -keep class com.pandora.**{*;}
   -keep class com.ss.**{*;} 
   -keep class com.bytedance.**{*;}
   -keep class com.pandora.ttlicense2.**{*;}
   -keep class com.bytertc.**{*;}
   -keep class log.**{*;}
   ```
   


<span id="29b43fe9"></span>
#### iOS


1. 在 Xcode 的 app target 中停用 Bitcode。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f0309bc1e2f428aa19208511b308682~tplv-goo7wpa0wc-image.image) </span>

   1. 點選 **Build Settings** 分頁。

   2. 於 **Build Options** 區段，將 **Enable Bitcode** 設為 **No**。

2. 開啟您的 iOS 專案的 `Podfile` 檔案，並新增以下來源。

   ```YAML
   source 'https://github.com/cocoapods/Specs.git'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">建議您使用 CocoaPods 1.11.0 或以上版本。若您的 iOS 專案尚未使用 CocoaPods，請於 iOS 專案根目錄執行 <code>pod init && pod install</code> 指令，以建立 <code>Podfile</code> 檔案。   </div>
   

3. 開啟終端機視窗並執行 `cd` 指令，切換至您的 iOS 專案目錄。然後執行 `pod install` 指令。


<span id="8841c34f"></span>
### 步驟 3：新增授權檔案


1. 將您取得的授權檔案放入您的 Flutter 專案中。以下範例將授權檔案放置於專案根目錄下的 `assets` 資料夾。

   ```YAML
   ├── assets
   │   └── live.lic
   ├── pubspec.yaml
   ```
   

2. 在 `pubspec.yaml` 檔案中，於 `assets` 下新增授權檔案的路徑。

   ```YAML
   assets:
     - assets/live.lic
   ```
   

3. 初始化 SDK 時，必須傳入授權檔案的路徑。如需更多資訊，請參閱 [初始化 Flutter 的 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter-zh-TW)。


<span id="c2391fea"></span>
## 後續步驟

初始化 Player SDK for Flutter。如需更多資訊，請參閱 [初始化 Flutter 的 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter-zh-TW)。
