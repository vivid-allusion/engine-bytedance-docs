---
title: "在 Android 上运行 VeLiveQuickStartDemo"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-android-zh-CN"
---

要探索 BytePlus MediaLive SDK 的功能，可以在 Android 设备上运行 VeLiveQuickStartDemo。按照本主题中的步骤操作，可以帮助你成功编译并启动该演示程序，演示内容包括基础的流推拉、如自适应码率等高级功能，以及如连麦等互动功能。

VeLiveQuickStartDemo 包含三类功能：


* 基础功能，包括流推拉。

* 高级功能，包括：

   * 自适应码率

   * 推送外部音视频源

   * H.265 硬件编码

   * 画中画（PiP）

* 互动直播功能，包括与观众连麦和连麦 PK。


<span id="e42b27e5"></span>
## 系统要求


* Android 5.0（SDK API Level 21）及以上

* Android Studio 4.0 及以上

* 一台运行 Android 5.0 或更高版本的实体 Android 设备

* 确保 CPU 架构为 armeabi\-v7a 或 arm64\-v8a


<span id="d1ed29bd"></span>
## 前提条件


* 注册 BytePlus 账号。详细操作请参见 [注册并认证 BytePlus 账号](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account)。

* 开通 BytePlus MediaLive 服务，并在控制台添加用于流推拉的域名。详细操作请参见 [BytePlus MediaLive 入门](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-zh-CN)。

* 要体验互动直播功能，还需开通火山引擎实时音视频服务。详细操作请参见 [开通火山引擎实时音视频服务](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865)。


<span id="5ba9ae47"></span>
## 准备工作

在运行演示程序前，获取 SDK 许可证、App ID 和 Token 信息。

<span id="0706aa76"></span>
### **下载 MediaLive 许可证**

按照 [SDK 管理](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management) 的说明创建 SDK 应用，并下载对应的 SDK 许可证。记录 App ID 和包名，后续会用到。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab6a8e0a0518458bbc61967cbc9e88cb~tplv-goo7wpa0wc-image.image) </span>

<span id="9ae537a8"></span>
### **获取 RTC App ID 和 App Key**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果你不打算测试互动直播功能，可以跳过本节。</div>



1. 登录 [火山引擎实时音视频控制台。](https://console.byteplus.com/rtc/workplaceRTC)

2. 在左侧导航栏，点击 **应用管理**。

3. 点击 **创建应用**，并在弹出的对话框中输入应用名称。**所属项目** 字段保持默认值。

4. 点击 **确定** 保存设置。

5. 在应用列表中找到你的应用，记录 App ID 和 App Key。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b565075eda70420d85d70cc7cc950223~tplv-goo7wpa0wc-image.image) </span>


<span id="b01ced66"></span>
## 运行演示程序

本节介绍设置和运行演示程序的详细步骤。

<span id="30f72781"></span>
### 下载源码


1. 前往 GitHub，克隆 [VeLiveQuickStartDemo](https://github.com/byteplus-sdk/VeLiveQuickStartDemo.git) 仓库。

2. 演示程序的目录结构如下：

   ```Plain
   Android/VeLiveQuickStartDemo/app/src/main/java/com/ttsdk/quickstart
   ├── app // Entry point of the demo app
   ├── features // Features
   │   ├── basic // Basic features
   │   │   ├── PullStreamActivity.java // Stream pulling
   │   │   └── PushCameraActivity.java // Video capture and stream pushing
   │   ├── advanced // Advanced features
   │   │   ├── PictureInPictureActivity.java // PiP
   │   │   ├── PushAutoBitrateActivity.java // Adaptive bitrate
   │   │   ├── PushBeautyActivity.java // Beauty AR and special effects
   │   │   ├── PushCustomActivity.java // Pushing external audio and video sources
   │   │   ├── PushH265CodecActivity.java // H.265 hardware encoding
   │   │   └── PullRTMActivity.java // Pulling an RTM stream
   │   └── interact // Interactive live features
   │       ├── link // Co-hosting with audience members
   │       ├── manager // Common host and audience activities
   │       └── pk // Host PK battle
   └── helper // Utilities, such as SDK initialization and external video capture
   ```
   


<span id="743d56e6"></span>
### 集成 SDK 许可证


1. 将已下载的 MediaLive SDK 许可证重命名为 `ttsdk.lic`。

2. 将 `Android/VeLiveQuickStartDemo/app/src/main/assets/` 目录下原有的 `ttsdk.lic` 文件替换为你自己的 SDK 许可证。


<span id="e7a73684"></span>
### Gradle 同步


1. 在 Android Studio 中打开 `Android/VeLiveQuickStartDemo`。

2. 点击 **Sync Project with Gradle Files**，同步项目与 Gradle 文件。


<span id="77e37fbf"></span>
### 配置流推拉


1. 在 Android Studio 中，进入 `app/src/main/java/com.ttsdk.quickstart/helper`，并打开 `VeLiveSDKHelper.java` 文件。

2. 完成以下配置。

   ```Java
   // The app ID
   public static String TTSDK_APP_ID = "536123";
   
   // License 文件名。如果你替换了 License 文件，则需要在此处修改文件名。为快速验证 SDK，你可以替换原有 License 文件（ttsdk.lic）的内容。
   public static String TTSDK_LICENSE_NAME = "ttsdk.lic";
   
   // 配置 AccessKey ID 和 AccessKey secret，用于 API 请求鉴权。
   public static String ACCESS_KEY_ID = "";
   public static String SECRET_ACCESS_KEY = "";
   
   // The domain name space
   public static String LIVE_VHOST = "push.example.com";
       
   /*
   * 推流和拉流地址示例：https://{域名}/{应用}/{StreamName}.flv
   * 推流和拉流地址中使用的 AppName，支持大小写字母、数字、下划线</a> (_)和连字符 (-)，最大长度为 30 个字符。例如：live
   */
   public static String LIVE_APP_NAME = "live";
   
   // 配置推流域名
   public static String LIVE_PUSH_DOMAIN = "push.example.com";
   
   // 配置拉流域名
   public static String LIVE_PULL_DOMAIN = "pull.example.com";
   ```
   


<span id="5609c16c"></span>
### 配置连麦和连麦 PK


1. 在 Android Studio 中，打开 `app/src/main/java/com.ttsdk.quickstart/helper/VeLiveSDKHelper.java` 文件。

2. 填写 RTC App ID 和 App Key。

   ```Java
   // The RTC app ID
   public static String RTC_APPID ="";   
   // The RTC app key
   public static String RTC_APPKEY ="";    
   ```
   


<span id="3c9d8600"></span>
### 配置包名


1. 在 Android Studio 中，打开 `app/build.gradle` 文件。

2. 将 `applicationId` 设置为你在 [下载 MediaLive 许可证](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-android#0706aa76) 环节创建 SDK 应用时使用的包名。


<span id="67945fc7"></span>
### 编译演示程序


1. 将你在 [前提条件](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-android#d1ed29bd) 环节准备的实体 Android 设备连接到电脑，并在 Android Studio 中设置为目标设备。

2. 点击**运行**以启动编译流程。


如果编译流程顺利完成且无任何错误，演示应用将会安装到已连接的移动设备上。
