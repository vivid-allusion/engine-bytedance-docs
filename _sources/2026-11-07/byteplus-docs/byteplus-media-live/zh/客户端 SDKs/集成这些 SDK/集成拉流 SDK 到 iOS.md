---
title: "集成拉流 SDK 到 iOS"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios-zh-CN"
---

本主题介绍如何集成拉流 SDK 到 iOS。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本指南适用于 SDK 1.40.200 及以上版本。如果你已集成旧版本 SDK，可参考 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-ios-dynamic-library-upgrade-guide">iOS 动态库升级指南</a>，了解升级或从静态库切换到动态库的操作方法。</div>


<span id="2178b17a"></span>
## 系统要求


* 运行 iOS 11.0 或更高版本的实体设备

* Xcode 14.1 或更高版本


<span id="43e22af2"></span>
## 前提条件

你已创建 SDK 应用并获得 SDK 许可证。更多信息，请参见 [获取您的 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-CN)。

<span id="d2f677b3"></span>
## 集成 SDK

你可以通过以下方法之一集成 SDK：


* 自动集成（推荐）：使用 CocoaPods 或 Swift Package Manager（SPM）自动下载 SDK 包。对于 CocoaPods，你可以选择集成动态库或静态库，而对于 SPM，只能集成动态库。

* 手动集成：[联系你的技术支持](https://console.byteplus.com/workorder/create)，以获得手动集成 SDK 的协助。


本节介绍如何自动集成 SDK。


<Tabs>
<Tab zoneid="uSmZPsVrPJ" title="使用 CocoaPod">
<TabTitle>使用 CocoaPod</TabTitle>

<span id="e266c047"></span>
### 集成动态库（推荐）

<span id="64362f11"></span>
#### 步骤 1：安装 CocoaPods

在 Mac 上安装 Ruby，并在终端运行以下命令以安装 CocoaPods。

```Ruby
sudo gem install cocoapods
```


<span id="5fb664bc"></span>
#### 步骤 2：创建 Podfile

在项目目录下运行以下命令以创建 Podfile。

```Ruby
pod init
```


<span id="22dee6b4"></span>
#### 步骤 3：添加依赖

将以下代码添加到你的 Podfile。

```Ruby
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
pod 'TTSDKFramework', 'x.x.x.x-premium', :subspecs => ['LivePull']
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">将 <code>x.x.x.x-premium</code> 替换为具体的 SDK 版本。建议使用最新版本。关于版本号的更多信息，请参见 <a href="https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes-zh-CN">iOS 拉流 SDK 发行说明</a>。</div>


* <div data-tips="true" data-tips-type="tip">如需使用 RTM 协议拉取流，请使用 <code>'LivePull-RTS'</code> 替代 <code>'LivePull'</code>：<code>pod 'TTSDKFramework', 'x.x.x.x-premium', :subspecs => ['LivePull-RTS']</code>。</div>


* <div data-tips="true" data-tips-type="tip">从 1.51.300.2\-premium 版本起，如需使用超分辨率（SR）和视频锐化功能，需在 <code>'LivePull'</code> 基础上添加 <code>'LivePull-BMF'</code>：<code>pod 'TTSDKFramework', 'x.x.x.x-premium', :subspecs => ['LivePull', 'LivePull-BMF']</code>。</div>



<span id="627e080c"></span>
#### 步骤 4：安装 SDK

在终端运行以下命令，安装 Podfile 中指定的 SDK 依赖。

```Plain
pod install
```


<span id="cd337301"></span>
### 集成静态库

如需集成静态库，请按照动态库的步骤操作，但将 pod 名称 TTSDKFramework 替换为 TTSDK。

```Ruby
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
pod 'TTSDK', 'x.x.x.x-premium', :subspecs => ['LivePull']
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">将 <code>x.x.x.x-premium</code> 替换为具体的 SDK 版本。建议使用最新版本。关于版本号的更多信息，请参见 <a href="https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes-zh-CN">iOS 拉流 SDK 发行说明</a>。</div>


* <div data-tips="true" data-tips-type="tip">要使用 RTM 协议拉取流，请使用 <code>'LivePull-RTS'</code>，而不是 <code>'LivePull'</code>：<code>pod 'TTSDK', 'x.x.x.x-premium', :subspecs => ['LivePull-RTS']</code>。</div>


* <div data-tips="true" data-tips-type="tip">从 1.51.300.2\-premium 版本开始，如需使用超分辨率（SR）和视频锐化功能，除了 <code>'LivePull'</code> 外，还需添加 <code>'LivePull-BMF'</code>：<code>pod 'TTSDK', 'x.x.x.x-premium', :subspecs => ['LivePull', 'LivePull-BMF']</code>。</div>



</Tab>
<Tab zoneid="BaWPsiSyzD" title="使用 SPM">
<TabTitle>使用 SPM</TabTitle>

1. 在 Xcode 项目中，点击  **+**  按钮，位于 **Package Dependencies** 标签页下。

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b6519c733fb4d17a41f535fab1039da~tplv-goo7wpa0wc-image.image" width="2516px" />   </div>
   

2. 在弹出的对话框右上角输入 `git@github.com:byteplus-sdk/TTSDK_BytePlus_SPM.git`。然后输入你要集成的 SDK 版本，并点击 **Add Package**，以添加 TTSDK 依赖。

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f2260bdeb5c41fea0aa4a023aaa4ccf~tplv-goo7wpa0wc-image.image" width="1872px" />   </div>
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">建议将 <strong>Exact Version</strong> 设置为 <strong>Dependency Rule</strong>。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">只能指定支持通过 SPM 集成的 SDK 版本。有关具体版本的更多信息，请参见 <a href="https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes-zh-CN">iOS 拉流 SDK 发行说明</a>。   </div>
   

3. 选择所需组件，并点击 **Add Package**，将其添加到你的目标。

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f922aa76e474e02b625c653262b3c3d~tplv-goo7wpa0wc-image.image" width="1312px" />   </div>
   

   你可以为 BytePlus MediaLive SDK 选择以下组件：

   * `TTSDK_LivePull`：使用 FLV、HLS 或 RTMP 协议拉取在线流。

   * `TTSDK_LivePull-RTS`：使用 FLV、HLS、RTMP 或 RTM 协议拉取在线流。


</Tab>
</Tabs>


<span id="bee4f6c1"></span>
## 添加许可证文件

将许可证文件复制到你的项目目录。你需要在 SDK 初始化时使用该文件路径。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">确保许可证文件关联的 bundle ID 和 app ID 与项目一致。否则，许可证认证将失败。</div>
