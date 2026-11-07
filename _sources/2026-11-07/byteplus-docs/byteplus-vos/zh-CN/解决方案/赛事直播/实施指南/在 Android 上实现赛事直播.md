---
title: "在 Android 上实现赛事直播"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-live-sport-streaming-for-android-zh-CN"
---

本指南介绍如何使用 BytePlus MediaLive SDK 在 Android 上实现赛事直播观看体验。您将学习如何初始化直播播放器、通过低延迟协议拉流、切换机位和画质，以及在播放之上叠加互动功能。

<span id="lsa-env"></span>
## 环境要求


* Android Studio Arctic Fox 或更高版本。我们建议使用最新版本的 Android Studio 以获得最佳性能。

* 一台运行 Android 6.0 或更高版本的真机移动设备。

* 确保您使用的 CPU 架构为 armv7 或 arm64。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">暂不支持模拟器。</div>


<span id="lsa-prereq"></span>
## 前提条件


* 一个已激活 [BytePlus MediaLive](https://console.byteplus.com/live) 的有效 [BytePlus 账户](http://console.byteplus.com/)。

* 完成 [直播的基础设置](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)：

   * 获取 BytePlus MediaLive SDK 许可证。

      * 有关如何获取许可证的详细说明，请参见 [访问您的 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license)。

      * 要详细了解如何根据您的需求选择合适的许可证类型，请参考 [SDK 简介](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)。


<span id="lsa-version"></span>
## 版本要求


* 要使用 **直播拉流** 功能，您必须使用 BytePlus MediaLive SDK。请记得在 [客户端 SDK 组件](https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination) 页面选择正确的 SDK。


<span id="lsa-integrate"></span>
## 集成 SDK

<span id="lsa-maven"></span>
### 步骤 1: 添加 maven 仓库

打开位于项目根目录下的项目 `build.gradle` 文件，在 `repositories` 代码块中添加仓库地址，如下所示：

```Groovy
allprojects { 
    repositories { 
        google() 
        mavenCentral() 
        // BytePlus SDK maven repository
        maven { url 'https://artifact.byteplus.com/repository/public/' }
        maven { url 'https://artifact.bytedance.com/repository/Volcengine/' }
    } 
} 
```


<span id="lsa-dep"></span>
### 步骤 2: 集成 SDK

要集成 SDK，请将以下依赖项添加到模块的 `build.gradle` 文件中：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">要获取最新的版本号，请参见 <a href="https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination">客户端 SDK 组件</a>。</div>


```Groovy
dependencies {
    def ttsdkVersion = "1.50.300.1"
    // BytePlus MediaLive SDK dependencies
    implementation "com.bytedanceapi:ttsdk-ttlivepull_premium:$ttsdkVersion"
    implementation 'commons-net:commons-net:3.9.0'
    implementation 'com.bytedance.applog:RangersAppLog-Lite-global:6.14.3'
}
```


<span id="lsa-perm"></span>
### 步骤 3: 声明应用权限

在 `AndroidManifest.xml` 中声明 SDK 所需的权限。

```XML
<uses-permission android:name="android.permission.INTERNET" /> 
```


<span id="lsa-impl"></span>
## 实现

本节介绍 Android Demo 如何实现赛事直播体验。Demo 代码组织在以下模块中：

```text
solutions/media-live/live-sport
```


该模块包含三个面向用户的体验：


* **Live Watch**：播放赛事直播流，支持机位切换、播放设置、评论、礼物、点赞和全屏控制。

* **Live Comparison**：并排对比延迟、图像增强以及 H.265/H.264 降本流。

* **Custom Stream URL**：允许观众输入 FLV、RTM、HLS 或 RTMP 拉流 URL 并预览播放。


<span id="lsa-enter"></span>
### 步骤 1: 进入赛事直播场景

赛事直播入口注册在 VideoOne 首页场景列表中。当观众打开赛事直播卡片时，应用会初始化直播 SDK 环境并启动赛事直播首页。

关键代码：


* `app/src/main/kotlin/com/videoone/app/protocol/SceneEntry.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/videoone/app/protocol/LiveSportEntry.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/entry/LiveSportHomeActivity.kt`


<span id="lsa-init"></span>
### 步骤 2: 初始化 TTSDK 和许可证

在播放开始前，初始化 TTSDK 并加载有效的许可证。Demo 将此逻辑集中在 `SportLiveEnv.ensureInitialized()` 中，该方法可安全地多次调用。

关键代码：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/player/SportLiveEnv.kt`

* `solutions/media-live/live-sport/gradle.properties`


```Kotlin
Env.init(
    Config.Builder()
        .setApplicationContext(appContext)
        .setAppID(BuildConfig.LIVE_TTSDK_APP_ID)
        .setAppName(BuildConfig.LIVE_TTSDK_APP_NAME)
        .setAppChannel(BuildConfig.LIVE_TTSDK_APP_CHANNEL)
        .setLicenseUri(BuildConfig.LIVE_TTSDK_LICENSE_URI)
        .setLicenseCallback(SportLicenseCallback())
        .build()
)
```


<span id="lsa-channel"></span>
### 步骤 3: 准备频道数据

预设的赛事频道是数据驱动的。每个频道都可以声明机位 ID、拉流协议策略、FLV 流档位、码率信息、低延迟 FLV 偏好以及 ABR 偏好。

关键代码：


* `solutions/media-live/live-sport/src/main/assets/live_sport_channels.json`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/data/SportChannelRepo.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/data/SportChannel.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/player/SportPlayerModels.kt`


`SportChannelRepo` 加载 JSON 频道列表，`SportChannel.toPlayerConfig()` 将选定的频道转换为播放器层使用的 `SportPlayerConfig`。

```Kotlin
val config = channel.toPlayerConfig(
    protocol = protocolOption,
    abrAuto = abrOn,
    pinnedResolution = pinnedResolution,
    enableSR = srEnabled,
    enableSharpen = sharpenEnabled,
)
```


<span id="lsa-player"></span>
### 步骤 4: 创建直播播放器

观看页面使用 `SportLivePlayer` 作为 `VeLivePlayer` 的封装。该封装处理播放器生命周期、`TextureView` 绑定、流数据设置、低延迟 FLV、ABR、超分辨率、锐化、播放事件以及播放统计。

关键代码：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/player/SportLivePlayer.kt`


```Kotlin
player = SportLivePlayer(this).apply {
    setListener(playerListener)
    bindTextureView(playerTexture)
}
```


当播放开始时，该封装会创建一个 `VideoLiveManager`，应用 `VeLivePlayerConfiguration`，设置流数据，附加渲染表面，并调用 `play()`。

对于预设的赛事频道，Demo 使用 `setPlayStreamData()`，使一个频道可以承载多个 FLV 档位，用于画质选择和 ABR。

对于用户输入的自定义流 URL，Demo 使用 `setPlayUrl()`，并让 SDK 从 URL 中检测协议。

<span id="lsa-start"></span>
### 步骤 5: 开始播放

`LiveWatchActivity` 在页面设置期间准备初始频道，并在页面进入前台时开始播放。

关键代码：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`


<span id="lsa-switch"></span>
### 步骤 6: 切换机位、协议和画质

机位切换由观看页面处理。当观众选择另一个机位时，页面会准备一个新的频道配置，并以选定的频道重新开始播放。

关键代码：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/camera/CameraListAdapter.kt`


播放设置在设置面板中暂存。协议或 ABR 的更改会使用新的 `SportPlayerConfig` 重建播放。超分辨率和锐化是运行时开关，无需重建播放器。

关键代码：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/panel/PlayerSettingsPanel.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/player/SportLivePlayer.kt`


画质选择基于选定频道声明的 FLV 档位。启用 ABR 时，播放器可以在可用档位之间自适应。禁用 ABR 时，在重建播放前会将选定的分辨率固定在 `SportPlayerConfig` 中。

<span id="lsa-interact"></span>
### 步骤 7: 添加全屏和互动功能

互动功能作为叠加在直播播放之上的 UI 层实现。

关键代码：


* 评论：`solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/comment`

* 礼物：`solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/gift`

* 点赞：`solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/like`

* 全屏控制：`solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/fullscreen`

* 观看页面编排：`solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`


在全屏模式下，`LandscapeController` 会将现有的 `TextureView` 移入横屏浮层。这样可以保持同一个播放器实例，并避免在进入或退出全屏时重新开始播放。

<span id="lsa-compare"></span>
### 步骤 8: 添加对比和自定义流体验

对比页面使用独立的播放器插槽，以并排对比多种播放体验。只有处于激活状态的对比标签页会保持其播放器运行。

关键代码：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/compare/LiveCompareActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/compare/CompareSlot.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/compare/CompareConfig.kt`

* `solutions/media-live/live-sport/src/main/assets/live_sport_compare.json`


自定义流页面会校验观众输入的 URL，并以自定义流模式打开观看页面。

关键代码：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/stream/LiveStreamAddressActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/stream/CustomStreamUrlParser.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/stream/CustomStreamSettingsBinder.kt`


<span id="lsa-code"></span>
## 示例代码

请参考 Demo 源代码，将此功能集成到您的应用中。


* Android：[live-sport](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/media-live/live-sport)
