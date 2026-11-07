---
title: "在 iOS 上构建您的第一个应用"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-running-the-demo-ios--zh-CN"
---

要构建具备互动直播和视频播放功能的 iOS 应用，您可以按照本分步指南运行 VideoOne Demo 项目。本文档将带您完成整个流程，包括完成前置条件、配置项目、编译并在实体设备上运行应用。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">GitHub 示例项目不包含示例应用中的全部功能，例如美颜 AR。请参考解决方案实施指南，了解这些功能的实现方法。如需进一步协助，请联系您的<a href="https://console.byteplus.com/workorder/create">技术支持</a>。</div>


<span id="5a07e3aa"></span>
## 前置条件

在开始之前，请完成以下任务。建议您集中记录每项任务完成后获得的信息，以便在项目设置过程中随时查阅。

部分任务针对特定功能，如果您不需要这些功能，可以跳过。例如，如果您只需使用视频播放，则无需激活 BytePlus RTC 和 BytePlus MediaLive 服务。


|**任务** |**相关功能** |**任务说明** |**完成后获得的信息** |
|---|---|---|---|
|1. 注册 BytePlus 账号。<br><br>2. 为账号创建访问密钥。 |全部功能 |* [注册 BytePlus 账号](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account)<br><br>* [创建访问密钥](https://docs.byteplus.com/byteplus-platform/docs/creating-an-accesskey) |* 访问密钥 ID（AK）<br><br>* 访问密钥（SK） |
|1. 开通 BytePlus RTC 服务。<br><br>2. 创建 RTC 应用。 |* 互动直播<br><br>* RTC API 示例 |* [使用 RTC 服务前](https://docs.byteplus.com/byteplus-rtc/docs/69865) |* AppId<br><br>* AppKey |
|1. 开通 BytePlus MediaLive 服务。<br><br>2. 创建 MediaLive 应用并获取许可证。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果您已创建 BytePlus VOD 应用，请绑定已有应用，无需新建。   </div><br>    |互动直播 |* [开通 MediaLive 服务](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started#activating-the-medialive-service)<br><br>* SDK 管理<br><br>   * [创建 SDK 应用](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application)<br><br>   * [访问您的 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license) |* App ID<br><br>* BytePlus MediaLive SDK 许可证文件 |
|1. 开通 BytePlus VOD 服务。<br><br>2. 创建 VOD 应用并获取许可证。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果您已创建 BytePlus MediaLive 应用，请绑定已有应用，无需新建。   </div><br>    |视频播放 |* [步骤 1：启用 BytePlus VOD 服务](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started#step-1-enable-the-byteplus-vod-service)<br><br>* [应用管理](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management)<br><br>* [许可证管理](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management) |* App ID<br><br>* BytePlus VOD SDK 许可证文件 |


<span id="bfda08e6"></span>
### 系统要求


* Xcode 14.0 或更高版本

* CocoaPods 1.10.0 或更高版本

* 运行 iOS 13.0 或更高版本的实体移动设备。


<span id="74286d48"></span>
## 操作流程

部分任务仅针对特定功能，如果您不需要体验这些功能，可以跳过。例如，如果您只需体验互动直播，则无需完成视频播放的设置。

<span id="9d161712"></span>
### 克隆项目

请按照以下步骤克隆 Demo 项目：


1. 前往 GitHub，克隆 [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions) 仓库。

2. 打开 Terminal，并将当前目录切换到 `Client/iOS`，该目录为项目根目录。

3. 将您在[前置条件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-CN#5a07e3aa)部分获取的许可证文件移动到 `Component/AppConfig/License` 目录。如果您有多个同名许可证文件，可能需要重命名这些文件。

4. 运行 `pod install` 以安装依赖项。


<span id="32bcb285"></span>
### 设置应用服务器


1. 在项目根目录下，使用 Xcode 打开 `VideoOne.xcworkspace` 文件。

2. 导航至 `Pods/Development Pods/AppConfig`，并在 Xcode 中打开 `BuildConfig.h` 文件。

3. 指定您的应用服务器地址：

   * 如需使用 BytePlus 提供的应用服务器，将 `ServerUrl` 字段设置为 `https://videocloud.byteplusapi.com/videoone_opensource`。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">该地址仅用于测试，不能用于生产环境。      </div>
      

   * 如需部署自有应用服务器，请参照部署应用服务器（[为 Android 和 iOS 部署服务器](https://docs.byteplus.com/docs/byteplus-vos/docs-backend-deployment-guide-zh-CN)、[部署 Web 服务器](https://docs.byteplus.com/docs/byteplus-vos/docs-deploying-the-server-web-zh-CN)）的说明操作，并将 `ServerUrl` 字段设置为 `http://{your_server_address}:{port_number}/videoone_opensource`。


<span id="60922590"></span>
### 项目设置


1. 在 Xcode 中使用您的 Apple ID 登录。

2. 参考 [Assign a project to a team](https://help.apple.com/xcode/mac/current/#/dev23aab79b4) 配置应用签名。

3. 设置 **Bundle Identifier**。如果您申请了 BytePlus MediaLive SDK 或 BytePlus VOD SDK 的许可证，Bundle Identifier 必须与申请许可证时填写的名称一致。

4. 如果您使用 Xcode 15，需额外完成构建设置配置：

   1. 导航至 **TARGETS** 页面，并切换到 **Build Settings** 标签页。

   2. 搜索 **Other Linker Flags** 设置项。

   3. 在 **Other Linker Flags** 行的数值区域双击。

   4. 在弹出窗口中，点击  **+**  按钮，添加 `-ld64` 链接器标志。


<span id="a1e62caa"></span>
### RTC 设置

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需使用互动直播功能，必须完成此任务。</div>


在 Xcode 中，导航至 `Pods/Development Pods/AppConfig`，并打开 `BuildConfig.h` 文件。使用您在[前置条件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-CN#5a07e3aa)部分获得的数值配置以下字段。该信息用于客户端与 BytePlus RTC 服务通信时的身份验证。


|**字段名称** |**说明** |**示例** |
|---|---|---|
|RTCAPPID |您的 BytePlus RTC 应用的 **AppId**。 |123456\*\*\*\*\*\*\*\*3deb567a86 |
|RTCAPPKey |您的 BytePlus RTC 应用的 **AppKey**。 |1bfaa8e\*\*\*\*\*\*\*\*fjb6j6hhde68c07d |
|AccessKeyID |您的 BytePlus 账号的 **访问密钥 ID（AK）** 。 |AKAPZ7\*\*\*\*\*\*\*\*FLB0D38CM8DK49SO39D83KD820DFK4k9 |
|SecretAccessKey |您的 BytePlus 账号的 **访问密钥（SK）** 。 |8dk39vK\*\*\*\*\*\*\*\*k7D93KDHS8DJSLud830DJEO37EI3UDK37WODKu3oQ |


<span id="f15de15f"></span>
### MediaLive 设置

<span id="b758f198"></span>
#### 准备域名

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需使用互动直播功能，必须完成此任务。</div>



|**子任务** |**任务说明** |**所需信息** |
|---|---|---|
|**添加域名。** <br><br>您应至少添加两个域名，一个用于推流，另一个用于拉流。 |[添加域名](https://docs.byteplus.com/en/byteplus-media-live/docs/domain?version=v1.0#bb9e1337) |* 推流域名<br><br>* 拉流域名 |
|**为您的域名添加 CNAME 记录。** <br><br>添加域名后，系统会自动为您的域名分配一个 BytePlus MediaLive 域名。您必须为您的域名添加 CNAME 记录，将其指向分配的 BytePlus MediaLive 域名。 |[添加 CNAME 记录](https://docs.byteplus.com/en/byteplus-media-live/docs/adding-a-cname-record?version=v1.0) |/ |
|**启用 URL 鉴权。** <br><br>为保障推流安全并防止直播信息被未经授权下载，您可以启用 URL 鉴权。此步骤可防止域名被未经授权使用。 |[URL 鉴权](https://docs.byteplus.com/en/byteplus-media-live/docs/url-authentication?version=v1.0) |* 主密钥 |
|**配置转码模板。** <br><br>您可以对原始直播流进行转码，以满足不同用户的观看需求。 |[配置转码任务](https://docs.byteplus.com/en/byteplus-media-live/docs/configuring-transcoding) |* AppName |


<span id="cf1eeec6"></span>
#### 设置流地址

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需体验互动直播场景，此任务为必选项。</div>


在 Xcode 中，导航至 `Pods/Development Pods/AppConfig`，打开 `BuildConfig.h` 文件，并将上一步获取的信息填写到对应字段。这些信息用于拼接推流和拉流地址。


|**字段名称** |**描述** |**示例** |
|---|---|---|
|LivePullDomain |http://{domain_name}，其中“domain_name”指 **拉流域名**。 |`http://pull-demo.com` |
|LivePushDomain |rtmp://{domain_name}，其中“domain_name”指 **推流域名**。 |`rtmp://push-demo.com` |
|LivePushKey |**主密钥**，用于 URL 鉴权。 |`XED45d5dDLSH********KDFD` |
|LiveAppName |您已配置转码模板的 **AppName**。 |`videoone_demo` |


<span id="2c5d644a"></span>
#### 集成许可证

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需体验互动直播场景或直播相关功能，此任务为必选项。</div>


请按照以下步骤集成 BytePlus MediaLive SDK 许可证：


1. 在 Xcode 中，导航至 `Pods/Development Pods/AppConfig`，打开 `BuildConfig.h` 文件。

2. 设置以下字段：



|**字段名称** |**描述** |**示例** |
|---|---|---|
|LiveAPPID |您在[前置条件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-CN#5a07e3aa)部分创建或绑定的 MediaLive 应用的 **App ID**。 |5\*\*\*\*1 |
|LiveLicenseName |您在[前置条件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-CN#5a07e3aa)部分获得的 **BytePlus MediaLive SDK 许可证文件**名称。 |livelicense.lic |



3. 参考 [生成流地址](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-address-generator)，准备推流和拉流 URL。


<span id="047a3955"></span>
### VOD 设置

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需体验视频播放场景及相关功能，此任务为必选项。</div>


请按照以下步骤集成 BytePlus VOD SDK 许可证：


1. 在 Xcode 中，导航至 `Pods/Development Pods/AppConfig`，打开 `BuildConfig.h` 文件。

2. 设置以下字段：

   
   |**字段名称** |**描述** |**示例** |
   |---|---|---|
   |VODAPPID |您在[前置条件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-CN#5a07e3aa)部分创建或绑定的 VOD 应用的 **App ID**。 |5\*\*\*\*1 |
   |VODLicenseName |您在[前置条件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-CN#5a07e3aa)部分获得的 **BytePlus VOD SDK 许可证文件**名称。 |vodlicense.lic |
   


<span id="02dbf3ad"></span>
### 项目编译


1. 将移动设备连接至电脑，并在 Xcode 中设置为目标设备。

2. 点击 **Product** \> **Run**，启动编译流程。


<span id="cc07540a"></span>
### 应用体验

若编译流程无错误完成，VideoOne 应用将安装到已连接的移动设备上，并自动跳转至登录界面。使用邮箱登录应用后，即可开始探索应用内提供的不同场景和功能。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您使用的是免费 Apple 开发者账号，可能需要调整移动设备设置以允许来自非信任开发者的应用运行。大多数情况下，您可以进入 <strong>设置</strong> \> <strong>通用</strong> \> <strong>设备管理</strong>，信任开发者证书。</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fbbafc47ec843529888b307d1af14f2~tplv-goo7wpa0wc-image.image) </span>

<span id="f5f5fc6f"></span>
## 代码解析

示例项目的目录结构如下：

```Plain
. 
├── VideoOne                           # Entry point of the project 
└── Pods 
    ├── Podfile 
    └── Development Pods 
        ├── App                        # Entry point of the demo app 
        ├── AppConfig                  # App configurations 
        ├── LoginKit                   # Login          
        ├── ToolKit                    # Common tools  
        ├── InteractiveLive            # The interactive live streaming solution 
        │   ├── Common                 # Common components 
        │   └── Feature                # Features 
        │       ├── Controller 
        │       ├── Model 
        │       └── View 
        ├── RTCAPIExample               # The RTC API Example solution 
        │   ├── QuickStart            
        │   ├── VideoManager
        │   ├── AudioManager       
        │   └── ...                    # Many other RTC features       
        ├── MediaLive                   # The MediaLive solution 
        │   ├── Entry                   # Entrance
        │   ├── MediaLive.podspec
        │   ├── Pull                    # Live stream pulling
        │   ├── Push                    # Live stream pushing
        │   ├── Resources               # Multilingual copywriting
        │   ├── ScreenCapture           # Screen-sharing stream pushing
        │   ├── VELCommon               # Common tools
        │   └── VELSettings             # Configuration related to stream pushing and pulling
        └── VideoPlaybackEdit          # The video playback and editing solution     
            ├── FeedVideo              # Mid-form video 
            ├── LongVideo              # Long-form video 
            └── ShortVideo             # Short-form video 
            └── SingleFunction         # Code for separate functions 
                 ├── PlayList          # Video playlist 
# Screen capture protection
                 ├── SmartSubtitles    # Smart subtitling 
                 ├── VideoPlayback     # Other playback-related functions 
```
