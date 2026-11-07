---
title: "集成 Player SDK for Android"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android-zh-CN"
---

本主题介绍如何集成 Player SDK for Android。

## 系统要求

* Android 5.0 (API 21) 或更高版本。

* CPU 架构：armeabi\-v7a 或 arm64\-v8a

## 前提条件

你已创建 SDK 应用并获取 SDK 许可证。更多信息，请参见[获取 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)。

> **说明**

> 有关每种许可证类型支持的功能，请参见[客户端 SDK：SDK 概述](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction)。有关价格，请参见 [SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-licenses)。

## 集成 SDK

你可以通过以下任一方式集成 SDK：

* 自动集成（推荐）：使用 Gradle 自动下载 SDK 包。

* 手动集成：手动下载 AAR 文件并将其导入项目。有关详细说明，请[联系技术支持](https://console.byteplus.com/workorder/create)。

本节介绍如何自动集成 SDK。

### 步骤 1：配置 Maven 仓库

要集成 SDK，请配置多个 Maven 仓库，确保正确下载所有必要依赖项。请按以下步骤操作：

1. 打开根目录中的 `build.gradle` 文件。

2. 将主仓库 URL 设置为 `https://artifact.byteplus.com/repository/public`。以下示例代码展示了相关配置：

   ```Groovy
   allprojects {
       repositories {
           google()
           mavenCentral()
           maven {
               url "https://artifact.byteplus.com/repository/public" // BytePlus 公共 Maven 仓库
           }
       }
   }
   ```

3. 为主仓库中没有的组件配置其他 Maven 仓库：

   * **对于低于 7.1 的 AGP 版本**：将此行添加到根目录的 `build.gradle`：

      ```Groovy
      apply from: 'https://ve-vos.volccdn.com/script/vevos-repo-base.gradle'
      ```

   * **对于 AGP 7.1 及更高版本**：将 `https://ve-vos.volccdn.com/script/vevos-repo-base.gradle` 中的 Maven 配置复制到 `settings.gradle` 的 `dependencyResolutionManagement` 块中。

### 步骤 2：配置环境和依赖项

1. 打开 `app/build.gradle` 文件并添加以下配置：

   * 在 `defaultConfig` 中配置应用使用的 CPU 架构。SDK 支持 armeabi\-v7a 和 arm64\-v8a。

   * 在 `dependencies` 中添加依赖项。

   ```Groovy
   android {
      defaultConfig {
          ndk {
              // 设置 SO（Shared Object）库架构，以支持 armeabi-v7a 或 arm64-v8a。
              abiFilters 'armeabi-v7a', 'arm64-v8a'
           }
      }
   }
   
   dependencies {
      // ...
      // 对于 1.49.100.2 或更高版本，添加此依赖项以使用基础拉流功能。
      implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:x.x.x.x' 
   }
   ```

   * 对于 1.51.300.2 或更高版本，请同时添加 `implementation 'com.bytedanceapi:ttsdk-ttbmf:x.x.x.x'` 和 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'`，以使用超分辨率（SR）和视频锐化功能。

   * 对于 1.49.100.2 或更高版本，请将 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:x.x.x.x'` 替换为 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'`，以使用高级许可证支持的功能。

   * 对于 1.49.100.2 或更高版本，请同时添加 `implementation 'com.bytedanceapi:ttsdk-ttquic:x.x.x.x'` 和 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'`，以通过 QUIC 拉流。

   * 对于 1.49.100.2 或更高版本，请同时添加 `implementation 'com.bytedanceapi:ttsdk-ttcmaf:x.x.x.x'` 和 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'`，以播放 CMAF 流。

   > **说明**

   * > 将 `x.x.x.x` 替换为你要集成的 SDK 版本。建议使用最新版本。有关可用版本，请参见 [Player SDK for Android 发布说明](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes)。

   * > 对于 1.48.200.2 版本：

      * > 要使用基础拉流功能，请添加 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:1.48.200.2'`。

      * > 要通过 QUIC 拉流，请同时添加 `implementation 'com.bytedanceapi:ttsdk-ttquic:1.48.200.2'` 和 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:1.48.200.2'`。

      * > 要通过 RTM 拉流，请添加 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:1.48.200.2'`。

      * > 要播放 CMAF 流，请同时添加 `implementation 'com.bytedanceapi:ttsdk-ttcmaf:1.48.200.2'` 和 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:1.48.200.2'`。

   * > 对于 1.48.100.103 或更早版本：

      * > 要使用基础拉流功能，包括通过 QUIC 拉流和播放 CMAF 流，请添加 `implementation 'com.bytedanceapi:ttsdk-ttlivepull:x.x.x.x'`。

      * > 要通过 RTM 拉流，请添加 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_rtc:x.x.x.x'`。

2. 单击 **Sync Project with Gradle Files** 以同步 SDK。SDK 将自动下载并集成到项目中。如果集成失败，请检查到 Maven 仓库的网络连接。

## 配置权限

在 `AndroidManifest.xml` 文件中声明 Player SDK 所需的权限。

```XML
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

## 添加许可证

将按照[获取 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)获取的许可证文件复制到你的项目目录。例如，将 `License2_test.lic` 文件复制到 `assets` 目录，如以下截图所示。请记下许可证文件的路径，因为初始化 SDK 时需要使用该路径。

![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/0c295cb-file_path2.png)

## 实现代码混淆

将以下行添加到 `proguard-rules.pro` 文件，以从混淆中排除 SDK 相关类。

```Plain
-keep class com.pandora.**{*;}
-keep class com.ss.**{*;}
-keep class com.bytedance.**{*;}
-keep class com.pandora.ttlicense2.**{*;}
-keep class com.bytertc.**{*;}
-keep class log.**{*;}
```

如果你正在集成 RTC SDK，还需要为 RTC SDK 配置混淆规则。详情请参见[混淆 Android 应用代码](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-78295)。
