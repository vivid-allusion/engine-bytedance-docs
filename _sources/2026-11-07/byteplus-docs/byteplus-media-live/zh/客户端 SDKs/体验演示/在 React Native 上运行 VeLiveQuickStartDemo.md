---
title: "在 React Native 上运行 VeLiveQuickStartDemo"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-rn-zh-CN"
---

为探索 BytePlus MediaLive SDK 的功能，您可以在集成 React Native SDK 的应用上运行 VeLiveQuickStartDemo。本主题中的步骤将帮助您成功运行该演示。

<span id="a21722ee"></span>
## 系统要求


* 开发配置描述文件

* React Native 0.73.0 及以上版本

* Android

   * Android 5.0（SDK API Level 21）或更高版本

   * Android Studio 4.0 或更高版本

   * 运行 Android 5.0 或更高版本的实体 Android 设备

   * 确保 CPU 架构为 armeabi\-v7a 或 arm64\-v8a

* iOS

   * Xcode 14.0 或更高版本

   * CocoaPods 1.11.3 或更高版本

   * 运行 iOS 11.0 或更高版本的实体 iOS 设备


<span id="ed62ded1"></span>
## 前提条件

在开始之前，请完成以下任务：


* 注册 BytePlus 账号。详细操作说明请参见[注册并验证 BytePlus 账号](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account)。

* 开通 BytePlus MediaLive 服务，并在控制台添加用于推流和拉流的域名。详细操作说明请参见[BytePlus MediaLive 入门](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-zh-CN)。


<span id="073dc5e5"></span>
## 准备工作

在运行演示前，您需要准备 SDK 许可证、应用 ID 和 token 信息。

<span id="ba69c964"></span>
### **下载 MediaLive SDK 许可证**

按照[SDK 管理](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)中的说明创建 SDK 应用，然后下载对应的 SDK 许可证。请记录应用 ID 和 bundle ID，以备后续使用。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bea7ca3024e46998c225be78e7dff60~tplv-goo7wpa0wc-image.image) </span>

<span id="ec13e57b"></span>
## 运行演示

本节介绍设置和运行演示的详细步骤。

<span id="9dde0df8"></span>
### 下载源代码

请通过[提交工单](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)联系技术支持，获取演示源代码。

<span id="bb219e9f"></span>
### 集成 SDK 许可证


1. 将下载的 MediaLive SDK 许可证文件重命名为`ttsdk.lic`。

2. 将`android/app/src/main/assets/`和`ios`目录下原有的`ttsdk.lic`文件替换为您自己的 SDK 许可证。

   * Android

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_044c1ec77126f9426239e8b66c25c310.jpg) </span>

   * iOS

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_837d406299865f1c08b552e8cdece2ce.jpg) </span>


<span id="0212a64a"></span>
### Gradle 同步


1. 在 Android Studio 中打开`Android/VeLiveQuickStartDemo`。

2. 点击**Sync Project with Gradle Files**。

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5cc7b8c264de379a8e295f701c75bee2.png) </span>


<span id="80b9feb1"></span>
### 更新 CocoaPods 仓库


1. 打开 Terminal 并将当前目录切换到`ios`。

2. 运行`pod install --repo-update`以更新本地 CocoaPods 仓库副本并安装项目依赖。


<span id="6e21bd77"></span>
### 配置推流和拉流


* 集成推流和拉流，或仅集成推流时，需要打开`src/store/push/pusher.ts`文件并进行如下修改。

   ```JavaScript
   // 使用推流或同时使用推流和拉流
   import {initEnv} from '@byteplus/react-native-live-push';
   
   initEnv({
     AppID: 'appId', // 应用 ID，在 MediaLive 控制台的 SDK 管理页面获取。
     // 设置 iOS 的 bundle ID 或 Android 的 package name。
     AppName: 'xxx'
     })
   
     // The channel through which to download the app.您也可以通过该参数区分不同环境的应用构建，例如生产、测试和调试。
     AppChannel: Platform.select({
         android: 'GoogleStore',
         ios: 'AppStore',
         default: ''
     }),
   
     // The version number of your Android app.有效的版本号应包含两个或更多分隔符，例如“1.3.2”。
     AppVersion: '1.0.0',
     
     // 许可证文件名。如果替换了许可证文件，需要在此处修改文件名。为快速验证 SDK，您可以替换原始许可证文件（ttsdk.lic）的内容。
     LicenseUri: {
       android: 'assets:///ttsdk.lic', 
       ios: 'ttsdk.lic'
     },
     UserUniqueID: 'VeLiveQuickStartDemo',
   });
   ```
   

* 仅集成拉流时，需要打开`src/store/pull/player.ts`文件并进行如下修改。

   ```JavaScript
   // 仅使用拉流
   import {initEnv} from '@byteplus/react-native-live-pull';
   
   initEnv({
     AppID: 'appId', // 应用 ID，你可以在 MediaLive 控制台的 SDK 管理页面获取。
     // 请为 iOS 设置应用的 bundle ID，或为 Android 设置包名。
     AppName: Platform.select({
         android: 'xxx', 
         ios: 'xxx'
     })
   
     // The channel through which to download the app.你也可以使用此参数区分不同环境下的应用构建，例如生产、测试和调试。
     AppChannel: Platform.select({
         android: 'GoogleStore',
         ios: 'AppStore',
         default: ''
     }),
   
     // The version number of your Android app.有效的版本号应包含两个或更多分隔符，例如“1.3.2”。
     AppVersion: '1.0.0',
     
     // 许可证文件名。如果替换了许可证文件，需要在此处修改文件名。要快速验证 SDK，可以替换原始许可证文件（ttsdk.lic）的内容。
     LicenseUri: {
       android: 'assets:///ttsdk.lic', 
       ios: 'ttsdk.lic'
     },
     UserUniqueID: 'VeLiveQuickStartDemo',
   });
   ```
   


<span id="266db972"></span>
### 编译演示

请参阅[React Native 文档](https://reactnative.dev/docs/running-on-device)。
