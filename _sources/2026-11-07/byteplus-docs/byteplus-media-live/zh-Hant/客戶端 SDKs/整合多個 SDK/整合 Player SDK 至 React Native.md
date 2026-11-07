---
title: "整合 Player SDK 至 React Native"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn-zh-TW"
---

本主題介紹如何將 Player SDK 整合至 React Native。

<span id="b1be2e82"></span>
## 系統需求


* React Native 0.70 或以上版本

* Node v16 或以上版本

* Android：

   * Android 4.3 或以上版本

   * CPU 架構：armeabi\-v7a 或 arm64\-v8a

* iOS 與 macOS：

   * 運行 iOS 11.0 或以上版本的實體裝置

   * Xcode 14.1 或以上版本

* 請確保您的專案具有有效的開發者簽名。

* 如需設定環境的說明，請參閱 [官方文件](https://reactnative.dev/docs/environment-setup)。


<span id="23566c94"></span>
## 先決條件

您已建立 SDK 應用程式並取得 SDK 授權。如需更多資訊，請參閱 [取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-TW)。

<span id="33c06caa"></span>
## 整合 SDK

請使用以下 npm 套件安裝 SDK。

```Plain
npm i @byteplus/react-native-live-pull
```


<span id="c7fa4b6f"></span>
### Step 1: 設定 Maven 儲存庫


1. 在 Android 根目錄中開啟 `build.gradle` 檔案。

2. 定義 Maven 儲存庫並設定儲存庫網址。

   ```Plain
   allprojects {
       repositories {
           google()
           mavenCentral()
           maven {
               url "https://artifact.bytedance.com/repository/Volcengine/"
           }
           maven {
               url "https://artifact.byteplus.com/repository/public/"
           }
       }
   }
   
   apply from: 'https://ve-vos.volccdn.com/script/vevos-repo-base.gradle'
   ```
   


<span id="75d013a7"></span>
### Step 2: 新增相依套件

將相依套件新增至您的 iOS Podfile。

```Plain
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
source 'https://cdn.cocoapods.org/'
```


<span id="db904c49"></span>
## 設定權限

<span id="07327795"></span>
### Android

在 `AndroidManifest.xml` 檔案中宣告應用程式所需的權限：

```Plain
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.INTERNET" />
```


<span id="22b41bb8"></span>
## 新增授權檔案

將授權檔案複製到您的專案目錄，並記錄授權檔案的路徑。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">請確保授權檔案所關聯的 bundle ID 與 app ID 與您的專案一致。否則，授權驗證將會失敗。</div>
