---
title: "初始化 Flutter 的 Player SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter-zh-TW"
---

在使用 Flutter 的 Player SDK 功能之前，必須先初始化 SDK。本主題提供必要的範例程式碼與配置步驟，協助你使用應用程式資訊與授權正確初始化 SDK，確保其可用於播放。

<span id="e5519615"></span>
## 先決條件


* 你已整合 Flutter 的 Player SDK。如需更多資訊，請參閱[整合 Player SDK 至 Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter-zh-TW)。

* 你已取得 app ID 及其他基本資訊。如需更多資訊，請參閱[取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-TW)。


<span id="7b6eeb47"></span>
## 導入標頭檔案

```Dart
import 'package:byteplus_live/velive_flutter_sdk.dart';
```


<span id="249e3e10"></span>
## 初始化 SDK

為確保正確初始化，建議於專案的 `runApp` 方法（位於 `main.dart`檔案）中初始化 SDK。

```Java
TTSDKConfiguration config = TTSDKConfiguration(
  appID: 'APP_ID',// Replace APP_ID with the app ID.
  bundleID: 'BUNDLE_ID', // 將 BUNDLE_ID 替換為 iOS 應用程式的 bundle identifier。
  appName: 'APP_NAME', // 將 APP_NAME 替換為應用程式名稱。
  channel: 'CHANNEL_NAME', // 將 CHANNEL_NAME 替換為下載應用程式的渠道名稱，例如 App Store。
  licenseFilePath: 'LICENSE_PATH', // 將 LICENSE_PATH 替換為授權檔案的路徑，例如 assets/live.lic。
  appVersion: 'APP_VERSION',  // 將 APP_VERSION 替換為應用程式版本。有效的版本號必須包含至少兩個分隔符，例如 1.3.2。
);
VeLivePlayer.startWithConfiguration(config);
```


<span id="d5f62e90"></span>
## 後續步驟

如需更多關於如何使用 Flutter 的 Player SDK，例如建立播放器、啟動播放及設定影片縮放模式，請參閱[Player SDK for Flutter: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-basic-features)。
