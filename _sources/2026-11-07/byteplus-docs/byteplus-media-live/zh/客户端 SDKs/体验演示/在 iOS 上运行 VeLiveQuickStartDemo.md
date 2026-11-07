---
title: "在 iOS 上运行 VeLiveQuickStartDemo"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-ios-zh-CN"
---

要探索 BytePlus MediaLive SDK 的功能，可以在你的 iOS 设备上运行 VeLiveQuickStartDemo。本主题中的以下步骤将帮助你成功编译并启动该演示程序，展示基础流推拉、如自适应码率等高级功能，以及如连麦等互动功能。

VeLiveQuickStartDemo 包含三类功能：


* 基础功能，包括流推拉。

* 高级功能，包括：

   * 自适应码率

   * 推送外部音视频源

   * H.265 硬件编码

   * 画中画（PiP）

* 互动直播功能，包括与观众连麦及主播连麦 PK。


<span id="208fe723"></span>
## 系统要求


* Xcode 14.0 或更高版本

* CocoaPods 1.11.3 或更高版本

* 运行 iOS 11.0 或更高版本的实体 iOS 设备

* 开发配置描述文件


<span id="4cff3e13"></span>
## 前提条件


* 注册 BytePlus 账号。详细操作请参见 [注册并验证 BytePlus 账号](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account)。

* 开通 BytePlus MediaLive 服务，并在控制台添加用于流推拉的域名。详细操作请参见 [BytePlus MediaLive 入门](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-zh-CN)。

* 如需体验互动直播功能，还需开通火山引擎实时音视频服务。详细操作请参见 [启用实时音视频服务](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865)。


<span id="66cf45e9"></span>
## 准备工作

在运行演示程序前，获取 SDK 许可证、应用 ID 和 token 信息。

<span id="96bcd67f"></span>
### 加速域名配置


1. 登录 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏点击 **域名**。

3. 添加用于流推拉的域名。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0dec0195bac047c384081882dfec2e64~tplv-goo7wpa0wc-image.image) </span>

<span id="9dacd3e8"></span>
### **下载 MediaLive 许可证**

按照 [SDK 管理](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management) 的指引创建 SDK 应用，并下载对应的 SDK 许可证。记录应用 ID 和 bundle ID，后续使用。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bea7ca3024e46998c225be78e7dff60~tplv-goo7wpa0wc-image.image) </span>

<span id="9377cabf"></span>
### **获取实时音视频应用 ID 和应用密钥**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果你不打算测试互动直播功能，可跳过本节。</div>



1. 登录 [火山引擎实时音视频控制台](https://console.byteplus.com/rtc/workplaceRTC)。

2. 在左侧导航栏点击 **应用管理**。

3. 点击 **创建应用**，在弹出的对话框中输入你的应用名称。保持 **所属项目** 字段为默认值。

4. 点击 **确定** 保存设置。

5. 在应用列表中找到你的应用，并记录应用 ID 和应用密钥。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b565075eda70420d85d70cc7cc950223~tplv-goo7wpa0wc-image.image) </span>


<span id="abc77f0b"></span>
## 运行演示程序

本节介绍设置和运行演示程序的详细步骤。

<span id="619e2c8e"></span>
### 下载源代码


1. 前往 GitHub，克隆 [VeLiveQuickStartDemo](https://github.com/byteplus-sdk/VeLiveQuickStartDemo.git) 仓库。

2. 演示程序的目录结构如下：

   ```Bash
   iOS/VeLiveQuickStartDemo
   └── VeLiveQuickStartDemo
       ├── App // Entry point of the demo app
       ├── Features // Features
       │   ├── Basic // Basic features
       │   │   ├── PullStream // Stream pulling
       │   │   └── PushCamera // Video capture and stream pushing
       │   ├── Advanced // Advanced features
       │   │   ├── PullRTM // Pulling an RTM stream
       │   │   ├── PushAutoBitrate // Adaptive bitrate
       │   │   ├── PushBeauty // Beauty AR and special effects
       │   │   ├── PushCustom // Pushing external audio and video sources
       │   │   ├── PushH265Codec // H.265 hardware encoding
       │   │   ├── PictureInPicture // PiP
       │   │   └── ScreenCapture // Screen recording and streaming
       │   └── Interact // Interactive live features
       │       ├── Link // Co-hosting with audience members
       │       ├── Manager // Common host and audience activities
       │       └── PK // Host PK battle
       ├── Helper // Utilities, such as SDK initialization and external video capture
   ```
   


<span id="6febb740"></span>
### 集成 SDK 许可证


1. 将已下载的 MediaLive SDK 许可证重命名为 `ttsdk.lic`。

2. 用你的 SDK 许可证替换 `iOS/VeLiveQuickStartDemo/VeLiveQuickStartDemo/Resource/` 目录下原有的 `ttsdk.lic` 文件。


<span id="055049ad"></span>
### 更新 Cocoapods 仓库


1. 打开 Terminal，将当前目录切换到 `iOS/VeLiveQuickStartDemo`。

2. 运行 `pod install --repo-update`，更新本地 Cocoapods 仓库并安装项目依赖。


<span id="817a8f22"></span>
### 流推拉配置


1. 在项目根目录下，用 Xcode 打开 `VeLiveQuickStartDemo.xcworkspace` 文件。

2. 在项目树视图中，定位到 `VeLiveQuickStartDemo/Helper`，并打开 `VeLiveSDKHelper.h` 文件。

3. 完成以下配置。

   ```Java
   // The app ID
   #define TTSDK_APP_ID @"53**10"
   
   // License 文件名。如果替换了 License 文件，则需要在此处修改文件名。为快速验证 SDK，你可以替换原始 License 文件（ttsdk.lic）的内容。
   #define TTSDK_LICENSE_NAME @"ttsdk.lic"
   
   // 配置 AccessKey ID 和 AccessKey secret，用于 API 请求鉴权。
   #define ACCESS_KEY_ID @""
   #define SECRET_ACCESS_KEY @""
   
   // 域名空间
   #define LIVE_VHOST @"push.example.com"
   
   /* 
   * 示例推流和拉流地址：https://{DomainName}/{AppName}/{StreamName}.flv
   * 推流和拉流地址中使用的AppName，支持大小写字母、数字、下划线 (_)和连字符 (-)，最大长度为 30 个字符。例如：live
   */
   #define LIVE_APP_NAME @"live"
   
   // 配置推流域名
   #define LIVE_PUSH_DOMAIN @"push.example.com"
   
   // 配置拉流域名
   #define LIVE_PULL_DOMAIN @"pull.example.com"
   ```
   


<span id="ca1f9885"></span>
### 连麦及主播连麦 PK 配置


1. 在 Xcode 中打开 `VeLiveQuickStartDemo/Helper/VeLiveSDKHelper.h` 文件。

2. 输入实时音视频应用 ID 和应用密钥。


```Java
// The RTC app ID
#define RTC_APPID @""

// The RTC app key
#define RTC_APPKEY @""
```


<span id="fa7c2a86"></span>
### 项目配置


1. 在 Xcode 的项目编辑器中选择目标。

2. 点击 **Signing & Capabilities**。

3. 将**Bundle Identifier**设置为你在[Downloading a MediaLive license](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-ios#9dacd3e8)章节准备的标识符。

4. 选择开发用的签名配置文件（Provisioning Profile）。


<span id="36503b02"></span>
### 配置 bundle ID


1. 打开`VeLiveQuickStartDemo/VeLiveQuickStartDemo.xcworkspace`。

2. 修改配置文件 Podfile，以启用或禁用屏幕录制与流推送功能。如果你修改了该变量，则必须重新运行 pod install。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/797eb2573d214d16b54cd219d1c99b98~tplv-goo7wpa0wc-image.image) </span>

3. 修改主项目应用及屏幕录制与流推送扩展的 Bundle Identifier 和 GroupID 配置。

   1. 将主项目应用的 Bundle Identifier 修改为创建 BytePlus MediaLive 应用时指定的 Bundle Identifier。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0db405f62f804ed09064860e242007dd~tplv-goo7wpa0wc-image.image) </span>

   2. 修改屏幕录制与流推送扩展的 Bundle Identifier。该 Bundle Identifier 必须以应用的 Bundle Identifier 为前缀。如果屏幕录制与流推送功能未开启，可跳过此步骤。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b20ab98536c44e79fba177d165090ef~tplv-goo7wpa0wc-image.image) </span>

   3. 修改 GroupID 配置。如果未开启屏幕录制与流推送功能，可跳过此步骤。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6bee18d237a4a36b128947b50b1ff63~tplv-goo7wpa0wc-image.image) </span>

4. 选择主项目的开发者签名文件（Provisioning Profile）。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27fb2efe3b704291bdb9f9cfde43c237~tplv-goo7wpa0wc-image.image) </span>

5. 选择屏幕录制与流推送扩展的开发者签名文件（Provisioning Profile）。如果未开启屏幕录制与流推送功能，可跳过此步骤。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b590d748ec32437a9d8b55203e108af4~tplv-goo7wpa0wc-image.image) </span>


<span id="6e1c77df"></span>
### 编译 demo


1. 将你在[Prerequisites](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-ios#4cff3e13)章节准备的物理 iOS 设备连接到电脑，并在 Xcode 中设置为目标设备。

2. 点击**Run**以启动编译流程。


如果编译流程无错误完成，demo 应用将会安装到已连接的移动设备上。
