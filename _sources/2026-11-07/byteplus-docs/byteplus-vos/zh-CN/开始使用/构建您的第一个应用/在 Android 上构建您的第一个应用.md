---
title: "在 Android 上构建您的第一个应用"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-running-the-demo-android--zh-CN"
---

要在 Android 上构建您的第一个视频应用，请按照本分步指南运行 VideoOne Demo 项目。编译成功后，您将获得一个包含互动直播和视频播放功能的 Android 应用。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">该 Demo 项目未包含 Demo 应用中的所有功能，例如美颜 AR。请参考解决方案实施指南，了解如何实现这些功能。如需进一步协助，请联系您的<a href="https://console.byteplus.com/workorder/create">技术支持</a>。</div>


<span id="a0c6863a"></span>
## 前置条件

在开始之前，请完成以下任务。建议您在完成每项任务后集中记录获得的信息，以便在项目设置过程中随时查阅。

部分任务仅针对特定功能，如果您不需要这些功能，可以跳过相应任务。例如，如果您只需使用视频播放功能，则无需开通 BytePlus RTC 和 BytePlus MediaLive 服务。


|**任务** |**相关功能** |**任务说明** |**需记录的信息** |
|---|---|---|---|
|1. 注册 BytePlus 账号。<br><br>2. 为账号创建访问密钥。 |全部功能 |* [注册 BytePlus 账号](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account)<br><br>* [创建访问密钥](https://docs.byteplus.com/byteplus-platform/docs/creating-an-accesskey) |* 访问密钥 ID（AK）<br><br>* 访问密钥（SK） |
|1. 开通 BytePlus RTC 服务。<br><br>2. 创建 RTC 应用。 |互动直播 |* [使用 RTC 服务前](https://docs.byteplus.com/byteplus-rtc/docs/69865) |* AppId<br><br>* AppKey |
|1. 开通 BytePlus MediaLive 服务。<br><br>2. 创建 MediaLive 应用并获取许可证。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果您已创建 BytePlus VOD 应用，请绑定已有应用，无需新建。   </div><br>    |互动直播 |* [开通 MediaLive 服务](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started)<br><br>* SDK 管理<br><br>   * [创建 SDK 应用](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application)<br><br>   * [访问您的 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license) |* App ID<br><br>* BytePlus MediaLive SDK 许可证文件 |
|1. 开通 BytePlus VOD 服务。<br><br>2. 创建 VOD 应用并获取许可证。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果您已创建 BytePlus MediaLive 应用，请绑定已有应用，无需新建。   </div><br>    |视频播放 |* [步骤 1：启用 BytePlus VOD 服务](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started#step-1-enable-the-byteplus-vod-service)<br><br>* [应用管理](https://docs.byteplus.com/byteplus-vod/docs/sdk-management)<br><br>* [许可证管理](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management) |* App ID<br><br>* BytePlus VOD SDK 许可证文件 |


<span id="db012043"></span>
## 系统要求


* Android Studio Arctic Fox 或更高版本。建议使用最新版本的 Android Studio 以获得最佳性能。

* 一台运行 Android 5.0 或更高版本的实体移动设备。

* 请确保您使用的 CPU 架构为 armv7 或 arm64。


<span id="7114bbd5"></span>
## 操作流程

部分任务仅针对特定功能，如果您不需要体验这些功能，可以跳过相应任务。例如，如果您只需体验互动直播功能，则无需完成视频播放的相关设置。

<span id="a4ed37cb"></span>
### 克隆项目

请按照以下步骤克隆 Demo 项目：


1. 前往 GitHub 并克隆 [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions) 仓库。

2. 在 `Client` 目录下，使用 Android Studio 打开 `Android` 文件夹。该文件夹为 Demo 项目的根目录。


<span id="bd8233cf"></span>
### 设置应用服务器

在根目录下，打开 `gradle.properties` 文件，并指定您的应用服务器地址：


* 如需使用 BytePlus 提供的应用服务器，将 `SERVER_URL` 字段设置为 `https://videocloud.byteplusapi.com/videoone_opensource`。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">该地址仅用于测试，不能用于生产环境。   </div>
   

* 如需部署自有应用服务器，请参照部署应用服务器（[为 Android 和 iOS 部署服务器](https://docs.byteplus.com/docs/byteplus-vos/docs-backend-deployment-guide-zh-CN)、[部署 Web 服务器](https://docs.byteplus.com/docs/byteplus-vos/docs-deploying-the-server-web-zh-CN)）的说明操作，然后将 `SERVER_URL` 字段设置为 `http://{your_server_address}:{port_number}/videoone_opensource`。


<span id="8ec44536"></span>
### 设置包名

在 `app` 目录下，打开 `build.gradle` 文件，并将 `applicationId` 设置为您的 Android 应用包名。如果您已申请 BytePlus MediaLive 或 VOD SDK 许可证，包名必须与申请许可证时填写的名称完全一致。

<span id="ab53744f"></span>
### RTC 配置

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需体验互动直播，该任务为必选项。</div>


在根目录下，打开 `gradle.properties` 文件，并将[前置条件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-CN#a0c6863a)部分获取的值配置到以下字段中。这些信息用于客户端与 BytePlus RTC 服务通信时的身份验证。


|**字段名称** |**描述** |**示例** |
|---|---|---|
|APP_ID |您的 BytePlus RTC 应用的**AppId**。 |123456\*\*\*\*\*\*\*\*3deb567a86 |
|APP_KEY |您的 BytePlus RTC 应用的**AppKey**。 |1bfaa8e\*\*\*\*\*\*\*\*fjb6j6hhde68c07d |
|ACCESS_KEY_ID |您的 BytePlus 账号的**访问密钥 ID（AK）** 。 |AKAPZ7\*\*\*\*\*\*\*\*FLB0D38CM8DK49SO39D83KD820DFK4k9 |
|SECRET_ACCESS_KEY |您的 BytePlus 账号的**访问密钥密钥（SK）** 。 |8dk39vK\*\*\*\*\*\*\*\*k7D93KDHS8DJSLud830DJEO37EI3UDK37WODKu3oQ |


<span id="1653077f"></span>
### MediaLive 配置

<span id="81fa8179"></span>
#### 准备域名

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需体验互动直播场景，该任务为必选项。</div>



|**子任务** |**任务说明** |**必填信息** |
|---|---|---|
|**添加域名。** <br><br>您需至少添加两个域名，一个用于推流，另一个用于拉流。 |[添加域名](https://docs.byteplus.com/byteplus-media-live/docs/domain) |* 推流域名<br><br>* 拉流域名 |
|**为您的域名添加 CNAME 记录。** <br><br>添加域名后，BytePlus MediaLive 会自动为其分配一个对应的 MediaLive 域名。然后，您必须添加 CNAME 记录，将您的域名指向分配的 MediaLive 域名。 |[添加 CNAME 记录](https://docs.byteplus.com/byteplus-media-live/docs/adding-a-cname-record) |/ |
|**启用 URL 鉴权。** <br><br>启用 URL 鉴权可保护您的流媒体内容，防止未授权的域名使用。 |[URL 鉴权](https://docs.byteplus.com/en/byteplus-media-live/docs/url-authentication?version=v1.0) |* 主密钥 |
|**配置转码模板。** <br><br>您可以对原始直播流进行转码，以满足不同用户的观看需求。 |[配置转码任务](https://docs.byteplus.com/en/byteplus-media-live/docs/configuring-transcoding) |* AppName |


<span id="a001fbcb"></span>
#### 设置流地址

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需体验互动直播场景，需完成此任务。</div>


在 Demo 项目的 `solutions/interactivelive` 目录下，打开 `gradle.properties` 文件，并将上一步获取的信息填写到对应字段中。这些信息用于构建推流和拉流地址。


|**字段名** |**说明** |**示例** |
|---|---|---|
|LIVE_PULL_DOMAIN |http://{domain_name}，其中 "domain_name" 表示**拉流域名**。 |`http://pull-demo.com` |
|LIVE_PUSH_DOMAIN |rtmp://{domain_name}，其中 "domain_name" 表示**推流域名**。 |`rtmp://push-demo.com` |
|LIVE_PUSH_KEY |用于 URL 鉴权的**主密钥**。 |`XED45d5dDLSH********KDFD` |
|LIVE_APP_NAME |已配置转码模板的**AppName**。 |`videoone_demo` |


<span id="d9803aef"></span>
#### 集成许可证

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需体验互动直播场景或直播相关功能，需完成此任务。</div>


请按照以下步骤集成在[前置条件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-CN#a0c6863a)部分获取的 **BytePlus MediaLive SDK 许可证文件**：


1. 将许可证文件重命名为 `ttsdk.lic`。

2. 将许可证文件移动到目标目录：

   1. 如需体验互动直播场景，请将许可证文件移动到 `solutions/interactivelive/src/main/assets`。

   2. 如果您希望体验与直播相关的功能，请将许可证文件移动到 `solutions/media-live/live-entrance/src/main/assets`。

3. 打开 `gradle.properties` 文件，并将 `LIVE_TTSDK_APP_ID` 设置为您在[前置条件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-CN#a0c6863a)部分创建的 MediaLive 应用的**App ID**。

4. 请参考[生成流地址](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-address-generator)，准备用于推流的直播流 URL 和用于拉流的直播流 URL。


<span id="f8211e2d"></span>
### 点播设置

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需体验视频播放场景及相关功能，需完成此任务。</div>


集成您在[前置条件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-CN#a0c6863a)部分获得的 BytePlus VOD SDK 许可证：


1. 将许可证文件移动到 `solutions/vod/vod-common/src/main/assets/vodlicense` 目录。

2. 在 `solutions/vod/vod-common/` 目录下，打开 `gradle.properties` 文件，并配置以下字段：



|**字段名** |**说明** |**示例** |
|---|---|---|
|VOD_APP_ID |您在[前置条件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-CN#a0c6863a)部分创建的 VOD 应用的**App ID**。 |5\*\*\*\*1 |
|VOD_APP_CHANNEL |您的应用分发渠道。 |googleplay |
|VOD_LICENSE_URI |您在[前置条件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-CN#a0c6863a)部分获取的**BytePlus VOD SDK 证书文件**的存储路径。 |assets:///vodlicense/{LICENSE_NAME}.lic |


<span id="00c4fcba"></span>
### 项目编译


1. 将移动设备连接到您的电脑，并在 Android Studio 中设置为目标设备。

2. 点击**Sync Project with Gradle Files**按钮，同步项目与 Gradle 文件。

3. 点击**Run**按钮，启动编译流程。


<span id="2669bf25"></span>
### 应用运行

如果编译过程无错误完成，VideoOne 应用将安装到已连接的移动设备上，并自动跳转至登录界面。使用您的邮箱登录应用，开始探索其功能与特性。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33f9ae7de2ca4e41a5c73e26ae22d630~tplv-goo7wpa0wc-image.image) </span>

<span id="7d5db6c4"></span>
## 代码解析

Demo 项目的目录结构如下：

```Plain
. 
├── app                    # Entry point of the app 
├── build.gradle 
├── component              # Public components 
│   ├── Avatars                # Avatar resources 
│   ├── LoginKit               # Login 
│   └── SolutionBase           # Base library 
│   └── ToolKit                # Common tools 
├── gradle 
├── gradle.properties           # Common configurations 
├── gradlew 
├── gradlew.bat 
├── local.properties 
├── settings.gradle 
└── solutions                 # Solutions 
    ├── VideoPlaybackEdit     # The video playback and editing demo 
    │   └── Vod
    ├── interactivelive       # The interactive live streaming demo 
    │   ├── build.gradle
    │   ├── consumer-rules.pro
    │   ├── gradle.properties
    │   ├── proguard-rules.pro
    │   └── src
    ├── media-live            # MediaLive SDK configurations 
    │   ├── live-common       # Common tools  
    │   ├── live-entrance     # Entrance
    │   ├── live-player       # Live stream pulling
    │   ├── live-pusher       # Live stream pushing
    └── rtc-api-example       # RTC API Example 
         └── rtc-api-example-entry    # Entrance
```
