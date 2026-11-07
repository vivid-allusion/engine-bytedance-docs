---
title: "在 iOS 上实现媒体上下滑动"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/Implementing-media-up-and-down-swiping-for-iOS-zh-CN"
---

为了在您的 iOS 应用中创建高性能、可滑动的媒体信息流，本指南为点播（VOD）和直播内容提供优化策略。您将学习如何使用 BytePlus VOD SDK 实现短视频的预加载和预渲染，以及使用 BytePlus MediaLive SDK 对直播内容进行预流，确保用户滑动时播放体验流畅、缓冲最小。

<span id="a04bd286"></span>
# 开发环境


* Xcode 14.0 或更高版本。

* CocoaPods 1.10.0 或更高版本

* 运行 iOS 13.0 或更高版本的实体移动设备。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">暂不支持模拟器。</div>


<span id="3d1ba1f0"></span>
# 前置条件


* 拥有一个有效的 [BytePlus 账号](http://console.byteplus.com/)，并已激活 [BytePlus VOD](https://console.byteplus.com/vodpaas) 和 [BytePlus MediaLive](https://console.byteplus.com/live)。

* 在 [SDK 管理](https://console.byteplus.com/vodpaas/sdk/)页面的 [BytePlus VOD 控制台](https://docs.byteplus.com/en/byteplus-vod/docs/sdk-management)上完成以下操作：

   * 创建应用并获取应用 ID 及应用英文名称。

   * 为应用注册，并购买及下载用于 Player 的许可证。

   * 需要高级版 SDK 与许可证以支持 预加载和预渲染。

      * [Player SDK 功能](https://docs.byteplus.com/docs/byteplus-vod/docs-player-features)

      * [iOS Player SDK：自定义预加载](https://docs.byteplus.com/en/docs/byteplus-vod/docs-custom-preloading-ios)

* 已完成 [直播基础配置](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)。

* 已获得 BytePlus MediaLive SDK 许可证。

   * 有关获取许可证的详细说明，请参见 [访问您的 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license)。

   * 如需了解如何选择适合您需求的许可证类型，请参考 [SDK 介绍](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)。


<span id="c4e0d0bf"></span>
# 版本要求


* 要访问 **视频播放**和**直播**功能，必须使用 BytePlus VOD 和 BytePlus MediaLive SDK。

> 有关各方案所用 SDK 的对应版本，请参见[客户端 SDK 组件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-CN)。


<span id="8cf67321"></span>
# 集成

<span id="4e4b9a14"></span>
## 步骤 1：修改 Podfile

在项目目录中按如下方式修改 Podfile：

```Ruby
source 'https://cdn.cocoapods.org/'
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
source 'https://github.com/volcengine/volcengine-specs.git'

$RTC_SDK = 'TTSDK/RTCSDK'
target 'YourProjectTarget' do
  # BytePlus VOD SDK and MediaLive SDK dependencies
  pod 'TTSDK', '1.43.300.2-premium', :subspecs => ['LivePull-RTS', 'Player', 'RTCSDK']
end
```


<span id="e1b77a40"></span>
## 步骤 2：安装 Podfile 中列出的指定依赖项

要完成 SDK 安装，请在终端运行 `pod install`。安装成功后，可打开生成的 `VideoOne.xcworkspace` 文件配置项目。

```Bash
pod install
```


<span id="b1d3e711"></span>
# 实现

<span id="9f99730b"></span>
## 短视频优化策略

<span id="16117a3f"></span>
### 步骤 1：实现视频播放

如需集成 BytePlus VOD 播放器实现视频播放功能，可参考[在 iOS 上实现视频播放](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-video-playback-edit-for-ios-zh-CN)。

<span id="3fd93a31"></span>
### 步骤 2：启用 BytePlus VOD 播放器的预加载与预渲染策略

调用 [TTVideoEngine:enableEngineStrategy: scene:](https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-api-details#enableenginestrategy-scene) 启用预加载与预渲染策略

```objectivec
- (void)startVideoStrategy {
    [TTVideoEngine enableEngineStrategy:TTVideoEngineStrategyTypePreload scene:TTVEngineStrategySceneSmallVideo];
    [TTVideoEngine enableEngineStrategy:TTVideoEngineStrategyTypePreRender scene:TTVEngineStrategySceneSmallVideo];
    [TTVideoEngine setPreRenderVideoEngineDelegate:self];
}
```


<span id="47c37d97"></span>
### 步骤 3：设置预加载源

在适当时机将播放列表设置为预加载源，例如视频播放列表的网络请求返回后。


1. 首次加载播放源数据或刷新页面显示新数据时，调用 [TTVideoEngine:setStrategyVideoSources:](https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-api-details#setstrategyvideosources)。

2. 加载更多数据时，调用 [TTVideoEngine:addStrategyVideoSources:](https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-api-details#addstrategyvideosources)。

> 在此场景下，点播媒体与直播媒体混合，因此设置预加载源时需排除直播媒体。否则可能导致意外问题。


根据所提供的播放列表，BytePlus VOD SDK 会根据当前播放状态自动管理预加载的时机与配置，如并发预加载数量及数据大小。

```objectivec
// Set preload sources
- (void)configVideoEngineStrategyMediaSources:(NSArray<VEVideoModel *> *)videoModels refresh:(BOOL)refresh {
    NSMutableArray *sources = [NSMutableArray array];
    [videoModels enumerateObjectsUsingBlock:^(VEVideoModel * _Nonnull obj, NSUInteger idx, BOOL * _Nonnull stop) {
        [sources addObject:[VEVideoModel videoEngineVidSource:obj]];
    }];
    if (refresh) { 
        /// Called when loading for the first time or refreshing the list
        [TTVideoEngine setStrategyVideoSources:sources];
    } else { 
        /// Called when loading more by scrolling up
        [TTVideoEngine addStrategyVideoSources:sources];
    }
}
```


<span id="b22f4dfa"></span>
### 步骤 4：封面展示与预渲染

开启预渲染后，SDK 会根据您提供的播放列表提前创建播放器，并在播放当前视频时对播放列表中的下一个视频进行解码和渲染。通过调用[TTVideoEngine:getPreRenderVideoEngineWithVideoSource: ](https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-api-details#getprerendervideoenginewithvideosource)，可以判断预渲染是否完成。

在滑动视频流场景下，当下一个视频即将显示时，我们会加载其封面图片。如果此时视频已完成预渲染，则不再加载封面图片，直接使用视频的首帧作为封面。

```objectivec
// using the prerendered player.
TTVideoEngine *preRenderVideoEngine = [TTVideoEngine getPreRenderFinishedVideoEngineWithVideoSource:mediaSource];
// set prerendered player scaling mode
[preRenderVideoEngine setOptionForKey:VEKKeyViewScaleMode_ENUM value:@(TTVideoEngineScalingModeAspectFill)];
if (preRenderVideoEngine) {
    preRenderVideoEngine.playerView.hidden = NO;
    preRenderVideoEngine.playerView.backgroundColor = [UIColor clearColor];
    // hide image cover
    self.posterImageView.hidden = YES;
    // attach prerender view
    [self.view insertSubview:preRenderVideoEngine.playerView aboveSubview:self.posterImageView];
    [preRenderVideoEngine.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.edges.equalTo(self.view);
    }];
    return;
}
// prerender not ready, using image cover
self.posterImageView.hidden = NO;
[self.posterImageView sd_setImageWithURL:[NSURL URLWithString:[self __getBackgroudImageUrl:mediaSource]] completed:nil];
```


<span id="7419411b"></span>
### 步骤 5：播放视频

播放下一个视频时，若预渲染已完成，则直接使用预渲染播放器；否则新建一个播放器。

```objectivec
TTVideoEngine *preRenderVideoEngine = [TTVideoEngine getPreRenderVideoEngineWithVideoSource:mediaSource];
if (preRenderVideoEngine) {
    self.videoEngine = nil;
    self.videoEngine = preRenderVideoEngine;
} else {
    self.videoEngine = [[TTVideoEngine alloc] initWithOwnPlayer:YES];;
}
```


<span id="46d1216b"></span>
## 直播流优化策略

<span id="87c5e4a2"></span>
### 步骤 1：初始化 SDK

使用如下代码初始化 SDK：

```objectivec
#import <TTSDK/TTSDKManager.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Your code.
    [self configTTSDK];
    // Your code.
    return YES;
}

- (void)configTTSDK {
    // Create TTSDKConfiguration with your App ID.
    TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:@"Your App ID"];
    // Configure information about your SDK application.
    configuration.appName = @"Your application name";
    configuration.channel = @"Your app channel";
    configuration.bundleID = @"Your bundle ID";
    
    // Configure the URI of your license file.
    configuration.licenseFilePath = [NSBundle.mainBundle pathForResource:@"Your license path" ofType:nil];
    
    // Pass TTSDKConfiguration to TTSDKManager.
    [TTSDKManager startWithConfiguration:configuration];
}
```


<span id="9ee7765d"></span>
### 步骤 2：初始化播放器

```objectivec
- (void)setupPlayer {
    _playerManager = [[TVLManager alloc] initWithOwnPlayer:YES];
    if (!_playerManager) {
        return;
    }

    VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc] init];
    config.enableStatisticsCallback = YES;
    [self.playerManager setConfig:config];
    
    [self.playerManager setPlayerViewRenderType:(TVLPlayerViewRenderTypeMetal)];
    [self.playerManager setObserver:self];
    [self.playerManager setProjectKey:[NSBundle.mainBundle.infoDictionary objectForKey:@"CFBundleName"]];
}
```


<span id="676a7e04"></span>
### 步骤 3：预加载流

滑动开始时将流静音，滑动完成后取消静音。

```objectivec
- (void)partiallyShow {
    [self.view  addSubview:self.playerContainer]
    [self.playerContainer mas_makeConstraints:^(MASConstraintMaker *make) {
        make.edges.equalTo(streamView);
    }];

    [self.playerManager setPlayUrl:url];
    [self.playerManager play];
    [self.player setMute:YES];
}
```


<span id="cdf30ccd"></span>
### 步骤 4：取消静音

当前视图显示时取消流静音

```objectivec
- (void)completelyShow {
   [self.player setMute:NO];
}
```


<span id="e050c92c"></span>
### 步骤 5：播放器状态重置

当前视频滑出后，重置播放状态并停止流。

```objectivec
- (void)endShow {
    [self.playerManager stop];
}
```
