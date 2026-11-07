---
title: "集成 React Native 的拉流 SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn-zh-CN"
---

本主题介绍如何集成 React Native 的拉流 SDK。

<span id="b1be2e82"></span>
## 系统要求


* React Native 0.70 或更高版本

* Node v16 或更高版本

* Android：

   * Android 4.3 或更高版本

   * CPU 架构：armeabi\-v7a 或 arm64\-v8a

* iOS & macOS：

   * 运行 iOS 11.0 或更高版本的实体设备

   * Xcode 14.1 或更高版本

* 请确保您的项目具有有效的开发者签名。

* 有关环境搭建的说明，请参见 [官方文档](https://reactnative.dev/docs/environment-setup)。


<span id="23566c94"></span>
## 前提条件

您已创建 SDK 应用并获得 SDK 许可证。更多信息，请参见 [获取您的 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-CN)。

<span id="33c06caa"></span>
## 集成 SDK

使用以下 npm 包安装 SDK。

```Plain
npm i @byteplus/react-native-live-pull
```


<span id="c7fa4b6f"></span>
### Step 1: 配置 Maven 仓库


1. 在 Android 根目录下打开 `build.gradle` 文件。

2. 定义 Maven 仓库并配置仓库 URL。

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
### Step 2: 添加依赖项

将依赖项添加到您的 iOS Podfile。

```Plain
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
source 'https://cdn.cocoapods.org/'
```


<span id="db904c49"></span>
## 配置权限

<span id="07327795"></span>
### Android

在 `AndroidManifest.xml` 文件中声明应用所需的权限：

```Plain
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.INTERNET" />
```


<span id="22b41bb8"></span>
## 添加许可证文件

将许可证文件复制到您的项目目录，并记录许可证文件的路径。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">确保与许可证文件关联的 bundle ID 和 app ID 与您的项目一致。否则，许可证认证将失败。</div>
