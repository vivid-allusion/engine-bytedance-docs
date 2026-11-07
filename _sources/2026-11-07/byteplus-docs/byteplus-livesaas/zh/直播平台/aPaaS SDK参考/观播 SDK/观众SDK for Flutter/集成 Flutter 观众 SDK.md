---
title: "集成 Flutter 观众 SDK"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-flutter-zh-CN"
---

为在你的 Flutter 应用中实现直播和点播回放功能，本指南提供集成观众 SDK 的分步操作说明。请按照以下步骤添加依赖项，配置 Android 和 iOS 的平台相关设置，并添加所需的许可证文件，以准备项目开发。

<span id="60f21c26"></span>
## 系统要求


* Flutter 版本：Flutter stable channel 3.0.0 或更高版本

* Dart 版本：Dart 2.17.0 及以上

* 系统版本：

   * iOS 12.0 及以上

   * Android 5.0（minSdkVersion: 21）及以上

* 开发工具：Visual Studio Code 或 Android Studio（建议使用最新版本）


<span id="494cbce1"></span>
## 前提条件

请联系 BytePlus Live 技术支持，获取你的直播和点播许可证文件、用于申请许可证的应用名称，以及生成的应用 ID。

<span id="da55573e"></span>
## 项目结构

Flutter 观众 SDK 的项目结构如下。

```Shell
├── CHANGELOG.md
├── LICENSE
├── README.md
├── analysis_options.yaml
├── android
├── example
├── ios
├── lib
├── pubspec.lock
└── pubspec.yaml
```


主要目录及其对应说明如下。


|目录 |接口行为 |必需 |
|---|---|---|
|lib |基于原生SDK构建的Flutter插件层。 |是 |
|android |Android的原生代码。 |是 |
|ios |iOS的原生代码。 |是 |
|example |使用Flutter构建的完整直播间演示。 |否 |


<span id="f27e47f0"></span>
## 集成步骤

<span id="a40a1392"></span>
### Step 1: Add dependencies

目前，Flutter 观众 SDK 仅支持本地依赖。


1. 点击[此处](https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/release/flutter/1.65.0/bdlive-flutter-viewer.zip)下载最新版本的 SDK 包到本地环境并解压。

2. 将 SDK 文件夹复制到你的项目目录。

3. 在`pubspec.yaml`文件中，按如下方式添加`bdlive_flutter_viewer`依赖项。

   ```YAML
   dependencies:
       flutter:
           sdk: flutter
       # 将<SDK_PATH>替换为项目中SDK的文件路径。
       bdlive_flutter_viewer: 
           path: <SDK_PATH>
   ```
   


<span id="c7fc6e43"></span>
### Step 2: Platform configuration

配置 Android 和 iOS 的相关设置。

<span id="43fb4df8"></span>
#### Android


1. 打开`build.gradle`文件（位于`app`目录），并添加以下配置。

   ```Groovy
   android {
       defaultConfig {
           minSdkVersion 21
           ndk {
           // Recommended CPU architectures to filter.
               abiFilters "arm64-v8a"
           }
       } 
    
      // Enable data binding.
       buildFeatures {
           dataBinding true
       }
   } 
   ```
   

2. 打开`AndroidManifest.xml`文件（位于`app`目录），并添加以下权限。

   ```XML
   <!-- 访问本地存储 -->
   <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
   <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
   
   <!-- 网络状态 -->
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
   <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE"/>
   <uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>
   
   <!-- 系统悬浮窗 -->
   <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
   
   <!-- 日历 --> 
   <uses-permission android:name="android.permission.READ_CALENDAR"/> 
   <uses-permission android:name="android.permission.WRITE_CALENDAR"/>
   ```
   

3. 打开`proguard-rules.pro`文件（位于`app`目录），并添加以下混淆规则。

   ```XML
   -keep class com.pandora.**{*;}
   -keep class com.ss.**{*;} 
   -keep class com.bytedance.**{*;}
   -keep class com.pandora.ttlicense2.**{*;}
   -keep class com.bytertc.**{*;}
   -keep class org.webrtc.**{*;}
   -keep class log.**{*;}
   ```
   


<span id="08ea213e"></span>
#### iOS


1. 打开终端窗口，运行命令`cd`，进入你的 iOS 项目目录。运行命令`pod install`以安装依赖项。

2. 在 Xcode 的应用 target 下，完成以下步骤：

   1. 打开`info.plist`文件，添加参数`SSAppID`，并将参数值设置为你已批准许可证申请的应用 ID。

   2. 在`info.plist`文件中，通过以下方式之一添加权限：

      * 点击\*\*+ **，添加 ** **`NSPhotoLibraryAddUsageDescription`** ** 键（显示为**Privacy \- Photo Library Additions Usage Description\*\*）和 `NSCalendarsUsageDescription` 键（显示为**Privacy \- Calendars Usage Description**），选择**String**作为**Type**，然后在**Value**中输入系统授权弹窗显示的提示信息。

      * 以源码模式打开`info.plist`文件，添加以下键值对和字符串。你可以自定义字符串的值作为系统授权弹窗显示的提示信息。

         ```JavaScript
         <!-- Write access to photo library -->
         <key>NSPhotoLibraryAddUsageDescription</key> 
         <string>The app needs permission to save images to your photo library. 
         <!-- 日历写入权限 -->
         <key>NSCalendarsUsageDescription</key>
         <string>Used to remind viewers before live stream starts</string>
         ```
         

3. （可选）如需应用在后台运行时继续播放音频，或需要使用画中画（PiP）功能，请完成以下步骤：

   1. 在**Signing & Capabilities**标签下点击\*\*+ Capability\*\*，并双击添加**Background Modes**。

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_acd720b361e33d38cd9d34fa8778bc0c.png) </span>

   2. 在**Background Modes**部分，勾选**Audio, AirPlay, and Picture in Picture**复选框。

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7fd45366e83df22b9d668b0df54fb16.png) </span>

4. （可选）如果你的 iOS 项目启用了 Bitcode，则需要关闭 Bitcode。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b66610c96ad455dbc270fdfb55f28a6~tplv-goo7wpa0wc-image.image) </span>

   1. 点击**Build Settings**标签。

   2. 在**Build Options**部分，将**Enable Bitcode**设置为**No**。

5. 配置在全屏模式下播放在线流、预告或回放时支持的屏幕方向。

   1. 点击**General**标签页。

   2. 在**Deployment Info**部分，为**iPhone Orientation**和**iPad Orientation**选择**Portrait**和**Landscape Right**复选框。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d945974cbdbe4e50b94b1d69391ea5b0~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">要实现全屏模式下屏幕在横屏方向间自动旋转，需满足以下条件：   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">观众设备的竖屏方向锁已关闭。关于如何关闭竖屏方向锁，请参见<a href="https://support.apple.com/en-us/118226">官方Apple文档</a>。   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">在Deployment Info部分，Landscape Left和Landscape Right复选框均已选中。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">为避免观众点击全屏按钮时出现全屏动画显示异常，请确保选中Landscape Right复选框。   </div>
   


<span id="c6ec173e"></span>
### Step 3: 添加许可证文件


1. 将获取到的在线流许可证文件和点播许可证文件放入你的Flutter项目中。以下示例将文件放置在项目根目录下的`assets`文件夹中。

   ```YAML
   ├── assets
   │   ├── live.lic
   │   └── vod.lic
   ├── pubspec.yaml
   ```
   

2. 在`pubspec.yaml`文件中，将许可证文件路径添加到`assets`下。

   ```YAML
    assets:
     - assets/live.lic
     - assets/vod.lic
   ```
   

3. 初始化SDK时，必须传递许可证文件的路径。更多信息，请参见[Initializing the SDK](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation#a4ab4a00)。


<span id="77ab57b8"></span>
## 包体大小


* iOS

   对于iOS，包体大小指：

   * 集成后压缩IPA文件大小的增加量。这是集成SDK前后文件大小的差值。

   * 集成后未压缩IPA文件大小的增加量。这是集成SDK前后文件大小的差值。

      压缩IPA文件大小代表你的应用的下载大小，未压缩IPA文件大小对应设备上已安装应用的大小。

      设备上的实际未压缩IPA文件大小比下表列出的数值更小，因为安装时只保留适用于当前设备的资源。

   
   |版本 |增量压缩IPA文件大小 |增量未压缩IPA文件大小 |
   |---|---|---|
   |1.58.0\-1 |约30.8 MB |约64.7 MB |
   

* Android

   对于Android，指集成SDK后APK文件大小的增加量。即集成前后APK大小的差值。

   以下数据基于应用仅支持arm64\-v8a CPU架构。

   若你的应用支持多种CPU架构，包体大小会相应增加。

   
   |版本 |增量包体大小 |
   |---|---|
   |1.58.0\-1 |约19.4 MB |
   


<span id="fbb6c796"></span>
## 后续步骤

关于如何在Flutter中使用观众SDK，例如加入和离开直播间，详见[Feature implementation](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation)。
