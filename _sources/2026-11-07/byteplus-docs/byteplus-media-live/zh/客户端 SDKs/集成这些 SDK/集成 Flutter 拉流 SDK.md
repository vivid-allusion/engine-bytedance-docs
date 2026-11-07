---
title: "集成 Flutter 拉流 SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter-zh-CN"
---

本主题介绍如何将 Flutter 拉流 SDK 集成到您的应用中。

<span id="c8bc54ac"></span>
## 开发环境要求


* Flutter 版本：Flutter stable channel 3.0.0 或更高版本

* Dart 版本：Dart 2.17.0 或更高版本

* 系统版本：

   * 运行 iOS 11.0 或更高版本的物理设备

   * 运行 Android 5.0（minSdkVersion: 21）或更高版本的物理设备

* 开发工具：Visual Studio Code 或 Android Studio（建议使用最新版本）


<span id="bcda95b5"></span>
## 前提条件

您已创建 SDK 应用并获得 SDK 许可证。更多信息，请参见 [获取您的 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-CN)。

<span id="addbcbfe"></span>
## 集成步骤

<span id="950f7a4d"></span>
### 步骤 1：添加依赖项


1. 在 `pubspec.yaml` 文件中，按如下方式添加 `byteplus_live` 依赖项：

   ```YAML
   dependencies:
     flutter:
       sdk: flutter
     byteplus_live: x.x.x
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">将 <code>x.x.x</code> 替换为具体的 SDK 版本号。建议您使用最新版本。关于版本号的更多信息，请参见 <a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-release-notes-zh-CN">Flutter 拉流 SDK 发布说明</a>。   </div>
   

2. 打开终端窗口，运行命令 `cd`，进入您的 Flutter 项目目录。运行命令 `flutter pub get`，获取所有项目所需依赖项，并确保成功编译和运行。


<span id="0de5bfe2"></span>
### 步骤 2：平台配置

配置 Android 和 iOS 的相关设置。

<span id="22c08d7f"></span>
#### Android


1. 打开 `AndroidManifest.xml` 文件（位于 `app` 目录），声明 SDK 所需的权限。

   ```XML
   <!-- 相机 -->
   <uses-permission android:name="android.permission.CAMERA" />
   <!-- 录制 --> 
   <uses-permission android:name="android.permission.RECORD_AUDIO" />
   <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
   <!-- 网络类型状态 -->
   <uses-permission android:name="android.permission.INTERNET" />
   ```
   

2. 打开 `proguard-rules.pro` 文件（位于 `app` 目录），添加如下混淆规则。

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


1. 在 Xcode 的应用 target 中禁用 Bitcode。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f0309bc1e2f428aa19208511b308682~tplv-goo7wpa0wc-image.image) </span>

   1. 点击 **Build Settings** 标签页。

   2. 在 **Build Options** 部分，将 **Enable Bitcode** 设置为 **No**。

2. 打开 iOS 项目的 `Podfile` 文件，添加如下源。

   ```YAML
   source 'https://github.com/cocoapods/Specs.git'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">建议您使用 CocoaPods 1.11.0 或更高版本。如果您的 iOS 项目尚未使用 CocoaPods，请在 iOS 项目根目录下运行命令 <code>pod init && pod install</code>，以创建 <code>Podfile</code> 文件。   </div>
   

3. 打开终端窗口，运行命令 `cd`，进入您的 iOS 项目目录。然后，运行命令 `pod install`。


<span id="8841c34f"></span>
### 步骤 3：添加许可证文件


1. 将您获得的许可证文件放入 Flutter 项目中。以下示例将许可证文件放在项目根目录下的 `assets` 文件夹中。

   ```YAML
   ├── assets
   │   └── live.lic
   ├── pubspec.yaml
   ```
   

2. 在 `pubspec.yaml` 文件中，在 `assets` 下添加许可证文件的路径。

   ```YAML
   assets:
     - assets/live.lic
   ```
   

3. 初始化 SDK 时，必须传递许可证文件的路径。更多信息，请参见 [初始化 Flutter 版拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter-zh-CN)。


<span id="c2391fea"></span>
## 后续步骤

初始化 Flutter 拉流 SDK。更多信息，请参见 [初始化 Flutter 版拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter-zh-CN)。
