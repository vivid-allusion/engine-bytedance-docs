---
title: "初始化 Flutter 版拉流 SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter-zh-CN"
---

在使用 Flutter 版拉流 SDK 的功能前，必须先初始化该 SDK。本主题提供了必要的示例代码和配置步骤，帮助你使用应用信息和许可证正确初始化 SDK，确保其可用于回放。

<span id="e5519615"></span>
## 前提条件


* 你已集成 Flutter 版拉流 SDK。如需了解更多信息，请参见[集成 Flutter 拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter-zh-CN)。

* 你已获取应用 ID 及其他基本信息。如需了解更多信息，请参见[获取您的 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-CN)。


<span id="7b6eeb47"></span>
## 导入头文件

```Dart
import 'package:byteplus_live/velive_flutter_sdk.dart';
```


<span id="249e3e10"></span>
## 初始化 SDK

为确保正确初始化，建议在项目的`runApp`方法中初始化 SDK，main.dart 文件中。

```Java
TTSDKConfiguration config = TTSDKConfiguration(
  appID: 'APP_ID',// Replace APP_ID with the app ID.
  bundleID: 'BUNDLE_ID', // 将 BUNDLE_ID 替换为 iOS 应用的 bundle identifier。
  appName: 'APP_NAME', // 将 APP_NAME 替换为应用名称。
  channel: 'CHANNEL_NAME', // 将 CHANNEL_NAME 替换为下载应用的渠道名称，例如 App Store。
  licenseFilePath: 'LICENSE_PATH', // 将 LICENSE_PATH 替换为你的许可证文件路径，例如 assets/live.lic。
  appVersion: 'APP_VERSION',  // 将 APP_VERSION 替换为应用版本号。有效的版本号必须包含至少两个分隔符，例如 1.3.2。
);
VeLivePlayer.startWithConfiguration(config);
```


<span id="d5f62e90"></span>
## 后续步骤

如需了解如何使用 Flutter 版拉流 SDK，例如创建播放器、开始回放和配置视频缩放模式，请参见[Player SDK for Flutter: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-basic-features)。
