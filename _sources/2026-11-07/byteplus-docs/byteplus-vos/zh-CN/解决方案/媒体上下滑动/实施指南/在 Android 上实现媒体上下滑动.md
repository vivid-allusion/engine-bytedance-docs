---
title: "在 Android 上实现媒体上下滑动"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/Implementing-media-up-and-down-swiping-for-Android-zh-CN"
---

为了在您的 Android 应用中创建流畅可滑动的视频内容流，本指南将介绍如何实现视频点播（VOD）和直播流播放。您将学习关键优化策略，例如针对 VOD 的预加载和预渲染，以及针对直播内容的预流，以确保用户体验的无缝流畅。

<span id="a3521dd9"></span>
# 环境要求


* Android Studio Arctic Fox 或更高版本。我们建议使用最新版本的 Android Studio，以获得最佳性能。

* 一台运行 Android 5.0 或更高版本的实体移动设备。

* 请确保您使用的 CPU 架构为 armv7 或 arm64。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">暂不支持模拟器。</div>


<span id="76cb7082"></span>
# 前置条件


* 一个有效的[BytePlus 账号](http://console.byteplus.com/)，并已激活[BytePlus VOD](https://console.byteplus.com/vodpaas)和[BytePlus MediaLive](https://console.byteplus.com/live)。

* 在[SDK 管理](https://console.byteplus.com/vodpaas/sdk/)页面的[BytePlus VOD 控制台](https://docs.byteplus.com/en/byteplus-vod/docs/sdk-management)中完成以下操作：

   * 创建应用并获取其应用 ID 和名称。

   * 为应用注册，并购买及下载用于 Player 的许可证。

   * 您需要高级版 SDK 和许可证，以支持预加载与预渲染。

      * [Player SDK 功能](https://docs.byteplus.com/docs/byteplus-vod/docs-player-features)

      * [Android Player SDK：自定义预加载](https://docs.byteplus.com/docs/byteplus-vod/docs-custom-preloading-android)

* 完成[直播流基础设置](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)。

* 获取 BytePlus MediaLive SDK 许可证。

   * 有关获取许可证的详细说明，请参见[访问您的 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license)。

   * 如需了解如何选择适合您需求的许可证类型，请参考[SDK 介绍](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)。


<span id="1c99b955"></span>
# 版本要求


* 要访问**视频播放**和直播流**功能**，必须使用 BytePlus VOD 和 BytePlus MediaLive SDK。请记得在[客户端 SDK 组件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-CN)页面选择正确的 SDK。


<span id="f86cb645"></span>
# 集成 SDK

<span id="f5922109"></span>
## 步骤 1：添加 maven 仓库

打开项目根目录下的 `build.gradle` 文件，并在 `repositories` 代码块中添加仓库地址，如下所示：

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
 
// BytePlus VOD SDK maven repository
apply from: 'https://ve-vos.volccdn.com/script/vevos-repo-base.gradle'
```


<span id="4448e58f"></span>
## 步骤 2：集成 SDK

要集成 SDK，请将以下依赖项添加到您的模块 `build.gradle` 文件中：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">要获取最新版本号，请参见<a href="https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-CN">客户端 SDK 组件</a>。</div>


```Groovy
dependencies {
    def ttsdkVersion = "1.43.300.3"
    // BytePlus VOD SDK dependencies
    implementation "com.bytedanceapi:ttsdk-player_premium:$ttsdkVersion"
    
    // BytePlus MediaLive SDK dependencies
    implementation "com.bytedanceapi:ttsdk-ttlivepull_rtc:$ttsdkVersion"
    implementation 'commons-net:commons-net:3.9.0'
    
    implementation 'com.bytedance.applog:RangersAppLog-Lite-global:6.14.3'
}
```


<span id="38b05b45"></span>
## 步骤 3：声明应用权限

在 `AndroidManifest.xml` 中声明 SDK 所需的权限。

```XML
<uses-permission android:name="android.permission.INTERNET" /> 
```


<span id="06ca11af"></span>
# 实现

<span id="1690b16f"></span>
## 短视频优化策略

<span id="9a37c9aa"></span>
### 步骤 1：实现视频播放

如需了解如何使用 BytePlus VOD 播放器进行视频播放，请参见[在 Android 上实现视频播放](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-video-playback-edit-for-android-zh-CN)。

<span id="c8e4d2c6"></span>
### 步骤 2：启用 BytePlus VOD 播放器的预加载与预渲染策略

调用[TTVideoEngine.enableEngineStrategy(int, int)](https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-sdk-api-details#enableenginestrategy)以启用预加载和预渲染策略

```Java
public static void setSceneStrategyEnabled(){
        TTVideoEngine.enableEngineStrategy(
                StrategyManager.STRATEGY_TYPE_PRELOAD,
                StrategyManager.STRATEGY_SCENE_SMALL_VIDEO
        );
        TTVideoEngine.enableEngineStrategy(
                StrategyManager.STRATEGY_TYPE_PRE_RENDER,
                StrategyManager.STRATEGY_SCENE_SMALL_VIDEO
        );
}
```


<span id="fe5ebf44"></span>
### 步骤 3：设置预加载源

在合适的时机（如获取到视频播放列表后），将播放列表设置为预加载源。


1. 首次加载播放源数据或刷新页面获取新数据时，调用[TTVideoEngine.setStrategySources(List](https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-sdk-api-details#TTVideoEngine-setstrategysources)。

2. 在加载更多数据的场景下，调用[TTVideoEngine.addStrategySources(List)](https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-sdk-api-details#TTVideoEngine-addStrategySources)。

> 在该场景下，播放列表包含 VOD 和直播流媒体，因此设置预加载源时，务必排除直播流媒体。否则可能导致意外问题。


根据所提供的播放列表，BytePlus VOD SDK 会根据当前播放状态自动管理预加载的时机和配置，例如并发预加载数量和数据大小。

```Java
// Set preload sources
if (page == 0) {
    TTVideoEngine.setStrategySources(items.filterMediaSource());
    // ... more codes here
} else { // append items
    TTVideoEngine.addStrategySources(items.filterMediaSource());
    // ... more codes here
}
```


<span id="dacb2db7"></span>
### 步骤 4：封面显示与预渲染

启用预渲染后，SDK 会根据您提供的播放列表提前创建播放器，并在播放当前视频时，对播放列表中的下一个视频进行解码和渲染。

在滚动视频流场景下，当下一个视频即将可见时，我们会加载该视频的封面图片。如果此时视频已被预渲染，我们将不再加载封面图片，而是直接使用视频的第一帧作为封面。

```Java
// using the prerendered player.
final TTVideoEngine player = TTVideoEngine.getPreRenderEngine(mediaSource.getMediaId());

if (player != null && player != StrategyManager.instance().getPlayEngine()) {
    // call forceDraw to prerender
    player.setSurface(surface);
    player.forceDraw();
} else {
    // prerender not ready, using image cover
    showVideoCover();
}
```


<span id="8978e0b9"></span>
### 步骤 5：播放视频

播放下一个视频时，如果预渲染已完成且有可用的预渲染播放器，则使用该播放器。否则，创建一个新的播放器。

```Java
TTVideoEngine player = TTVideoEngine.getPreRenderEngine(mediaSource.getMediaId());
if (player == null) {
    player = create(mContext, mediaSource);
}
```


<span id="d6d50092"></span>
## 直播流优化策略

<span id="e32ad1e1"></span>
### 步骤 1：初始化 SDK

使用以下代码初始化 SDK：

```Java
// Initialize the environment.
   Env.init(new Config.Builder()
   .setApplicationContext(sApplicationContext)
   .setAppID("Your App ID")
   .setAppName("Your application name")
   .setAppVersion(BuildConfig.VERSION_NAME) // A valid version number should contain two or more separators, such as "1.3.2".
   .setAppChannel("Your app channel")
   .setLicenseUri("Your license URI")
   .setLicenseCallback(mLicenseCallback) // Set the license callbacks.
   .build());

// Enable logcat. It is recommended to enable logcat during development and disable logcat when compiling the release APK.
// LicenseManager.turnOnLogcat(true);

// License callbacks.
LicenseManager.Callback mLicenseCallback =new LicenseManager.Callback() {
        @Override
        public void onLicenseLoadSuccess(@NonNull String licenseUri, @NonNull String licenseId) {
            licenseID = licenseId; // License ID, through which you can get the license information.
        }

        @Override
        public void onLicenseLoadError(@NonNull String licenseUri, @NonNull Exception e, boolean retryAble) {
           
        }

        @Override
        public void onLicenseLoadRetry(@NonNull String licenseUri) {
           
        }

        @Override
        public void onLicenseUpdateSuccess(@NonNull String licenseUri, @NonNull String licenseId) {
          licenseID = licenseId;
        }

        @Override
        public void onLicenseUpdateError(@NonNull String licenseUri, @NonNull Exception e, boolean retryAble) {
           
        }

        @Override
        public void onLicenseUpdateRetry(@NonNull String licenseUri) {
          
        }
    };
    
// Get the license information.
License license = LicenseManager.getInstance().getLicense(licenseID); // You can get the license ID through mLicenseCallback.
if (license != null) {
    StringBuilder builder = new StringBuilder();
    builder.append("License id:" + license.getId()).append("\n")
           .append("License package:" + license.getPackageName()).append("\n")
           .append("License test:" + license.getType()).append("\n")
           .append("License version:" + license.getVersion()).append("\n");

    if (license.getModules() != null) {
        String names = "";
        for (License.Module module : license.getModules()) {
            names = "module name:" + module.getName() + ", start time:" +
            TimeUtil.format(module.getStartTime(), Times.YYYY_MM_DD_KK_MM_SS)
                    + ", expire time:" + TimeUtil.format(module.getExpireTime(), Times.YYYY_MM_DD_KK_MM_SS) + "\n";
            builder.append("License modules:" + names);
        }
    }
 }
```


<span id="ff105711"></span>
### 步骤 2：初始化播放器

```Java
// Create a player
VeLivePlayer player = new VideoLiveManager(Env.getApplicationContext());

// Set the player observer
player.setObserver(mLivePlayerObserver)；

// Configure the player
VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
config.enableStatisticsCallback = true;
config.enableLiveDNS = true;
player.setConfig(config);
```


<span id="e8b8a7da"></span>
### 步骤 3：预加载流

当用户开始滑动时，将流静音，滑动完成后取消静音。

```Java
@Override
public void onPositionVisibilityChanged(int oldPosition, int newPosition) {
    super.onPositionVisibilityChanged(oldPosition, newPosition);

    LiveFeedHolder holder = getHolder(newPosition);
    LiveFeedItem item = (LiveFeedItem) getItem(newPosition);

    VideoLiveManager player = holder.getPlayer();
    if (player == null) {
        player = createLivePlayer(context, item.getRoomId());
        holder.bindPlayer(player);
    }

    player.setPlayUrl(item.getLiveUrl());
    player.setMute(true);
    player.play();
}
```


<span id="32c6f252"></span>
### 步骤 4：取消静音

当前视图显示时，取消流的静音状态。

```Java
@Override
public void onPageSelected(int position) {
    super.onPageSelected(position);

    LiveFeedHolder holder = getHolder(position);
    LiveFeedItem item = (LiveFeedItem) getItem(position);

    VideoLiveManager player = holder.getPlayer();
    if (player == null) {
        player = createLivePlayer(context, item.getRoomId());
        holder.bindPlayer(player);
    }

    player.setPlayUrl(item.getLiveUrl());
    player.setMute(false);
    player.play();
}
```


<span id="262dad51"></span>
### 步骤 5：重置播放器状态

当当前视频滑出视图时，重置播放状态并停止流。

```Java
@Override
public void onPageSelected(int position) {
    super.onPageSelected(position);
    
    if (lastHolder != null) {
        VideoLiveManager player = lastHolder.getPlayer();
        if (player != null) {
            player.stop();
        }
    }

    // more codes here
}
```
